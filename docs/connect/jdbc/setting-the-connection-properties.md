---
title: 設定連接屬性 |Microsoft 文件
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f1b62700-f046-488d-bd6b-a5cd8fc345b7
caps.latest.revision: 154
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 96122307555645f908e8c7ddc0a47bc71bda4f22
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32853233"
---
# <a name="setting-the-connection-properties"></a>設定連接屬性
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

連接字串屬性可以指定在不同的方式： 是  
-   做為名稱 = 值屬性，在連接 URL 中的，當您連線時使用 DriverManager 類別。
-   做為名稱 = 值屬性中的*屬性*DriverManager 類別中的 Connect 方法的參數。
-   作為驅動程式資料來源的適當 setter 方法中的值。 例如：  
  
    ```java
    datasource.setServerName(value)  
    datasource.setDatabaseName(value)  
    ```  
  
## <a name="remarks"></a>備註
屬性名稱需區分大小寫，而重複的屬性名稱將以下列順序解析：  
  
1.  API 引數 (例如使用者及密碼)
2.  屬性集合。  
3.  連接字串內的最後一個執行個體。
  
此外，屬性名稱可允許未知的值，JDBC 驅動程式並不會針對屬性值的大小寫進行驗證。

容許同義字並會依序解析，如同是重複的屬性名稱一般。

下表列出 JDBC 驅動程式目前所有可用的連接字串屬性。


| 屬性<br />型別<br />預設值 | Description |
| :------------------------------ | :---------- |
| accessToken<br />字串<br />null | 此屬性可以用於連接到 SQL 資料庫使用存取權杖。 **accessToken**無法使用連接 URL 設定。 |
| applicationIntent<br />字串<br />ReadWrite | 宣告連接到伺服器時的應用程式工作負載類型。 可能的值為**ReadOnly**和**ReadWrite**。 如需詳細資訊，請參閱[JDBC 驅動程式支援的高可用性、 災害復原](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)。 |
| applicationName<br /><br />字串<br />[&lt;= 128 char]<br /><br />null | 應用程式名稱，或 「[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]"如果未提供名稱。 用來識別特定的應用程式中各種[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]分析和記錄工具。 |
| 驗證 (authentication)<br />字串<br />NotSpecified | 此選用性屬性之 SQL Server 的 Microsoft JDBC Driver 6.0 開始，表示要用於連接的 SQL 驗證方法。 可能的值為**ActiveDirectoryIntegrated**， **ActiveDirectoryPassword**， **SqlPassword**，且預設**NotSpecified**.<br /><br /> 使用**ActiveDirectoryIntegrated**連接到 SQL 資料庫使用整合式的 Windows 驗證。<br /><br /> 使用**ActiveDirectoryPassword**連接到 SQL 資料庫使用的 Azure AD 主體名稱和密碼。<br /><br /> 使用**SqlPassword**來連接 SQL Server 使用**userName**/**使用者**和**密碼**屬性。<br /><br /> 使用**NotSpecified**如果不需要這些驗證方法的任何一個。<br /><br /> **重要事項：** 如果驗證已設為 ActiveDirectoryIntegrated，必須安裝下列兩個程式庫： **SQLJDBC_AUTH。DLL** （適用於 JDBC 驅動程式套件） 和 Azure Active Directory Authentication Library for SQL Server (**ADALSQL。DLL**) 可在多國語言 （x86 和 amd64） 從下載中心[Microsoft Active Directory Authentication Library for Microsoft SQL Server](https://www.microsoft.com/download/details.aspx?id=48742)。 JDBC 驅動程式只支援版本**1.0.2028.318 （含） 以上**ADALSQL 的。DLL。<br /><br /> **注意：** 當驗證 屬性設定為任何值以外**NotSpecified**，根據預設，驅動程式會使用 Secure Sockets Layer (SSL) 加密。<br /><br /> 如需如何設定 Azure Active Directory 驗證的詳細資訊，請造訪[連接到 SQL 資料庫使用 Azure Active Directory 驗證](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。 |
| authenticationScheme<br />字串<br />"NativeAuthentication" | 表示您希望應用程式使用的整合式安全性種類。 可能的值為**JavaKerberos**和預設**NativeAuthentication**。<br /><br /> 當使用**authenticationScheme = JavaKerberos**，您必須指定完整的網域名稱 (FQDN) 中**serverName**或**serverSpn**屬性。 否則，就會發生錯誤 （Kerberos 資料庫中找不到伺服器）。<br /><br /> 如需有關使用**authenticationScheme**，請參閱[使用 Kerberos 整合式驗證來連接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。 |
| columnEncryptionSetting<br /><br />字串<br />["Enabled"&#124;"Disabled"]<br /><br />已停用 | 若要使用一律加密 (AE) 功能以 Microsoft JDBC Driver 6.0 for SQL Server 設定為"Enabled"。 如有啟用 AE，JDBC 驅動程式會透明加密及解密儲存在 SQL Server 中經過加密之資料庫資料行中的敏感性資料。<br /><br /> 請參閱[使用一律加密與 JDBC 驅動程式](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)如需詳細資訊。<br /><br /> **注意：** 永遠加密 是適用於 SQL Server 2016 或更新版本。 |
| 資料庫名稱，<br />[資料庫]<br /><br />字串<br />[&lt;= 128 char]<br /><br />null | 要連接的資料庫名稱。 如果沒有指定，將連接到預設資料庫。 |
| disableStatementPooling<br /><br />boolean<br />["true"&#124;"false"]<br /><br />true | 表示是否應該用於陳述式集區的旗標。 |
| enablePrepareOnFirst...<br />PreparedStatementCall<br /><br />boolean<br />["true"&#124;"false"]<br />false | *enablePrepareOnFirstPreparedStatementCall*<br />如果這項設定設為 false 的已備妥的陳述式的第一次執行 sp_executesql 不準備的陳述式，它會呼叫 sp_prepexec 會發生的第二次執行之後和實際安裝的已備妥的陳述式控制代碼。 |
| encrypt<br /><br />boolean<br />["true"&#124;"false"]<br /><br />false | 設定為"true"以指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]使用安全通訊端層 (SSL) 加密，如果伺服器已安裝憑證，用戶端與伺服器之間傳送的所有資料。 預設值為 false。<br /><br /> 從 Microsoft JDBC Driver 6.0 for SQL Server，還有新連線設定 「 驗證 」，根據預設，會使用 SSL 加密。 如需詳細資訊，請參閱 'authentication' 屬性。 |
| failoverPartner<br />字串<br />null | 用於資料庫鏡像組態的容錯移轉伺服器名稱。 初始連接到主體伺服器若失敗，將使用此屬性；在建立初始連接之後，將忽略此屬性。 必須與 databaseName 屬性一起使用。<br /><br /> **注意：** 驅動程式不支援指定容錯移轉夥伴執行個體的伺服器執行個體連接埠號碼當做 failoverPartner 屬性中的連接字串的一部分。 不過，指定的 serverName、 instanceName 和 portNumber 屬性，主體伺服器執行個體和 failoverPartner 屬性的容錯移轉的支援相同的連接字串中的夥伴執行個體。<br /><br /> 如果您指定虛擬網路名稱在**伺服器**連接屬性，您無法使用資料庫鏡像。 請參閱[JDBC 驅動程式支援的高可用性、 災害復原](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)如需詳細資訊。 |
| fips<br /><br />boolean<br />["，則為 true/false"]<br /><br />"false" | 這個屬性應該是 FIPS 已啟用則為 JVM **true**。 |
| fipsProvider<br />字串<br />null | JVM 中所設定的 FIPS 提供者。 例如，BCFIPS 或 SunPKCS11 NSS。 6.4.0-版本中移除，請參閱詳細資料[這裡](https://github.com/Microsoft/mssql-jdbc/pull/460)。 |
| gsscredential<br />org.ietf.jgss.GSSCredential<br />null | 之 SQL Server 的 Microsoft JDBC 驅動程式 6.2 開始，可以在這個屬性中傳遞使用者認證來進行 Kerberos 限制委派。 <br />這應搭配**integratedSecurity**為**true**和**JavaKerberos** **authenticationscheme**。 |
| hostNameInCertificate<br />字串<br />null | 要用於驗證的主機名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SSL 憑證。<br /><br /> 如果 hostNameInCertificate 屬性，未指定或設為 null，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]使用**serverName**屬性值做為主機名稱在連接 URL 來驗證上的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SSL 憑證。<br /><br /> **注意：** 這個屬性用於搭配**加密**/**驗證**屬性和**trustServerCertificate**屬性。 這個屬性會影響憑證驗證，如果且只有在連線使用安全通訊端層 (SSL) 加密和**trustServerCertificate**設為"false"。 請確定傳遞給的值**hostNameInCertificate**完全相符的一般名稱 (CN) 或 DNS 名稱中主旨替代名稱 (SAN) SSL 連接的伺服器憑證中才會成功。 如需詳細資訊，請參閱[了解 SSL 支援](../../connect/jdbc/understanding-ssl-support.md)。 |
| INSTANCENAME<br /><br />字串<br />[&lt;= 128 char]<br /><br />null | [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]來連接到執行個體名稱。 如果未指定，將會連接到預設執行個體。 如果已指定 instanceName 與通訊埠，請參閱通訊埠的注意事項。<br /><br /> 如果您指定虛擬網路名稱在**伺服器**連接屬性，您不能使用**instanceName**連接屬性。 請參閱[JDBC 驅動程式支援的高可用性、 災害復原](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)如需詳細資訊。 |
| integratedSecurity<br /><br />boolean<br />["true"&#124;"false"]<br /><br />false | 設定為"true"，表示會使用的 Windows 認證[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Windows 作業系統上。 若為 "true"，JDBC 驅動程式會搜尋本機電腦認證快取，以取得電腦上已提供的認證或網路登入。<br /><br /> 設定為"true"(與**authenticationscheme = JavaKerberos**)，以表示會使用的 Kerberos 認證[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如需有關 Kerberos 驗證的詳細資訊，請參閱[使用 Kerberos 整合式驗證來連接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。 <br /><br /> 若為 "false"，必須提供使用者名稱及密碼。 |
| jaasConfigurationName<br />字串<br />SQLJDBCDriver | 每個連接至 SQL Server 之 SQL Server 的 Microsoft JDBC 驅動程式 6.2 開始，可以有它自己建立 Kerberos 連接的 JAAS 登入組態檔。 這個屬性可以傳遞登入組態檔的名稱。 <br /> 根據預設，驅動程式設定屬性`useDefaultCcache = true`如 IBM JVMs 和`useTicketCache = true`的其他 JVMs。 |
| keyStoreAuthentication<br />字串<br />null | 從 Microsoft JDBC Driver 6.0 for SQL Server，這個屬性識別要順暢地設定為使用 永遠加密連線的金鑰存放區，並判斷用來驗證的金鑰存放區的驗證機制。 Microsoft JDBC Driver 6.0 for SQL Server 設定最多可支援 Java 金鑰存放區的順暢地使用您要設定這個屬性 」**keyStoreAuthentication = JavaKeyStorePassword**"。 請注意，若要使用這個屬性，您也需要設定**keyStoreLocation**和**keyStoreSecret** Java 金鑰存放區的屬性。 <br /><br />如需詳細資訊，請瀏覽[使用一律加密與 JDBC 驅動程式](https://msdn.microsoft.com/library/mt591987%28v=sql.110%29.aspx?f=255&MSPPError=-2147217396)。 |
| keyStoreLocation<br />字串<br />null | 當**keyStoreAuthentication = JavaKeyStorePassword**、 **keyStoreLocation**屬性會識別儲存以用於永遠加密的資料行主要金鑰的 Java keystore 檔案路徑資料。 請注意，此路徑必須包含的金鑰存放區檔案名稱。<br /><br />如需詳細資訊，請瀏覽[使用一律加密與 JDBC 驅動程式](https://msdn.microsoft.com/library/mt591987%28v=sql.110%29.aspx?f=255&MSPPError=-2147217396)。 |
| keyStoreSecret<br />字串<br />null | 當**keyStoreAuthentication = JavaKeyStorePassword**、 **keyStoreSecret**屬性會識別要用於 keystore 以及金鑰的密碼。 請注意，使用 Java 金鑰存放區的金鑰存放區和金鑰的密碼必須相同。<br /><br />如需詳細資訊，請瀏覽[使用一律加密與 JDBC 驅動程式](https://msdn.microsoft.com/library/mt591987%28v=sql.110%29.aspx?f=255&MSPPError=-2147217396)。 |
| lastUpdateCount<br /><br />boolean<br />["true"&#124;"false"]<br /><br />true | "true" 值只會從傳至伺服器的 SQL 陳述式傳回上次更新計數，而且它可以用在單一 SELECT、INSERT 或 DELETE 陳述式，以忽略伺服器觸發程序所導致的其他更新計數。 將此屬性設為 "false" 會導致傳回所有更新計數，包括伺服器觸發程序所傳回的更新計數。<br /><br /> **注意：** 搭配使用時，此屬性只適用於[executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)方法。 所有其他執行方法傳回所有結果，並更新計數。 這個屬性只會影響伺服器觸發程序所傳回的更新計數。 它不會影響結果集或觸發程序執行期間產生的錯誤。 |
| lockTimeout<br />int<br />-1 | 等候資料庫報告鎖定逾時的毫秒數。預設的行為是無限期等待。 如果已指定，則此值為連接上所有陳述式的預設值。 請注意， **Statement.setQueryTimeout()** 可以用來設定特定陳述式的逾時。 此值可以為 0，表示不等待。 |
| loginTimeout<br /><br />int<br />[0..65535]<br /><br />15 | 驅動程式應等待失敗連接逾時的秒數。 值為零表示此逾時為預設系統逾時，預設指定為 15 秒。 非零值為驅動程式應等待失敗連接之逾時的秒數。<br /><br /> 如果您指定虛擬網路名稱在**伺服器**連接屬性，您應該指定三分鐘或更多，提供足夠的時間才會成功的容錯移轉連接的逾時值。 請參閱[JDBC 驅動程式支援的高可用性、 災害復原](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)如需詳細資訊。 |
| multiSubnetFailover<br />布林<br />false | 請務必指定**multiSubnetFailover = true**連接到可用性群組接聽程式時[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]可用性群組或[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]容錯移轉叢集執行個體。 **multiSubnetFailover = true**設定[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]來提供更快速偵測與 （目前） 使用中伺服器的連接。 可能的值為 true 和 false。 請參閱[JDBC 驅動程式支援的高可用性、 災害復原](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)如需詳細資訊。<br /><br /> 您可以程式設計方式存取**multiSubnetFailover**連接屬性[getPropertyInfo](../../connect/jdbc/reference/getpropertyinfo-method-sqlserverdriver.md)， [getMultiSubnetFailover](../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)，和[setMultiSubnetFailover](../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)。<br /><br /> **注意：** 從 Microsoft JDBC Driver 6.0 for SQL Server 已不再需要設定為 true，連接到可用性群組接聽程式時 multiSubnetFailover。 新的屬性，**則 transparentNetworkIPResolution**，這預設啟用，提供偵測與連接到 （目前） 使用中的伺服器。 |
| packetSize<br /><br />int<br />[-1 &#124; 0 &#124; 512..32767]<br /><br />8000 | 用來與 SQL Server 通訊的網路封包大小 (以位元組指定)。 -1 這個值表示使用伺服器的預設封包大小。 0 這個值表示使用最大值，也就是 32767。 如果這個屬性設定為可接受的範圍以外的值，就會發生例外狀況。<br /><br /> **重要事項：** 我們不建議使用 packetSize 屬性，啟用加密時 (加密 = true)。 否則，驅動程式可能會引發連接錯誤。 如需詳細資訊，請參閱[setPacketSize](../../connect/jdbc/reference/setpacketsize-method-sqlserverdatasource.md)方法[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)類別。 |
| 密碼<br /><br />字串<br />[&lt;= 128 char]<br /><br />null | 資料庫密碼，如果連線與 SQL 使用者名稱和密碼。<br />Kerberos 連接的主體名稱和密碼，此屬性設定為 Kerberos 主體密碼。 |
| 通訊埠編號，<br />port<br /><br />int<br />[0..65535]<br /><br />1433 | 連接埠其中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]正在接聽。 如果連接字串中指定的連接埠號碼，不需要對 SQLbrowser 要求。 同時指定 port 和 instanceName 時，會連接至指定的通訊埠。 不過， **instanceName**驗證時，如果它不符合通訊埠，會擲回錯誤。<br /><br /> **重要事項：** 建議，永遠指定連接埠號碼，因為這是比使用 SQLbrowser 更安全。 |
| queryTimeout<br />int<br />0 | 查詢發生逾時之前要等待的秒數。 預設值為 0，這表示無限逾時。 |
| responseBuffering<br /><br />字串<br />[「 完整 」 &#124; "adaptive"]<br /><br />adaptive | 如果此屬性設定為 "adaptive"，就會在必要時緩衝處理可能的資料下限。 預設模式為"adaptive"。<br /><br /> 如果此屬性設定為 "full"，執行陳述式時，就會從伺服器讀取整個結果集。<br /><br /> **注意：** 升級之後 JDBC driver 從 1.2 版，預設的緩衝行為將成為"adaptive"。 如果您的應用程式從未設定"responseBuffering"屬性，而且您想要在應用程式中保留 1.2 版的預設行為，您就必須設定為"full"responseBufferring 屬性，在連接屬性或使用[setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)物件。 |
| selectMethod<br /><br />字串<br />[「 直接 」 &#124; "cursor"]<br /><br />直接 | 如果將此屬性設定為 "cursor"，便會為每個在 TYPE_FORWARD_ONLY 及 CONCUR_READ_ONLY 資料指標之連接上建立的查詢，建立資料庫資料指標。 只有當應用程式所產生的大型結果集，無法完全包含在用戶端記憶體中通常需要這個屬性。 此屬性設定為 "cursor" 時，用戶端記憶體中只會保留有限數量的結果集資料列。 預設的行為是用戶端記憶體中保留了所有結果集資料列。 當應用程式處理所有資料列時，此行為提供最快的效能。 |
| sendStringParameters...<br />AsUnicode<br /><br />boolean<br />["true" &#124; "false"]<br /><br />true | *sendStringParametersAsUnicode*<br />如果**sendStringParametersAsUnicode**屬性設定為 [true]，參數就會傳送到伺服器以 Unicode 格式的字串。<br /><br /> 如果**sendStringParametersAsUnicode**屬性設定為"false"，String 參數傳送至非 Unicode 格式 （例如 ASCII/MBCS) 而非 Unicode 伺服器。<br /><br /> 預設值為**sendStringParametersAsUnicode**屬性為"true"。<br /><br /> **注意：** **sendStringParametersAsUnicode**傳送的參數值時，才會檢查屬性**CHAR**， **VARCHAR**，或**LONGVARCHAR** JDBC 類型。 新的 JDBC 4.0 國家字元方法，例如的 setNString、 setNCharacterStream、 和 setNClob 方法[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)和[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)一律類別將參數值傳送至以 Unicode 伺服器，不論這個屬性的設定。<br /><br /> 為了達到最佳效能與**CHAR**， **VARCHAR**，和**LONGVARCHAR** JDBC 資料類型，應用程式應該設定**sendStringParametersAsUnicode**屬性設為"false"，並使用 setString、 setCharacterStream、 和非國家字元方法 setClob [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)和[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)類別。<br /><br /> 當應用程式會設定**sendStringParametersAsUnicode**屬性為"false"並且使用非國家字元方法來存取 Unicode 資料類型在伺服器端 (例如**nchar**， **nvarchar**和**ntext**)，如果資料庫定序不支援非國家字元方法所傳遞之 String 參數中的字元，某些資料可能會遺失。<br /><br /> 請注意，應用程式應該使用 setNString、 setNCharacterStream、 和 setNClob 國家字元方法[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)和[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)類別的**NCHAR**， **NVARCHAR**，和**LONGNVARCHAR** JDBC 資料類型。 |
| sendTimeAsDatetime<br /><br />boolean<br />["true" &#124; "false"]<br /><br />false | 這個屬性已加入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]JDBC 驅動程式 3.0。<br /><br /> 若為 true，要將 java.sql.Time 值傳送至伺服器的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **datetime**值。<br /><br /> 若為 false，要將 java.sql.Time 值傳送至伺服器的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**時間**值。<br /><br /> **sendTimeAsDatetime**也可以修改以程式設計的方式與[SQLServerDataSource.setSendTimeAsDatetime](../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)。<br /><br /> 這個屬性的預設值在後續版本可能會變更。<br /><br /> 如需有關如何[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]設定 java.sql.Time 值然後傳送給伺服器，請參閱[如何設定 java.sql.Time 值傳送給伺服器](../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。 |
| 伺服器名稱，<br />伺服器<br /><br />字串<br /><br />null | 執行的電腦[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br /> 您也可以指定虛擬網路名稱的[!INCLUDE[ssHADR](../../includes/sshadr_md.md)]可用性群組。 請參閱[JDBC 驅動程式支援的高可用性、 災害復原](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)如需詳細資訊。 |
| serverNameAsACE<br /><br />boolean<br />["true" &#124; "false"]<br /><br />false | 自 SQL Server 的 Microsoft JDBC 驅動程式 6.0 起，設為 "true" 表示驅動程式應將連接中的 Unicode 伺服器名稱轉譯成 ASCII 相容的 Unicode 編碼 (Punycode)。 若此設定為 false，驅動程式會使用使用者所提供的伺服器名稱進行連接。<br /><br /> 請參閱[JDBC driver 的國際功能](../../connect/jdbc/international-features-of-the-jdbc-driver.md)如需詳細資訊。 |
| serverPreparedStatement...<br />DiscardThreshold<br />Integer<br />10 | *serverPreparedStatementDiscardThreshold*<br />控制多少未完成備妥的陳述式捨棄之前呼叫，以清除伺服器上未處理的控制代碼將會執行動作 (sp_unprepare) 可以是未處理的每個連接。 如果設定為&lt;= 1 unprepare 動作會立即關閉已備妥的陳述式上執行。 如果設定為&gt;1 這些呼叫會一起批次處理，以避免太過頻繁呼叫 sp_unprepare 的額外負荷。 |
| serverSpn<br />字串<br />null | 從 Microsoft JDBC Driver 4.2 for SQL Server 開始，此選擇性屬性可以用來指定 Java Kerberos 連接的服務主體名稱 (SPN)。  它用於搭配**authenticationScheme**。<br /><br /> 若要指定 SPN，它可以採用的格式:"MSSQLSvc/fqdn:port@REALM"其中 fqdn 是完整的網域名稱，port 是連接埠號碼，而領域是大寫字母中的 SQL Server 的 Kerberos 領域。<br /><br /> 注意：@REALM是選擇性的預設領域 （如 Kerberos 設定中指定） 用戶端是否與 SQL Server 的 Kerberos 領域相同。<br /><br /> 如需有關使用**serverSpn** Java kerberos，請參閱[使用 Kerberos 整合式驗證來連接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。 |
| statementPooling...<br />CacheSize<br />int<br />0 | *statementPoolingCacheSize*<br />定義陳述式加入集區快取的大小。 0 表示無快取。 |
| socketTimeout<br />int<br />0 | 讀取通訊端上發生逾時之前要等候的毫秒數，或接受。 預設值為 0，這表示無限逾時。 |
| sslProtocol<br />字串<br />TLS | 版本 6.4.0 中新增。 設定此值，指定 TLS 通訊協定關鍵字。 可能的值為： **TLS**， **TLSv1**， **TLSv1.1**，和**TLSv1.2**。 如需詳細資訊，請參閱[SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol)。 |
| transparentNetwork...<br />IPResolution<br /><br />boolean<br />["true" &#124; "false"]<br /><br />true | *transparentNetworkIPResolution*<br />從 Microsoft JDBC Driver 6.0 for SQL Server，此屬性，則 transparentNetworkIPResolution，提供更快速偵測與連接到 （目前） 使用中的伺服器。 可能的值為 true 和 false 為 true 會當做預設值。<br /><br /> 在 Microsoft JDBC Driver 6.0 for SQL Server 之前, 的應用程式必須設定連接字串包含"multiSubnetFailover = true"以表示它已連接到 AlwaysOn 可用性群組。 如果沒有設定為 true 的 multiSubnetFailover 連接關鍵字，應用程式連接到 AlwaysOn 可用性群組時可能會遇到逾時。 從 Microsoft JDBC Driver 6.0 for SQL Server，應用程式不會不需要設定為 true，不再 multiSubnetFailover。 <br /><br />**注意：** 時則 transparentNetworkIPResolution = 逾時為 true 時，第一個連接嘗試會使用 500 毫秒。 任何後續的嘗試使用相同的逾時邏輯所用的 multiSubnetFailover 屬性。 |
| trustManagerClass<br />字串<br />null | 自訂 javax.net.ssl.TrustManager 完整的類別名稱。 |
| trustManager...<br />ConstructorArg<br />字串<br />null | *trustManagerConstructorArg*<br />選擇性引數傳遞至 TrustManager 的建構函式。 如果指定 trustManagerClass 要求加密的連接時，自訂 TrustManager 使用而不是預設系統 JVM 金鑰存放區為基礎的 TrustManager。 |
| trustServerCertificate<br /><br />boolean<br />["true" &#124; "false"]<br /><br />false | 設定為"true"以指定[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]不會驗證[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SSL 憑證。<br /><br /> 若為"true"，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]當使用 SSL 加密通訊層時，會自動信任 SSL 憑證。<br /><br /> 若為"false"[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]會驗證伺服器 SSL 憑證。 如果伺服器憑證驗證失敗，驅動程式就會引發錯誤，並終止連線。 預設值為 "false"。 請確定傳遞給的值**serverName**完全符合主體替代名稱中的 SSL 連接的伺服器憑證中成功的一般名稱 (CN) 或 DNS 名稱。 如需詳細資訊，請參閱[了解 SSL 支援](../../connect/jdbc/understanding-ssl-support.md)。<br /><br /> **注意：** 這個屬性用於搭配**加密**/**驗證**屬性。 如果且只有在連線使用 SSL 加密，這個屬性只會影響伺服器 SSL 憑證驗證。 |
| trustStore<br />字串<br />null | trustStore 憑證檔案的路徑 (包括檔案名稱)。 trustStore 檔案包含用戶端所信任之憑證的清單。<br /><br /> 當未指定此屬性，或設為 null，驅動程式會依賴信任管理員 factory 的查閱規則，以決定要使用的憑證存放區。<br /><br /> **預設的 SunX509 TrustManagerFactory 會嘗試以下列搜尋順序找出信任的資料：**<br /><br /> 由 "javax.net.ssl.trustStore" Java Virtual Machine (JVM) 系統屬性所指定的檔案。<br /><br /> 「&lt;java 首頁&gt;/lib/security/jssecacerts"檔案。<br /><br /> 「&lt;java 首頁&gt;/lib/security/cacerts"檔案。<br /><br /> <br /><br /> 如需詳細資訊，請參閱 Sun Microsystems 網站上的 SUNX509 TrustManager 介面文件。<br /><br /> **注意：** 這個屬性只會影響憑證 trustStore 查閱，如果且只有在連線使用 SSL 加密和**trustServerCertificate**屬性設定為"false"。 |
| trustStorePassword<br />字串<br />null | 用於檢查 trustStore 資料完整性的密碼。<br /><br /> 如果有設定 trustStore 屬性，但是未設定 trustStorePassword 屬性，就不會檢查 trustStore 的完整性。<br /><br /> 當 trustStore 和 trustStorePassword 屬性都未指定時，則驅動程式會使用 JVM 系統屬性"javax.net.ssl.trustStore"和"javax.net.ssl.trustStorePassword"。 如果未指定 "javax.net.ssl.trustStorePassword" 系統屬性，就不會檢查 trustStore 的完整性。<br /><br /> 如果未設定 trustStore 屬性，但有設定 trustStorePassword 屬性，JDBC 驅動程式會使用"javax.net.ssl.trustStore"所指定的檔案做為信任存放區，就會使用指定的 trustStorePassword 檢查信任存放區的完整性。 當用戶端應用程式不要在 JVM 系統屬性中儲存密碼時，可能需要這個動作。<br /><br /> **注意：** trustStorePassword 屬性才會影響憑證 trustStore 查閱，如果且只有在連線使用 SSL 連線和**trustServerCertificate**屬性設定為"false"。 |
| trustStoreType<br />字串<br />JKS | FIPS 模式設定的信任存放區類型 PKCS12 或型別 FIPS 提供者所定義。 |
| 使用者名稱，<br />user<br /><br />字串<br />[&lt;= 128 char]<br /><br />null | 資料庫使用者，如果連線與 SQL 使用者名稱和密碼。<br />Kerberos 連接的主體名稱和密碼，這個屬性設定為 Kerberos 主體名稱。 |
| workstationID<br /><br />字串<br />[&lt;= 128 char]<br /><br />&lt;空字串&gt; | 工作站識別碼。 用來識別各種中的特定工作站[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]分析和記錄工具。 如果未指定，&lt;空字串&gt;用。 |
| xopenStates<br /><br />boolean<br />["true" &#124; "false"]<br /><br />false | 設定為 "true"，以指定驅動程式傳回例外狀況的 XOPEN 相容狀態碼。 預設為傳回 SQL 99 狀態碼。 |
| &nbsp; | &nbsp; |


> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]採用伺服器預設值，針對連接屬性，但是 ANSI_DEFAULTS 和 IMPLICIT_TRANSACTIONS 除外。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]自動將 ANSI_DEFAULTS 設為 ON 並將 IMPLICIT_TRANSACTIONS 為 OFF。  

> [!Important]
> 如果驗證已設為 ActiveDirectoryPassword，必須在 classpath 中包含下列的程式庫： [azure-activedirectory-程式庫-如-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)。 您可以找到上[Maven 儲存機制](https://mvnrepository.com/artifact/com.microsoft.azure/adal4j)。 若要下載的程式庫和其相依性最簡單的方式使用 Maven: 
> 1. 首先，在系統上安裝 Maven 
> 2. 移至[GitHub 頁面](https://github.com/Microsoft/mssql-jdbc)驅動程式
> 3. 下載 pom.xml 檔案
> 4. 執行下列的 Maven 命令，以下載的程式庫和其相依性： `mvn dependency:copy-dependencies`

## <a name="see-also"></a>另請參閱
[使用 JDBC Driver 連接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
[FIPS 模式](../../connect/jdbc/fips-mode.md)

