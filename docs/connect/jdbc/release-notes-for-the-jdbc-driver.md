---
title: JDBC Driver 的版本資訊 | Microsoft Docs
ms.custom: ''
ms.date: 02/26/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 76607fbe96ef954ce90c7d24daf9a12b69a3fce6
ms.sourcegitcommit: 6ee40a2411a635daeec83fa473d8a19e5ae64662
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2020
ms.locfileid: "77903735"
---
# <a name="release-notes-for-the-microsoft-jdbc-driver"></a>Microsoft JDBC Driver 的版本資訊

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文會列出 _Microsoft JDBC Driver for SQL Server_ 的版本。 針對每個發行版本，會將變更命名並加以描述。

## <a name="821"></a>8.2.1

### <a name="compliance"></a>法規遵循

2020 年 2 月 26 日

| 合規性變更 | 詳細資料 |
| :---------------- | :------ |
| 下載 JDBC Driver 8.2 的最新更新。 | &bull; &nbsp; [Microsoft 下載中心](https://go.microsoft.com/fwlink/?linkid=2116870)<br/>&bull; &nbsp; [GitHub，8.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v8.2.1)<br/>&bull; &nbsp; [Maven 中心](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| 完全符合 JDBC API 規格 4.2 的規範。 | 8\.2 套件中的 jar 會根據 Java 版本相容性命名。<br/><br/>例如，8.2 套件的 mssql-jdbc-8.2.1.jre11.jar 檔案應搭配 Java 11 一起使用。 |
| 與 Java 開發套件 (JDK) 13.0、11.0 和 1.8 版相容。 | 除了 JDK 11.0 和 1.8 之外，Microsoft JDBC Driver 8.2 for SQL Server 現在還與 Java 開發套件 (JDK) 13.0 版相容。 |
| &nbsp; | &nbsp; |

### <a name="support-for-jdk-13"></a>JDK 13 支援

除了 JDK 11.0 與 1.8 之外，Microsoft JDBC Driver 8.2.1 for SQL Server 現在也與 Java 開發套件 (JDK) 13.0 版相容。

### <a name="always-encrypted-with-secure-enclaves"></a>具有安全記憶體保護區的 Always Encrypted

| Always Encrypted 變更 | 詳細資料 |
| :--------- | :------ |
| Microsoft JDBC Driver 8.2.1 for SQL Server 現也支援使用安全記憶體保護區的 Always Encrypted。 在這裡可以找到詳細資料：具有安全記憶體保護區的 Always Encrypted。 |
| 更多詳細資料和範例程式碼。 | 請參閱[具有安全記憶體保護區的 Always Encrypted](../../connect/jdbc/always-encrypted-with-secure-enclaves.md)。 |
| &nbsp; | &nbsp; |

### <a name="performance-improvement-when-retrieving-temporal-datatypes-from-sql-server"></a>從 SQL Server 擷取時態性資料類型時的效能改善

| 時態性資料類型變更 | 詳細資料 |
| :---------- | :------ |
| Microsoft JDBC Driver 8.2.1 for SQL Server 改善了從 SQL Server 擷取暫存資料類型時的效能。 | 這項變更會盡可能避免使用 java.util.Calendar，藉以排除不必要的時態性資料類型轉換。 |
| 下列為受此效能改善影響的時態性資料類型清單；格式為 SQL Server 資料類型，後面接著個別的 Java 對應。 | date (java.sql.Date)、datetime (java.sql.Timestamp)、datetime2 (java.sql.Timestamp)、smalldatetime (java.sql.Timestamp) 和 time (java.sql.Time)。 |
| &nbsp; | &nbsp; |

> [!NOTE]
> 由於 java.util.Calendar 與 java.time.LocalDateTime API 之間處理時區方式的差異，因此使用者所提供 java.util.Calendar 物件與其建立關聯的時態性資料類型或 microsoft.sql.DateTimeOffset 資料類型，都無法從這項改善中受益。

### <a name="deployment-of-mssql-jdbc_auth-version-archdll-previously-sqljdbc_authdll-to-maven-repository"></a>將 mssql-jdbc_auth-\<版本>-\<架構>.dll (之前為 sqljdbc_auth.dll) 部署至 Maven 存放庫

| sqljdbc_auth.dll 變更 | 詳細資料 |
| :------------------- | :------ |
| 自 Microsoft JDBC Driver 8.2.1 for SQL Server 起，驅動程式將會使用 mssql-jdbc_auth-\< 版本>-\< 架構>.dll (而不是 sqljdbc_auth.dll)，從而使用 Azure Active Directory Authentication 功能。 | &nbsp; |
| DLL 也已上傳至 Maven 存放庫，以方便存取。 | 請參閱[本頁面](https://search.maven.org/artifact/com.microsoft.sqlserver/mssql-jdbc_auth)。 |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>已知問題

| 已知問題 | 詳細資料 |
| :----------- | :------ |
| 搭配使用具有安全記憶體保護區的 Always Encrypted 與 Java 8。 | 使用者必須包含 BouncyCastle 提供者作為相依性，或對應/載入支援 RSASSA-PSS 簽章演算法的安全性提供者。 |
| &nbsp; | &nbsp; |

## <a name="741"></a>7.4.1

### <a name="compliance"></a>法規遵循

2019 年 8 月 2 日

| 合規性變更 | 詳細資料 |
| :---------------- | :------ |
| 下載 JDBC Driver 7.4 的最新更新。 | &bull;&nbsp;[Microsoft 下載中心](https://go.microsoft.com/fwlink/?linkid=2099962)<br/>&bull; &nbsp; [GitHub，7.4.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.4.1)<br/>&bull; &nbsp; [Maven 中心](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| 完全符合 JDBC API 規格 4.2 的規範。 | 7\.4 套件中的 jar 會根據 Java 版本相容性命名。<br/><br/>例如，來自 7.4 套件的 mssql-jdbc-7.4.1.jre11.jar 檔案應該與 Java 11 搭配使用。 |
| 與 Java 開發套件 (JDK) 12.0、11.0 和 1.8 版相容。 | 除了 JDK 11.0 和 1.8 之外，Microsoft JDBC Driver 7.4 for SQL Server 現在還與 Java 開發套件 (JDK) 12.0 版相容。 |
| &nbsp; | &nbsp; |

### <a name="support-for-jdk-12"></a>JDK 12 支援

除了 JDK 11.0 和 1.8 之外，Microsoft JDBC Driver 7.4 for SQL Server 現在還與 Java 開發套件 (JDK) 12.0 版相容。

### <a name="introduces-ntlm-authentication"></a>引進 NTLM 驗證

| NTLM 變更 | 詳細資料 |
| :--------- | :------ |
| 支援 NTLM 驗證模式。 | 這種驗證模式可讓 Windows 與非 Windows 用戶端，使用 Windows 網域使用者身分針對 SQL Server 自行驗證。 |
| 更多詳細資料及一個範例應用程式來使用此驗證模式。 | 請參閱 [使用 NTLM 驗證連線](../../connect/jdbc/using-ntlm-authentication-to-connect-to-sql-server.md)。 |
| &nbsp; | &nbsp; |

### <a name="introduces-querying-parametermetadata-via-_usefmtonly_"></a>介紹如何透過 _useFmtOnly_ 查詢 ParameterMetaData

| useFmtOnly 變更 | 詳細資料 |
| :---------- | :------ |
| 已新增 **useFmtOnly** 連線屬性屬性。 | 此功能可讓使用者透過 `SET FMTONLY ON` 舊版 API 選擇性地查詢 ParameterMetaData。 這對於 `sp_describe_undeclared_parameters` 未如預期執行的情況很有用。 |
| 更多詳細資料與限制。 | 請參閱 [Using useFmtOnly](../../connect/jdbc/using-usefmtonly.md) |
| &nbsp; | &nbsp; |

### <a name="updated-_microsoft-azure-key-vault-sdk-for-java_-version-121"></a>更新了「適用於 Java 的 Microsoft Azure Key Vault SDK」  1.2.1 版

| Key Vault SDK 變更 | 詳細資料 |
| :------------------- | :------ |
| 其在「適用於 Java 的 Microsoft Azure Key Vault SDK」  上的 Maven 相依性已更新為 1.2.1 版。 | &nbsp; |
| 移除 Maven 相依性中的 _Microsoft Azure SDK for Key Vault WebKey_。 | &nbsp; |
| 其他詳細資料。 | 請參閱 [Microsoft JDBC Driver for SQL Server 的功能相依性](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)。 |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>已知問題

| 已知問題 | 詳細資料 |
| :----------- | :------ |
| 使用 NTLM 驗證時。 | 目前不支援同時啟用擴充保護與加密連線。 |
| 使用 useFmtOnly 時。 | 有一些功能問題與是由 SQL 剖析邏輯中的缺陷所造成。 如需更多詳細資料與因應措施建議，請參閱[使用 useFmtOnly](../../connect/jdbc/using-usefmtonly.md)。 |
| &nbsp; | &nbsp; |

## <a name="722"></a>7.2.2

### <a name="compliance"></a>法規遵循

2019 年 4 月 16 日

| 合規性變更 | 詳細資料 |
| :---------------- | :------ |
| 下載 JDBC Driver 7.2 的最新更新。 | &bull; &nbsp; [Microsoft 下載中心](https://go.microsoft.com/fwlink/?linkid=2063159)<br/>&bull; &nbsp; [GitHub，7.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.2)<br/>&bull; &nbsp; [Maven 中心](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| 完全符合 JDBC API 規格 4.2 的規範。 | 7\.2 套件中的 jar 會根據 Java 版本相容性進行命名。<br/><br/>例如，來自 7.2 套件的 mssql-jdbc-7.2.2.jre11.jar 檔案應該與 Java 11 搭配使用。 |
| 除了 JDK 1.8 之外，還與 Java Development Kit (JDK) 11.0 版相容。 | 除了 JDK 1.8 之外，Microsoft JDBC Driver 7.2 for SQL Server 現在還與 Java 開發套件 (JDK) 11.0 版相容。 |
| &nbsp; | &nbsp; |

> [!NOTE]
> 在已於 2019 年 1 月 31 日發行的 JDBC 7.2 Release To Web (RTW) 驅動程式中發現了 SQL 陳述式剖析的問題。 此變更已回復，並且已於 2019 年 2 月 11 日發行新的 jar (版本 7.2.1)。
>
> 已在該驅動程式上進行另一個更新，以修正無法適當清除 ActivityID 的問題。 新的 jar (版本 7.2.2) 已於 2019 年 4 月 16 日發行。
> 
> 我們建議更新您的專案以使用 7.2.2 版的 jar。 如需詳細資訊，請檢視 [GitHub，7.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.1) 和 [GitHub，7.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.2) 的版本資訊。

### <a name="active-directory-_managed-service-identity_-msi-authentication"></a>Active Directory _受控服務識別_ (MSI) 驗證

| MSI 變更 | 詳細資料 |
| :--------- | :------ |
| 支援 Active Directory 受控服務識別 (MSI) 驗證模式。 | 此驗證模式適用於支援已啟用「身分識別」功能的 Azure 資源。<br/><br/>此驅動程式支援這兩種類型的受控服務識別 (MSI)，以取得 **accessToken** 來建立安全的連線。 |
| 更多詳細資料及一個範例應用程式來使用此驗證模式。 | 請參閱[使用 Azure Active Directory 驗證連線](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)。 |
| &nbsp; | &nbsp; |

### <a name="introduces-_open-service-gateway-initiative_-osgi-support"></a>引進「開放式服務閘道協議」  (OSGi) 支援

| OSGi 變更 | 詳細資料 |
| :---------- | :------ |
| 已新增 **DataSourceFactory** 實作。 | &bull; &nbsp; `org.osgi.service.jdbc.DataSourceFactory`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.SQLServerDataSourceFactory` |
| 已新增 **Activator** 實作。 | &bull; &nbsp; `org.osgi.framework.BundleActivator`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.Activator` |
| &nbsp; | &nbsp; |

### <a name="introduces-_sqlservererror_-apis"></a>引進 _SQLServerError_ API

| 錯誤 API 變更 | 詳細資料 |
| :--------------- | :------ |
| 已引進 SQLServerError API。 | Getter API 以擷取有關從伺服器產生之錯誤的其他詳細資料。<br/><br/>&bull; &nbsp; `SQLServerException.getSQLServerError()`<br/>&bull; &nbsp; `SQLServerError` |
| 其他詳細資料。 | 請參閱[處理錯誤](../../connect/jdbc/handling-errors.md)。 |
| &nbsp; | &nbsp; |

### <a name="updated-_microsoft-azure-active-directory-authentication-library-adal4j-for-java_-version-163"></a>已更新「適用於 Java 的 Microsoft Azure Active Directory 驗證程式庫 (ADAL4J)」  ，1.6.3 版

| ADAL4J 變更 | 詳細資料 |
| :------------ | :------ |
| 已將其在 ADAL4J 上的 Maven 相依性更新為版本 1.6.3。 | &nbsp; |
| 引進 _Java Client Runtime for AutoRest_ 作為 Maven 相依性版本 1.6.5。 | &nbsp; |
| 其他詳細資料。 | 請參閱 [Microsoft JDBC Driver for SQL Server 的功能相依性](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)。 |
| &nbsp; | &nbsp; |

### <a name="updated-_microsoft-azure-key-vault-sdk-for-java_-version-120"></a>已更新「適用於 Java 的 Microsoft Azure Key Vault SDK」  1.2.0 版

| Key Vault SDK 變更 | 詳細資料 |
| :------------------- | :------ |
| 已將其在「適用於 Java 的 Microsoft Azure Key Vault SDK」  上的 Maven 相依性更新為 1.2.0 版。 | &nbsp; |
| 引進 _Microsoft Azure SDK for Key Vault WebKey_ 作為 Maven 相依性，1.2.0 版。 | &nbsp; |
| 其他詳細資料。 | 請參閱 [Microsoft JDBC Driver for SQL Server 的功能相依性](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)。 |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>已知問題

| 已知問題 | 詳細資料 |
| :----------- | :------ |
| 已在某些情況下將查詢參數化。 | 已於 2019 年 2 月發行 7.2.0 版本的更新 (v7.2.1) 來解決此問題。 |
| 清除 Activityid。 | 已於 2019 年 4 月發行 7.2.1 版本的更新 (v7.2.2) 來解決此問題。 |
| &nbsp; | &nbsp; |

## <a name="70"></a>7.0

Microsoft JDBC Driver 7.0 for SQL Server 完全符合 JDBC API 規格 4.2 的規範。 7\.0 套件中的 jar 會根據 Java 版本相容性進行命名。 例如，來自 7.0 套件的 mssql-jdbc-7.0.0.jre10.jar 檔案應該與 Java 10 搭配使用。

### <a name="support-for-jdk-10"></a>JDK 10 支援

除了 JDK 1.8 之外，Microsoft JDBC Driver 7.0 for SQL Server 現在還與 Java 開發套件 (JDK) 10.0 版相容。 此更新也會透過其資訊清單檔來公開驅動程式的 `Automatic-Module-Name` 作為 `com.microsoft.sqlserver.jdbc`。

### <a name="support-for-spatial-datatypes"></a>空間資料類型的支援

Microsoft JDBC Driver 7.0 for SQL Server 現在提供 SQL Server 空間資料類型「地理」和「幾何」的支援。 如需有關空間資料類型 API 及其使用方式的詳細資訊，請參閱[使用空間資料類型](../../connect/jdbc/use-spatial-datatypes.md)。

### <a name="implementation-for-jdbc-43-introduced-javasqlconnection-apis-beginrequest-and-endrequest"></a>為 JDBC 4.3 引進的 java.sql.Connection API beginRequest() 和 endRequest() 新增實作

Microsoft JDBC Driver 7.0 for SQL Server 現在會從 `java.sql.Connection` 類別實作 `beginRequest()` 和 `endRequest()` API。 這些 API 均會透過 JDBC 4.3 規格和 JDK 9 來引進。 如需驅動程式如何實作這些 API 的詳細資訊，請參閱[適用於 JDBC Driver 的 JDBC 4.3 合規性](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md)。

### <a name="support-for-sql-data-discovery-and-classification"></a>針對「SQL 資料探索與分類」的支援

適用於 SQL Server 的 Microsoft JDBC 驅動程式 7.0 利用任何支援此功能的目標資料庫，來提供「SQL 資料探索與分類」的支援。 此驅動程式現在會公開 `SQLServerResultSet.getSensitivityClassification()` API，從擷取的 `ResultSet` 中擷取此資訊。

如需如何搭配 JDBC 驅動程式使用此功能的詳細資訊，請參閱 [SQL 資料探索與分類](../../connect/jdbc/data-discovery-classification-sample.md)中的範例。

### <a name="added-connection-property-usebulkcopyforbatchinsert"></a>已新增連線屬性：useBulkCopyForBatchInsert

Microsoft JDBC Driver 7.0 for SQL Server 會引進新的連線屬性 `useBulkCopyForBatchInsert`。 僅 Azure SQL 資料倉儲支援此屬性。

預設會停用此屬性。 當您要將大量資料推送到 Azure SQL 資料倉儲時，可以啟用它來提升使用者應用程式的效能。 啟用此屬性會變更批次插入作業的行為，以切換到使用者提供資料的大量複製作業。 如需這個屬性及其限制的詳細資訊，請參閱[使用大量複製 API 執行批次插入作業](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md)。

### <a name="added-connection-property-cancelquerytimeout"></a>已新增連線屬性：cancelQueryTimeout

Microsoft JDBC Driver 7.0 for SQL Server 會引進新的連線屬性 `cancelQueryTimeout`，以取消 `java.sql.Connection` 和 `java.sql.Statement` 物件上的 `queryTimeout`。

### <a name="added-azure-key-vault-provider-constructors"></a>已新增 Azure Key Vault Provider 建構函式

Microsoft JDBC Driver 7.0 for SQL Server 會針對 `SQLServerColumnEncryptionAzureKeyVaultProvider` 重新引進先前移除的建構函式。 它已允許透過 `SQLServerKeyVaultAuthenticationCallback` 實作的自訂方法進行驗證以擷取存取權杖。

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

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-160"></a>已更新「適用於 Java 的 Microsoft Azure Active Directory 驗證程式庫 (ADAL4J)」版本：1.6.0

Microsoft JDBC Driver 7.0 for SQL Server 已將其在「適用於 Java 的 Microsoft Azure Active Directory 驗證程式庫 (ADAL4J)」上的 Maven 相依性更新為 1.6.0 版。 如需有關相依性的詳細資訊，請參閱 [Microsoft JDBC Driver for SQL Server 的功能相依性](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)。

## <a name="64"></a>6.4

Microsoft JDBC Driver 6.4 for SQL Server 完全符合 JDBC 規格 4.1 和 4.2 的規範。 6\.4 套件中的 jar 會根據 Java 版本相容性進行命名。 例如，來自 6.4 套件的 mssql-jdbc-6.4.0.jre8.jar 檔案必須與 Java 8 搭配使用。

### <a name="support-for-jdk-9"></a>JDK 9 支援

除了 JDK 8.0 和 7.0，此驅動程式還支援 JDK 9.0 版。

### <a name="jdbc-43-compliance"></a>JDBC 4.3 合規性

除了 4.1 與 4.2 之外，此驅動程式還支援 Java 資料庫連線 API 4.3 規格。 已新增 JDBC 4.3 API 方法，但尚未實作。 如需詳細資訊，請參閱[適用於 JDBC 驅動程式的 JDBC 4.3 合規性](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md)。

### <a name="added-connection-property-sslprotocol"></a>已新增連線屬性：sslProtocol

新的連線屬性讓使用者能夠指定 TLS 通訊協定關鍵字。 可能的值包括：TLS、TLSv1、TLSv1.1 與 TLSv1.2。 如需詳細資訊，請參閱 [SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol) \(英文\)。

### <a name="deprecated-connection-property-fipsprovider"></a>已取代連線屬性：fipsProvider

已從可接受的連線屬性清單中移除連線屬性 `fipsProvider`。 如需詳細資訊，請參閱相關的 [GitHub 提取要求](https://github.com/Microsoft/mssql-jdbc/pull/460) \(英文\)。

### <a name="added-connection-properties-for-specifying-a-custom-trustmanager"></a>已新增連線屬性來指定自訂 TrustManager

此驅動程式現在支援利用已新增的 `trustManagerClass` 和 `trustManagerConstructorArg` 連線屬性來指定自訂 TrustManager。 您可以針對每個連線動態指定一組信任的憑證，而不需修改 Java 虛擬機器 (JVM) 環境的全域設定。

### <a name="added-support-for-datetimesmalldatetime-in-table-valued-parameters"></a>已新增支援資料表值參數中的 datetime/smallDatetime

當您使用資料表值參數 (TVP) 時，此驅動程式現在支援資料類型 `datetime` 和 `smallDatetime`。

### <a name="added-support-for-the-sql_variant-datatype"></a>已新增支援 sql_variant 資料類型

此 JDBC Driver 現在支援可與 SQL Server 搭配使用的 `sql_variant` 資料類型。 `sql_variant` 資料類型也可透過 TVP 和大量複製等功能來支援，但有下列限制：

* **針對資料值**： 

  當您使用 TVP 來填入包含 `sql_variant` 資料行中所儲存之 `datetime`、`smalldatetime` 或 `date` 值的資料表時，在結果集上呼叫 `getDateTime()`、`getSmallDateTime()` 或 `getDate()` 方法就無法運作，並會擲回下列例外狀況：

  `java java.lang.String cannot be cast to java.sql.Timestamp`
    
  因應措施為改用 `getString()` 和 `getObject()` 方法。

* **針對 Null 值搭配 sql_variant 使用 TVP**：
  
  如果您使用 TVP 來填入資料表，並將 NULL 值傳送到 `sql_variant` 資料行類型，您將會遇到例外狀況。 目前不支援在 TVP 中使用資料行類型 `sql_variant` 插入 NULL 值。

### <a name="implemented-prepared-statement-metadata-caching"></a>已實作備妥的陳述式中繼資料快取

此 JDBC Driver 已實作備妥的陳述式中繼資料快取來改進效能。 此驅動程式目前會透過 `disableStatementPooling` 和 `statementPoolingCacheSize` 連線屬性，來支援快取驅動程式中的備妥陳述式中繼資料。 此功能預設為停用。 如需詳細資訊，請參閱 [JDBC Driver 的備妥陳述式中繼資料快取](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)。

### <a name="added-support-for-azure-ad-integrated-authentication-on-linuxmac"></a>已在 Linux/Mac 上新增支援 Azure AD 整合式驗證

JDBC 驅動程式現在透過 Kerberos，在所有支援的作業系統 (Windows、Linux 與 Mac) 上支援 Azure Active Directory (Azure AD) 整合式驗證。 或者，在 Windows 作業系統上，使用者可以使用 mssql-jdbc_auth-\<版本>-\<架構>.dll 進行驗證。

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-140"></a>已更新「適用於 Java 的 Microsoft Azure Active Directory 驗證程式庫 (ADAL4J)」版本：1.4.0

此 JDBC Driver 已將其在「適用於 Java 的 Microsoft Azure Active Directory 驗證程式庫 (ADAL4J)」上的 Maven 相依性更新為 1.4.0 版。 如需有關相依性的詳細資訊，請參閱 [Microsoft JDBC Driver for SQL Server 的功能相依性](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)。

## <a name="62"></a>6.2

Microsoft JDBC Driver 6.2 for SQL Server 完全符合 JDBC 規格 4.1 和 4.2 的規範。 6\.2 套件中的 jar 會根據 Java 版本相容性進行命名。 例如，建議將來自 6.2 套件的 mssql-jdbc-6.2.2.jre8.jar 檔案與 Java 8 搭配使用。

> [!NOTE]  
> 在已於 2017 年 6 月 29 日發行的 JDBC 6.2 RTW 中發現了中繼資料快取改進的問題。 此改進已回復，並且已於 2017 年 7 月 17 日發行新的 jar (版本 6.2.1)。 
>
> 另一項改進已將 Azure Key Vault 相依程式庫版本升級為 1.0.0，而新的 jar (版本 6.2.2) 已於 2017 年 10 月 19 日發行。
>
> 從 [Microsoft 下載中心](https://go.microsoft.com/fwlink/?linkid=852460)、[GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2) 及 [Maven 中心](https://search.maven.org/search?q=g:com.microsoft.sqlserver)下載 JDBC Driver 6.2 的最新更新。 請更新您的專案以使用 6.2.2 版的 jar。 如需詳細資訊，請檢視 [6.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) 和 [6.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2) 的版本資訊。

### <a name="azure-ad-support-for-linux"></a>適用於 Linux 的 Azure AD 支援

透過使用者名稱/密碼和存取權杖方法使用 Azure AD 驗證，將您的 Linux 應用程式連線到 Azure SQL Database。

### <a name="fips-enabled-jvms"></a>已啟用 FIPS 的 JVM

此 JDBC Driver 現在可在符合美國聯邦資訊處理標準 (FIPS) 140 相容性模式中執行的 JVM 上使用，以符合有關合規性的美國聯邦標準。

### <a name="kerberos-authentication-improvements"></a>Kerberos 驗證改進

此 JDBC Driver 現已支援：

- 適用於應用程式的主體/密碼方法，其中的 Kerberos 設定無法修改，或無法擷取新的權杖或 Keytab。 此方法可用來對只允許 Kerberos 驗證的 SQL Server 執行個體進行驗證。
- 跨領域的驗證會使用 Kerberos 整合式驗證，而不需明確地設定伺服器 SPN。 即使未提供，此驅動程式現在還是會自動計算領域。
- Kerberos 限制委派，其會透過資料來源來接受模擬的使用者認證作為 GSS 認證物件。 這個模擬的認證接著可用來建立 Kerberos 連線。

### <a name="added-timeouts"></a>已新增逾時

此 JDBC Driver 現在支援下列可設定的逾時。 您可以根據應用程式的需求加以變更。

- 查詢逾時，可控制當您執行查詢時在發生逾時之前要等待的秒數。
- 通訊端逾時，可指定在通訊端讀取或接受時逾時發生之前要等候的毫秒數。

## <a name="61"></a>6.1

Microsoft JDBC Driver 6.1 for SQL Server 完全符合 JDBC 規格 4.1 和 4.2 的規範。 這是 JDBC Drive 的最初開放原始碼版本。 它包含 mssql-jdbc-6.1.0.jre8.jar 和 mssql-jdbc-6.1.0.jre7.jar 檔案，其對應至 Java 版本相容性。

## <a name="60"></a>6.0

Microsoft JDBC Driver 6.0 for SQL Server 完全符合 JDBC 規格 4.1 和 4.2 的規範。 6\.0 套件中的 jar 會根據其與 JDBC API 版本的合規性進行命名。 例如，6.0 套件中的 sqljdbc42.jar 檔案會符合 JDBC API 4.2 的規範。 同樣地，sqljdbc41.jar 檔案會符合 JDBC API 4.1 的規範。

若要確保您擁有正確的 sqljdbc42.jar 或 sqljdbc41.jar 檔案，請執行下列程式碼行。 如果輸出為「驅動程式版本：6.0.7507.100」，表示您有 JDBC 驅動程式 6.0 套件。

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="always-encrypted"></a>Always Encrypted

此驅動程式支援 SQL Server 2016 中的 Always Encrypted 功能。 此功能可確保絕對不會在 SQL Server 執行個體中看見純文字格式的敏感性資料。 Always Encrypted 的運作方式為明確加密應用程式中的資料，以便 SQL Server 就只會處理加密的資料和非純文字的值。 即使 SQL Server 執行個體或主機電腦被入侵，攻擊者所能得到的也只是敏感性資料的加密文字。 如需詳細資訊，請參閱[搭配使用 Always Encrypted 與 JDBC 驅動程式](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)。

### <a name="internationalized-domain-names"></a>國際化網域名稱

此驅動程式支援針對伺服器名稱使用國際化網域名稱 (IDN)。 如需詳細資訊，請參閱 [JDBC Driver 的國際功能](../../connect/jdbc/international-features-of-the-jdbc-driver.md)一文中的「使用國際網域名稱」。

### <a name="parameterized-queries"></a>參數化查詢

驅動程式現在支援針對子查詢和/或聯結等複雜查詢，使用備妥陳述式來擷取參數中繼資料。 請注意，只有使用 SQL Server 2012 與更新版本時，才能使用此改進功能。

### <a name="azure-active-directory"></a>Azure Active Directory

Azure AD 驗證是使用 Azure AD 中的身分識別連線至 Azure SQL Database v12 的機制。 使用 Azure AD 驗證集中管理資料庫使用者的身分識別，並作為 SQL Server 的替代驗證。 

您可以使用 JDBC Driver 6.0，在連線到 Azure SQL Database 的 JDBC 連接字串中指定 Azure AD 認證。 如需詳細資訊，請參閱[設定連線屬性](../../connect/jdbc/setting-the-connection-properties.md)一文中的驗證屬性。

### <a name="table-valued-parameters"></a>資料表值參數

TVP 提供從用戶端應用程式，將多個資料列的資料封送至 SQL Sever 的簡便方式，而不需多次來回存取或特殊的伺服器端邏輯才能處理資料。 您可以使用 TVP，以一個參數化命令在用戶端應用程式中封裝資料列的資料，並傳送至伺服器。 傳入的資料列會儲存於資料表變數中，讓您之後可使用 Transact-SQL 進行運算。 如需詳細資訊，請參閱[使用資料表值參數](../../connect/jdbc/using-table-valued-parameters.md)。

### <a name="always-on-availability-groups"></a>AlwaysOn 可用性群組

此驅動程式現在支援以透明的方式連線至 AlwaysOn 可用性群組。 驅動程式會快速探索伺服器基礎結構目前的 Always On 拓撲，並以透明的方式連線至目前使用中的伺服器。

## <a name="42"></a>4.2

Microsoft JDBC Driver 4.2 for SQL Server 完全符合 JDBC 規格 4.1 和 4.2 的規範。 4\.2 套件中的 jar 會根據其與 JDBC API 版本的合規性進行命名。 例如，4.2 套件中的 sqljdbc42.jar 檔案會符合 JDBC API 4.2 的規範。 同樣地，sqljdbc41.jar 檔案會符合 JDBC API 4.1 的規範。

若要確保您擁有正確的 sqljdbc42.jar 或 sqljdbc41.jar 檔案，請執行下列程式碼行。 如果輸出為「驅動程式版本：4.2.6420.100」，表示您有 JDBC 驅動程式 4.2 套件。

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="support-for-jdk-8"></a>支援 JDK 8

除了 JDK 7.0、6.0 及 5.0，此驅動程式還支援 JDK 8.0 版。

### <a name="jdbc-41-and-42-compliance"></a>JDBC 4.1 和 4.2 相容性

除了 Java 資料庫連線 API 4.0 規格之外，驅動程式也支援 Java 資料庫連線 API 4.1 與 4.2 規格。 如需詳細資訊，請參閱[適用於 JDBC Driver 的 JDBC 4.1 合規性](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md)和[適用於 JDBC Driver 的 JDBC 4.2 合規性](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)。

### <a name="bulk-copy"></a>大量複製

您使用大量複製功能可用來快速將大量資料複製到 SQL Server 資料庫中的資料表或檢視。 如需詳細資訊，請參閱[搭配 JDBC 驅動程式使用大量複製](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)。

### <a name="xa-transaction-rollback-option"></a>XA 交易回復選項

對於已取消準備交易的現有自動回復，驅動程式有新的逾時選項。 如需詳細資訊，請參閱[了解 XA 交易](../../connect/jdbc/understanding-xa-transactions.md)。

### <a name="new-kerberos-principal-connection-property"></a>新的 Kerberos 主體連線屬性

驅動程式使用新的連線屬性，讓 Kerberos 連線更具彈性。 如需詳細資訊，請參閱[使用 Kerberos 整合式驗證連線到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。

## <a name="41"></a>4.1

### <a name="support-for-jdk-7"></a>JDK 7 支援

除了 JDK 6.0 和 5.0，此驅動程式還支援 JDK 7.0 版。

## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>JDBC Driver 6.4、6.0、4.2 與 4.1 應用程式不支援 Itanium

不支援在 Itanium 電腦上執行 Microsoft JDBC Drivers 6.4、6.0、4.2 與 4.1 for SQL Server 應用程式。

## <a name="see-also"></a>另請參閱

[JDBC Driver 概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)