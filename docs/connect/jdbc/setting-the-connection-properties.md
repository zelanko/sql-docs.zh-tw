---
title: 設定連線屬性 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f1b62700-f046-488d-bd6b-a5cd8fc345b7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b82161b5fad292c1fc15ad68f807364e3d182143
ms.sourcegitcommit: c6e71ed14198da67afd7ba722823b1af9b4f4e6f
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 01/16/2019
ms.locfileid: "54327849"
---
# <a name="setting-the-connection-properties"></a>設定連接屬性

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

您可以使用各種方法指定連接字串屬性：

- 當您使用 DriverManager 類別進行連線時，連線 URL 中的屬性為 name=value。
- 做為名稱 = 值中的屬性*屬性*DriverManager 類別中的 Connect 方法的參數。
- 作為驅動程式資料來源的適當 setter 方法中的值。 例如：  
  
    ```java
    datasource.setServerName(value)  
    datasource.setDatabaseName(value)  
    ```  
  
## <a name="remarks"></a>備註

屬性名稱需區分大小寫，而重複的屬性名稱將以下列順序解析：  
  
1. API 引數 (例如使用者及密碼)
2. 屬性集合。  
3. 連接字串內的最後一個執行個體。
  
此外，屬性名稱允許未知的值，且 JDBC 驅動程式並不會驗證屬性值的大小寫。

容許同義字並會依序解析，如同是重複的屬性名稱一般。

下表列出 JDBC 驅動程式目前所有可用的連接字串屬性。

| 屬性<br/>類型<br/>預設 | Description |
| :------------------------------ | :---------- |
| accessToken<br/><br/>String<br/><br/>null | 此屬性可以用於連接到 SQL database 使用存取權杖。 **accessToken**無法使用連接 URL 來設定。 |
| applicationIntent<br/><br/>String<br/><br/>ReadWrite | 宣告連接到伺服器時的應用程式工作負載類型。 <br/><br/>可能的值為 **ReadOnly** 和 **ReadWrite**。 <br/><br/>如需詳細資訊，請參閱 <<c0> [ 高可用性、 災害復原的 JDBC 驅動程式支援](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)。 |
| applicationName<br/><br/>String<br/>[&lt;=128 char]<br/><br/>null | 應用程式名稱，如果未提供名稱，則為 "[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]"。<br/><br/>用以識別各種 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分析與記錄工具中的特定應用程式。 |
| 驗證 (authentication)<br/><br/>String<br/><br/>NotSpecified | 從 Microsoft JDBC Driver 6.0 for SQL Server，此選擇性屬性，表示要用於連線的 SQL 驗證方法。 可能的值為**ActiveDirectoryIntegrated**， **ActiveDirectoryPassword**， **SqlPassword**，而預設**NotSpecified**.<br/><br/> 使用**ActiveDirectoryIntegrated**連接到 SQL Database，使用整合式的 Windows 驗證。<br/><br/> 使用**ActiveDirectoryPassword**連接到 SQL Database，使用 Azure AD 主體名稱和密碼。<br/><br/> 使用**SqlPassword**連接到 SQL Server using **userName**/**使用者**並**密碼**屬性。<br/><br/> 使用**NotSpecified**如果沒有任何一種驗證方法所需。<br/><br/> **重要：** 如果驗證已設為 ActiveDirectoryIntegrated，就必須安裝下列兩個程式庫：**SQLJDBC_AUTH。DLL** （適用於 JDBC 驅動程式套件） 和 Azure Active Directory Authentication Library for SQL Server (**ADALSQL。DLL**) 便可在不同的語言 （x86 和 amd64） 從下載中心[Microsoft Active Directory Authentication Library for Microsoft SQL Server](https://www.microsoft.com/download/details.aspx?id=48742)。 JDBC 驅動程式僅支援版本**1.0.2028.318 及更高版本**ADALSQL 的。DLL。<br/><br/> **注意：** 當驗證 屬性設定為任何值以外**NotSpecified**，預設的驅動程式會使用 Secure Sockets Layer (SSL) 加密。<br/><br/> 如需如何設定 Azure Active Directory 驗證的詳細資訊，請造訪[連接到 SQL 資料庫使用 Azure Active Directory 驗證](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。 |
| authenticationScheme<br/><br/>String<br/><br/>NativeAuthentication | 表示您希望應用程式使用的整合式安全性種類。 可能的值為**JavaKerberos** ，預設值**NativeAuthentication**。<br/><br/> 使用時**authenticationScheme = JavaKerberos**，您必須指定完整的網域名稱 (FQDN)，在**serverName**或是**serverSpn**屬性。 否則，會發生錯誤 (Kerberos 資料庫中找不到伺服器)。<br/><br/> 如需有關使用 **authenticationScheme** 的詳細資訊，請參閱[使用 Kerberos 整合式驗證連線到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md) \(機器翻譯\)。 |
| cancelQueryTimeout<br/><br/>ssNoversion<br/><br/>-1 | 從 Microsoft JDBC Driver 6.4 for SQL Server，此屬性可用來取消**queryTimeout**在連接上設定。 查詢執行會停止回應，並不會擲回例外狀況如果 SQL Server 的 TCP 連線以無訊息方式卸除。 這個屬性才適用 'queryTimeout' 也會設定在連接上。 <br/><br/>驅動程式會等候的總數量**cancelQueryTimeout** + **queryTimeout**秒，若要卸除的連接，並關閉通道。 <br/><br/>這個屬性的預設值為-1，行為是無限期等候。 |
| columnEncryptionSetting<br/><br/>String<br/>["Enabled" &#124; "Disabled"]<br/><br/>已停用 | 自 Microsoft JDBC Driver 6.0 for SQL Server 起，設為 "Enabled" 會使用 Always Encrypted (AE) 功能。 如有啟用 AE，JDBC 驅動程式會透明加密及解密儲存在 SQL Server 中經過加密之資料庫資料行中的敏感性資料。<br/><br/> 如需詳細資訊**columnEncryptionSetting**，請參閱[JDBC 驅動程式搭配使用 Always Encrypted](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)如需詳細資訊。<br/><br/> **注意：** Always Encrypted 是適用於 SQL Server 2016 或更新版本。 |
| databaseName,<br/>[資料庫]<br/><br/>String<br/>[&lt;=128 char]<br/><br/>null | 要連接的資料庫名稱。 <br/><br/>如果沒有指定，將連接到預設資料庫。 |
| disableStatementPooling<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>true | 表示是否應該用於陳述式共用的旗標。 |
| enablePrepareOnFirst...<br/>PreparedStatementCall<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>false | _enablePrepareOnFirstPreparedStatementCall_<br/><br/> 設定為"true"，以藉由呼叫的已備妥的陳述式控制代碼建立<code>sp_prepexec</code>備妥的陳述式的第一次執行中。 <br/><br/>若要變更已備妥的陳述式來呼叫第一次執行設定為"false"<code>sp_executesql</code>並不準備陳述式之後它會呼叫的第二次執行發生,<code>sp_prepexec</code>設定備妥的陳述式控制代碼。 |
| encrypt<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>false | 如果伺服器有安裝憑證，設定為 "true" 以指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將安全通訊端層 (SSL) 加密用於用戶端與伺服器之間傳送的所有資料。 預設值為 "false"。<br/><br/> 從 Microsoft JDBC Driver 6.0 for SQL Server，沒有新連線設定 「 驗證 」，預設會使用 SSL 加密。 <br/><br/>如需詳細資訊，請參閱 'authentication' 屬性。 |
| failoverPartner<br/><br/>String<br/><br/>null | 用於資料庫鏡像組態的容錯移轉伺服器名稱。 初始連接到主體伺服器若失敗，將使用此屬性；在建立初始連接之後，將忽略此屬性。 必須與 databaseName 屬性一起使用。<br/><br/> **注意：** 此驅動程式不支援在連接字串中指定容錯移轉夥伴執行個體的伺服器執行個體通訊埠號碼當做 failoverPartner 屬性的一部分。 不過，它支援在相同的連接字串中指定主體伺服器執行個體的 serverName、instanceName 和 portNumber 屬性以及容錯移轉夥伴執行個體的 failoverPartner 屬性。<br/><br/> 如果您在 **Server** 連線屬性中指定虛擬網路名稱，則不能使用資料庫鏡像。 如需詳細資訊，請參閱[高可用性、 災害復原的 JDBC 驅動程式支援](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md) |
| fips<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>"false" | 這個屬性應該是針對啟用 FIPS 的 JVM **，則為 true**。 |
| fipsProvider<br/><br/>String<br/><br/>null | FIPS 的 JVM 設定提供者。 比方說，BCFIPS 或 SunPKCS11 NSS。 版本 6.4.0-移除查看詳細資料[此處](https://github.com/Microsoft/mssql-jdbc/pull/460)。 |
| gsscredential<br/><br/>org.ietf.jgss.GSSCredential<br/><br/>null | 從 Microsoft JDBC Driver 6.2 for SQL Server，可以在這個屬性中傳遞使用者認證來進行 Kerberos 限制委派。 <br/><br/>這必須搭配**integratedSecurity**作為 **，則為 true**並**JavaKerberos** **authenticationscheme**。 |
| hostNameInCertificate<br/><br/>String<br/><br/>null | 用於驗證 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSL 憑證的主機名稱。<br/><br/> 如果未指定 hostNameInCertificate 屬性或設定為 null，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 將會在連線 URL 上使用 **serverName** 屬性值，當作驗證 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSL 憑證的主機名稱。<br/><br/> **注意：** 這個屬性可搭配**加密**/**驗證**屬性和**trustServerCertificate**屬性。 只有連線會使用 Secure Sockets Layer (SSL) 加密，這個屬性會影響憑證驗證，而**trustServerCertificate**設為"false"。 確定傳遞給 **hostNameInCertificate** 的值完全符合伺服器憑證中主體替代名稱 (SAN) 內的一般名稱 (CN) 或 DNS 名稱，SSL 連線才會成功。 如需詳細資訊，請參閱 <<c0> [ 了解 SSL 支援](../../connect/jdbc/understanding-ssl-support.md)。 |
| INSTANCENAME<br/><br/>String<br/>[&lt;=128 char]<br/><br/>null | 要連線的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。 如果未指定，將會連接到預設執行個體。 如果已指定 instanceName 與通訊埠，請參閱通訊埠的注意事項。<br/><br/> 如果您在 **Server** 連線屬性中指定虛擬網路名稱，則不能使用 **instanceName** 連線屬性。 請參閱[高可用性、 災害復原的 JDBC 驅動程式支援](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)如需詳細資訊。 |
| integratedSecurity<br/><br/>boolean<br/>["true"&#124;"false"]<br/><br/>false | 設定為"true"，表示 Windows 認證由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Windows 作業系統上。 若為 "true"，JDBC 驅動程式會搜尋本機電腦認證快取，以取得電腦上已提供的認證或網路登入。<br/><br/> 設為 「 true 」 (具有**authenticationscheme = JavaKerberos**)，以表示 Kerberos 認證由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需有關 Kerberos 驗證的詳細資訊，請參閱[使用 Kerberos 整合式驗證來連線到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md) \(機器翻譯\)。 <br/><br/> 若為 "false"，必須提供使用者名稱及密碼。 |
| jaasConfigurationName<br/><br/>String<br/><br/>SQLJDBCDriver | 從 Microsoft JDBC Driver 6.2 for SQL Server，SQL Server 的每個連線可以有它自己 JAAS 登入組態檔來建立 Kerberos 連接。 這個屬性可以傳遞登入組態檔的名稱。 <br/> 根據預設，驅動程式設定屬性`useDefaultCcache = true`IBM Jvm 的和`useTicketCache = true`如其他的 Jvm。 |
| keyStoreAuthentication<br/><br/>String<br/><br/>null | 從 Microsoft JDBC Driver 6.0 for SQL Server，此屬性會識別要順暢地使用 永遠加密的連接設定的金鑰存放區，並判斷用來驗證的金鑰存放區的驗證機制。 Microsoft JDBC Driver 6.0 for SQL Server 支援設定啟動 Java 金鑰存放區順暢地使用您要設定這個屬性 」**keyStoreAuthentication = JavaKeyStorePassword**"。 請注意，若要使用這個屬性，您也需要設定**keyStoreLocation**並**keyStoreSecret** Java 金鑰存放區的屬性。 <br/><br/>如需詳細資訊，請瀏覽[搭配 JDBC 驅動程式使用 Always Encrypted](https://msdn.microsoft.com/library/mt591987%28v=sql.110%29.aspx?f=255&MSPPError=-2147217396)。 |
| keyStoreLocation<br/><br/>String<br/><br/>null | 當**keyStoreAuthentication = JavaKeyStorePassword**，則**keyStoreLocation**屬性會識別儲存資料行主要金鑰，以搭配 Always Encrypted 的 Java 金鑰儲存區檔案的路徑資料。 請注意，路徑必須包含的金鑰儲存區檔案名稱。<br/><br/>如需詳細資訊，請瀏覽[搭配 JDBC 驅動程式使用 Always Encrypted](https://msdn.microsoft.com/library/mt591987%28v=sql.110%29.aspx?f=255&MSPPError=-2147217396)。 |
| keyStoreSecret<br/><br/>String<br/><br/>null | 當**keyStoreAuthentication = JavaKeyStorePassword**，則**keyStoreSecret**屬性會識別要使用 keystore 以及金鑰的密碼。 請注意，使用 Java 金鑰存放區的金鑰存放區和金鑰的密碼必須相同。<br/><br/>如需詳細資訊，請瀏覽[搭配 JDBC 驅動程式使用 Always Encrypted](https://msdn.microsoft.com/library/mt591987%28v=sql.110%29.aspx?f=255&MSPPError=-2147217396)。 |
| lastUpdateCount<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>true | "true" 值只會從傳至伺服器的 SQL 陳述式傳回上次更新計數，而且它可以用在單一 SELECT、INSERT 或 DELETE 陳述式，以忽略伺服器觸發程序所導致的其他更新計數。 將此屬性設為 "false" 會導致傳回所有更新計數，包括伺服器觸發程序所傳回的更新計數。<br/><br/> **注意：** 此屬性只有在與 [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) 方法搭配使用時才適用。 所有其他 execute 方法都會傳回所有結果並更新計數。 這個屬性只會影響伺服器觸發程序所傳回的更新計數。 它不會影響結果集或觸發程序執行期間產生的錯誤。 |
| lockTimeout<br/><br/>ssNoversion<br/><br/>-1 | 等候資料庫報告鎖定逾時的毫秒數。預設的行為是無限期等待。 如果已指定，則此值為連接上所有陳述式的預設值。 請注意， **Statement.setQueryTimeout()** 可用來設定特定陳述式的逾時。 此值可以為 0，表示不等待。 |
| loginTimeout<br/><br/>ssNoversion<br/>[0..65535]<br/><br/>15 | 驅動程式應等待失敗連接逾時的秒數。 值為零表示此逾時為預設系統逾時，預設指定為 15 秒。 非零值為驅動程式應等待失敗連接之逾時的秒數。<br/><br/> 如果您在 **Server** 連線屬性中指定虛擬網路名稱，您應該指定三分鐘或更長的逾時值，好讓容錯移轉連線有充足的時間可以順利完成。 請參閱[高可用性、 災害復原的 JDBC 驅動程式支援](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)如需詳細資訊。 |
| multiSubnetFailover<br/><br/>布林<br/><br/>false | 在連線到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 可用性群組的可用性群組接聽程式或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 容錯移轉叢集執行個體時，一律指定 **multiSubnetFailover=true**。 **multiSubnetFailover=true** 會設定 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，以提供對 (目前) 使用中伺服器更快速的偵測與連線。 可能的值為 true 和 false。 請參閱[高可用性、 災害復原的 JDBC 驅動程式支援](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)如需詳細資訊。<br/><br/> 您可以透過程式設計方式，使用 [getPropertyInfo](../../connect/jdbc/reference/getpropertyinfo-method-sqlserverdriver.md)、[getMultiSubnetFailover](../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md) 及 [setMultiSubnetFailover](../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md) 存取 **multiSubnetFailover** 連線屬性。<br/><br/> **注意：** 從 Microsoft JDBC Driver 6.0 for SQL Server，它已不再需要設定**multiSubnetFailover**為"true"時連接到可用性群組接聽程式。 新屬性**transparentNetworkIPResolution**，預設會啟用提供偵測與 （目前） 作用中伺服器的連線。 |
| packetSize<br/><br/>ssNoversion<br/>[-1 &#124; 0 &#124; 512..32767]<br/><br/>8000 | 用來與 SQL Server 通訊的網路封包大小 (以位元組指定)。 -1 這個值表示使用伺服器的預設封包大小。 0 這個值表示使用最大值，也就是 32767。 如果將此屬性設定為可接受範圍以外的值，則會發生例外狀況。<br/><br/> **重要：** 啟用加密 (encrypt=true) 時，不建議使用 packetSize 屬性。 否則，驅動程式可能會引發連接錯誤。 如需詳細資訊，請參閱 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 類別的 [setPacketSize](../../connect/jdbc/reference/setpacketsize-method-sqlserverdatasource.md) 方法。 |
| 密碼<br/><br/>String<br/>[&lt;=128 char]<br/><br/>null | 資料庫密碼，如果使用 SQL 使用者名稱和密碼的連線。<br/>Kerberos 主體名稱和密碼的連接，此屬性設定為 Kerberos 主體密碼。 |
| portNumber,<br/>port<br/><br/>ssNoversion<br/>[0..65535]<br/><br/>1433 | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在接聽的連接埠。 如果已在連接字串中指定連接埠號碼，就不需要對 SQLbrowser 進行要求。 同時指定 port 和 instanceName 時，會連接至指定的通訊埠。 然而，系統會驗證 **instanceName**，如果它不符合連接埠，則會發生錯誤。<br/><br/> **重要：** 建議您一律指定連接埠號碼，因為這比使用 SQLbrowser 更安全。 |
| queryTimeout<br/><br/>ssNoversion<br/><br/>-1 | 查詢發生逾時之前要等待的秒數。 預設值是-1，表示無限逾時。 設定此選項以 0 也表示無限期等候。 |
| responseBuffering<br/><br/>String<br/>["full" &#124; "adaptive"]<br/><br/>adaptive | 如果此屬性設定為 "adaptive"，就會在必要時緩衝處理可能的資料下限。 預設模式為 "adaptive"。<br/><br/> 如果此屬性設定為 "full"，執行陳述式時，就會從伺服器讀取整個結果集。<br/><br/> **注意：** 在將 JDBC Driver 從 1.2 版升級之後，預設的緩衝行為將成為 "adaptive"。 若您的應用程式永遠不會需要設定 "responseBuffering" 屬性，所以您想要在應用程式中繼續保留 1.2 版的預設行為，您必須在連接字串中或使用 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 物件的 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 方法將 responseBufferring 屬性設為 "full"。 |
| selectMethod<br/><br/>String<br/>["direct" &#124; "cursor"]<br/><br/>直接 | 如果將此屬性設定為 "cursor"，便會為在 **TYPE_FORWARD_ONLY** 及 **CONCUR_READ_ONLY** 資料指標之連線上建立的每個查詢，建立資料庫資料指標。 通常只有當應用程式所產生的結果集過於龐大而用戶端記憶體無法全數包含時，才需要此屬性。 此屬性設定為 "cursor" 時，用戶端記憶體中只會保留有限數量的結果集資料列。 <br/><br/>預設的行為是用戶端記憶體中保留了所有結果集資料列。 當應用程式處理所有資料列時，此行為提供最快的效能。 |
| sendStringParameters...<br/>AsUnicode<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>true | *sendStringParametersAsUnicode*<br/><br/>如果 **sendStringParametersAsUnicode** 屬性設定為 "true"，String 參數就會以 Unicode 格式傳送至伺服器。<br/><br/> 如果 **sendStringParametersAsUnicode** 屬性設定為 "false"，String 參數就會以非 Unicode 格式 (例如 ASCII/MBCS) 而非 Unicode 傳送至伺服器。<br/><br/> **sendStringParametersAsUnicode** 屬性的預設值為 "true"。<br/><br/> **注意：** 只有在傳送具有 **CHAR**、**VARCHAR** 或 **LONGVARCHAR** JDBC 類型的參數值時，才會檢查 **sendStringParametersAsUnicode** 屬性。 新的 JDBC 4.0 國際字元方法 (例如 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 和 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 類別的 setNString、setNCharacterStream 及 setNClob methods方法) 無論此屬性的設定為何，一律會以 Unicode 將其參數值傳送到伺服器。<br/><br/> 若要讓 **CHAR**、**VARCHAR** 和 **LONGVARCHAR** JDBC 資料類型達到最佳效能，應用程式應該將 **sendStringParametersAsUnicode** 屬性設定為 "false"，並且使用 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 和 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 類別的 setString、setCharacterStream 及 setClob 非國家字元方法。<br/><br/> 當應用程式將 **sendStringParametersAsUnicode** 屬性設定為 "false" 並且使用非國家字元方法來存取伺服器端的 Unicode 資料類型 (例如 **nchar**、**nvarchar** 和 **ntext**) 時，如果資料庫定序不支援非國家字元方法所傳遞之 String 參數中的字元，某些資料可能會遺失。<br/><br/> 請注意，應用程式應該使用 setNString、 setNCharacterStream、 和 setNClob 國家字元方法[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)並[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)類別**NCHAR**， **NVARCHAR**，並**LONGNVARCHAR** JDBC 資料類型。 |
| sendTimeAsDatetime<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>true | 這個屬性是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] JDBC Driver 3.0 中所新增。<br/><br/> 設為"true"以將 java.sql.Time 值傳送至伺服器，當做[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime**值。 <br/>將 java.sql.Time 值傳送至伺服器的設定為"false" [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **時間**值。<br/><br/> 這個屬性的預設值是目前"，則為 true 」，而且在未來版本可能變更。<br/><br/> 如需有關如何[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]設定 java.sql.Time 值然後傳送給伺服器，請參閱[如何設定 java.sql.Time 值傳送到伺服器](../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。 |
| serverName,<br/>伺服器<br/><br/>String<br/><br/>null | 執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦。<br/><br/> 您也可以指定 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)] 可用性群組的虛擬網路名稱。 請參閱[高可用性、 災害復原的 JDBC 驅動程式支援](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)如需詳細資訊。 |
| serverNameAsACE<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>false | 自 SQL Server 的 Microsoft JDBC 驅動程式 6.0 起，設為 "true" 表示驅動程式應將連接中的 Unicode 伺服器名稱轉譯成 ASCII 相容的 Unicode 編碼 (Punycode)。 若此設定為 false，驅動程式會使用使用者所提供的伺服器名稱進行連接。<br/><br/> 請參閱[JDBC Driver 的國際功能](../../connect/jdbc/international-features-of-the-jdbc-driver.md)如需詳細資訊。 |
| serverPreparedStatement...<br/>DiscardThreshold<br/><br/>Integer<br/><br/>10 | *serverPreparedStatementDiscardThreshold*<br/><br/>從 JDBC Driver 6.2 for SQL Server，此屬性可用來控制多少未完成已備妥陳述式捨棄動作 (<code>sp_unprepare</code>) 可以是未處理的每個連接，呼叫以清除 在伺服器上未處理的控制代碼會在執行之前. <br/><br/> 如果這個屬性設定為&lt;= 1，unprepare 關閉已備妥的陳述式會立即執行動作。 如果設定為&gt;1 這些呼叫會一起批次處理，以避免太頻繁呼叫 sp_unprepare 的額外負荷。 |
| serverSpn<br/><br/>String<br/><br/>null | 從 Microsoft JDBC Driver 4.2 for SQL Server 開始，此選擇性屬性可以用來指定 Java Kerberos 連接的服務主體名稱 (SPN)。  它用於搭配**authenticationScheme**。<br/><br/> 若要指定 SPN，可以使用下列格式："MSSQLSvc/fqdn:port@REALM"，其中 fqdn 是完整網域名稱，port 是連接埠號碼，REALM 是以大寫字母表示的 SQL Server Kerberos 領域。<br/><br/> 注意：如果該用戶端的預設領域 (如 Kerberos 設定中所指定) 與 SQL Server 的 Kerberos 領域相同，則 @REALM 是選擇性項目。<br/><br/> 如需有關使用**serverSpn** Java kerberos，請參閱[使用 Kerberos 整合式驗證來連接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。 |
| statementPooling...<br/>CacheSize<br/><br/>ssNoversion<br/><br/>0 | *statementPoolingCacheSize*<br/><br/>從 JDBC Driver 6.4 for SQL Server，此屬性可以用來驅動程式中啟用 備妥陳述式處理快取。 <br/><br/>這個屬性會定義陳述式加入集區快取大小。 <br/><br/>這個屬性只可以用於搭配**disableStatementPooling**連接屬性應該設定為"false"。 設定**disableStatementPooling**為"true"或**statementPoolingCacheSize**準備陳述式的 0 會停用來處理快取。|
| socketTimeout<br/><br/>ssNoversion<br/><br/>0 | 讀取的通訊端上發生逾時之前要等候的毫秒數，或接受。 預設值為 0，這表示無限逾時。 |
| sslProtocol<br/><br/>String<br/><br/>TLS | 從 JDBC Driver 6.4 for SQL Server，此屬性可以用來指定才會被視為安全的連線期間的 TLS 通訊協定。 <br/>可能的值為：**TLS**， **TLSv1**， **TLSv1.1**，和**TLSv1.2**。 <br/><br/>如需詳細資訊，請參閱 < [SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol)。 |
| transparentNetwork...<br/>IPResolution<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>true | *transparentNetworkIPResolution*<br/><br/>從 Microsoft JDBC Driver 6.0 for SQL Server，此屬性會提供更快速的偵測和 （目前） 作用中伺服器的連線。 可能的值為"true"和"false"，"true"是預設值。<br/><br/> Microsoft JDBC Driver 6.0 for SQL Server 前, 應用程式，必須設定連接字串包含"multiSubnetFailover = true"，表示它已連接到 AlwaysOn 可用性群組。 如果沒有設定**multiSubnetFailover**連接關鍵字為"true"，應用程式可能會遇到逾時在連接到 AlwaysOn 可用性群組。 從 Microsoft JDBC Driver 6.0 for SQL Server，應用程式不會不需要設定為 true，再 multiSubnetFailover。 <br/><br/>**注意：** 當 transparentNetworkIPResolution = 逾時為 true 時，第一次連接嘗試使用 500 毫秒。 任何後續的嘗試使用相同的逾時邏輯所用的 multiSubnetFailover 屬性。 |
| trustManagerClass<br/><br/>String<br/><br/>null | 自訂的完整的類別名稱<code>javax.net.ssl.TrustManager</code>實作。 |
| trustManager...<br/>ConstructorArg<br/><br/>String<br/><br/>null | *trustManagerConstructorArg*<br/><br/>選擇性引數傳遞至 TrustManager 的建構函式。 如果指定 trustManagerClass 並要求加密的連接時，自訂 TrustManager 會使用而不是預設系統 JVM 金鑰存放區為基礎的 TrustManager。 |
| trustServerCertificate<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>false | 設定為 "true" 以指定 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 將不會驗證 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSL 憑證。<br/><br/> 若為 "true"，當通訊層使用 SSL 加密時，會自動信任 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSL 憑證。<br/><br/> 若為"false"，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]驗證伺服器 SSL 憑證。 如果伺服器憑證驗證失敗，驅動程式將引發錯誤，並中止連線。 預設值為 "false"。 確定傳遞給 **serverName** 的值完全符合伺服器憑證中主體替代名稱內的一般名稱 (CN) 或 DNS 名稱，SSL 連線才會成功。 如需詳細資訊，請參閱 <<c0> [ 了解 SSL 支援](../../connect/jdbc/understanding-ssl-support.md)。<br/><br/> **注意：** 這個屬性可搭配**加密**/**驗證**屬性。 這個屬性只會影響伺服器 SSL 憑證驗證，才連線會使用 SSL 加密。 |
| trustStore<br/><br/>String<br/><br/>null | trustStore 憑證檔案的路徑 (包括檔案名稱)。 trustStore 檔案包含用戶端所信任之憑證的清單。<br/><br/> 未指定此屬性或將其設定為 null 時，驅動程式會依賴信任管理員 Factory 的查閱規則，決定要使用的憑證存放區。<br/><br/> **預設的 SunX509 TrustManagerFactory 會嘗試以下列的搜尋順序，找出信任的資料：**<br/><br/> 由 "javax.net.ssl.trustStore" Java Virtual Machine (JVM) 系統屬性所指定的檔案。<br/><br/> "&lt;java 主目錄&gt;/lib/security/jssecacerts" 檔案。<br/><br/> "&lt;java 主目錄&gt;/lib/security/cacerts" 檔案。<br/><br/> <br/><br/> 如需詳細資訊，請參閱 Sun Microsystems 網站上的 SUNX509 TrustManager 介面文件。<br/><br/> **注意：** 這個屬性只會影響憑證 trustStore 查閱，才連線會使用 SSL 加密並**trustServerCertificate**屬性設定為"false"。 |
| trustStorePassword<br/><br/>String<br/><br/>null | 用於檢查 trustStore 資料完整性的密碼。<br/><br/> 如果有設定 trustStore 屬性，但是未設定 trustStorePassword 屬性，就不會檢查 trustStore 的完整性。<br/><br/> 當 trustStore 和 trustStorePassword 屬性都未指定時，驅動程式會使用 JVM 系統屬性 "javax.net.ssl.trustStore" 和 "javax.net.ssl.trustStorePassword"。 如果未指定 "javax.net.ssl.trustStorePassword" 系統屬性，就不會檢查 trustStore 的完整性。<br/><br/> 如果未設定 trustStore 屬性，但是有設定 trustStorePassword 屬性，JDBC 驅動程式會使用 "javax.net.ssl.trustStore" 指定的檔案作為信任存放區，並使用指定的 trustStorePassword 來檢查信任存放區的完整性。 當用戶端應用程式不要在 JVM 系統屬性中儲存密碼時，可能需要這個動作。<br/><br/> **注意：** TrustStorePassword 屬性才會影響憑證 trustStore 查閱，才連線會使用 SSL 連線並**trustServerCertificate**屬性設定為"false"。 |
| trustStoreType<br/><br/>String<br/><br/>JKS | 設定這個屬性來指定要用於 FIPS 模式的信任存放區類型。 <br/><br/>可能的值都是**PKCS12**或 FIPS 提供者所定義的類型。 |
| useBulkCopyFor...<br/>BatchInsert<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>false | _useBulkCopyForBatchInsert_<br/><br/> 適用於 SQL Server 從 Microsoft JDBC Driver 7.0 開始，此連接屬性可以啟用來執行使用的批次插入作業時使用大量複製 API<code>java.sql.PreparedStatement</code>改進效能。 <br/><br/>只有當目標伺服器類型，這項功能是功能性**Azure 資料倉儲**。 它預設會停用，此屬性設定為"true"，若要啟用這項功能。 <br/></br> **重要事項：** 這項功能只支援完全參數化的 INSERT 查詢。 如果插入的查詢會結合其他的 SQL 查詢，或包含在值中的資料，執行會回到基本的批次插入作業。 <br/><br/> 如需有關如何使用這個屬性的詳細資訊，請參閱[批次插入作業中使用大量複製 API](use-bulk-copy-api-batch-insert-operation.md)|
| userName,<br/>user<br/><br/>String<br/>[&lt;=128 char]<br/><br/>null | 資料庫使用者，如果使用 SQL 使用者名稱和密碼的連線。<br/><br/>Kerberos 主體名稱和密碼的連接，這個屬性是設定為 Kerberos 主體名稱。 |
| workstationID<br/><br/>String<br/>[&lt;=128 char]<br/><br/>&lt;空字串&gt; | 工作站識別碼。 用以識別各種 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分析與記錄工具中的特定工作站。 <br/><br/>若未指定，將會使用 &lt;空字串&gt;。 |
| xopenStates<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>false | 設定為 "true"，以指定驅動程式傳回例外狀況的 XOPEN 相容狀態碼。 <br/><br/>預設為傳回 SQL 99 狀態碼。 |
| &nbsp; | &nbsp; |

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 會針對連線屬性採用伺服器預設值，但是 ANSI_DEFAULTS 和 IMPLICIT_TRANSACTIONS 除外。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 會自動將 ANSI_DEFAULTS 設定為 ON，並將 IMPLICIT_TRANSACTIONS 設定為 OFF。

> [!Important]
> 如果驗證已設為 ActiveDirectoryPassword，必須在 classpath 中包含下列的程式庫： [azure active directory-程式庫-針對-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)。 它可以在找到[Maven 儲存機制](https://mvnrepository.com/artifact/com.microsoft.azure/adal4j)。 若要下載的程式庫和其相依性最簡單的方式使用 Maven: 
> 1. 首先，您的系統上安裝 Maven 
> 2. 移至[GitHub 頁面](https://github.com/Microsoft/mssql-jdbc)的驅動程式
> 3. 下載 pom.xml 檔案
> 4. 執行下列 Maven 命令以下載程式庫和其相依性： `mvn dependency:copy-dependencies`

## <a name="see-also"></a>另請參閱

[使用 JDBC Driver 連接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
[FIPS 模式](../../connect/jdbc/fips-mode.md)
