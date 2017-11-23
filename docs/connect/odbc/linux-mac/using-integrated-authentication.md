---
title: "使用整合式的驗證 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: integrated authentication
ms.assetid: 9499ffdf-e0ee-4d3c-8bca-605371eb52d9
caps.latest.revision: "23"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 162b94d551ea8625b6b22fafec61e19038dc2051
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="using-integrated-authentication"></a>使用整合式驗證
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

[!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Linux 及 macOS 支援連線使用 Kerberos 整合式驗證。 它支援 MIT Kerberos 金鑰發佈中心 (KDC)，並可搭配一般安全性服務應用程式介面 (GSSAPI) 和 Kerberos v5 文件庫。
  
## <a name="using-integrated-authentication-to-connect-to-includessnoversionincludesssnoversionmdmd-from-an-odbc-application"></a>使用整合式的驗證連接到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]從 ODBC 應用程式  

您可以藉由啟用 Kerberos 整合式的驗證**Trusted_Connection = yes**的連接字串中**SQLDriverConnect**或**SQLConnect**。 例如：  

```
Driver='ODBC Driver 13 for SQL Server';Server=your_server;Trusted_Connection=yes  
```
  
連接時的 DSN，您也可以加入**Trusted_Connection = yes** DSN 中的項目`odbc.ini`。
  
`-E`選項`sqlcmd`和`-T`選項`bcp`也可用來指定整合式的驗證，請參閱 <<c8> [ 連接**sqlcmd** ](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)和[使用連接**bcp** ](../../../connect/odbc/linux-mac/connecting-with-bcp.md)如需詳細資訊。

確定要連接到的用戶端主體[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]向 Kerberos KDC 已經過驗證。
  
**ServerSPN** 和 **FailoverPartnerSPN** 不受支援。  
  
## <a name="deploying-a-linux-or-macos-odbc-driver-application-designed-to-run-as-a-service"></a>執行部署 Linux 或 macOS ODBC 驅動程式應用程式所設計，做為服務

系統管理員可以部署成服務，以使用 Kerberos 驗證連接到執行的應用程式[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。  
  
您首先要在用戶端上設定 Kerberos，然後確定 應用程式可以使用預設主體的 Kerberos 認證。

請確定您使用`kinit`或 PAM （插入式驗證模組） 來取得並快取連接所使用，透過下列方法之一主體的 TGT:  
  
-   執行`kinit`，傳入主體名稱和密碼。  
  
-   執行`kinit`，傳入主體名稱和包含主體金鑰所建立的 keytab 檔案的位置`ktutil`。  
  
-   請確定已完成登入系統使用 Kerberos PAM （插入式驗證模組）。

當應用程式執行為服務，因為 Kerberos 認證依設計會過期時，請更新認證，以確保持續的服務可用性。 ODBC 驅動程式不會更新認證本身;請確認有`cron`作業或以更新其到期時間之前的認證會定期執行的指令碼。 若要避免每次更新後需要密碼，您可以使用 keytab 檔案。  
  
[Kerberos 的設定和用法](http://commons.oreilly.com/wiki/index.php/Linux_in_a_Windows_World/Centralized_Authentication_Tools/Kerberos_Configuration_and_Use) 詳細說明如何在 Linux 上 Kerberize 服務。
  
## <a name="tracking-access-to-a-database"></a>追蹤對資料庫的存取

使用系統帳戶來存取時，資料庫管理員可以建立資料庫的存取權的稽核記錄[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]使用整合式驗證。  
  
登入[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]使用系統帳戶和 Linux 模擬安全性內容中沒有任何功能。 因此，需要有更多線索來判別使用者。
  
若要稽核中的活動[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]代表系統帳戶以外的使用者，應用程式必須使用[!INCLUDE[tsql](../../../includes/tsql_md.md)] **EXECUTE AS**。  
  
若要改善應用程式效能，應用程式可以將連接共用與整合式驗證和稽核搭配使用。 不過，結合連接共用，整合式驗證和稽核會產生安全性風險因為 unixODBC 驅動程式管理員允許不同的使用者重複使用共用的連接。 如需詳細資訊，請參閱 [ODBC 連接共用](http://www.unixodbc.org/doc/conn_pool.html)。  

重複使用之前，應用程式必須重設共用的連接執行`sp_reset_connection`。  

## <a name="using-active-directory-to-manage-user-identities"></a>使用 Active Directory 管理使用者身分識別

應用程式系統管理員不需要管理不同的登入認證集[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。 Active Directory 可以設定為整合式驗證的金鑰發佈中心 (KDC)。 請參閱[Microsoft Kerberos](https://msdn.microsoft.com/en-us/library/windows/desktop/aa378747(v=vs.85).aspx)如需詳細資訊。

## <a name="using-linked-server-and-distributed-queries"></a>使用連結的伺服器和分散式查詢

開發人員可以部署使用連結的伺服器或分散式查詢的應用程式，而無需資料庫管理員負責維護個別的 SQL 認證集。 在此情況下，開發人員必須設定應用程式使用整合式的驗證：  
  
-   使用者登入用戶端電腦，並向應用程式伺服器進行驗證。  
  
-   應用程式伺服器會驗證為不同的資料庫，並連接到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]另一個資料庫的資料庫使用者身分進行驗證 ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。  
  
在設定整合式驗證之後，認證將會傳遞至連結的伺服器。  
  
## <a name="integrated-authentication-and-sqlcmd"></a>整合式驗證和 sqlcmd
若要存取[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]使用整合式的驗證時，使用`-E`選項`sqlcmd`。 請確定其執行的帳戶`sqlcmd`與預設的 Kerberos 用戶端主體相關聯。

## <a name="integrated-authentication-and-bcp"></a>整合式驗證和 bcp
若要存取[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]使用整合式的驗證時，使用`-T`選項`bcp`。 請確定其執行的帳戶`bcp`與預設的 Kerberos 用戶端主體相關聯。 
  
它是使用錯誤`-T`與`-U`或`-P`選項。
  
## <a name="supported-syntax-for-an-spn-registered-by-includessnoversionincludesssnoversionmdmd"></a>支援註冊的 SPN 語法[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]

Spn 在連接字串或連接屬性中所使用的語法如下所示：  

|語法|描述|  
|----------|---------------|  
|MSSQLSvc/*fqdn*:*port*|使用 TCP 時，此為提供者產生的預設 SPN。 *port* 是 TCP 通訊埠編號。 *fqdn* 是完整的網域名稱。|  
  
## <a name="authenticating-a-linux-or-macos-computer-with-active-directory"></a>Linux 或 macOS 電腦與 Active Directory 驗證

若要設定 Kerberos，輸入資料`krb5.conf`檔案。 `krb5.conf`處於`/etc/`但您可以參考另一個檔案，例如使用語法`export KRB5_CONFIG=/home/dbapp/etc/krb5.conf`。 下列是範例`krb5.conf`檔案：  
  
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
  
如果您的 Linux 或 macOS 電腦設定為使用動態主機設定通訊協定 (DHCP) 與 Windows DHCP 伺服器提供的 DNS 伺服器使用，您可以使用**dns_lookup_kdc = true**。 現在，您可以使用 Kerberos 來發出命令登入您的網域`kinit alias@YYYY.CORP.CONTOSO.COM`。 參數傳遞給`kinit`會區分大小寫和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]設定為網域中的電腦必須具有該使用者`alias@YYYY.CORP.CONTOSO.COM`加入登入。 現在，您可以使用信任的連接 (**Trusted_Connection = YES**在連接字串中， **bcp-T**，或**sqlcmd-E**)。  
  
Linux 或 macOS 電腦上的時間和 Kerberos 金鑰發佈中心 (KDC) 上的時間必須關閉。 請確認您的系統時間已正確設定，例如使用網路時間通訊協定 (NTP)。  

如果 Kerberos 驗證失敗，ODBC driver on Linux 或 macOS 不使用 NTLM 驗證。  

如需驗證與 Active Directory 的 Linux 或 macOS 電腦的詳細資訊，請參閱[與 Active Directory 驗證 Linux 用戶端](http://technet.microsoft.com/magazine/2008.12.linux.aspx#id0060048)和[與 Active Directory整合OSX的最佳作法](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf). 如需有關設定 Kerberos 的詳細資訊，請參閱[MIT Kerberos 文件](https://web.mit.edu/kerberos/krb5-1.12/doc/index.html)。

## <a name="see-also"></a>請參閱＜  
[程式設計指導方針](../../../connect/odbc/linux-mac/programming-guidelines.md)

[版本資訊](../../../connect/odbc/linux-mac/release-notes.md)

[使用 Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md)
