---
title: 教學課程：針對 Linux 上的 SQL Server 使用 AD 驗證
titleSuffix: SQL Server
description: 本教學課程提供在 Linux 上的 SQL Server 的 AD 驗證的設定步驟。
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: rothja
ms.date: 04/01/2019
manager: craigg
ms.topic: tutorial
ms.prod: sql
ms.custom: seodec18
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 5e9d7ee2c086f188041fbf6c42448d21953b008d
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822782"
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>教學課程：使用 Linux 上的 SQL Server 的 Active Directory 驗證

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本教學課程說明如何設定[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]來支援作用中的目錄 （廣告） 驗證，也稱為整合式驗證的 Linux 上。 如需概觀，請參閱[Linux 上的 SQL Server 的 Active Directory 驗證](sql-server-linux-active-directory-auth-overview.md)。

本教學課程包含下列工作：

> [!div class="checklist"]
> * 加入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到 AD 網域的主機
> * 建立 AD 使用者輸入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，並設定 SPN
> * 設定[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]服務 keytab
> * 安全 keytab 檔案
> * 設定 SQL Server 以使用 keytab 檔案進行 Kerberos 驗證
> * 在考慮改用 SQL 建立 AD 架構的登入
> * 連線到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 AD 驗證

## <a name="prerequisites"></a>先決條件

設定 AD 驗證之前，您必須：

* 設定網路上的 AD 網域控制站 (Windows)  
* 安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
  * [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server (SLES)](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a id="join"></a> 加入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到 AD 網域的主機

您必須將您的 SQL Server Linux 主機與 Active Directory 網域控制站。 如需如何加入 active directory 網域的詳細資訊，請參閱[聯結到 Active Directory 網域的 Linux 主機上的 SQL Server](sql-server-linux-active-directory-join-domain.md)。

## <a id="createuser"></a> 建立 AD 使用者 （或 MSA）[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]和設定的 SPN

> [!NOTE]
> 下列步驟會使用您[完整的網域名稱](https://en.wikipedia.org/wiki/Fully_qualified_domain_name)。 如果您是在**Azure**，您必須 **[建立一個](https://docs.microsoft.com/azure/virtual-machines/linux/portal-create-fqdn)** 再繼續進行。

1. 在您的網域控制站上執行[New-aduser](https://technet.microsoft.com/library/ee617253.aspx) PowerShell 命令來建立新的 AD 使用者與密碼永不過期。 下列範例會命名為帳戶`mssql`，但帳戶名稱可以是任何您喜歡的項目。 系統會提示您輸入帳戶的新密碼。

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > 使 SQL Server 認證不與其他服務正在使用相同的帳戶共用，就有專用的 AD 帳戶的 SQL Server 的安全性最佳作法。 不過，您可以選擇性地重複使用現有的 AD 帳戶如果您知道帳戶的密碼 （其為所需的下一個步驟中產生 keytab 檔案）。

2. 設定此帳戶使用 ServicePrincipalName (SPN) **setspn.exe**工具。 SPN 格式必須完全在下列範例中所指定。 您可以找到的完整的網域名稱[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主機電腦，執行`hostname --all-fqdns`上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主應用程式。 除非您已設定的 TCP 連接埠應該是 1433年[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用不同的連接埠號碼。

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   setspn -A MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > 如果您收到錯誤， `Insufficient access rights`，與您的網域系統管理員檢查您是否有足夠的權限，此帳戶設定 SPN。
   >
   > 如果您在未來變更的 TCP 連接埠，您必須執行**setspn**命令再次使用新的連接埠號碼。 您也需要將新的 SPN 新增至 SQL Server 服務 keytab，依照下一節的步驟。

如需詳細資訊，請參閱 [註冊 Kerberos 連接的服務主體名稱](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)。

## <a id="configurekeytab"></a> 設定[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]服務 keytab

有兩種不同的方式，來設定 SQL Server 服務 keytab 檔案。 第一個選項是使用電腦帳戶 (UPN)，而第二個選項是使用受控服務帳戶 (MSA) keytab 組態中。 這兩個機制可以同樣的功能，以及您可以選擇最適合您環境的方法。

在這兩種情況下，在先前步驟中建立的 SPN 為必要項，並 keytab 中必須註冊 SPN。

若要設定 SQL Server 服務 keytab 檔案：

1. 設定[SPN keytab 項目](#spn)下一節。

1. 然後任一[新增 UPN](#upn) （選項 1） 或[MSA](#msa) （選項 2） 中的個別區段中的步驟，為 keytab 檔案的項目。

> [!IMPORTANT]
> 如果 UPN/msa 密碼已變更或 Spn 會指派給帳戶的密碼已變更，您必須以新密碼和金鑰版本號碼 (KVNO) 更新 keytab。 某些服務也可能自動輪替的密碼。 檢閱任何有問題的帳戶的密碼輪替原則，並將它們與排程的維護活動，以避免非預期停機時間對齊。

### <a id="spn"></a> SPN keytab 項目

1. 請檢查上一個步驟中建立的 AD 帳戶的金鑰版本號碼 (KVNO)。 它通常是 2，但它可能是另一個整數，如果您變更帳戶的密碼多次。 SQL Server 主機電腦上，執行下列命令：

   ```bash
   kinit user@CONTOSO.COM
   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**
   ```

   > [!NOTE]
   > Spn 可能需要幾分鐘的時間才能傳播至您的網域，整個，尤其是網域較大。 如果您收到錯誤， `kvno: Server not found in Kerberos database while getting credentials for MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM`，請等候幾分鐘的時間，然後再試一次。  

1. 開始**ktutil**:

   ```bash
   sudo ktutil
   ```

1. 使用下列命令的每個 spn 新增 keytab 項目：

   ```bash
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   ```

1. 寫入 keytab 檔案，然後結束 ktutil:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

   > [!NOTE]
   > **Ktutil**工具不會驗證密碼，因此請確定您輸入它正確出現提示時。

### <a id="upn"></a> 選項 1:若要設定 keytab 使用 UPN

將電腦帳戶新增至與您 keytab **ktutil**。 電腦帳戶 （也稱為 UPN） 是存在於 **/etc/krb5.keytab**形式`<hostname>$@<realm.com>`(比方說， `sqlhost$@CONTOSO.COM`)。 複製這些項目 **/etc/krb5.keytab**要**mssql.keytab**。

1. 開始**ktuil**使用下列命令：

   ```bash
   sudo ktutil
   ```

1. 使用**rkt**命令來讀取所有的項目，從 **/etc/krb5.keytab**。

   ```bash
   rkt /etc/krb5.keytab
   ```

1. 接下來，列出的項目。

   ```bash
   list
   ```

1. 刪除所有這些項目的位置編號不是 UPN 的項目。 執行此逐一重複下列命令：

   ```bash
   delent <slot num>
   ```

   > [!IMPORTANT]
   > 當項目刪除時，例如位置 1，所有值投影片組成一個取代它的位置。 這表示插槽 2 中的項目移至插槽 1 的項目刪除時，插槽 1。

1. 列出的項目一次只能 UPN 的項目會保留之前。

   ```bash
   list
   ```

1. 當保留只能 UPN 的項目時，這些將值附加到**mssql.keytab**:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   ```

1. 結束**ktutil**。

   ```bash
   quit
   ```

### <a id="msa"></a> 選項 2:若要設定 keytab 使用 MSA

MSA 選項時，您必須建立 SQL Server 的 Kerberos keytab。 它應該包含的所有[第一個步驟中登錄的 Spn](#spn)和 MSA Spn 已登錄的認證。 

1. SPN keytab 項目會建立後，從已加入網域的 Linux 機器中執行下列命令：

   ```bash
   kinit <AD user>
   kvno <any SPN registered in step 1>
      <spn>@CONTOSO.COM: kvno = <KVNO>
   ```

   此步驟中會顯示 KVNO 指派 SPN 擁有權的使用者帳戶。 此步驟中運作，SPN 必須已指派給 MSA 帳戶在其建立期間。 如果 SPN 已不會指派給 MSA，顯示 KVNO 會是目前的 SPN 擁有者帳戶，並會用於設定不正確。  

1. 開始**ktutil**:

   ```bash
   sudo ktutil
   ```

1. 新增下列兩個命令使用 MSA:

   ```bash
   addent -password -p <MSA> -k <kvno from command above> -e aes256-cts-hmac-sha1-96
   addent -password -p <MSA> -k <kvno from command above> -e rc4-hmac
   ```

1. 寫入 keytab 檔案，然後結束 ktutil:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

1. 使用 MSA 方法時，必須設定與組態選項**mssql conf**指定 MSA 時存取 keytab 檔案使用的工具。 確定以下的值位於 **/var/opt/mssql/mssql.conf**。

   ```bash
   sudo mssql-conf set network.privilegedadaccount <MSA_Name>
   ```

   > [!NOTE]
   > 只包含 MSA 名稱而不是網域 \ 帳戶名稱。

## <a id="securekeytab"></a> 安全 keytab 檔案

此 keytab 檔案的存取權的任何人都可以模擬網域上的 SQL Server，因此請確定您將限制存取檔案，使得只有 mssql 帳戶具有讀取權限：

```bash
sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
```

## <a id="keytabkerberos"></a> 設定 SQL Server 以使用 keytab 檔案進行 Kerberos 驗證

使用下列步驟來設定 SQL Server，若要開始使用 keytab 檔案來進行 Kerberos 驗證。

```bash
sudo mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
sudo systemctl restart mssql-server
```

選擇性地停用網域控制站，以改善效能的 UDP 連接。 在許多情況下，UDP 連線持續失敗時連線到網域控制站，因此您可以設定組態選項 **/etc/krb5.conf**略過 UDP 呼叫。 編輯 **/etc/krb5.conf**並設定下列選項：

```/etc/krb5.conf
[libdefaults]
udp_preference_limit=0
```

此時，您已準備好使用 AD 為基礎的登入 SQL Server 中，如下所示。

## <a id="createsqllogins"></a> 在考慮改用 SQL 建立 AD 架構的登入

1. 連接到 SQL Server，並建立新的 AD 型登入：

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

1. 確認 登入現在會列在[sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)系統目錄檢視：

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a id="connect"></a> 連接到 SQL Server 使用 AD 驗證

用戶端電腦使用您的網域認證登入。 現在您可以連接到 SQL Server，無需重新輸入您的密碼，使用 AD 驗證。 如果您建立的 AD 群組的登入，屬於該群組的任何 AD 使用者可以連線相同的方式。

若要使用 AD 驗證的用戶端的特定連接字串參數取決於您所使用的驅動程式。 請考慮下列各節中的範例。

### <a name="sqlcmd-on-a-domain-joined-linux-client"></a>已加入網域的 Linux 用戶端上的 sqlcmd

登入使用的已加入網域的 Linux 用戶端**ssh**和您的網域認證：

```bash
ssh -l user@contoso.com client.contoso.com
```

請確定您已安裝[mssql 工具](sql-server-linux-setup-tools.md)套件，然後使用連接**sqlcmd**未指定任何認證：

```bash
sqlcmd -S mssql-host.contoso.com
```

### <a name="ssms-on-a-domain-joined-windows-client"></a>已加入網域的 Windows 用戶端上的 SSMS

已加入網域的 Windows 用戶端使用您的網域認證登入。 請確定已安裝 SQL Server Management Studio，然後連接至您的 SQL Server 執行個體 (例如`mssql-host.contoso.com`) 指定**Windows 驗證**中**連接到伺服器**對話方塊。

### <a name="ad-authentication-using-other-client-drivers"></a>使用其他用戶端驅動程式的 AD 驗證

下表說明其他用戶端驅動程式的建議：

| 用戶端驅動程式 | 建議 |
|---|---|
| **JDBC** | 您可以使用 Kerberos 整合式的驗證來連接 SQL Server。 |
| **ODBC** | 使用整合式的驗證。 |
| **ADO.NET** | 連接字串語法。 |

## <a id="additionalconfig"></a> 其他組態選項

如果您正在使用協力廠商公用程式，例如[PBI](https://www.beyondtrust.com/)， [VAS](https://www.oneidentity.com/products/authentication-services/)，或[Centrify](https://www.centrify.com/)將 Linux 主機加入 AD 網域，而您想要強制使用 openldap 中的 SQL server程式庫直接，您可以設定**disablesssd**選項搭配**mssql conf** ，如下所示：

```bash
sudo mssql-conf set network.disablesssd true
systemctl restart mssql-server
```

> [!NOTE]
> 有公用程式的這類**realmd**其中設定 SSSD，同時其他的工具例如 PBI、 VAS 和 Centrify 未安裝 SSSD。 如果用來加入 AD 網域的公用程式未安裝 SSSD，它會建議您設定**disablesssd**選項設定為`true`。 雖然它不需要為 SQL Server 會嘗試使用 SSSD ad 回到 openldap 機制之前，它會更好的效能設定它，讓 SQL Server 會直接略過 SSSD 機制的 openldap 呼叫。

如果您的網域控制站支援 LDAPS，您可以強制從 SQL Server 的所有連線到網域控制站，要透過 LDAPS。 若要檢查您的用戶端可以連絡網域控制站，透過 ldaps，執行下列 bash 命令， `ldapsearch -H ldaps://contoso.com:3269`。 若要設定 SQL Server，僅使用 LDAPS，執行下列命令：

```bash
sudo mssql-conf set network.forcesecureldap true
systemctl restart mssql-server
```

這將會透過 SSSD 使用 LDAPS，如果在加入 AD 網域主機已透過 SSSD 封裝及**disablesssd**未設定為 true。 如果**disablesssd**設為 true，連同**forcesecureldap**設為 true，則它將在 SQL Server 所做的 openldap 程式庫呼叫上使用 LDAPS 通訊協定。

### <a name="post-sql-server-2017-cu14"></a>將 SQL Server 2017 CU14 張貼

從 SQL Server 2017 CU14，如果 SQL Server 加入了使用協力廠商提供者的 AD 網域控制站，而且已設定為使用 openldap 呼叫一般 AD 查閱，只要**disablesssd**來為 true，您也可以使用**enablekdcfromkrb5**選項來強制使用 krb5 程式庫，而不是 KDC 伺服器的反向 DNS 對應的 KDC 查閱的 SQL Server。

這可能是適用於您要手動設定 SQL Server 會嘗試與通訊的網域控制站的案例。 而且您使用 [KDC] 清單中的使用 openldap 程式庫機制**krb5.conf**。

首先，設定**disablessd**並**enablekdcfromkrb5conf**為 true，然後再重新啟動 SQL Server:

```bash
sudo mssql-conf set network.disablesssd true
sudo mssql-conf set network.enablekdcfromkrb5conf true
systemctl restart mssql-server
```

然後設定 KDC 列入 **/etc/krb5.conf** ，如下所示：

```/etc/krb5.conf
[realms]
CONTOSO.COM = {
  kdc = dcWithGC1.contoso.com
  kdc = dcWithGC2.contoso.com
}
```

> [!NOTE]
> 不建議時，就可以使用公用程式，例如**realmd**，同時加入至定義域，Linux 主機設定時設定 SSSD **disablesssd**為 true，讓 SQL Server 使用openldap 呼叫改為 SSSD Active directory 的相關的呼叫。

## <a name="next-steps"></a>後續步驟

在本教學課程中，我們逐步解說如何設定與 Linux 上的 SQL Server 的 Active Directory 驗證。 您已學到如何以：
> [!div class="checklist"]
> * 加入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到 AD 網域的主機
> * 建立 AD 使用者輸入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，並設定 SPN
> * 設定[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]服務 keytab
> * 在考慮改用 SQL 建立 AD 架構的登入
> * 連線到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 AD 驗證

接下來，瀏覽其他安全性案例適用於 SQL Server on Linux。

> [!div class="nextstepaction"]
> [將 Linux 上的 SQL Server 連線加密](sql-server-linux-encrypted-connections.md)
