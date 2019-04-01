---
title: JDBC 驅動程式的版本資訊 |Microsoft Docs
ms.custom: ''
ms.date: 02/07/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 083eda191d51ec7043f24511d03c90beff9bfe84
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2019
ms.locfileid: "58657733"
---
# <a name="release-notes-for-the-microsoft-jdbc-driver"></a>Microsoft JDBC Driver 的版本資訊

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文列出的版本_Microsoft JDBC Driver for SQL Server_。 如需每個發行版本，是名為的變更，並將其描述中。

## <a name="721"></a>7.2.1

### <a name="compliance"></a>遵循

2019 年 2 月 11 日

| 合規性變更 | 詳細資料 |
| :---------------- | :------ |
| 下載 JDBC 驅動程式 7.2 最新的更新。 | &bull; &nbsp; [Microsoft 下載中心](https://go.microsoft.com/fwlink/?linkid=2063159)<br/>&bull; &nbsp; [GitHub, 7.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.1)<br/>&bull; &nbsp; [Maven 中心](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| JDBC API 規格的 4.2 完全相容。 | 7.2 的封裝中的 jar 會命名為根據 Java 版本相容性。<br/><br/>比方說，7.2 封裝 mssql-jdbc-7.2.1.jre11.jar 檔案應該搭配 Java 11。 |
| 除了 JDK 1.8 之外，還與 Java Development Kit (JDK) 11.0 版相容。 | 適用於 SQL Server 的 Microsoft JDBC Driver 7.2 現在是 Java Development Kit (JDK) 版本為 11.0 除了 JDK 1.8 具有相容的。 |
| &nbsp; | &nbsp; |

> [!NOTE]
> 找不到於 2019 年 1 月 31 日發行的 JDBC 7.2 發行至 Web (RTW) 驅動程式中的 SQL 陳述式剖析的問題。 變更已回復，並於 2019 年 2 月 11 日發行新的 jar （版本 7.2.1）。
>
> 更新專案以使用 7.2.1 發行的 jar。 如需詳細資訊，請檢視版本資訊[GitHub 7.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.1)。

### <a name="active-directory-managed-service-identity-msi-authentication"></a>Active Directory_受控服務識別_(MSI) 驗證

| MSI 變更 | 詳細資料 |
| :--------- | :------ |
| 支援 Active Directory 受控服務識別 (MSI) 驗證模式。 | 這種驗證模式是適用於 Azure 資源與啟用的 「 身分識別 」 功能的支援。<br/><br/>若要取得的驅動程式支援這兩種類型的管理系統的身分識別 (MSI) **accessToken**來建立安全的連線。 |
| 更多詳細資料和範例應用程式使用此驗證模式。 | 請參閱[使用 Azure Active Directory 驗證連線](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)。 |
| &nbsp; | &nbsp; |

### <a name="introduces-open-service-gateway-initiative-osgi-support"></a>導入了_開啟服務閘道 Initiative_ (OSGi) 支援

| OSGi 變更 | 詳細資料 |
| :---------- | :------ |
| **DataSourceFactory**新增的實作。 | &bull; &nbsp; `org.osgi.service.jdbc.DataSourceFactory`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.SQLServerDataSourceFactory` |
| **啟動項**新增的實作。 | &bull; &nbsp; `org.osgi.framework.BundleActivator`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.Activator` |
| &nbsp; | &nbsp; |

### <a name="introduces-sqlservererror-apis"></a>導入了_SQLServerError_ Api

| 錯誤 API 變更 | 詳細資料 |
| :--------------- | :------ |
| 導入 SQLServerError API。 | Getter Api 來擷取從伺服器產生的錯誤相關的其他詳細資料。<br/><br/>&bull; &nbsp; `SQLServerException.getSQLServerError()`<br/>&bull; &nbsp; `SQLServerError` |
| 其他詳細資料。 | 請參閱[處理錯誤](../../connect/jdbc/handling-errors.md)。 |
| &nbsp; | &nbsp; |

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-163"></a>已更新「適用於 Java 的 Microsoft Azure Active Directory 驗證程式庫 (ADAL4J)」，1.6.3 版

| ADAL4J 變更 | 詳細資料 |
| :------------ | :------ |
| 更新版本 1.6.3 ADAL4J 上的其 Maven 相依性。 | &nbsp; |
| 導入了_AutoRest 的 Java 用戶端執行階段_為 Maven 相依性，1.6.5 的版本。 | &nbsp; |
| 其他詳細資料。 | 請參閱 [Microsoft JDBC Driver for SQL Server 的功能相依性](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)。 |
| &nbsp; | &nbsp; |

### <a name="updated-microsoft-azure-key-vault-sdk-for-java-version-120"></a>更新_Microsoft Azure 金鑰保存庫 SDK for Java_，1.2.0 版

| 金鑰保存庫 SDK 變更 | 詳細資料 |
| :------------------- | :------ |
| 在更新其 Maven 相依性_Microsoft Azure 金鑰保存庫 SDK for Java_到 1.2.0 版。 | &nbsp; |
| 引進 _Microsoft Azure SDK for Key Vault WebKey_ 作為 Maven 相依性，1.2.0 版。 | &nbsp; |
| 其他詳細資料。 | 請參閱 [Microsoft JDBC Driver for SQL Server 的功能相依性](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)。 |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>已知問題

| 已知問題 | 詳細資料 |
| :----------- | :------ |
| 參數化的查詢，在某些情況下。 | 7.2 的版本中，將會 v7.2.1，更新將會發行將 2019 年 2 月來解決此問題。 |
| &nbsp; | &nbsp; |

## <a name="70"></a>7.0

適用於 SQL Server 的 Microsoft JDBC Driver 7.0 是完全符合 JDBC API 規格的 4.2。 在 7.0 版的封裝中的 jar 會命名為根據 Java 版本相容性。 比方說，從 7.0 封裝 mssql-jdbc-7.0.0.jre10.jar 檔案應該搭配 Java 10。

### <a name="support-for-jdk-10"></a>JDK 10 支援

適用於 SQL Server 的 Microsoft JDBC Driver 7.0 現在是相容的 Java Development Kit (JDK) 除了 JDK 1.8 10.0 版使用。 此更新也會公開駕`Automatic-Module-Name`做為`com.microsoft.sqlserver.jdbc`透過其資訊清單檔。

### <a name="support-for-spatial-datatypes"></a>空間資料類型的支援

適用於 SQL Server 的 Microsoft JDBC Driver 7.0 現在提供 SQL Server 空間資料類型，Geography 和 Geometry 的支援。 如需有關空間資料類型的 Api 和使用方式的詳細資訊，請參閱 <<c0> [ 使用空間資料型別](../../connect/jdbc/use-spatial-datatypes.md)。

### <a name="implementation-for-jdbc-43-introduced-javasqlconnection-apis-beginrequest-and-endrequest"></a>為 JDBC 4.3 引進的 java.sql.Connection API beginRequest() 和 endRequest() 新增實作

針對 SQL Server 現在實作的 Microsoft JDBC 驅動程式 7.0`beginRequest()`並`endRequest()`Api`java.sql.Connection`類別。 這些 Api 中引進 JDBC 4.3 規格和 JDK 9。 如需驅動程式的實作，這些 api 的詳細資訊，請參閱[JDBC driver 的 JDBC 4.3 合規性](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md)。

### <a name="support-for-sql-data-discovery-and-classification"></a>針對「SQL 資料探索與分類」的支援

適用於 SQL Server 的 Microsoft JDBC Driver 7.0 提供 SQL 資料探索和分類與任何目標資料庫，可支援這項功能的支援。 驅動程式現在會公開`SQLServerResultSet.getSensitivityClassification()`Api 來擷取此資訊擷取`ResultSet`。

如需如何使用 JDBC 驅動程式的這項功能的詳細資訊，請參閱中的範例[SQL 資料探索與分類](../../connect/jdbc/data-discovery-classification-sample.md)。

### <a name="added-connection-property-usebulkcopyforbatchinsert"></a>加入連接屬性： useBulkCopyForBatchInsert

適用於 SQL Server 的 Microsoft JDBC 驅動程式 7.0 引進了新的連接屬性， `useBulkCopyForBatchInsert`。 僅針對 Azure SQL 資料倉儲支援這個屬性。

這個屬性預設為停用。 您可以啟用它提升使用者應用程式的效能，當您要將大量資料推送到 Azure SQL 資料倉儲。 啟用此屬性會變更以切換到與使用者提供資料的大量複製作業的批次插入作業的行為。 如需有關這個屬性，而且其限制的詳細資訊，請參閱 <<c0> [ 批次中使用大量複製 API 插入作業](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md)。

### <a name="added-connection-property-cancelquerytimeout"></a>加入連接屬性： cancelQueryTimeout

適用於 SQL Server 的 Microsoft JDBC 驅動程式 7.0 引進了新的連接屬性， `cancelQueryTimeout`; 若要取消`queryTimeout`上`java.sql.Connection`和`java.sql.Statement`物件。

### <a name="added-azure-key-vault-provider-constructors"></a>新增的 Azure 金鑰保存庫提供者建構函式

適用於 SQL Server 的 Microsoft JDBC Driver 7.0 重新先前移除的建構函式，引進的`SQLServerColumnEncryptionAzureKeyVaultProvider`。 它透過自訂的方法，透過實作允許驗證`SQLServerKeyVaultAuthenticationCallback`擷取存取權杖。

新的建構函式具有下列定義：

```java
/* This constructor is added to provide backward compatibility with 6.0
* version of the driver. It is marked deprecated for removal in the next
* stable release.
*/
@Deprecated
public SQLServerColumnEncryptionAzureKeyVaultProvider(
        SQLServerKeyVaultAuthenticationCallback authenticationCallback,
        ExecutorService executorService) throws SQLServerException;

/*New constructor to replace the above constructor*/
public SQLServerColumnEncryptionAzureKeyVaultProvider(
            SQLServerKeyVaultAuthenticationCallback authenticationCallback) throws SQLServerException;
```

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-160"></a>更新「適用於 Java 的 Microsoft Azure Active Directory 驗證程式庫 (ADAL4J)」。版本：1.6.0

適用於 SQL Server 的 Microsoft JDBC Driver 7.0 已更新為 1.6.0 版的 「 Microsoft Azure Active Directory Authentication Library (ADAL4J) 適用於 Java 」 上的其 Maven 相依性。 如需有關相依性的詳細資訊，請參閱[適用於 SQL Server 功能的 Microsoft JDBC Driver 的相依性](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)。

## <a name="64"></a>6.4

Microsoft JDBC Driver 6.4 for SQL Server 是完全符合 JDBC 規格 4.1 和 4.2。 6.4 版的封裝中的 jar 會命名為根據 Java 版本相容性。 比方說，必須使用 mssql-jdbc-6.4.0.jre8.jar 檔案 6.4 版的封裝，使用 Java 8。

### <a name="support-for-jdk-9"></a>JDK 9 支援

此驅動程式支援 JDK 除了 JDK 8.0 和 7.0 的 9.0 版。

### <a name="jdbc-43-compliance"></a>JDBC 4.3 合規性

除了 4.1 與 4.2 之外，此驅動程式還支援 Java 資料庫連線 API 4.3 規格。 JDBC 4.3 API 方法已加入，但尚未實作。 如需詳細資訊，請參閱[適用於 JDBC 驅動程式的 JDBC 4.3 合規性](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md)。

### <a name="added-connection-property-sslprotocol"></a>加入連接屬性： sslProtocol

新的連接屬性可讓使用者指定 TLS 通訊協定關鍵字。 可能的值為:"TLS"、"TLSv1"、"TLSv1.1 」 和 「 TLSv1.2"。 如需詳細資訊，請參閱 < [SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol)。

### <a name="deprecated-connection-property-fipsprovider"></a>連接屬性已被取代： fipsProvider

連接屬性`fipsProvider`從可接受的連接屬性的清單中移除。 如需詳細資訊，請參閱相關[GitHub 提取要求](https://github.com/Microsoft/mssql-jdbc/pull/460)。

### <a name="added-connection-properties-for-specifying-a-custom-trustmanager"></a>加入的連接屬性來指定自訂 TrustManager

驅動程式現在支援指定自訂 TrustManager 與新增`trustManagerClass`和`trustManagerConstructorArg`連接屬性。 以動態方式，您可以指定每個連線一組信任的憑證而不需修改 Java 虛擬機器 (JVM) 環境的全域設定。

### <a name="added-support-for-datetimesmalldatetime-in-table-valued-parameters"></a>已新增的支援資料表值參數中的 datetime/smallDatetime

此驅動程式現在支援資料型別`datetime`和`smallDatetime`當您使用資料表值參數 (Tvp)。

### <a name="added-support-for-the-sqlvariant-datatype"></a>已新增的支援 sql_variant 資料類型

JDBC 驅動程式現在支援`sql_variant`搭配 SQL Server 的資料類型。 `sql_variant` Tvp 和大量複製，但有下列限制等功能也支援資料類型：

* **針對資料值**： 

  當您使用 TVP 來填入資料表，其中包含`datetime`， `smalldatetime`，或`date`中所儲存值`sql_variant`資料行，並呼叫`getDateTime()`， `getSmallDateTime()`，或`getDate()`無法運作的結果集上的方法和會擲回下列例外狀況：

  `java java.lang.String cannot be cast to java.sql.Timestamp`
    
  因應措施，請使用`getString()`或`getObject()`方法改為。

* **針對 Null 值搭配 sql_variant 使用 TVP**：
  
  如果您使用 TVP 填入資料表，並傳送 NULL 值則`sql_variant`資料行類型，您會遇到例外狀況。 將 NULL 值插入資料行類型`sql_variant`TVP 中目前不支援。

### <a name="implemented-prepared-statement-metadata-caching"></a>實作已備妥的陳述式中繼資料快取

JDBC 驅動程式已實作已備妥的陳述式中繼資料快取的效能改進。 此驅動程式現在支援快取已備妥的陳述式中使用的驅動程式的中繼資料`disableStatementPooling`和`statementPoolingCacheSize`連接屬性。 此功能預設為停用。 如需詳細資訊，請參閱 <<c0> [ 備妥陳述式中繼資料快取的 JDBC 驅動程式](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)。

### <a name="added-support-for-azure-ad-integrated-authentication-on-linuxmac"></a>已新增的支援在 Linux/Mac 上 Azure AD 整合式驗證

JDBC 驅動程式現在透過 Kerberos，在所有支援的作業系統 (Windows、Linux 與 Mac) 上支援 Azure Active Directory (Azure AD) 整合式驗證。 或者，在 Windows 作業系統中，使用者可以向 sqljdbc_auth.dll。

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-140"></a>更新「適用於 Java 的 Microsoft Azure Active Directory 驗證程式庫 (ADAL4J)」。版本：1.4.0

JDBC 驅動程式已更新為 1.4.0 版的 「 Microsoft Azure Active Directory Authentication Library (ADAL4J) 適用於 Java 」 上的其 Maven 相依性。 如需有關相依性的詳細資訊，請參閱[適用於 SQL Server 功能的 Microsoft JDBC Driver 的相依性](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)。

## <a name="62"></a>6.2

Microsoft JDBC Driver 6.2 for SQL Server 是完全符合 JDBC 規格 4.1 和 4.2。 6.2 的封裝中的 jar 會命名為根據 Java 版本相容性。 比方說，從 6.2 封裝 mssql-6.2.2.jre8.jar 檔案被建議搭配 Java 8。

> [!NOTE]  
> 在已於 2017 年 6 月 29 日發行 JDBC 6.2 RTW 中找不到中繼資料快取改進的問題。 改進已回復，並在 2017 年 7 月 17 日發行新的 jar （版本 6.2.1）。 
>
> 另一項改進升級 Azure Key Vault 相依程式庫版本為 1.0.0，而新的 jar （版本 6.2.2） 已於 2017 年 10 月 19 日發行。
>
> 下載最新的更新從 JDBC Driver 6.2 [Microsoft 下載中心](https://go.microsoft.com/fwlink/?linkid=852460)， [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2)，並[Maven 中央](https://search.maven.org/search?q=g:com.microsoft.sqlserver)。 請更新您的專案，以使用 6.2.2 發行的 jar。 如需詳細資訊，請檢視版本資訊[6.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1)並[6.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2)。

### <a name="azure-ad-support-for-linux"></a>適用於 Linux 的 azure AD 支援

使用 Azure AD 驗證的使用者名稱/密碼和存取權杖的方法，以連接您的 Linux 應用程式到 Azure SQL Database。

### <a name="fips-enabled-jvms"></a>啟用 FIPS 的 Jvm

JDBC 驅動程式現在可以用在以符合美國聯邦標準符合性的美國聯邦資訊處理標準 (FIPS) 140 相容性模式中執行的 Jvm 上。

### <a name="kerberos-authentication-improvements"></a>Kerberos 驗證的增強功能

JDBC 驅動程式現已支援：

- 其中 Kerberos 設定不能修改，或無法擷取新的權杖或 keytab 應用程式的主體/密碼方法。 這個方法可以用於驗證 SQL Server 執行個體，讓只有 Kerberos 驗證。
- 跨領域驗證使用 Kerberos 整合式驗證，而不需要明確地設定伺服器的 SPN。 驅動程式現在會自動計算領域即使它不提供。
- 接受 Kerberos 限制委派會模擬 GSS 認證物件，透過資料來源為使用者認證。 此模擬的認證則用來建立 Kerberos 連接。

### <a name="added-timeouts"></a>已新增的逾時

JDBC 驅動程式現在支援下列可設定的逾時。 您可以根據您的應用程式需求加以變更。

- 當您執行查詢時，就會發生查詢逾時，若要控制的逾時之前要等待的秒數。
- 若要指定的通訊端上發生逾時之前要等候的毫秒數讀取，或接受通訊端逾時。

## <a name="61"></a>6.1

適用於 SQL Server 的 Microsoft JDBC Driver 6.1 是完全符合 JDBC 規格 4.1 和 4.2。 這是 JDBC 驅動程式的初始開放原始碼版本。 它包含 mssql-jdbc-6.1.0.jre8.jar 和 mssql-jdbc-6.1.0.jre7.jar 檔案，其對應至 Java 版本相容性。

## <a name="60"></a>6.0

Microsoft JDBC Driver 6.0 for SQL Server 是完全符合 JDBC 規格 4.1 和 4.2。 根據合規性的 JDBC API 版本為 6.0 套件中的 jar。 例如，6.0 套件中的 sqljdbc42.jar 檔案是 API 符合 JDBC 4.2 規格。 同樣地，sqljdbc41.jar 檔案會遵守 JDBC API 4.1。

若要確保您擁有正確的 sqljdbc42.jar 或 sqljdbc41.jar 檔案，請執行下列程式碼行。 如果輸出已 「 驅動程式版本： 6.0.7507.100 」，您有 JDBC Driver 6.0 封裝。

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="always-encrypted"></a>Always Encrypted

驅動程式支援 SQL Server 2016 中的 Always Encrypted 功能。 這項功能可確保機密資料沒看過的純文字中的 SQL Server 執行個體。 Always Encrypted 的運作方式為明確加密應用程式中的資料，以便 SQL Server 就只會處理加密的資料和非純文字的值。 即使 SQL Server 執行個體或主機電腦被入侵，攻擊者所能得到的也只是敏感性資料的加密文字。 如需詳細資訊，請參閱[搭配使用 Always Encrypted 與 JDBC 驅動程式](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)。

### <a name="internationalized-domain-names"></a>國際化網域名稱

此驅動程式支援國際化的網域名稱 (Idn) 的伺服器名稱。 如需詳細資訊，請參閱 「 使用國際化網域名稱 」 中[JDBC Driver 的國際功能](../../connect/jdbc/international-features-of-the-jdbc-driver.md)文章。

### <a name="parameterized-queries"></a>參數化查詢

驅動程式現在支援針對子查詢和/或聯結等複雜查詢，使用備妥陳述式來擷取參數中繼資料。 請注意，只有使用 SQL Server 2012 與更新版本時，才能使用此改進功能。

### <a name="azure-active-directory"></a>Azure Active Directory

Azure AD 驗證是使用 Azure AD 中的身分識別連接到 Azure SQL Database v12 的機制。 使用 Azure AD 驗證集中管理資料庫使用者的身分識別，並作為 SQL Server 的替代驗證。 

您可以使用 JDBC Driver 6.0 連接到 Azure SQL Database 的 JDBC 連接字串中指定您的 Azure AD 認證。 如需詳細資訊，請參閱中的 [驗證] 屬性[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)文章。

### <a name="table-valued-parameters"></a>資料表值參數

TVP 提供從用戶端應用程式，將多個資料列的資料封送至 SQL Sever 的簡便方式，而不需多次來回存取或特殊的伺服器端邏輯才能處理資料。 您可以使用 TVP，以一個參數化命令在用戶端應用程式中封裝資料列的資料，並傳送至伺服器。 內送資料列會儲存在資料表變數中，您可以再操作的藉由使用 TRANSACT-SQL。 如需詳細資訊，請參閱 <<c0> [ 使用資料表值參數](../../connect/jdbc/using-table-valued-parameters.md)。

### <a name="always-on-availability-groups"></a>AlwaysOn 可用性群組

驅動程式現在支援 Alwayson 可用性群組的透明連接。 驅動程式會快速探索伺服器基礎結構目前的 Always On 拓撲，並以透明的方式連線至目前使用中的伺服器。

## <a name="42"></a>4.2

Microsoft JDBC Driver 4.2 for SQL Server 是完全符合 JDBC 規格 4.1 和 4.2。 4.2 套件中的 jar 會命名為根據的 JDBC API 版本合規性。 比方說，從 4.2 封裝 sqljdbc42.jar 檔案是 API 符合 JDBC 4.2 規格。 同樣地，sqljdbc41.jar 檔案會遵守 JDBC API 4.1。

若要確保您有正確 sqljdbc42.jar 或 sqljdbc41.jar 檔案中，執行下列程式碼行。 如果輸出是 「 驅動程式版本： 4.2.6420.100 」，您有 JDBC Driver 4.2 套件。

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="support-for-jdk-8"></a>支援 JDK 8

此驅動程式支援 JDK 版本 8.0 除了 JDK 7.0、 6.0 及 5.0。

### <a name="jdbc-41-and-42-compliance"></a>JDBC 4.1 和 4.2 相容性

除了 Java 資料庫連線 API 4.0 規格之外，驅動程式也支援 Java 資料庫連線 API 4.1 與 4.2 規格。 如需詳細資訊，請參閱 < [JDBC driver 的 JDBC 4.1 相容性](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md)並[JDBC driver 的 JDBC 4.2 相容性](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)。

### <a name="bulk-copy"></a>大量複製

您使用大量複製功能可用來快速將大量資料複製到 SQL Server 資料庫中的資料表或檢視。 如需詳細資訊，請參閱[搭配 JDBC 驅動程式使用大量複製](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)。

### <a name="xa-transaction-rollback-option"></a>XA 交易回復選項

對於已取消準備交易的現有自動回復，驅動程式有新的逾時選項。 如需詳細資訊，請參閱 <<c0> [ 了解 XA 交易](../../connect/jdbc/understanding-xa-transactions.md)。

### <a name="new-kerberos-principal-connection-property"></a>新的 Kerberos 主體連線屬性

驅動程式使用新的連線屬性，讓 Kerberos 連線更具彈性。 如需詳細資訊，請參閱[使用 Kerberos 整合式驗證連線到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。

## <a name="41"></a>4.1

### <a name="support-for-jdk-7"></a>JDK 7 支援

此驅動程式支援 JDK 7.0 除了 JDK 6.0 與 5.0 版。

## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>JDBC Driver 6.4、6.0、4.2 與 4.1 應用程式不支援 Itanium

不支援在 Itanium 電腦上執行 Microsoft JDBC Drivers 6.4、6.0、4.2 與 4.1 for SQL Server 應用程式。

## <a name="see-also"></a>另請參閱

[JDBC Driver 概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)
