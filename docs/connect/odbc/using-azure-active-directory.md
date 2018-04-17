---
title: ODBC 驅動程式搭配使用 Azure Active Directory |SQL Server 的 Microsoft 文件
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 52205f03-ff29-4254-bfa8-07cced155c86
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5536acb053dbb7dd934150e797a2ba6bc38d9ffd
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/05/2018
---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>使用 Azure Active Directory 的 ODBC 驅動程式
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>目的

Microsoft ODBC Driver for SQL Server 版本 13.1 或以上版本可讓 ODBC 應用程式連接到 SQL Azure 的執行個體與使用者名稱/密碼、 Azure Active Directory 存取權杖或 Windows 使用 Azure Active Directory 中的同盟識別身分整合式驗證 (_Windows 驅動程式只_)。 ODBC driver 13.1，Azure Active Directory 存取權杖驗證版本_僅限 Windows_。 ODBC Diver 17 和 17.1 版支援此驗證，跨所有平台 （Windows、 Linux 和 Mac）。 適用於 Windows 中的 ODBC 驅動程式版本 17.1 引進新 Azure Active Directory 互動式驗證與登入識別碼。 它們都是透過使用新的資料來源名稱和連接字串關鍵字和連接屬性來完成。

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>新增及/或修改過的資料來源名稱和連接字串關鍵字

`Authentication`關鍵字可用於使用 DSN 或連接字串進行連接時控制的驗證模式。 設定連接字串中的值會覆寫，在 DSN 中，如果有提供。 _屬性值的預先_的`Authentication`設定是從連接字串和 DSN 值計算的值。

|名稱|值|預設值|Description|
|-|-|-|-|
|`Authentication`|（未設定） （空字串）、 `SqlPassword`， `ActiveDirectoryPassword`， `ActiveDirectoryIntegrated`， `ActiveDirectoryInteractive`|(未設定)|控制驗證模式。<table><tr><th>Value<th>Description<tr><td>(未設定)<td>驗證模式取決於其他關鍵字 （現有傳統的連線選項）。<tr><td>(空字串)<td>（只有連接字串。）覆寫並取消設定`Authentication`DSN 中的設定值。<tr><td>`SqlPassword`<td>直接驗證使用者名稱和密碼的 SQL Server 執行個體。<tr><td>`ActiveDirectoryPassword`<td>以 Azure Active Directory 識別身分的使用者名稱及密碼進行驗證。<tr><td>`ActiveDirectoryIntegrated`<td>_只有 Windows 驅動程式_。 使用 Azure Active Directory 識別身分，使用整合式的驗證進行驗證。<tr><td>`ActiveDirectoryInteractive`<td>_只有 Windows 驅動程式_。 向 Azure Active Directory 識別身分，使用互動式的驗證。</table>|
|`Encrypt`|（未設定）， `Yes`， `No`|（請參閱說明）|控制連接的加密。 如果前屬性值的`Authentication`未設定_無_，預設值是`Yes`。 否則，預設值是`No`。 前屬性值的加密是`Yes`如果值設定為`Yes`DSN 或連接字串中。|

## <a name="new-andor-modified-connection-attributes"></a>新增及/或修改連接屬性

下列預先連接屬性已導入了或修改為支援 Azure Active Directory 驗證連線。 當連接屬性都有對應的連接字串或 DSN 關鍵字，且設定時，「 連接 」 屬性會優先使用。

|Attribute|型別|值|預設值|Description|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`, `SQL_AU_PASSWORD`, `SQL_AU_AD_INTEGRATED`, `SQL_AU_AD_PASSWORD`, `SQL_AU_AD_INTERACTIVE`, `SQL_AU_RESET`|(未設定)|請參閱描述`Authentication`上述的關鍵字。 `SQL_AU_NONE` 提供以明確覆寫一組`Authentication`DSN 和/或連接字串中的值時`SQL_AU_RESET`取消設定屬性，如果它已設定，以較高的優先順序的 DSN 或連接字串值。|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|指標`ACCESSTOKEN`或 NULL|NULL|如果不是 null，指定 azure Ad 存取權杖來使用。 它會指定存取權杖以及`UID`， `PWD`， `Trusted_Connection`，或`Authentication`連接字串關鍵字或其相等的屬性。 <br> **注意：** ODBC Driver 13.1 版本只支援這上_Windows_。|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`, `SQL_EN_ON`|（請參閱說明）|控制連接的加密。 `SQL_EN_OFF` 和`SQL_EN_ON`停用和啟用加密，分別。 如果前屬性值的`Authentication`未設定_無_或`SQL_COPT_SS_ACCESS_TOKEN`設定，和`Encrypt`未指定在 DSN 或連接字串中，預設值是`SQL_EN_ON`。 否則，預設值是`SQL_EN_OFF`。 這個屬性會控制的有效值[是否使用加密連接。](https://docs.microsoft.com/en-us/sql/relational-databases/native-client/features/using-encryption-without-validation)|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|不支援與 Azure Active Directory，因為無法完成密碼變更到 AAD 主體透過 ODBC 連接。 <br><br>SQL Server 2005 中引進了 SQL Server 驗證的密碼到期日。 `SQL_COPT_SS_OLDPWD`屬性已加入，以允許用戶端連接提供舊的和新的密碼。 設定這個屬性之後，提供者將不會針對第一次連接或後續連接使用連接集區，因為連接字串將會包含已經變更的「舊密碼」。|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`,`SQL_IS_ON`|`SQL_IS_OFF`|_已被取代_; 使用`SQL_COPT_SS_AUTHENTICATION`設`SQL_AU_AD_INTEGRATED`改為。 <br><br>強制使用 Windows 驗證 (在 Linux 和 macOS Kerberos) 的伺服器登入存取驗證。 使用 Windows 驗證時，驅動程式會忽略使用者識別碼和密碼值的一部分`SQLConnect`， `SQLDriverConnect`，或`SQLBrowseConnect`處理。|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>新增 Azure Active Directory （Windows 驅動程式只） UI 項目

DSN 設定和連接的 Ui 驅動程式的已增強，以使用驗證搭配 Azure AD 所需的其他選項。

### <a name="creating-and-editing-dsns-in-the-ui"></a>建立和編輯在 UI 中的名稱 （dsn）

它可能會使用新的 Azure AD 驗證選項建立時或編輯使用驅動程式的安裝程式 UI 的現有資料來源名稱：

`Authentication=ActiveDirectoryIntegrated` Azure Active Directory 整合到 SQL Azure 驗證

![CreateNewDSN_ADIntegrated.png](windows/CreateNewDSN_ADIntegrated.png)

`Authentication=ActiveDirectoryPassword` SQL Azure 的 Azure Active Directory 使用者名稱/密碼驗證

![CreateNewDSN_ADPassword.png](windows/CreateNewDSN_ADPassword.png)

`Authentication=ActiveDirectoryInteractive` Azure Active Directory 互動式驗證 SQL Azure

![CreateNewDSN_ADInteractive.png](windows/CreateNewDSN_ADInteractive.png)

`Authentication=SqlPassword` SQL server 的使用者名稱/密碼驗證 （Azure 或其他）

![CreateNewDSN_SQLServer.png](windows/CreateNewDSN_SQLServer.png)

`Trusted_Connection=Yes` 適用於 Windows 舊版 SSPI 整合式驗證

![CreateNewDSN_winSSPI.png](windows/CreateNewDSN_winSSPI.png)

五個選項對應至`Trusted_Connection=Yes`(現有舊版的 Windows SSPI 專用的整合式驗證) 和`Authentication=` `ActiveDirectoryIntegrated`， `SqlPassword`， `ActiveDirectoryPassword`，和`ActiveDirectoryInteractive`分別。

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>SQLDriverConnect 提示 （僅 Windows 驅動程式）

SQLDriverConnect 要求完成整個連接時所需的資訊時顯示提示對話方塊包含三個新的 Azure AD 驗證的選項：

![ServerLogin.png](windows/ServerLogin.png)

這些選項會對應至相同的五個 DSN 安裝程式 UI 的上方。

### <a name="example-connection-strings"></a>範例連接字串
1. SQL Server 驗證 – 舊版的語法。 不會驗證伺服器憑證，和伺服器會強制執行它時，才會使用加密。 使用者名稱/密碼會在連接字串中傳遞。
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. SQL 驗證 – 新的語法。 用戶端要求加密 (預設值的`Encrypt`是`true`) 和伺服器憑證取得驗證，而不論加密設定 (除非`TrustServerCertificate`設`true`)。 使用者名稱/密碼會在連接字串中傳遞。
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. 整合式 Windows 驗證 (Kerberos Linux 及 macOS) 使用 SSPI （到 SQL Server 或 SQL IaaS）-目前的語法。 不驗證伺服器憑證，除非使用加密。 
`server=Server;database=Database;Trusted_Connection=yes;`
4. (_Windows 驅動程式只_。)整合式 Windows 驗證使用 SSPI （如果目標資料庫在 SQL Server 或 SQL IaaS） – 新的語法。 用戶端要求加密 (預設值的`Encrypt`是`true`) 和伺服器憑證取得驗證，而不論加密設定 (除非`TrustServerCertificate`設`true`)。 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. AAD 的使用者名稱/密碼驗證 （如果目標資料庫是在 Azure SQL DB）。 取得驗證伺服器憑證，不論加密設定 (除非`TrustServerCertificate`設`true`)。 使用者名稱/密碼會在連接字串中傳遞。 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_Windows 驅動程式只_。)使用 ADAL，這牽涉到兌換 AAD 發出存取權杖的 Windows 帳戶認證，假設目標資料庫 Azure SQL Database 中的整合式的 Windows 驗證。 取得驗證伺服器憑證，不論加密設定 (除非`TrustServerCertificate`設`true`)。 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
7. (_Windows 驅動程式只_。)AAD 互動式驗證使用 Azure multi-factor Authentication 技術來設定連線。 在此模式中，藉由提供登入識別碼，會觸發 Windows Azure 驗證對話方塊，並可讓使用者輸入密碼，以完成連線。 使用者名稱會在連接字串中傳遞。
`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

![WindowsAzureAuth.png](windows/WindowsAzureAuth.png)

> [!NOTE] 
>- 當您可以使用 新的 Active Directory 選項與 Windows ODBC 驅動程式，請確認[for SQL Server 的 Active Directory Authentication Library](http://go.microsoft.com/fwlink/?LinkID=513072)已安裝。 Linux 及 macOS 驅動程式不需要任何其他相依性來與 Azure Active Directory 驗證。
>- 若要使用的 SQL Server 帳戶的使用者名稱和密碼進行連接，您現在可以使用新`SqlPassword`選項，建議使用，特別是針對 SQL Azure 因為這個選項可讓更安全連接的預設值。
>- 若要使用的 Azure Active Directory 帳戶使用者名稱和密碼進行連接，指定`Authentication=ActiveDirectoryPassword`在連接字串和`UID`和`PWD`關鍵字的使用者名稱與密碼，分別。
>- 若要使用 Windows 整合式驗證或 Active Directory 整合式 （Windows 驅動程式只） 驗證進行連接，指定`Authentication=ActiveDirectoryIntegrated`連接字串中。 驅動程式會自動選擇正確的驗證模式。 `UID` 和`PWD`不可指定。
>- 若要使用 Active Directory 互動 （Windows 驅動程式只） 驗證，連接`UID`必須指定。

## <a name="authenticating-with-an-access-token"></a>使用存取權杖來進行驗證

`SQL_COPT_SS_ACCESS_TOKEN`預先連接屬性可讓您從 Azure AD 進行驗證，而不是使用者名稱和密碼，取得存取權杖使用，也會略過，交涉並取得存取權杖的驅動程式。 若要使用存取權杖，`SQL_COPT_SS_ACCESS_TOKEN`連接屬性，以便指向`ACCESSTOKEN`結構：

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

`ACCESSTOKEN`所組成，一個 4 位元組的可變長度結構_長度_後面_長度_表單的存取權杖的不透明資料的位元組。 其中一個透過由於 SQL Server 如何處理存取權杖，取得[OAuth 2.0](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-authentication-scenarios)必須展開 JSON 回應，使每個位元組後面是 0，填補位元組，以包含 ASCII 字元的 ucs-2 字串類似; 不過，語彙基元不透明值，指定，以位元組為單位的長度不能包含任何 null 結束字元。 由於其相當大的長度和格式的限制，這種驗證方法才可用以程式設計方式透過`SQL_COPT_SS_ACCESS_TOKEN`coonnection 屬性; 沒有對應的 DSN 或連接字串關鍵字。 連接字串必須包含`UID`， `PWD`， `Authentication`，或`Trusted_Connection`關鍵字。

> [!NOTE]
> ODBC Driver 13.1 版本只支援此驗證上_Windows_。

## <a name="azure-active-directory-authentication-sample-code"></a>Azure Active Directory 驗證的範例程式碼

下列範例顯示連接到 SQL Server 所需的程式碼使用 Azure Active Directory 與連接關鍵字。 請注意，不需要變更應用程式程式碼本身。連接字串或如果使用其中一種資料來源名稱是唯一使用 AAD 進行驗證所需的修改：
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    ...
~~~
下列範例將示範使用 Azure Active Directory 存取權杖的驗證與連接到 SQL Server 所需的程式碼。 在此情況下，就必須修改應用程式程式碼來處理存取權杖，並將相關聯的連接屬性。
~~~
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server}"
    SQLCHAR accessToken[] = "eyJ0eXAiOi..."; // In the format extracted from an OAuth JSON response
    ...
    DWORD dataSize = 2 * strlen(accessToken);
    ACCESSTOKEN *pAccToken = malloc(sizeof(ACCESSTOKEN) + dataSize);
    pAccToken->dataSize = dataSize;
    // Expand access token with padding bytes
    for(int i = 0, j = 0; i < dataSize; i += 2, j++) {
        pAccToken->data[i] = accessToken[j];
        pAccToken->data[i+1] = 0;
    }
    ...
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_ACCESS_TOKEN, (SQLPOINTER)pAccToken, SQL_IS_POINTER);
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);      
    ...
    free(pAccToken);
~~~
以下是與 Azure Active Directory 互動式驗證搭配使用的範例連接字串。 請注意，它不包含 PWD 欄位，會使用 Windows Azure 驗證 畫面上輸入密碼。
~~~
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myuser;Authentication=ActiveDirectoryInteractive"
~~~

## <a name="see-also"></a>另請參閱
[權杖型驗證使用 Azure AD 驗證的 Azure SQL DB 支援](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)

