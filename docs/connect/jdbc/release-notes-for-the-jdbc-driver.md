---
title: JDBC 驅動程式的版本資訊 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
caps.latest.revision: 206
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ec71defcba0a6f122d3c3ff9a098e163f07079c
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38021117"
---
# <a name="release-notes-for-the-jdbc-driver"></a>JDBC 驅動程式的版本資訊
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

## <a name="updates-in-microsoft-jdbc-driver-64-for-sql-server"></a>Microsoft JDBC Driver 6.4 for SQL Server 的更新
Microsoft JDBC Driver 6.4 for SQL Server 是完全符合 JDBC 規格 4.1 和 4.2。 6.4 封裝中包含的 jar 會命名為根據 Java 版本相容性。 比方說，建議從 6.4 封裝 mssql-jdbc-6.4.0.jre8.jar 檔案適用於 Java 8。 

**JDK 9 支援**  
  
除了 JDK 8.0 與 7.0 以外，還支援 Java Development Kit (JDK) 9.0 版。
  
**JDBC 4.3 合規性**  
  
除了 4.1 與 4.2 以外，還支援 Java 資料庫連線 API 4.3 規格。 JDBC 4.3 API 方法已加入，但尚未實作。 如需詳細資訊，請參閱[JDBC driver 的 JDBC 4.3 合規性](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md)。
 
**加入新的連接屬性： sslProtocol**

加入新的連接屬性，可讓使用者指定 TLS 通訊協定關鍵字。 可能的值為:"TLS"、"TLSv1 」、 「 TLSv1.1"、"TLSv1.2 」。 請參閱[SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol)如需詳細資訊。

**連接屬性已被取代： fipsProvider**

連接屬性 「 fipsProvider"是從可接受的連接屬性的清單中移除。 查看詳細資料[此處](https://github.com/Microsoft/mssql-jdbc/pull/460)。

**加入的連接屬性來指定自訂 TrustManager**

驅動程式現在支援使用已新增 「 trustManagerClass"和"trustManagerConstructorArg"連接屬性。 這可讓您動態指定一組以每個連接為基礎而不需修改 JVM 環境的全域設定受信任的憑證。

**已新增的支援 datetime/smallDatetime 在資料表值參數 (TVP)**

使用資料表值參數 (TVP) 時，驅動程式現在支援 datatypes DATETIME 和 SMALLDATETIME。

**已新增的支援 sql_variant 資料類型**

JDBC 驅動程式現在支援搭配 SQL Server 的 sql_variant 資料類型。 Sql_variant 也支援功能，例如資料表值參數 (TVP) 和大量複製具有以下限制：

1. 日期值： 當使用 TVP 填入資料表，其中包含儲存在 sql_variant 資料行中的 datetime/smalldatetime/date 值，對結果集呼叫 Getdatetime 方法無法運作並擲回下列例外狀況：
    ```
    java.lang.String cannot be cast to java.sql.Timestamp
    ```
    因應措施：請改用 "getString()" 或 "getObject()"。

2. 針對 Null 值搭配 SQL 變數使用 TVP

如果您使用 TVP 填入資料表，並將 NULL 值傳送至 sql_variant 資料行類型，就會發生例外狀況，因為目前不支援於 TVP 中的資料行類型 sql_variant 插入 NULL 值。

**實作已備妥的陳述式中繼資料快取**

JDBC 驅動程式已實作備妥陳述式中繼資料快取的效能改進。 驅動程式現在支援在將驅動程式與 「 disableStatementPooling"和"statementPoolingCacheSize"連接屬性中的快取的已備妥的陳述式中繼資料。 此功能預設為停用。 您可以在[這裡](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)找到更多資訊

**已新增的支援在 Linux/Mac 上的 AAD 整合式驗證**

JDBC 驅動程式現在也透過 Kerberos，在所有支援的作業系統 (Windows/Linux/Mac) 上支援 Azure Active Directory 整合式驗證。 或者，Windows 作業系統上，使用者可以向 sqljdbc_auth.dll。

**更新的 ADAL4J 版本 1.4.0 到**

JDBC 驅動程式已更新為 1.4.0 版的 azure active directory-程式庫-的-java (ADAL4J) 在其 maven 相依性。 如需有關相依性的詳細資訊，請參閱[這裡](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)

## <a name="updates-in-microsoft-jdbc-driver-62-for-sql-server"></a>Microsoft JDBC Driver 6.2 for SQL Server 的更新
Microsoft JDBC Driver 6.2 for SQL Server 是完全符合 JDBC 規格 4.1 和 4.2。 根據 Java 版本相容性為 6.0 套件中包含的 jar。 比方說，建議 mssql-jdbc-6.2.1.jre8.jar 檔案從 6.2 的套件，適用於 Java 8。 

> [!NOTE]  
>  在已於 2017 年 6 月 29 日發行 JDBC 6.2 RTW 中找不到中繼資料快取改進的問題。 改進已回復，而且新的 jar （版本 6.2.1） 上發行於 2017 年 7 月 17 日[Microsoft 下載中心](https://go.microsoft.com/fwlink/?linkid=852460)， [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1)，並[Maven 中央](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.sqlserver%22%20AND%20a%3A%22mssql-jdbc%22)。 請更新您的專案，以使用 6.2.1 發行的 jar。 請檢視[版本資訊](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1)如需詳細資訊。

**適用於 Linux 的 azure Active Directory (AAD) 支援**

您 Linux 應用程式連接至 Azure SQL Database 使用 AAD 驗證的使用者名稱/密碼和存取權杖的方法。

**聯邦資訊處理標準 (FIPS) 啟用 Jvm**

JDBC 驅動程式現在可以用在以符合美國聯邦標準與相容性的 FIPS 140 相容性模式中執行的 Jvm 上。 

**Kerberos 驗證的增強功能** 

JDBC 驅動程式現已支援： 
* 其中 Kerberos 設定不能修改或無法擷取新的權杖或 keytab 的應用程式的主體/密碼方法。 這個方法可以用於驗證 SQL Server，只允許 Kerberos 驗證。 
* 跨領域驗證使用 Kerberos 整合式驗證，而不需要明確地設定伺服器的 SPN。 驅動程式現在會自動計算領域即使在尚未提供。
* 接受 Kerberos 限制委派會模擬 GSS 認證物件，透過資料來源為使用者認證。 此模擬的認證則用來建立 Kerberos 連接。 

**已新增的逾時**

JDBC 驅動程式現在支援下列可設定逾時將會根據您的應用程式的需求： 
* 執行查詢時，就會發生查詢逾時，若要控制的逾時之前要等待的秒數。 
* 若要指定的通訊端上發生逾時之前要等候的毫秒數讀取，或接受通訊端逾時。 

## <a name="updates-in-microsoft-jdbc-driver-61-for-sql-server"></a>Microsoft JDBC Driver 6.1 for SQL Server 的更新

SQL Server 的 Microsoft JDBC Driver 6.1 是完全符合 JDBC 規格 4.1 和 4.2。 這是 JDBC 驅動程式的初始的開放原始碼版本，並包含對應至 Java 版本相容性 mssql-jdbc-6.1.0.jre8.jar mssql-jdbc-6.1.0.jre7.jar 檔案。 

## <a name="updates-in-microsoft-jdbc-driver-60-for-sql-server"></a>Microsoft JDBC Driver 6.0 for SQL Server 的更新

Microsoft JDBC Driver 6.0 for SQL Server 是完全符合 JDBC 規格 4.1 和 4.2。 根據合規性的 JDBC API 版本為 6.0 套件中包含的 jar。 例如，6.0 套件中的 sqljdbc42.jar 檔案是 API 符合 JDBC 4.2 規格。 同樣地，sqljdbc41.jar 檔案會遵守 JDBC API 4.1。

若要確保您有正確的 sqljdbc42.jar 或 sqljdbc41.jar，請執行下列程式碼行。 如果輸出已 「 驅動程式版本： 6.0.7507.100 」，您有 JDBC Driver 6.0 封裝。
```
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```  
 **永遠加密**  
  
 支援在 SQL Server 2016 中最新推出的 Always Encrypted 功能，這項新的安全性功能可確保沒有人能看到 SQL Server 執行個體中純文字形式的敏感性資料。 永遠加密的運作方式為明確加密應用程式中的資料，如此 SQL Server 就只會處理加密的資料和非純文字的值。 即使 SQL 執行個體或主機電腦遭到洩漏，攻擊者所能得到的也只是敏感性資料的加密文字。 如需詳細資料，請參閱[搭配使用 Always Encrypted 與 JDBC 驅動程式](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)。  
  
 **國際化網域名稱 (IDN)**  
  
 支援伺服器名稱使用國際化網域名稱 (IDN)。 如需詳細資訊，請參閱使用國際化網域名稱上[JDBC Driver 的國際功能](../../connect/jdbc/international-features-of-the-jdbc-driver.md)頁面。  
  
 **參數化查詢**  
  
 現在支援針對子查詢及 (或) 聯結等複雜查詢，使用備妥陳述式來擷取參數中繼資料。 請注意，只有使用 SQL Server 2012 及更新版本時，才可使用這項改進功能。  
  
 **Azure Active Directory (AAD)**  
  
 AAD 驗證是連接到 Azure SQL Database v12 的機制使用 AAD 中的身分識別。 使用 AAD 驗證集中管理資料庫使用者的身分識別，並作為 SQL Server 的替代驗證。 JDBC Driver 6.0 可讓您在連線到 Azure SQL DB 的 JDBC 連接字串中指定 AAD 認證。  如需詳細資訊，請參閱 [驗證] 屬性上[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)頁面。  
  
 **資料表值參數**  
  
 資料表值參數提供從用戶端應用程式，將多個資料列的資料封送至 SQL Sever 的簡便方式，而不需多次來回存取或特殊的伺服器端邏輯才能處理資料。 您可以使用資料表值參數，以一個參數化命令在用戶端應用程式中封裝資料列的資料，並傳送至伺服器。 內送資料列會儲存在資料表變數中，可以再由使用 TRANSACT-SQL。 如需詳細資訊，請參閱[Using Table-Valued 參數](../../connect/jdbc/using-table-valued-parameters.md)。  
  
 **AlwaysOn 可用性群組 (AG)**  
  
 驅動程式現在支援 AlwaysOn 可用性群組的透明連接。 驅動程式會快速探索伺服器基礎結構目前的 AlwaysOn 拓撲，並以透明的方式連線至目前使用中的伺服器。  
  
## <a name="updates-in-microsoft-jdbc-driver-42-for-sql-server-and-later"></a>Microsoft JDBC Driver 4.2 for SQL Server 及更新版本的更新  
Microsoft JDBC Driver 4.2 for SQL Server 是完全符合 JDBC 規格 4.1 和 4.2。 4.2 套件中包含的 jar 會命名為根據的 JDBC API 版本合規性。 比方說，從 4.2 封裝 sqljdbc42.jar 檔案是 API 符合 JDBC 4.2 規格。 同樣地，sqljdbc41.jar 檔案會遵守 JDBC API 4.1。

若要確保您有正確的 sqljdbc42.jar 或 sqljdbc41.jar，請執行下列程式碼行。 如果輸出是 「 驅動程式版本： 4.2.6420.100 」，您有 JDBC Driver 4.2 套件。
```
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```
 **JDK 8 支援**  
  
 支援 JDK 7.0、6.0 與 5.0 以外的 Java Development Kit (JDK) 8.0 版。  
  
 **JDBC 4.1 與 4.2 合規性**  
  
 除了 Java 資料庫連線 API 4.0 規格之外，也支援 Java 資料庫連線 API 4.1 和 4.2 規格。 如需詳細資訊，請參閱[JDBC driver 的 JDBC 4.1 相容性](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md)並[JDBC driver 的 JDBC 4.2 相容性](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)。  
  
 **大量複製**  
  
 大量複製功能可用來快速將大量資料複製到 SQL Server 資料庫中的資料表或檢視。 如需詳細資訊，請參閱[JDBC 驅動程式使用大量複製](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)。  
  
 **XA 交易回復選項**  
  
 對於已取消準備交易的現有自動回復，加入新的逾時選項。 如需詳細資料請參閱[了解 XA 交易](../../connect/jdbc/understanding-xa-transactions.md)。  
  
 **新的 Kerberos 主體連線屬性**  
  
 加入新的連接屬性，藉此讓 Kerberos 連線更具彈性。 如需詳細資料，請參閱[使用 Kerberos 整合式驗證連線到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。  
  
## <a name="updates-in-microsoft-jdbc-driver-41-for-sql-server-and-later"></a>Microsoft JDBC Driver 4.1 for SQL Server 及更新版的更新  
 **JDK 7 支援**  
  
 JDK 6.0 與 5.0 以外的 Java Development Kit (JDK) 7.0 版支援  
  
## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>JDBC Driver 6.4、6.0、4.2 與 4.1 應用程式不支援 Itanium  
  
 不支援在 Itanium 電腦上執行 Microsoft JDBC Drivers 6.4、6.0、4.2 與 4.1 for SQL Server 應用程式。  
  
## <a name="see-also"></a>另請參閱  
 [JDBC Driver 概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

