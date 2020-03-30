---
title: ODBC 驅動程式的 DSN 和連接字串關鍵字 - SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/04/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-chojas
ms.author: v-jizho2
author: karinazhou
ms.openlocfilehash: bf9b755176913ad144781c5be0ad53150aedcd1b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "76911242"
---
# <a name="dsn-and-connection-string-keywords-and-attributes"></a>DSN 和連接字串關鍵字和屬性

此頁面會列出連接字串和 DSN 的關鍵字，以及 ODBC Driver for SQL Server 中可用的 SQLSetConnectAttr 和 SQLGetConnectAttr 連接屬性。

## <a name="supported-dsnconnection-string-keywords-and-connection-attributes"></a>支援的 DSN/連接字串關鍵字和連接屬性

下表列出每個平台可用的關鍵字和屬性 (L: Linux；M: Mac；W: Windows)。 按一下關鍵字或屬性，以查看詳細資料。

| DSN/連接字串關鍵字 | 連線屬性 | 平台 |
|-|-|-|
| [Addr](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [位址](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [AnsiNPW](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_ANSI_NPW](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssansinpw) | LMW |
| [APP](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [ApplicationIntent](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_APPLICATION_INTENT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssapplicationintent) | LMW |
| [AttachDBFileName](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_ATTACHDBFILENAME](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssattachdbfilename) | LMW |
| [驗證](../../connect/odbc/dsn-connection-string-attribute.md#authentication---sql_copt_ss_authentication) | [SQL_COPT_SS_AUTHENTICATION](../../connect/odbc/dsn-connection-string-attribute.md#authentication---sql_copt_ss_authentication) | LMW |
| [AutoTranslate](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_TRANSLATE](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsstranslate) | LMW |
| [ColumnEncryption](../../connect/odbc/dsn-connection-string-attribute.md#columnencryption---sql_copt_ss_column_encryption) | [SQL_COPT_SS_COLUMN_ENCRYPTION](../../connect/odbc/dsn-connection-string-attribute.md#columnencryption---sql_copt_ss_column_encryption) | LMW |
| [ConnectRetryCount](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | [SQL_COPT_SS_CONNECT_RETRY_COUNT](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | W |
| [ConnectRetryInterval](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | [SQL_COPT_SS_CONNECT_RETRY_INTERVAL](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | W |
| [Database](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_ATTR_CURRENT_CATALOG](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| [說明](../../connect/odbc/dsn-connection-string-attribute.md#description) | | LMW |
| [驅動程式](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [DSN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [Encrypt](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_ENCRYPT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssencrypt) | LMW |
| [Failover_Partner](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_FAILOVER_PARTNER](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssfailoverpartner) | W |
| [FailoverPartnerSPN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_FAILOVER_PARTNER_SPN](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | W |
| [FileDSN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [KeepAlive](../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md) (v17.4+，僅限 DSN)| | LMW |
| [KeepAliveInterval](../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md) (v17.4+，僅限 DSN) | | LMW |
| [KeystoreAuthentication](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#connection-string-keywords) | | LMW |
| [KeystorePrincipalId](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#connection-string-keywords) | | LMW |
| [KeystoreSecret](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#connection-string-keywords) | | LMW |
| [語言](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [MARS_Connection](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_MARS_ENABLED](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssmarsenabled) | LMW |
| [MultiSubnetFailover](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_MULTISUBNET_FAILOVER](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssmultisubnetfailover) | LMW |
| [Net](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [Network](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [PWD](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [QueryLog_On](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_QUERY](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfquery) | W |
| [QueryLogFile](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_QUERY_LOG](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfquerylog) | W |
| [QueryLogTIme](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_QUERY_INTERVAL](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfqueryinterval) | W |
| [QuotedId](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_QUOTED_IDENT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssquotedident) | LMW |
| [Regional](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [SaveFile](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [Server](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [ServerSPN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_SERVER_SPN](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | LMW |
| [StatsLog_On](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_DATA](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfdata) | W |
| [StatsLogFile](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_DATA_LOG](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfdatalog) | W |
| [TransparentNetworkIPResolution](../../connect/odbc/dsn-connection-string-attribute.md#transparentnetworkipresolution---sql_copt_ss_tnir) | [SQL_COPT_SS_TNIR](../../connect/odbc/dsn-connection-string-attribute.md#transparentnetworkipresolution---sql_copt_ss_tnir) | LMW |
| [Trusted_Connection](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_INTEGRATED_SECURITY](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssintegratedsecurity) | LMW |
| [TrustServerCertificate](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_TRUST_SERVER_CERTIFICATE](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsstrustservercertificate) | LMW |
| [UID](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [UseFMTONLY](../../connect/odbc/dsn-connection-string-attribute.md#usefmtonly) | | LMW |
| [WSID](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| | [SQL_ATTR_ACCESS_MODE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_ACCESS_MODE) | LMW |
| | [SQL_ATTR_ASYNC_DBC_EVENT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_ASYNC_DBC_PCALLBACK](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_ASYNC_DBC_PCONTEXT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_ASYNC_ENABLE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_AUTO_IPD](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_AUTOCOMMIT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_AUTOCOMMIT) | LMW |
| | [SQL_ATTR_CONNECTION_DEAD](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_CONNECTION_TIMEOUT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_DBC_INFO_TOKEN](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_LOGIN_TIMEOUT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_LOGIN_TIMEOUT) | LMW |
| | [SQL_ATTR_METADATA_ID](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_ODBC_CURSORS](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_ODBC_CURSORS) | LMW |
| | [SQL_ATTR_PACKET_SIZE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_PACKET_SIZE) | LMW |
| | [SQL_ATTR_QUIET_MODE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_QUIET_MODE) | LMW |
| | [SQL_ATTR_RESET_CONNECTION](../../odbc/reference/develop-driver/upgrading-a-3-5-driver-to-a-3-8-driver.md#connection-pooling) <br> (SQL_COPT_SS_RESET_CONNECTION) | LMW |  
| | [SQL_ATTR_TRACE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_OPT_TRACE) | LMW |
| | [SQL_ATTR_TRACEFILE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_OPT_TRACEFILE) | LMW |
| | [SQL_ATTR_TRANSLATE_LIB](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_TRANSLATE_DLL) | LMW |
| | [SQL_ATTR_TRANSLATE_OPTION](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_TRANSLATE_OPTION) | LMW |
| | [SQL_ATTR_TXN_ISOLATION](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_TXN_ISOLATION) | LMW |
| | [SQL_COPT_SS_ACCESS_TOKEN](dsn-connection-string-attribute.md#sql_copt_ss_access_token) | LMW |
| | [SQL_COPT_SS_ANSI_OEM](dsn-connection-string-attribute.md#sql_copt_ss_ansi_oem)| W |
| | [SQL_COPT_SS_BCP](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssbcp) | LMW |
| | [SQL_COPT_SS_BROWSE_CACHE_DATA](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) | LMW |
| | [SQL_COPT_SS_BROWSE_CONNECT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssbrowseconnect) | LMW |
| | [SQL_COPT_SS_BROWSE_SERVER](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssbrowseserver) | LMW |
| | [SQL_COPT_SS_CEKEYSTOREDATA](dsn-connection-string-attribute.md#sql_copt_ss_cekeystoredata) | LMW |
| | [SQL_COPT_SS_CEKEYSTOREPROVIDER](dsn-connection-string-attribute.md#sql_copt_ss_cekeystoreprovider) | LMW |
| | [SQL_COPT_SS_CLIENT_CONNECTION_ID](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) | LMW |
| | [SQL_COPT_SS_CONCAT_NULL](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssconcatnull) | LMW |
| | [SQL_COPT_SS_CONNECTION_DEAD](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssconnectiondead) | LMW |
| | [SQL_COPT_SS_ENLIST_IN_DTC](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssenlistindtc) | W |
| | [SQL_COPT_SS_ENLIST_IN_XA](dsn-connection-string-attribute.md#sql_copt_ss_enlist_in_xa) | LMW |
| | [SQL_COPT_SS_FALLBACK_CONNECT](dsn-connection-string-attribute.md#sql_copt_ss_fallback_connect) | LMW |
| | [SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | LMW |
| | [SQL_COPT_SS_MUTUALLY_AUTHENTICATED](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | LMW |
| | [SQL_COPT_SS_OLDPWD](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssoldpwd) | LMW |
| | [SQL_COPT_SS_PERF_DATA_LOG_NOW](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfdatalognow) | W |
| | [SQL_COPT_SS_PRESERVE_CURSORS](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsspreservecursors) | LMW |
| | [SQL_COPT_SS_SPID](../../connect/odbc/dsn-connection-string-attribute.md#sql_copt_ss_spid) (v17.5+) | LMW |
| | [SQL_COPT_SS_TXN_ISOLATION](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsstxnisolation) | LMW |
| | [SQL_COPT_SS_USER_DATA](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssuserdata) | LMW |
| | [SQL_COPT_SS_WARN_ON_CP_ERROR](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsswarnoncperror) | LMW |
| [ClientCertificate](../../connect/odbc/dsn-connection-string-attribute.md#clientcertificate) | | LMW | 
| [ClientKey](../../connect/odbc/dsn-connection-string-attribute.md#clientkey) | | LMW | 


以下是[搭配 SQL Server Native Client 使用連接字串關鍵字](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)、[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 和 [SQLSetConnectAttr 函式](../../odbc/reference/syntax/sqlsetconnectattr-function.md)中所未記載的一些連接字串關鍵字和連接屬性。

### <a name="description"></a>描述

用於描述資料來源。

### <a name="sql_copt_ss_ansi_oem"></a>SQL_COPT_SS_ANSI_OEM

控制 ANSI 至 OEM 的資料轉換。 

| 屬性值 | 描述 |
|-|-|
| SQL_AO_OFF | (預設) 不執行轉譯。 |
| SQL_AO_ON | 執行轉譯。 |

### <a name="sql_copt_ss_fallback_connect"></a>SQL_COPT_SS_FALLBACK_CONNECT

控制 SQL Server 後援連線的使用。 這一項已不再支援。

| 屬性值 | 描述 |
|-|-|
| SQL_FB_OFF | (預設) 已停用後援連線。 |
| SQL_FB_ON | 已啟用後援連線。 |



## <a name="new-connection-string-keywords-and-connection-attributes"></a>新的連接字串關鍵字和連接屬性

###  <a name="authentication---sql_copt_ss_authentication"></a>驗證 - SQL_COPT_SS_AUTHENTICATION

設定連線到 SQL Server 時要使用的驗證模式。 如需詳細資訊，請參閱[使用 Azure Active Directory](using-azure-active-directory.md)。

| 關鍵字值 | 屬性值 | 描述 |
|-|-|-|
| |SQL_AU_NONE|(預設) 未設定。 其他屬性的組合會決定驗證模式。|
|SqlPassword|SQL_AU_PASSWORD|SQL Server 驗證 (使用使用者名稱和密碼)。|
|ActiveDirectoryIntegrated|SQL_AU_AD_INTEGRATED|Azure Active Directory 整合式驗證。|
|ActiveDirectoryPassword|SQL_AU_AD_PASSWORD|Azure Active Directory 密碼驗證。|
|ActiveDirectoryInteractive|SQL_AU_AD_INTERACTIVE|Azure Active Directory 互動式驗證。|
|ActiveDirectoryMsi|SQL_AU_AD_MSI|Azure Active Directory 受控服務識別驗證。 針對使用者指派的識別，UID 設成使用者身分識別的物件識別碼。 |
| |SQL_AU_RESET|未設定。 覆寫任何 DSN 或連接字串設定。|

> [!NOTE]
> 使用 `Authentication` 關鍵字或屬性時，明確地將 `Encrypt` 設定指定為連接字串/DSN/連接屬性中所要的值。 如需詳細資訊，請參閱[搭配 SQL Server Native Client 使用連接字串關鍵字](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。

### <a name="columnencryption---sql_copt_ss_column_encryption"></a>ColumnEncryption - SQL_COPT_SS_COLUMN_ENCRYPTION

控制透明的資料行加密 (Always Encrypted)。 如需詳細資訊，請參閱[使用 Always Encrypted (ODBC)](using-always-encrypted-with-the-odbc-driver.md)。

| 關鍵字值 | 屬性值 | 描述 |
|-|-|-|
|啟用|SQL_CE_ENABLED|啟用 Always Encrypted。|
|已停用|SQL_CE_DISABLED|(預設) 停用 Always Encrypted。|
| |SQL_CE_RESULTSETONLY|只啟用解密 (結果和傳回值)。|

### <a name="transparentnetworkipresolution---sql_copt_ss_tnir"></a>TransparentNetworkIPResolution - SQL_COPT_SS_TNIR

控制透明網路 IP 解析功能，它會與 MultiSubnetFailover 互動，以允許更快的重新連線嘗試。 如需詳細資訊，請參閱[使用透明網路 IP 解析](using-transparent-network-ip-resolution.md)。

| 關鍵字值 | 屬性值| 描述 |
|-|-|-|
|啟用|SQL_IS_ON|(預設) 啟用透明網路 IP 解析。|
|已停用|SQL_IS_OFF|停用透明網路 IP 解析。|

### <a name="usefmtonly"></a>UseFMTONLY

控制在連線到 SQL Server 2012 及更新版本時，對中繼資料使用 SET FMTONLY。

| 關鍵字值 | 描述 |
|-|-|
|否|(預設) 如果有的話，對中繼資料使用 sp_describe_first_result_set。 |
|是| 對中繼資料使用 SET FMTONLY。 |


## <a name="clientcertificate"></a>ClientCertificate

指定要用於驗證的憑證。 可用選項包括： 

| 選項值 | 描述 |
|-|-|
| sha1：`<hash_value>` | ODBC 驅動程式會使用 SHA1 雜湊來找出 Windows 憑證存放區中的憑證 |
| 主旨：`<subject>` | ODBC 驅動程式會使用主旨來找出 Windows 憑證存放區中的憑證 |
| file:`<file_location>`[,password:`<password>`] | ODBC 驅動程式會使用憑證檔案。 |

如果憑證採用 PFX 格式，且 PFX 憑證內的私密金鑰受到密碼保護，則需要密碼關鍵字。 若是 PEM 和 DER 格式的憑證，ClientKey 屬性為必要項


## <a name="clientkey"></a>ClientKey

針對 ClientCertificate 屬性所指定的 PEM 或 DER 憑證，請指定私密金鑰的檔案位置。 格式： 

| 選項值 | 描述 |
|-|-|
| file:`<file_location>`[,password:`<password>`] | 指定私密金鑰檔案的位置。 |

如果私密金鑰檔案受到密碼保護，則需要密碼關鍵字。 如果密碼包含任何 "," 字元，則會緊接在每個字元之後加入一個額外的 "," 字元。 例如，如果密碼是 "a,b,c"，則連接字串中的逸出密碼會是 "a,,b,,c"。 
    

### <a name="sql_copt_ss_access_token"></a>SQL_COPT_SS_ACCESS_TOKEN

允許使用 Azure Active Directory 存取權杖進行驗證。 如需詳細資訊，請參閱[使用 Azure Active Directory](using-azure-active-directory.md)。

| 屬性值 | 描述 |
|-|-|
| NULL | (預設) 不提供任何存取權杖。 |
| ACCESSTOKEN* | 存取權杖的指標。 |

### <a name="sql_copt_ss_cekeystoredata"></a>SQL_COPT_SS_CEKEYSTOREDATA

與載入的金鑰儲存區提供者程式庫通訊。 請參閱＜控制透明的資料行加密 (Always Encrypted)＞。 此屬性沒有預設值。 如需詳細資訊，請參閱[自訂金鑰儲存區提供者](custom-keystore-providers.md)。

| 屬性值 | 描述 |
|-|-|
| CEKEYSTOREDATA * | 金鑰儲存區提供者程式庫的通訊資料結構 |

### <a name="sql_copt_ss_cekeystoreprovider"></a>SQL_COPT_SS_CEKEYSTOREPROVIDER

載入 Always Encrypted 的金鑰儲存區提供者程式庫，或擷取載入的金鑰儲存區提供者程式庫名稱。 如需詳細資訊，請參閱[自訂金鑰儲存區提供者](custom-keystore-providers.md)。 此屬性沒有預設值。

| 屬性值 | 描述 |
|-|-|
| char * | 金鑰儲存區提供者程式庫路徑 |

### <a name="sql_copt_ss_enlist_in_xa"></a>SQL_COPT_SS_ENLIST_IN_XA

若要啟用與 XA 相容交易處理器 (TP) 的 XA 交易，應用程式需要呼叫 **SQLSetConnectAttr**，且使用 SQL_COPT_SS_ENLIST_IN_XA 與 `XACALLPARAM` 物件的指標。 這個選項在 Windows、(17.3 和更新版本) Linux 和 Mac 上受到支援。
```
SQLSetConnectAttr(hdbc, SQL_COPT_SS_ENLIST_IN_XA, param, SQL_IS_POINTER);  // XACALLPARAM *param
``` 
 若要將 XA 交易只與 ODBC 連接建立關聯，呼叫 **SQLSetConnectAttr** 時請使用 SQL_COPT_SS_ENLIST_IN_XA 而不是指標來提供 TRUE 或 FALSE。 這只在 Windows 上有效，不能用來透過用戶端應用程式指定 XA 作業。 
 ```
SQLSetConnectAttr(hdbc, SQL_COPT_SS_ENLIST_IN_XA, (SQLPOINTER)TRUE, 0);
``` 

|值|描述|平台|  
|-----------|-----------------|-----------------|  
|XACALLPARAM 物件*|指向 `XACALLPARAM` 物件的指標。|Windows、Linux 和 Mac|
|TRUE|建立 XA 交易與 ODBC 連接的關聯。 所有相關的資料庫活動都將在 XA 交易的保護底下進行。|Windows|  
|FALSE|取消 XA 交易與 ODBC 連接的關聯。|Windows|

 如需 XA 交易的詳細資訊，請參閱[使用 XA 交易](../../connect/odbc/use-xa-with-dtc.md)。

### <a name="sql_copt_ss_spid"></a>SQL_COPT_SS_SPID

擷取連接的伺服器處理序識別碼。 這相當於 T-SQL [@@SPID](../../t-sql/functions/spid-transact-sql.md) 變數，不同之處在於其不會對伺服器產生額外的往返。

| 屬性值 | 描述 |
|-|-|
| DWORD | SPID |
