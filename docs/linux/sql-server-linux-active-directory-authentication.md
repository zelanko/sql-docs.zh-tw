---
title: 教學課程：將 AD 驗證用於 Linux 上的 SQL Server
titleSuffix: SQL Server
description: 本教學課程提供 Linux 上 SQL Server 的 AD 驗證設定步驟。
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.date: 04/01/2019
ms.topic: tutorial
ms.prod: sql
ms.custom: seodec18
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 69bbeb31f8da4023bd0630ae0d944165407e2dec
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "68027336"
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>教學課程：透過 Linux 上的 SQL Server 使用 Active Directory 驗證

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本教學課程說明如何設定 Linux 上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，以支援 Active Directory (AD) 驗證 (也稱為整合式驗證)。 如需概觀，請參閱[適用於 Linux 上 SQL Server 的 Active Directory 驗證](sql-server-linux-active-directory-auth-overview.md)。

本教學課程包含下列工作：

> [!div class="checklist"]
> * 將 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 主機加入 AD 網域
> * 建立用於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的 AD 使用者並設定 SPN
> * 設定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服務 Keytab
> * 保護 Keytab 檔案
> * 設定 SQL Server 以使用 Keytab 檔案進行 Kerberos 驗證
> * 在 Transact-SQL 中建立以 AD 為基礎的登入
> * 使用 AD 驗證連線到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]

## <a name="prerequisites"></a>Prerequisites

設定 AD 驗證之前，您必須：

* 在您的網路上設定 AD 網域控制站 (Windows)  
* 安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
  * [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server (SLES)](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a id="join"></a> 將 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 主機加入 AD 網域

您必須將 SQL Server Linux 主機加入 Active Directory 網域控制站。 如需如何加入 Active Directory 網域的資訊，請參閱[將 Linux 主機上的 SQL Server 加入 Active Directory 網域](sql-server-linux-active-directory-join-domain.md)。

## <a id="createuser"></a> 建立用於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的 AD 使用者並設定 SPN

> [!NOTE]
> 下列步驟會使用您的[完整網域名稱](https://en.wikipedia.org/wiki/Fully_qualified_domain_name)。 如果您是在 **Azure** 上，您必須先 **[建立名稱](https://docs.microsoft.com/azure/virtual-machines/linux/portal-create-fqdn)** ，然後繼續執行。

1. 在您的網域控制站上執行 [New-ADUser](https://technet.microsoft.com/library/ee617253.aspx) PowerShell 命令，以建立密碼永不過期的新 AD 使用者。 下列範例會將帳戶命名為 `mssql`，但帳戶名稱可以是您喜歡的任何名稱。 系統將提示您輸入該帳戶的新密碼。

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > 安全性最佳做法是針對 SQL Server 使用專用的 AD 帳戶，讓 SQL Server 認證不會與使用相同帳戶的其他服務共用。 不過，如果您知道帳戶的密碼 (在下一個步驟中產生 Keytab 檔案所需的項目)，則可以選擇性地重複使用現有的 AD 帳戶。

2. 使用 **setspn.exe** 工具來設定此帳戶的 ServicePrincipalName (SPN)。 SPN 必須與下列範例中所指定的格式完全相同。 您可以在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 主機上執行 `hostname --all-fqdns`，以尋找 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 主機電腦的完整網域名稱。 除非您已將 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 設定為使用不同的連接埠號碼，否則 TCP 通訊埠應為 1433。

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   setspn -A MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > 如果您收到錯誤 `Insufficient access rights`，請洽詢您的網域系統管理員，確定您有足夠的權限可在此帳戶上設定 SPN。
   >
   > 如果您日後變更 TCP 通訊埠，則必須使用新的連接埠號碼再次執行 **setspn** 命令。 您還需要遵循下一節中的步驟，將新的 SPN 新增至 SQL Server 服務 Keytab。

如需詳細資訊，請參閱 [註冊 Kerberos 連接的服務主體名稱](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)。

## <a id="configurekeytab"></a> 設定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服務 Keytab

有兩種不同的方式可設定 SQL Server 服務 Keytab 檔案。 第一個選項是使用電腦帳戶 (UPN)，而第二個選項則使用 Keytab 設定中受控服務帳戶 (MSA)。 這兩種機制都具有相同的功能，您可以選擇最適合您環境的方法。

在這兩種情況下，在先前步驟中建立的 SPN 都是必要項目，且必須在 Keytab 中註冊 SPN。

設定 SQL Server 服務 Keytab 檔案：

1. 在下一節中設定 [SPN Keytab 項目](#spn)。

1. 然後，遵循其各自章節中的步驟，在 Keytab 檔案中[新增UPN](#upn) (選項 1) 或 [MSA](#msa) (選項 2) 項目。

> [!IMPORTANT]
> 如果 UPN/MSA 的密碼已變更，或 SPN 指派目標帳戶的密碼已變更，您就必須使用新的密碼和金鑰版本號碼 (KVNO) 來更新 Keytab。 某些服務也可能會自動輪替密碼。 請檢閱前述帳戶的任何密碼輪替原則，並將它們與排程的維護活動配合，以避免產生非預期的停機時間。

### <a id="spn"></a> SPN Keytab 項目

1. 檢查上一個步驟中所建立的 AD 帳戶金鑰版本號碼 (KVNO)。 通常是 2，但如果您多次變更帳戶的密碼，則可能是另一個整數。 在 SQL Server 主機電腦上，請執行下列命令：

   ```bash
   kinit user@CONTOSO.COM
   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM
   ```

   > [!NOTE]
   > SPN 可能需要幾分鐘的時間才能傳播到您的網域，特別是當網域很大時。 如果您收到錯誤 (`kvno: Server not found in Kerberos database while getting credentials for MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM`)，請稍候幾分鐘，然後再試一次。  

1. 啟動 **ktutil**：

   ```bash
   sudo ktutil
   ```

1. 使用下列命令，為每個 SPN 新增 Keytab 項目：

   ```bash
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   ```

1. 將 Keytab 寫入檔案，然後結束 ktutil：

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

   > [!NOTE]
   > **ktutil** 工具不會驗證密碼，因此請務必在出現提示時正確輸入密碼。

### <a id="upn"></a> 選項 1：使用 UPN 來設定 Keytab

使用 **ktutil** 將電腦帳戶新增至您的 Keytab。 電腦帳戶 (也稱為 UPN) 會以 `<hostname>$@<realm.com>` 的格式 (例如 `sqlhost$@CONTOSO.COM`) 出現在 **/etc/krb5.keytab** 中。 請將這些項目從 **/etc/krb5.keytab** 複製到 **mssql.keytab**。

1. 使用下列命令來啟動 **ktuil**：

   ```bash
   sudo ktutil
   ```

1. 使用 **rkt** 命令來讀取 **/etc/krb5.keytab** 中的所有項目。

   ```bash
   rkt /etc/krb5.keytab
   ```

1. 接下來，列出這些項目。

   ```bash
   list
   ```

1. 依照不是 UPN 的位置編號來刪除所有項目。 請重複下列命令，一次刪除一個項目：

   ```bash
   delent <slot num>
   ```

   > [!IMPORTANT]
   > 當刪除項目 (例如位置 1) 時，所有值都會上移一個位置以取代其位置。 這表示在刪除位置 1 的項目時，位置 2 中的項目會移至位置 1。

1. 再次列出項目，直到只剩下 UPN 項目為止。

   ```bash
   list
   ```

1. 在只剩下 UPN 項目時，請將這些值附加到 **mssql.keytab**：

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   ```

1. 結束 **ktutil**。

   ```bash
   quit
   ```

### <a id="msa"></a> 選項 2：使用 MSA 來設定 Keytab

針對 MSA 選項，您必須建立 SQL Server 的 Kerberos Keytab。 它應該包含[第一個步驟中註冊的所有 SPN](#spn)，以及 SPN 註冊目標 MSA 的認證。 

1. 建立 SPN Keytab 項目之後，請從已加入網域的 Linux 電腦執行下列命令：

   ```bash
   kinit <AD user>
   kvno <any SPN registered in step 1>
      <spn>@CONTOSO.COM: kvno = <KVNO>
   ```

   此步驟會顯示已指派 SPN 擁有權之使用者帳戶的 KVNO。 為了讓此步驟正常執行，您必須在建立 SPN 時將其指派給 MSA 帳戶。 如果 SPN 未指派給 MSA，則顯示的 KVNO 將會是目前 SPN 擁有者帳戶，無法正確用於設定。  

1. 啟動 **ktutil**：

   ```bash
   sudo ktutil
   ```

1. 使用下列兩個命令來新增 MSA：

   ```bash
   addent -password -p <MSA> -k <kvno from command above> -e aes256-cts-hmac-sha1-96
   addent -password -p <MSA> -k <kvno from command above> -e rc4-hmac
   ```

1. 將 Keytab 寫入檔案，然後結束 ktutil：

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

1. 使用 MSA 方法時，必須使用 **mssql-conf** 工具來為設定選項進行設定，以指定在存取 Keytab 檔案時所要使用的 MSA。 請確定下列值位在 **/var/opt/mssql/mssql.conf** 中。

   ```bash
   sudo mssql-conf set network.privilegedadaccount <MSA_Name>
   ```

   > [!NOTE]
   > 只包含 MSA 名稱，而不包含網域\帳戶名稱。

## <a id="securekeytab"></a> 保護 Keytab 檔案

有權存取此 Keytab 檔案的任何人都可以在網域上模擬 SQL Server，因此請務必限制檔案的存取權，只讓 mssql 帳戶具有讀取權限：

```bash
sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
```

## <a id="keytabkerberos"></a> 設定 SQL Server 以使用 Keytab 檔案進行 Kerberos 驗證

使用下列步驟來設定 SQL Server，以開始使用 Keytab 檔案進行 Kerberos 驗證。

```bash
sudo mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
sudo systemctl restart mssql-server
```

選擇性地停用對網域控制站的 UDP 連線，以改善效能。 在許多情況下，連線到網域控制站時，UDP 連線會一直失敗，因此您可以在 **/etc/krb5.conf** 中針對設定選項進行設定以略過 UDP 呼叫。 請編輯 **/etc/krb5.conf** 並設定下列選項：

```/etc/krb5.conf
[libdefaults]
udp_preference_limit=0
```

此時，您已準備好在 SQL Server 中使用以 AD 為基礎的登入，如下所示。

## <a id="createsqllogins"></a> 在 Transact-SQL 中建立以 AD 為基礎的登入

1. 連線到 SQL Server 並建立以 AD 為基礎的新登入：

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

1. 確認登入現在已列在 [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) 系統目錄檢視中：

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a id="connect"></a> 使用 AD 驗證連線到 SQL Server

使用您的網域認證來登入用戶端電腦。 現在您可以使用 AD 驗證連線到 SQL Server，而不需要重新輸入密碼。 如果您建立 AD 群組的登入，則任何屬於該群組成員的 AD 使用者都可以使用相同方式進行連線。

用戶端要使用 AD 驗證時的特定連接字串參數，取決於您所使用的驅動程式。 請考慮下列各節中的範例。

### <a name="sqlcmd-on-a-domain-joined-linux-client"></a>已加入網域的 Linux 用戶端上 sqlcmd

使用 **SH** 和您的網域認證登入已加入網域的 Linux 用戶端：

```bash
ssh -l user@contoso.com client.contoso.com
```

請確定您已安裝 [mssql-tools](sql-server-linux-setup-tools.md) 套件，然後使用 **sqlcmd** 進行連線，而不指定任何認證：

```bash
sqlcmd -S mssql-host.contoso.com
```

### <a name="ssms-on-a-domain-joined-windows-client"></a>已加入網域的 Windows 用戶端上 SSMS

使用網域認證登入已加入網域的 Windows 用戶端。 請確定已安裝 SQL Server Management Studio，然後在 [連線到伺服器]  對話方塊中指定 [Windows 驗證]  ，以連線到您的 SQL Server 執行個體 (例如 `mssql-host.contoso.com`)。

### <a name="ad-authentication-using-other-client-drivers"></a>使用其他用戶端驅動程式的 AD 驗證

下表描述其他用戶端驅動程式的建議：

| 用戶端驅動程式 | 建議 |
|---|---|
| **JDBC** | 使用 Kerberos 整合式驗證來連接 SQL Server。 |
| **ODBC** | 使用整合式驗證。 |
| **ADO.NET** | 連接字串語法。 |

## <a id="additionalconfig"></a> 其他設定選項

如果您使用 [PBIS](https://www.beyondtrust.com/)、[VAS](https://www.oneidentity.com/products/authentication-services/) 或 [Centrify](https://www.centrify.com/) 等協力廠商公用程式將 Linux 主機加入AD 網域，且想要強制 SQL Server 直接使用 openldap 程式庫，您可以使用 **mssql-conf** 來設定 **disablesssd** 選項，如下所示：

```bash
sudo mssql-conf set network.disablesssd true
systemctl restart mssql-server
```

> [!NOTE]
> 有些公用程式 (例如**realmd**) 會設定 SSSD，而 PBIS、VAS 和 Centrify 之類的其他工具則不會設定 SSSD。 如果用來加入 AD 網域的公用程式未設定 SSSD，則建議您將 **disablesssd** 選項設定為 `true`。 雖然這不是必要項目，因為 SQL Server 會在回到 openldap 機制之前嘗試針對 AD 使用 SSSD，但設定此項會提高效能，因此 SQL Server 會直接進行 openldap 呼叫並略過 SSSD 機制。

如果您的網域控制站支援 LDAPS，您可以強制所有從 SQL Server 到網域控制站的連線都是透過 LDAPS 來進行。 若要檢查您的用戶端是否可以透過 LDAPS 與網域控制站連線，請執行下列 Bash 命令 `ldapsearch -H ldaps://contoso.com:3269`。 若要將 SQL Server 設定為只使用 LDAPS，請執行下列命令：

```bash
sudo mssql-conf set network.forcesecureldap true
systemctl restart mssql-server
```

如果主機上的 AD 網域加入作業是透過 SSSD 套件完成，且 **disablesssd** 未設定為 true，則這會使用 LDAPS 而非 SSSD。 如果 **disablesssd** 設定為 true，且 **forcesecureldap** 設定為 true，則會使用 LDAPS 通訊協定，而非由 SQL Server 所進行的 openldap 程式庫呼叫。

### <a name="post-sql-server-2017-cu14"></a>SQL Server 2017 CU14 之後

從 SQL Server 2017 CU14 開始，如果 SQL Server 已使用協力廠商提供者加入 AD 網域控制站，且已設定為使用 openldap 呼叫進行一般 AD 查閱 (方法是將 **disablesssd** 設定為 true)，您也可以使用 **enablekdcfromkrb5** 選項，強制 SQL Server 使用 krb5 程式庫進行 KDC 查閱，而不是 KDC 伺服器的反向 DNS 查閱。

當您想要手動設定 SQL Server 嘗試與其通訊的網域控制站時，這可能會很有用。 而且您可以使用 openldap 程式庫機制，方法是在 **krb5.conf** 中使用 KDC 清單。

首先，將 **disablessd** 和 **enablekdcfromkrb5conf** 設定為 true，然後重新啟動 SQL Server：

```bash
sudo mssql-conf set network.disablesssd true
sudo mssql-conf set network.enablekdcfromkrb5conf true
systemctl restart mssql-server
```

然後，在 **/etc/krb5.conf** 中設定 KDC 清單，如下所示：

```/etc/krb5.conf
[realms]
CONTOSO.COM = {
  kdc = dcWithGC1.contoso.com
  kdc = dcWithGC2.contoso.com
}
```

> [!NOTE]
> 雖然不建議這麼做，但您可以使用 **realmd** 之類的公用程式，在將 Linux 主機加入網域時設定 SSSD，同時將 **disablesssd** 設為 true，讓 SQL Server 使用 openldap 呼叫，而不是使用用於 Active Directory 相關呼叫的 SSSD。

## <a name="next-steps"></a>後續步驟

在本教學課程中，我們已逐步解說如何利用 Linux 上的 SQL Server 設定 Active Directory 驗證。 您已了解如何：
> [!div class="checklist"]
> * 將 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 主機加入 AD 網域
> * 建立用於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的 AD 使用者並設定 SPN
> * 設定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服務 Keytab
> * 在 Transact-SQL 中建立以 AD 為基礎的登入
> * 使用 AD 驗證連線到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]

接下來，請探索 Linux 上 SQL Server 的其他安全性案例。

> [!div class="nextstepaction"]
> [加密 Linux 上 SQL Server 的連線](sql-server-linux-encrypted-connections.md)
