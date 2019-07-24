---
title: 搭配 ODBC 驅動程式使用 Azure Active Directory |SQL Server 的 Microsoft Docs
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
ms.openlocfilehash: 9e60c376e0bced63241674b82d05700281a06ad3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008493"
---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>搭配 ODBC 驅動程式使用 Azure Active Directory
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>目的

13.1 或更新版本的 Microsoft ODBC Driver for SQL Server 可讓 ODBC 應用程式使用 Azure Active Directory 中的同盟身分識別, 以使用者名稱/密碼、Azure Active Directory 存取權杖、Azure Active, 連接到 SQL Azure 實例。目錄受控服務識別或 Windows 整合式驗證 (_僅限 windows 驅動程式_)。 對於 ODBC 驅動程式版本 13.1, Azure Active Directory 的存取權杖驗證_僅限 Windows_。 ODBC 驅動程式17版和更新版本支援跨所有平臺 (Windows、Linux 和 Mac) 進行這種驗證。 具有登入識別碼的新 Azure Active Directory 互動式驗證是在適用于 Windows 的 ODBC 驅動程式17.1 版中引進。 針對系統指派和使用者指派的身分識別, 在 ODBC 驅動程式版本17.3.1.1 中新增了新的 Azure Active Directory 受控服務識別驗證方法。 所有這些都是透過使用新的 DSN 和連接字串關鍵字, 以及連接屬性來完成。

> [!NOTE]
> Linux 和 macOS 上的 ODBC 驅動程式不支援 Active Directory 同盟服務。 如果您使用來自 Linux 或 macOS 用戶端的 Azure Active Directory 使用者名稱/密碼驗證, 且您的 Active Directory 設定包含同盟服務, 則驗證可能會失敗。

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>新的和 (或) 修改的 DSN 和連接字串關鍵字

當`Authentication`連接到 DSN 或連接字串以控制驗證模式時, 可以使用關鍵字。 在連接字串中設定的值會覆寫 DSN 中的 (如果有提供的話)。 設定的_前置屬性值_是從連接字串和 DSN 值計算而來的值。 `Authentication`

|[屬性]|值|預設|Description|
|-|-|-|-|
|`Authentication`|(未設定)、(空字串)、 `SqlPassword` `ActiveDirectoryIntegrated`、 `ActiveDirectoryPassword` `ActiveDirectoryInteractive`、、、`ActiveDirectoryMsi` |(未設定)|控制驗證模式。<table><tr><th>ReplTest1<th>Description<tr><td>(未設定)<td>由其他關鍵字 (現有的舊版連接選項) 決定的驗證模式。<tr><td>(空字串)<td>連接字串是: "{0}"覆寫並`Authentication`取消設定在 DSN 中設定的值。<tr><td>`SqlPassword`<td>使用使用者名稱和密碼直接向 SQL Server 實例進行驗證。<tr><td>`ActiveDirectoryPassword`<td>使用使用者名稱和密碼, 以 Azure Active Directory 身分識別進行驗證。<tr><td>`ActiveDirectoryIntegrated`<td>_僅限 Windows 驅動程式_。 使用整合式驗證, 透過 Azure Active Directory 身分識別進行驗證。<tr><td>`ActiveDirectoryInteractive`<td>_僅限 Windows 驅動程式_。 使用互動式驗證以 Azure Active Directory 身分識別進行驗證。<tr><td>`ActiveDirectoryMsi`<td>使用受控服務識別驗證, 以 Azure Active Directory 身分識別進行驗證。 針對使用者指派的身分識別，UID 會設為使用者身分識別的物件識別碼。</table>|
|`Encrypt`|(未設定)、`Yes`、`No`|(請參閱描述)|控制連接的加密。 如果在 DSN 或連接字串中, `Authentication`設定的前置屬性值不是_none_ , 則預設為`Yes`。 否則預設為 `No`。 如果屬性`SQL_COPT_SS_AUTHENTICATION`會覆寫的前置屬性`Authentication`值, 請在 DSN 或連接字串或連接屬性中明確設定 Encryption 的值。 如果在 DSN 或連接字串中將`Yes`值設為`Yes` , 則 Encryption 的前置屬性值為。|

## <a name="new-andor-modified-connection-attributes"></a>新增和/或修改的連接屬性

下列預先連接的連接屬性已引進或修改, 以支援 Azure Active Directory 驗證。 當連接屬性具有對應的連接字串或 DSN 關鍵字, 而且已設定時, 連接屬性的優先順序會較高。

|attribute|類型|值|預設|Description|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`、`SQL_AU_PASSWORD`、`SQL_AU_AD_INTEGRATED`、`SQL_AU_AD_PASSWORD`、`SQL_AU_AD_INTERACTIVE`、`SQL_AU_AD_MSI`、`SQL_AU_RESET`|(未設定)|請參閱上述`Authentication`關鍵字的描述。 `SQL_AU_NONE`提供以明確覆寫 DSN 和/或`Authentication`連接字串中的集合值, 而`SQL_AU_RESET`取消設定屬性 (如果已設定的話), 允許 dsn 或連接字串值的優先順序較高。|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|或 Null `ACCESSTOKEN`的指標|NULL|如果不是 null, 則指定要使用的 AzureAD 存取權杖。 指定存取權杖`UID`, 以及`Trusted_Connection`、 `PWD`、或`Authentication`連接字串關鍵字或其對等屬性是錯誤的。 <br> **注意:** ODBC 驅動程式13.1 版僅支援在_Windows_上進行此操作。|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`, `SQL_EN_ON`|(請參閱描述)|控制連接的加密。 `SQL_EN_OFF`和`SQL_EN_ON`會分別停用和啟用加密。 如果`Authentication`設定的前置屬性值不是_none_或`SQL_COPT_SS_ACCESS_TOKEN`已設定, 而且`Encrypt`未在 DSN 或連接字串中指定, 則預設為`SQL_EN_ON`。 否則預設為 `SQL_EN_OFF`。 如果 [連接屬性`SQL_COPT_SS_AUTHENTICATION` ] 設定為 [非_none_], `SQL_COPT_SS_ENCRYPT`則會在 DSN 或連接字串中未指定時, 將明確設定為所需的值。 `Encrypt` 這個屬性的有效值[可控制是否將加密用於連接。](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation)|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|不支援 Azure Active Directory, 因為 AAD 主體的密碼變更無法透過 ODBC 連接完成。 <br><br>SQL Server 驗證的密碼逾期已在 SQL Server 2005 中推出。 已`SQL_COPT_SS_OLDPWD`加入屬性, 可讓用戶端為連接提供舊的和新密碼。 設定這個屬性之後，提供者將不會針對第一次連接或後續連接使用連接集區，因為連接字串將會包含已經變更的「舊密碼」。|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`、`SQL_IS_ON`|`SQL_IS_OFF`|已_淘汰_;請`SQL_COPT_SS_AUTHENTICATION`改用將`SQL_AU_AD_INTEGRATED`設為。 <br><br>強制使用 Windows 驗證 (Linux 和 macOS 上的 Kerberos) 進行伺服器登入時的存取驗證。 使用 Windows 驗證時, 驅動程式會忽略、 `SQLConnect` `SQLDriverConnect`或`SQLBrowseConnect`處理過程中提供的使用者識別碼和密碼值。|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>Azure Active Directory 的 UI 新增 (僅限 Windows 驅動程式)

驅動程式的 DSN 設定和連線 Ui 已透過使用 Azure AD 驗證所需的其他選項來增強。

### <a name="creating-and-editing-dsns-in-the-ui"></a>在 UI 中建立和編輯 Dsn

使用驅動程式的安裝 UI 建立或編輯現有的 DSN 時, 可以使用新的 Azure AD 驗證選項:

`Authentication=ActiveDirectoryIntegrated` 表示對 SQL Azure 進行 Azure Active Directory 整合式驗證

![CreateNewDSN_ADIntegrated.png](windows/CreateNewDSN_ADIntegrated.png)

`Authentication=ActiveDirectoryPassword`針對 SQL Azure Azure Active Directory 使用者名稱/密碼驗證

![CreateNewDSN_ADPassword.png](windows/CreateNewDSN_ADPassword.png)

`Authentication=ActiveDirectoryInteractive` 表示對 SQL Azure 進行 Azure Active Directory 互動式驗證

![CreateNewDSN_ADInteractive.png](windows/CreateNewDSN_ADInteractive.png)

`Authentication=SqlPassword`SQL Server 的使用者名稱/密碼驗證 (Azure 或其他)

![CreateNewDSN_SQLServer.png](windows/CreateNewDSN_SQLServer.png)

`Trusted_Connection=Yes`Windows 舊版 SSPI 整合式驗證

![CreateNewDSN_winSSPI.png](windows/CreateNewDSN_winSSPI.png)

五個選項分別對應`Trusted_Connection=Yes`至 (現有的舊版 Windows 僅限 SSPI 整合驗證`Authentication=` ) `SqlPassword`和`ActiveDirectoryPassword` `ActiveDirectoryIntegrated`、、 `ActiveDirectoryInteractive`和。

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>SQLDriverConnect 提示字元 (僅限 Windows 驅動程式)

當 SQLDriverConnect 要求完成連接所需的資訊時, 會顯示提示對話方塊, 其中包含三個 Azure AD 驗證的新選項:

![ServerLogin.png](windows/ServerLogin.png)

這些選項對應于上述 DSN 設定 UI 中的相同五個。

### <a name="example-connection-strings"></a>範例連接字串
1. SQL Server 驗證-舊版語法。 伺服器憑證不會經過驗證, 而且只有在伺服器強制執行加密時, 才會使用它。 使用者名稱/密碼會在連接字串中傳遞。
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. SQL 驗證-新的語法。 用戶端要求加密 (的`Encrypt`預設值是), 而不論加密設定為何 (除非`TrustServerCertificate`設定為`true`), 伺服器憑證都會`true`經過驗證。 使用者名稱/密碼會在連接字串中傳遞。
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. 整合式 Windows 驗證 (Linux 和 macOS 上的 Kerberos) 使用 SSPI (至 SQL Server 或 SQL IaaS)-目前的語法。 除非使用加密, 否則不會驗證伺服器憑證。 
`server=Server;database=Database;Trusted_Connection=yes;`
4. (_僅限 Windows 驅動程式_)。使用 SSPI 的整合式 Windows 驗證 (如果目標資料庫位於 SQL Server 或 SQL IaaS)-新的語法。 用戶端要求加密 (的`Encrypt`預設值是), 而不論加密設定為何 (除非`TrustServerCertificate`設定為`true`), 伺服器憑證都會`true`經過驗證。 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. AAD 使用者名稱/密碼驗證 (如果目標資料庫位於 Azure SQL DB)。 無論加密設定為何, 伺服器憑證都會經過驗證 (除非`TrustServerCertificate`設定為`true`)。 使用者名稱/密碼會在連接字串中傳遞。 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_僅限 Windows 驅動程式_)。使用 ADAL 的整合式 Windows 驗證, 其牽涉到兌換 AAD 發行之存取權杖的 Windows 帳號憑證, 假設目標資料庫在 Azure SQL Database 中。 無論加密設定為何, 伺服器憑證都會經過驗證 (除非`TrustServerCertificate`設定為`true`)。 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
7. (_僅限 Windows 驅動程式_)。AAD 互動式驗證會使用 Azure 多重要素驗證技術來設定連線。 在此模式中, 藉由提供登入識別碼, 會觸發 Windows Azure 驗證對話方塊, 並允許使用者輸入密碼以完成連接。 使用者名稱會在連接字串中傳遞。
`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

![WindowsAzureAuth.png](windows/WindowsAzureAuth.png)

8. AAD 受控服務識別驗證會使用系統指派或使用者指派的身分識別來進行驗證, 以設定連線。 針對使用者指派的識別，UID 設成使用者身分識別的物件識別碼。<br>
針對系統指派的身分識別，<br>
`server=Server;database=Database;Authentication=ActiveDirectoryMsi;`<br>
對於物件識別碼等於 myObjectId 的使用者指派身分識別,<br>
`server=Server;database=Database;UID=myObjectId;Authentication=ActiveDirectoryMsi;`

> [!NOTE] 
>- 使用新的 Active Directory 選項搭配 Windows ODBC 驅動程式時, 請確定已安裝[SQL Server 的 Active Directory 驗證程式庫](https://go.microsoft.com/fwlink/?LinkID=513072)。 使用 Linux 和 macOS 驅動程式時, 請確定`libcurl`已安裝。 若是驅動程式版本17.2 和更新版本, 這不是明確的相依性, 因為它不是其他驗證方法或 ODBC 作業的必要項。
>- 若要使用 SQL Server 帳戶使用者名稱和密碼進行連線, 您現在可以使用`SqlPassword`新的選項 (特別是針對 SQL Azure), 因為此選項會啟用更安全的連接預設值。
>- 若要使用 Azure Active Directory 的帳戶使用者名稱和密碼進行`Authentication=ActiveDirectoryPassword`連線, 請分別在連接`UID`字串`PWD`中指定, 並以使用者名稱和密碼指定和關鍵字。
>- 若要使用 Windows 整合式或 Active Directory 整合式 (僅限 Windows 驅動程式`Authentication=ActiveDirectoryIntegrated` ) 來連接, 請在連接字串中指定。 驅動程式將會自動選擇正確的驗證模式。 `UID`不得`PWD`指定和。
>- 若要使用 Active Directory Interactive (僅限 Windows 驅動程式) `UID`驗證來進行連接, 必須指定。

## <a name="authenticating-with-an-access-token"></a>使用存取權杖進行驗證

`SQL_COPT_SS_ACCESS_TOKEN`預先連接屬性允許使用從 Azure AD 取得的存取權杖來進行驗證, 而不是使用者名稱和密碼, 也會略過驅動程式對存取權杖的協商和取得。 若要使用存取權杖, 請將`SQL_COPT_SS_ACCESS_TOKEN`連接屬性設定為`ACCESSTOKEN`結構的指標:

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

是由4個位元組_長度_組成的可變長度結構, 後面接著構成存取權杖的不透明資料_長度_位元組。  `ACCESSTOKEN` 由於 SQL Server 如何處理存取權杖, 因此必須展開透過[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios) JSON 回應取得的權杖, 讓每個位元組後面接著0個填補位元組, 類似于僅包含 ASCII 字元的 UCS-2 字串。不過, 此標記是不透明的值, 而指定的長度 (以位元組為單位) 不得包含任何 null 結束字元。 由於這種驗證方法的長度和格式條件約束, 因此只能透過`SQL_COPT_SS_ACCESS_TOKEN`連接屬性以程式設計方式使用, 而且沒有對應的 DSN 或連接字串關鍵字。 連接字串不能`UID`包含、 `PWD`、 `Authentication`或`Trusted_Connection`關鍵字。

> [!NOTE]
> ODBC 驅動程式13.1 版僅支援在_Windows_上進行這種驗證。

## <a name="azure-active-directory-authentication-sample-code"></a>Azure Active Directory 驗證範例程式碼

下列範例顯示使用 Azure Active Directory 搭配連接關鍵字來連接 SQL Server 所需的程式碼。 請注意, 不需要變更應用程式程式碼本身;使用 AAD 進行驗證所需的唯一修改是連接字串, 或使用 DSN (如果有的話):
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    ...
~~~
下列範例顯示使用具有存取權杖驗證的 Azure Active Directory 連接到 SQL Server 所需的程式碼。 在此情況下, 您必須修改應用程式程式碼來處理存取權杖, 並設定相關聯的連接屬性。
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
以下是與 Azure Active Directory 互動式驗證搭配使用的範例連接字串。 請注意, 它不包含 [PWD] 欄位, 因為密碼會使用 Windows Azure 驗證畫面輸入。
~~~
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myuser;Authentication=ActiveDirectoryInteractive"
~~~
以下是與 Azure Active Directory 受控服務識別驗證搭配使用的範例連接字串。 請注意，針對使用者指派的身分識別，UID 會設為使用者身分識別的物件識別碼。
~~~
// For system-assigned identity,
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};Authentication=ActiveDirectoryMsi"
...
// For user-assigned identity with object ID equals to myObjectId
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myObjectId;Authentication=ActiveDirectoryMsi"
~~~

## <a name="see-also"></a>另請參閱
[以權杖為基礎的驗證支援使用 Azure AD auth 的 Azure SQL DB](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)

