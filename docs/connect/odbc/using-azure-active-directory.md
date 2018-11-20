---
title: 使用 ODBC 驅動程式使用 Azure Active Directory |適用於 SQL Server 的 Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 52205f03-ff29-4254-bfa8-07cced155c86
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 949ae2e19279db895ca9bca1441f06c2b2d8948f
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51604098"
---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>搭配 ODBC 驅動程式使用 Azure Active Directory
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>目的

Microsoft ODBC Driver for SQL Server 使用 13.1 版或更新可讓 ODBC 應用程式連接到 SQL Azure 的執行個體使用 Azure Active Directory 中的同盟識別身分，使用使用者名稱/密碼、 Azure Active Directory 存取權杖或 Windows整合式驗證 (_Windows 驅動程式只_)。 ODBC driver 13.1 版，權杖驗證是 Azure Active Directory 存取權_只有 Windows_。 ODBC 驅動程式第 17 版和以上支援此驗證跨所有平台 （Windows、 Linux 和 Mac）。 新的 Azure Active Directory 互動式驗證與登入識別碼是 Windows 推出 17.1 版本的 ODBC 驅動程式。 所有這些是在透過使用新的 DSN 和連接字串關鍵字和連接屬性來完成。

> [!NOTE]
> ODBC Driver on Linux 和 macOS 不支援 Active Directory Federation Services。 如果您使用 Azure Active Directory 使用者名稱/密碼驗證，從 Linux 或 macOS 用戶端與您的 Active Directory 設定包含同盟服務，驗證可能會失敗。

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>新增和/或修改過的資料來源名稱和連接字串關鍵字

`Authentication`關鍵字可用於使用 DSN 或連接字串進行連接時控制的驗證模式。 設定連接字串中的值覆寫 DSN 中如果有提供。 _屬性值的預先_的`Authentication`設定是從連接字串和資料來源名稱值所計算的值。

|[屬性]|值|預設|Description|
|-|-|-|-|
|`Authentication`|（未設定），（空字串）、 `SqlPassword`， `ActiveDirectoryPassword`， `ActiveDirectoryIntegrated`， `ActiveDirectoryInteractive`|(未設定)|控制驗證模式。<table><tr><th>ReplTest1<th>Description<tr><td>(未設定)<td>驗證模式取決於其他關鍵字 （現有舊版連線選項）。<tr><td>(空字串)<td>連接字串是: "{0}"覆寫並取消設定`Authentication`DSN 中的設定值。<tr><td>`SqlPassword`<td>直接驗證使用者名稱和密碼的 SQL Server 執行個體。<tr><td>`ActiveDirectoryPassword`<td>使用 Azure Active Directory 身分識別的使用者名稱和密碼進行驗證。<tr><td>`ActiveDirectoryIntegrated`<td>_Windows 驅動程式只_。 使用 Azure Active Directory 身分識別使用整合式的驗證進行驗證。<tr><td>`ActiveDirectoryInteractive`<td>_Windows 驅動程式只_。 使用 Azure Active Directory 身分識別使用互動式驗證進行驗證。</table>|
|`Encrypt`|(未設定)、`Yes`、`No`|（請參閱描述）|控制連接的加密。 如果前的屬性值`Authentication`未設定_無_DSN 或連接字串中，預設值是`Yes`。 否則預設為 `No`。 如果屬性`SQL_COPT_SS_AUTHENTICATION`前的屬性值會覆寫`Authentication`，明確地設定 DSN 或連接字串或連接屬性中的加密值。 加密前的屬性值是`Yes`值設定為如果`Yes`DSN 或連接字串中。|

## <a name="new-andor-modified-connection-attributes"></a>新增和/或修改連接屬性

下列預先連接屬性已導入或修改，以支援 Azure Active Directory 驗證連線。 當連接屬性都有對應的連接字串或 DSN 關鍵字，且設定時，連接屬性的優先順序較高。

|attribute|類型|值|預設|Description|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`、`SQL_AU_PASSWORD`、`SQL_AU_AD_INTEGRATED`、`SQL_AU_AD_PASSWORD`、`SQL_AU_AD_INTERACTIVE`、`SQL_AU_RESET`|(未設定)|請參閱說明`Authentication`上述的關鍵字。 `SQL_AU_NONE` 提供以明確覆寫一組`Authentication`值在 DSN 和/或連接字串中，雖然`SQL_AU_RESET`取消設定此屬性，如果它已設定，讓較高的優先順序的 DSN 或連接字串值。|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|指標`ACCESSTOKEN`或 NULL|NULL|如果不是 null，會指定 azure Ad 存取權杖來使用。 它會指定存取權杖，也`UID`， `PWD`， `Trusted_Connection`，或`Authentication`連接字串關鍵字或其對等的屬性。 <br> **注意︰** ODBC Driver 13.1 版僅支援這上_Windows_。|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`, `SQL_EN_ON`|（請參閱描述）|控制連接的加密。 `SQL_EN_OFF` 和`SQL_EN_ON`停用和啟用加密，分別。 如果前的屬性值`Authentication`未設定_無_或`SQL_COPT_SS_ACCESS_TOKEN`設定，並`Encrypt`中未指定的 DSN 」 或 「 連接字串，預設值是`SQL_EN_ON`。 否則預設為 `SQL_EN_OFF`。 如果連接屬性`SQL_COPT_SS_AUTHENTICATION`設定為不_無_，明確地設定`SQL_COPT_SS_ENCRYPT`所要的值如果`Encrypt`DSN 或連接字串中未指定。 此屬性可控制的有效值[是否使用加密連接。](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation)|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|不支援與 Azure Active Directory，因為 AAD 主體的密碼變更，無法透過 ODBC 連接來完成。 <br><br>SQL Server 驗證的密碼逾期已在 SQL Server 2005 中推出。 `SQL_COPT_SS_OLDPWD`屬性已新增至允許用戶端提供連線的舊和新的密碼。 設定這個屬性之後，提供者將不會針對第一次連接或後續連接使用連接集區，因為連接字串將會包含已經變更的「舊密碼」。|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`、`SQL_IS_ON`|`SQL_IS_OFF`|_已被取代_; 使用`SQL_COPT_SS_AUTHENTICATION`設定為`SQL_AU_AD_INTEGRATED`改。 <br><br>強制使用 Windows 驗證 (在 Linux 和 macOS 上的 Kerberos) 的伺服器登入的存取驗證。 使用 Windows 驗證時，驅動程式會忽略使用者識別碼和密碼值的一部分`SQLConnect`， `SQLDriverConnect`，或`SQLBrowseConnect`處理。|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>新增 Azure Active Directory （Windows 驅動程式只） UI 項目

DSN 設定和連接 Ui 的驅動程式已增強，以使用與 Azure AD 的驗證所需的其他選項。

### <a name="creating-and-editing-dsns-in-the-ui"></a>建立和編輯 UI 中的名稱 （dsn）

您可使用新的 Azure AD 驗證選項時建立或編輯現有的 DSN 使用驅動程式的安裝程式 UI:

`Authentication=ActiveDirectoryIntegrated` 表示對 SQL Azure 進行 Azure Active Directory 整合式驗證

![CreateNewDSN_ADIntegrated.png](windows/CreateNewDSN_ADIntegrated.png)

`Authentication=ActiveDirectoryPassword` SQL Azure 的 Azure Active Directory 使用者名稱/密碼驗證

![CreateNewDSN_ADPassword.png](windows/CreateNewDSN_ADPassword.png)

`Authentication=ActiveDirectoryInteractive` 表示對 SQL Azure 進行 Azure Active Directory 互動式驗證

![CreateNewDSN_ADInteractive.png](windows/CreateNewDSN_ADInteractive.png)

`Authentication=SqlPassword` SQL server 的使用者名稱/密碼驗證 （Azure 或其他方式）

![CreateNewDSN_SQLServer.png](windows/CreateNewDSN_SQLServer.png)

`Trusted_Connection=Yes` 針對 Windows 舊版 SSPI 整合式驗證

![CreateNewDSN_winSSPI.png](windows/CreateNewDSN_winSSPI.png)

五個選項會對應至`Trusted_Connection=Yes`(現有舊版 Windows SSPI 專用的整合式驗證) 和`Authentication=` `ActiveDirectoryIntegrated`， `SqlPassword`， `ActiveDirectoryPassword`，和`ActiveDirectoryInteractive`分別。

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>SQLDriverConnect 提示 （僅 Windows 驅動程式）

提示要求完成整個連接時所需的資訊時，SQLDriverConnect 所顯示的對話方塊包含三個 Azure AD 驗證的新選項：

![ServerLogin.png](windows/ServerLogin.png)

這些選項會對應至相同的五個用於 DSN 設定上述的 UI。

### <a name="example-connection-strings"></a>範例連接字串
1. SQL Server 驗證 – 舊版的語法。 不驗證伺服器憑證，以及伺服器強制執行它時，才會使用加密。 連接字串中傳遞使用者名稱/密碼。
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. SQL 驗證 – 新的語法。 用戶端要求加密 (預設值`Encrypt`是`true`) 和伺服器憑證取得已驗證，而不論加密設定 (除非`TrustServerCertificate`設定為`true`)。 連接字串中傳遞使用者名稱/密碼。
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. 整合式 Windows 驗證 (Kerberos Linux 和 macOS 上) 使用 SSPI （至 SQL Server 或 SQL IaaS） – 目前的語法。 不驗證伺服器憑證，除非使用加密。 
`server=Server;database=Database;Trusted_Connection=yes;`
4. (_Windows 驅動程式只_。)整合式 Windows 驗證使用 SSPI （如果目標資料庫是在 SQL Server 或 SQL IaaS） – 新的語法。 用戶端要求加密 (預設值`Encrypt`是`true`) 和伺服器憑證取得已驗證，而不論加密設定 (除非`TrustServerCertificate`設定為`true`)。 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. AAD 的使用者名稱/密碼驗證 （如果目標資料庫是 Azure SQL DB 中）。 取得驗證伺服器憑證，不論 [加密] 設定 (除非`TrustServerCertificate`設為`true`)。 連接字串中傳遞使用者名稱/密碼。 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_Windows 驅動程式只_。)使用 ADAL，這牽涉到兌換 AAD 簽發存取權杖的 Windows 帳戶認證，假設目標資料庫 Azure SQL Database 中的整合式的 Windows 驗證。 取得驗證伺服器憑證，不論 [加密] 設定 (除非`TrustServerCertificate`設為`true`)。 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
7. (_Windows 驅動程式只_。)AAD 互動式驗證會使用 Azure multi-factor Authentication 的技術，來設定連線。 在此模式中，藉由提供登入識別碼中，Windows Azure 驗證對話方塊就會觸發，並可讓使用者輸入密碼，以完成連線。 連接字串中傳遞使用者名稱。
`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

![WindowsAzureAuth.png](windows/WindowsAzureAuth.png)

> [!NOTE] 
>- 當新的 Active Directory 選項配合 Windows ODBC 驅動程式，請確認[適用於 SQL Server 的 Active Directory Authentication Library](https://go.microsoft.com/fwlink/?LinkID=513072)已安裝。 當使用 Linux 和 macOS 的驅動程式，請確定`libcurl`已安裝。 17.2 和更新版本的驅動程式版本，這是不明確的相依性因為不需要其他驗證方法或 ODBC 作業。
>- 若要使用的 SQL Server 帳戶的使用者名稱和密碼進行連接，您現在可以使用新`SqlPassword`選項，建議使用，特別是針對 SQL Azure 因為這個選項會啟用更安全連線的預設值。
>- 若要使用的 Azure Active Directory 帳戶的使用者名稱和密碼進行連接，指定`Authentication=ActiveDirectoryPassword`連接字串中，`UID`和`PWD`關鍵字的使用者名稱和密碼，分別。
>- 若要使用 Windows 整合式 」 或 「 Active Directory 整合式 （僅 Windows 驅動程式） 驗證連線，請指定`Authentication=ActiveDirectoryIntegrated`連接字串中。 驅動程式會自動選擇正確的驗證模式。 `UID` 和`PWD`不得指定。
>- 若要使用 Active Directory Interactive （僅 Windows 驅動程式） 的驗證，連接`UID`必須指定。

## <a name="authenticating-with-an-access-token"></a>使用存取權杖進行驗證

`SQL_COPT_SS_ACCESS_TOKEN`預先連接屬性允許從 Azure AD 進行驗證，而不是使用者名稱和密碼，取得存取權杖的使用，也會略過，交涉並取得存取權杖的驅動程式。 若要使用存取權杖，將`SQL_COPT_SS_ACCESS_TOKEN`連接屬性的指標`ACCESSTOKEN`結構：

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

`ACCESSTOKEN`是包含 4 個位元組的可變長度結構_長度_後面接著_長度_表單的存取權杖的不透明資料的位元組。 其中一個透過由於 SQL Server 如何處理存取權杖，取得[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)必須展開 JSON 回應，使每個位元組後面接著 0，填補位元組，類似於包含只能使用 ASCII 字元的 ucs-2 字串; 不過，此語彙基元不透明值和指定，以位元組為單位的長度不能包含任何 null 結束字元。 由於其大量長度和格式的限制，這種驗證方法是只提供以程式設計方式透過`SQL_COPT_SS_ACCESS_TOKEN`連接屬性，則沒有任何對應的 DSN 或連接字串關鍵字。 連接字串必須包含`UID`， `PWD`， `Authentication`，或`Trusted_Connection`關鍵字。

> [!NOTE]
> ODBC Driver 13.1 版僅支援此驗證上_Windows_。

## <a name="azure-active-directory-authentication-sample-code"></a>Azure Active Directory 驗證範例程式碼

下列範例會示範連接到 SQL Server 所需的程式碼使用 Azure Active Directory 與連接關鍵字。 請注意，則不需要變更應用程式程式碼本身;連接字串或如果使用的話，資料來源名稱是唯一的修改，才能使用 AAD 進行驗證：
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    ...
~~~
下列範例將示範使用 Azure Active Directory 存取權杖驗證與連接到 SQL Server 所需的程式碼。 在此情況下，就必須修改應用程式程式碼，來處理存取權杖，並將相關聯的連接屬性。
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
以下是搭配 Azure Active Directory 互動式驗證的範例連接字串。 請注意，它不包含 PWD 欄位，因為會使用 Windows Azure 驗證 畫面上輸入的密碼。
~~~
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myuser;Authentication=ActiveDirectoryInteractive"
~~~

## <a name="see-also"></a>另請參閱
[使用 Azure AD 驗證的 Azure SQL DB 的權杖型驗證支援](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)

