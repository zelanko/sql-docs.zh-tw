---
title: 使用整合式驗證 | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- integrated authentication
ms.assetid: 9499ffdf-e0ee-4d3c-8bca-605371eb52d9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 034df879dc79f920219a43e2faaaf0e3ac4fc17b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008698"
---
# <a name="using-integrated-authentication"></a>使用整合式驗證
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Linux 和 macOS 上的 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援使用 Kerberos 整合驗證的連線。 其支援 MIT Kerberos 金鑰發佈中心 (KDC) 並可使用一般安全性服務應用程式開發介面 (GSSAPI) 和 Kerberos v5 程式庫。
  
## <a name="using-integrated-authentication-to-connect-to-includessnoversionincludesssnoversion-mdmd-from-an-odbc-application"></a>使用整合驗證從 ODBC 應用程式連線至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  

您可以透過在 **SQLDriverConnect** 或 **SQLConnect** 的連接字串中指定 **Trusted_Connection=yes**，來啟用 Kerberos 整合驗證。 例如：  

```
Driver='ODBC Driver 13 for SQL Server';Server=your_server;Trusted_Connection=yes  
```
  
使用 DSN 連線時，您也可以將 **Trusted_Connection = yes** 新增至 `odbc.ini` 中的 DSN 項目。
  
`sqlcmd` 的 `-E` 選項和 `bcp` 的 `-T` 選項也可以用來指定整合式驗證；如需詳細資訊，請參閱[使用 **sqlcmd** 進行連線](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)和[使用 **bcp** 進行連線](../../../connect/odbc/linux-mac/connecting-with-bcp.md)。

請確定要連線到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的用戶端主體已經過 Kerberos KDC 驗證。
  
**ServerSPN** 和 **FailoverPartnerSPN** 不受支援。  
  
## <a name="deploying-a-linux-or-macos-odbc-driver-application-designed-to-run-as-a-service"></a>部署設計成以服務的形式執行的 Linux 或 macOS ODBC Driver 應用程式

系統管理員可部署應用程式，以作為使用 Kerberos 驗證連線至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的服務執行。  
  
您必須先在用戶端上設定 Kerberos，然後確定應用程式可使用預設主體的 Kerberos 認證。

請確定您透過以下其中一種方法，使用 `kinit` 或 PAM (插入式驗證模組) 獲取並快取連線使用的主體 TGT：  
  
-   執行 `kinit`，傳入主體名稱和密碼。  
  
-   執行 `kinit`，傳入主體名稱，以及包含 `ktutil` 所建立主體金鑰的 keytab 檔案位置。  
  
-   確定系統登入作業使用 Kerberos PAM (插入式驗證模組) 所完成。

當應用程式作為服務執行時，因為 Kerberos 認證依設計到期，請更新認證以確保服務可持續使用。 ODBC 驅動程式不會自行更新；請確定有定期執行的 `cron` 作業或指令碼會在認證到期之前加以更新。 若不想在每次進行此更新時都需要密碼，您可以使用 keytab 檔案。  
  
[Kerberos 的設定和用法](https://commons.oreilly.com/wiki/index.php/Linux_in_a_Windows_World/Centralized_Authentication_Tools/Kerberos_Configuration_and_Use) 詳細說明如何在 Linux 上 Kerberize 服務。
  
## <a name="tracking-access-to-a-database"></a>追蹤對資料庫的存取

使用系統帳戶透過整合式驗證存取 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時，資料庫管理員可以建立資料庫存取的稽核記錄。  
  
登入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時會使用系統帳戶，但 Linux 上並沒有模擬安全性內容的功能。 因此，需要有更多線索來判別使用者。
  
若要代表系統帳戶以外的使用者稽核 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的活動，應用程式必須使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] **EXECUTE AS**。  
  
若要改善應用程式效能，應用程式可以將連接共用與整合式驗證和稽核搭配使用。 不過，結合連線共用、整合驗證和稽核會產生安全性風險，原因是 unixODBC 驅動程式管理員允許不同使用者重複使用共用連線。 如需詳細資訊，請參閱 [ODBC 連接共用](http://www.unixodbc.org/doc/conn_pool.html)。  

在重複使用前，應用程式必須執行 `sp_reset_connection` 來重設共用連線。  

## <a name="using-active-directory-to-manage-user-identities"></a>使用 Active Directory 管理使用者身分識別

應用程式系統管理員不需要管理個別的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]登入認證集。 Active Directory 可以設定為整合式驗證的金鑰發佈中心 (KDC)。 如需詳細資訊，請參閱 [Microsoft Kerberos](/windows/desktop/SecAuthN/microsoft-kerberos)。

## <a name="using-linked-server-and-distributed-queries"></a>使用連結的伺服器和分散式查詢

開發人員可以部署使用連結的伺服器或分散式查詢的應用程式，而無需資料庫管理員負責維護個別的 SQL 認證集。 在此情況下，開發人員必須設定應用程式以使用整合驗證：  
  
-   使用者登入用戶端電腦，並向應用程式伺服器進行驗證。  
  
-   應用程式伺服器驗證為不同的資料庫，並連線到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會向另一個資料庫驗證為資料庫使用者 ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
在設定整合式驗證之後，認證將會傳遞至連結的伺服器。  
  
## <a name="integrated-authentication-and-sqlcmd"></a>整合式驗證和 sqlcmd
若要使用整合驗證存取 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，請使用 `sqlcmd` 的 `-E` 選項。 請確定執行 `sqlcmd` 的帳戶與預設的 Kerberos 用戶端主體建立關聯。

## <a name="integrated-authentication-and-bcp"></a>整合式驗證和 bcp
若要使用整合驗證存取 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，請使用 `bcp` 的 `-T` 選項。 請確定執行 `bcp` 的帳戶與預設的 Kerberos 用戶端主體建立關聯。 
  
`-T` 與 `-U` 或 `-P` 選項搭配使用是錯誤的。
  
## <a name="supported-syntax-for-an-spn-registered-by-includessnoversionincludesssnoversion-mdmd"></a>由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 註冊之 SPN 的支援語法

SPN 在連接字串或連線屬性中使用的語法如下：  

|語法|Description|  
|----------|---------------|  
|MSSQLSvc/*fqdn*:*port*|使用 TCP 時，此為提供者產生的預設 SPN。 *port* 是 TCP 通訊埠編號。 *fqdn* 是完整的網域名稱。|  
  
## <a name="authenticating-a-linux-or-macos-computer-with-active-directory"></a>使用 Active Directory 驗證 Linux 或 macOS 電腦

若要設定 Kerberos，請輸入資料到 `krb5.conf` 檔案。 `krb5.conf` 位於 `export KRB5_CONFIG=/home/dbapp/etc/krb5.conf` 中，但是您可以使用語法範例 `/etc/` 參考另一個檔案。 下列為 `krb5.conf` 檔案範例：  
  
```  
[libdefaults]  
default_realm = YYYY.CORP.CONTOSO.COM  
dns_lookup_realm = false  
dns_lookup_kdc = true  
ticket_lifetime = 24h  
forwardable = yes  
  
[domain_realm]  
.yyyy.corp.contoso.com = YYYY.CORP.CONTOSO.COM  
.zzzz.corp.contoso.com = ZZZZ.CORP.CONTOSO.COM  
```  
  
如果您的 Linux 或 macOS 電腦設定為使用動態主機設定通訊協定 (DHCP)，且 Windows DHCP 伺服器提供 DNS 伺服器來使用，則您可以使用 **dns_lookup_kdc=true**。 現在，您可以發出命令 `kinit alias@YYYY.CORP.CONTOSO.COM`，使用 Kerberos 登入您的網域。 傳遞至 `kinit` 的參數會區分大小寫，且設定要在網域中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 電腦必須新增該使用者 `alias@YYYY.CORP.CONTOSO.COM` 以供登入之用。 現在，您可以使用信任連接 (連接字串中的  、**bcp -T** 或 **sqlcmd -E**)。  
  
Linux 或 macOS 電腦上時間與 Kerberos 金鑰發佈中心 (KDC) 上的時間必須很接近。 請確認您的系統時間設定正確，例如使用 Network Time Protocol (NTP)。  

如果 Kerberos 驗證失敗， Linux 或 macOS 上的 ODBC 驅動程式不會使用 NTLM 驗證。  

如需使用 Active Directory 驗證 Linux 或 macOS 電腦的詳細資訊，請參閱[使用 Active Directory 驗證 Linux 用戶端](https://technet.microsoft.com/magazine/2008.12.linux.aspx#id0060048)和[整合 OS X 與 Active Directory 的最佳做法](https://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf)。 如需設定 Kerberos 的詳細資訊，請參閱 [MIT Kerberos 文件](https://web.mit.edu/kerberos/krb5-1.12/doc/index.html)。

## <a name="see-also"></a>另請參閱  
[程式設計指導方針](../../../connect/odbc/linux-mac/programming-guidelines.md)

[版本資訊](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)

[使用 Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md)
