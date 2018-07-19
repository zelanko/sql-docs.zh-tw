---
title: 使用中目錄驗證教學課程，Linux 上的 SQL Server 的 |Microsoft 文件
description: 本教學課程會提供 AAD 驗證 Linux 上的 SQL Server 中的設定步驟。
author: meet-bhagdev
ms.date: 02/23/2018
ms.author: meetb
manager: craigg
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 7f5f7a4840582afda25551161c4702a40c4977c8
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38980380"
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>教學課程： 使用 Active Directory Linux 上的 SQL Server 驗證

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本教學課程說明如何設定[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]來支援作用中的目錄 （廣告） 驗證，也稱為整合式驗證的 Linux 上。 如需概觀，請參閱[Linux 上的 SQL Server 的 Active Directory 驗證](sql-server-linux-active-directory-auth-overview.md)。

本教學課程包含下列工作：

> [!div class="checklist"]
> * 加入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到 AD 網域的主機
> * 建立 AD 使用者輸入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，並設定 SPN
> * 設定[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]服務 keytab
> * 在考慮改用 SQL 建立 AD 架構的登入
> * 連線到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 AD 驗證

## <a name="prerequisites"></a>先決條件

設定 AD 驗證之前，您必須：

* 設定網路上的 AD 網域控制站 (Windows)  
* 安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
  * [Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a id="join"></a> 加入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到 AD 網域的主機

使用下列步驟，加入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主機加入 Active Directory 網域：

1. 使用**[realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join.html)** 到 AD 網域加入您的主機電腦。 如果您尚未開始，將 [realmd] 與 Kerberos 用戶端封裝上安裝[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主機電腦使用您的 Linux 散發封裝管理員：

   ```bash
   # RHEL
   sudo yum install realmd krb5-workstation

   # SUSE
   sudo zypper install realmd krb5-client

   # Ubuntu
   sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
   ```

1. 如果 Kerberos 的用戶端封裝安裝將會提示您輸入領域名稱，請以大寫輸入您的網域名稱。

   > [!NOTE]
   > 這個逐步解說中使用"contoso.com"和"CONTOSO.COM"做為範例的網域和領域名稱，分別。 您應該將它們替換為您自己的值。 這些命令必須區分大小寫，所以請確定您使用大寫無論它用在這個逐步解說。

1. 設定您[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]作為 DNS large 的 AD 網域控制站的 IP 位址的主機電腦。 

   - **Ubuntu**:

      編輯`/etc/network/interfaces`檔案，以便 AD 網域控制站的 IP 位址列示為 dns large。 例如： 

      ```/etc/network/interfaces
      <...>
      # The primary network interface
      auto eth0
      iface eth0 inet dhcp
      dns-nameservers **<AD domain controller IP address>**
      dns-search **<AD domain name>**
      ```

      > [!NOTE]
      > 不同的電腦可能會不同的網路介面 (eth0)。 若要找出您正在使用哪一個，請執行 ifconfig，複製有 IP 位址及傳輸及收到位元組的介面。

      在編輯這個檔案之後, 重新啟動網路服務：

      ```bash
      sudo ifdown eth0 && sudo ifup eth0
      ```

      現在請檢查您`/etc/resolv.conf`檔案包含一條線，如下列範例所示：  

      ```Code
      nameserver **<AD domain controller IP address>**
      ```

   - **RHEL**:

     編輯`/etc/sysconfig/network-scripts/ifcfg-eth0`檔案 （或其他檔案為適當的介面設定），以便 AD 網域控制站的 IP 位址列示為 DNS 伺服器：

     ```/etc/sysconfig/network-scripts/ifcfg-eth0
     <...>
     PEERDNS=no
     DNS1=**<AD domain controller IP address>**
     ```

     在編輯這個檔案之後, 重新啟動網路服務：

     ```bash
     sudo systemctl restart network
     ```

     現在請檢查您`/etc/resolv.conf`檔案包含一條線，如下列範例所示：  

     ```Code
     nameserver **<AD domain controller IP address>**
     ```

1. 加入網域

   一旦您已經確認您的 DNS 設定正確，請執行下列命令來加入網域。 您必須使用具有足夠的權限，AD 以新的電腦加入網域中的 AD 帳戶進行驗證。

   尤其是，這個命令會建立新的電腦帳戶在 AD 中，建立`/etc/krb5.keytab`keytab 檔案，並設定網域中的`/etc/sssd/sssd.conf`:

   ```bash
   sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
   <...>
   * Successfully enrolled machine in realm
   ```

   > [!NOTE]
   > 如果您看到錯誤，"未安裝必要的封裝，"然後您應該安裝使用您的 Linux 散發封裝管理員，才能執行這些封裝`realm join`一次命令。
   >
   > 如果您收到 「 加入網域，沒有足夠權限 」 錯誤，您就需要網域系統管理員檢查您有足夠的權限 Linux 機器加入網域。
   >
   > 如果您收到錯誤，「 KDC 的回覆不符合期望，"然後您可能指定了不正確的領域名稱的使用者。 領域名稱區分大小寫、 通常大寫，並可識別的指令`realm discover contoso.com`。
   
   > SQL Server 會使用 SSSD 和 NSS 對應使用者帳戶和群組安全性識別碼 (SID)。 設定並執行 SQL Server，若要成功建立 AD 登入的順序，必須是 SSSD。 Realmd 通常會自動執行此一部分加入網域，但在某些情況下您必須執行這項操作分別。
   >
   > 簽出設定下列[SSSD 手動](https://access.redhat.com/articles/3023951)，和[設定若要使用 SSSD 的 NSS](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system-level_authentication_guide/configuring_services#Configuration_Options-NSS_Configuration_Options)

  
5. 請確認您現在可以收集使用者資訊從網域，而且您可以取得 Kerberos 票證，以該使用者。

   下列範例會使用**識別碼**，  **[kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html)**，以及**[klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html)** 這個命令。

   ```bash
   id user@contoso.com
   uid=1348601103(user@contoso.com) gid=1348600513(domain group@contoso.com) groups=1348600513(domain group@contoso.com)

   kinit user@CONTOSO.COM
   Password for user@CONTOSO.COM:

   klist
   Ticket cache: FILE:/tmp/krb5cc_1000
   Default principal: user@CONTOSO.COM
   <...>
   ```

   > [!NOTE]
   > 如果`id user@contoso.com`傳回 「 沒有這類使用者，「 請確定已成功啟動 SSSD 服務： 執行命令`sudo systemctl status sssd`。 如果服務正在執行，而且您仍然看見 「 沒有這類使用者 」 錯誤，請嘗試啟用 SSSD 的詳細資訊記錄。 如需詳細資訊，請參閱 Red Hat 文件[疑難排解 SSSD](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting)。
   >
   > 如果`kinit user@CONTOSO.COM`傳回時，"KDC 的回覆不符合預期時取得初始認證，「 請確定您以大寫指定領域。

如需詳細資訊，請參閱 Red Hat 文件[發掘並加入身分識別網域](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html)。 

## <a id="createuser"></a> 建立 AD 使用者[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]和設定的 SPN

  > [!NOTE]
  > 下一個步驟會使用您[完整的網域名稱](https://en.wikipedia.org/wiki/Fully_qualified_domain_name)。 如果您是在**Azure**，您必須**[建立一個](https://docs.microsoft.com/azure/virtual-machines/linux/portal-create-fqdn)** 再繼續進行。

1. 在您的網域控制站上執行[New-aduser](https://technet.microsoft.com/library/ee617253.aspx) PowerShell 命令來建立新的 AD 使用者與密碼永不過期。 此範例中命名的帳戶"mssql，"但帳戶名稱可以是您喜歡的任何項目。 系統會提示您輸入帳戶的新密碼：

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > 使 SQL Server 認證不與其他服務正在使用相同的帳戶共用，就有專用的 AD 帳戶的 SQL Server 的安全性最佳作法。 不過，您可以重複使用現有的 AD 帳戶如果您想，如果您知道帳戶的密碼 （需要在下一個步驟中產生 keytab 檔案）。

2. 設定此帳戶使用 ServicePrincipalName (SPN)`setspn.exe`工具。 SPN 格式必須完全在下列範例中所指定。 您可以找到的完整的網域名稱[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主機電腦，執行`hostname --all-fqdns`上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主機和 TCP 連接埠應該是 1433年除非您已設定[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用不同的連接埠號碼。

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > 如果您收到錯誤，< 足夠的存取權限 >，您就需要網域系統管理員檢查您有足夠的權限，此帳戶設定 SPN。
   >
   > 如果您在未來變更的 TCP 連接埠，您就需要使用新的連接埠號碼，再次執行 setspn 命令。 您也需要將新的 SPN 新增至 SQL Server 服務 keytab，依照下一節的步驟。

3. 如需詳細資訊，請參閱 [註冊 Kerberos 連接的服務主體名稱](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)。

## <a id="configurekeytab"></a> 設定[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]服務 keytab

1. 檢查上一個步驟中建立的 AD 帳戶的金鑰版本號碼 (kvno)。 它通常是 2，但它可能是另一個整數，如果您變更帳戶的密碼多次。 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主機電腦上，執行下列命令：

   ```bash
   kinit user@CONTOSO.COM

   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**
   ```

2. 建立的 keytab 檔案**[ktutil](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/admin_commands/ktutil.html)** 您在上一個步驟中建立 AD 使用者。 出現提示時，輸入該 AD 帳戶的密碼。

   ```bash
   sudo ktutil

   ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96

   ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac

   ktutil: wkt /var/opt/mssql/secrets/mssql.keytab

   quit
   ```

   > [!NOTE]
   > Ktutil 工具不會無法驗證的密碼，因此請確定輸入正確。

3. 任何人存取這`keytab`檔案，可模擬[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]網域，因此請確定您的檔案這類限制存取只有`mssql`帳戶具有讀取權限：

   ```bash
   sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
   sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
   ```

4. 設定[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]若要使用此`keytab`Kerberos 驗證的檔案：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
   sudo systemctl restart mssql-server
   ```

## <a id="createsqllogins"></a> 在考慮改用 SQL 建立 AD 架構的登入

1. 連接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]並建立新的 AD 為基礎的登入：

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

2. 確認 登入現在會列在[sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)系統目錄檢視：

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a id="connect"></a> 連接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 AD 驗證

用戶端電腦使用您的網域認證登入。 現在您可以連接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]無需重新輸入您的密碼，使用 AD 驗證。 如果您建立的 AD 群組的登入，屬於該群組的任何 AD 使用者可以連線相同的方式。

若要使用 AD 驗證的用戶端的特定連接字串參數取決於您所使用的驅動程式。 請考量下列範例：

* `sqlcmd` 已加入網域的 Linux 用戶端上

   登入已加入網域的 Linux 用戶端使用`ssh`和您的網域認證：

   ```bash
   ssh -l user@contoso.com client.contoso.com
   ```

   請確定您已安裝[mssql 工具](sql-server-linux-setup-tools.md)套件，然後使用連接`sqlcmd`未指定任何認證：

   ```bash
   sqlcmd -S mssql.contoso.com
   ```

* 已加入網域的 Windows 用戶端上的 SSMS

   已加入網域的 Windows 用戶端使用您的網域認證登入。 請確定[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]已安裝，然後連接至您[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]藉由指定的執行個體**Windows 驗證**中**連接到伺服器**對話方塊。

* 使用其他用戶端驅動程式的 AD 驗證

  * JDBC:[使用 Kerberos 整合式驗證來連接 SQL Server](https://docs.microsoft.com/sql/connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server)
  * ODBC:[使用整合式的驗證](https://docs.microsoft.com/sql/connect/odbc/linux/using-integrated-authentication)
  * ADO.NET:[連接字串語法](https://msdn.microsoft.com/library/system.data.sqlclient.sqlauthenticationmethod(v=vs.110).aspx)
  
## <a name="next-steps"></a>後續的步驟

在本教學課程中，我們逐步解說如何設定與 Linux 上的 SQL Server 的 Active Directory 驗證。 您已學到如何以：
> [!div class="checklist"]
> * 加入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到 AD 網域的主機
> * 建立 AD 使用者輸入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，並設定 SPN
> * 設定[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]服務 keytab
> * 在考慮改用 SQL 建立 AD 架構的登入
> * 連線到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 AD 驗證

接下來，瀏覽其他安全性案例適用於 SQL Server on Linux。

> [!div class="nextstepaction"]
>[將 Linux 上的 SQL Server 連線加密](sql-server-linux-encrypted-connections.md)
