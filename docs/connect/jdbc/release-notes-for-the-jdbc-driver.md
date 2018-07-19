---
title: JDBC 驅動程式的版本資訊 |Microsoft 文件
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
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32852483"
---
# <a name="release-notes-for-the-jdbc-driver"></a>JDBC 驅動程式的版本資訊
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

## <a name="updates-in-microsoft-jdbc-driver-64-for-sql-server"></a>Microsoft JDBC Driver 6.4 for SQL Server 中的更新
SQL Server 的 Microsoft JDBC 驅動程式 6.4 是完全符合 JDBC 規格 4.1 和 4.2。 （每瓶） 6.4 版的封裝中包含的命名為準 Java 版本相容性。 例如，6.4 版封裝的 mssql-jdbc-6.4.0.jre8.jar 檔案建議搭配 Java 8。 

**支援 JDK 9**  
  
Java Development Kit (JDK) 除了 JDK 8.0 和 7.0 9.0 版的支援。
  
**JDBC 4.3 相容性**  
  
支援 Java 資料庫連線 API 4.3 規格，除了 4.1 和 4.2。 JDBC 4.3 API 方法已加入，但是尚未實作。 如需詳細資訊，請參閱[JDBC 驅動程式的 JDBC 4.3 相容性](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md)。
 
**加入新的連接屬性： sslProtocol**

加入新的連接屬性，可讓使用者指定 TLS 通訊協定關鍵字。 可能的值為:"TLS"、"TLSv1"、"TLSv1.1"、"TLSv1.2"。 請參閱[SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol)如需詳細資訊。

**連接屬性已被取代： fipsProvider**

連接屬性 」 fipsProvider 」 會從可接受的連接屬性清單中移除。 請參閱詳細資料[這裡](https://github.com/Microsoft/mssql-jdbc/pull/460)。

**加入的連接屬性來指定自訂 TrustManager**

驅動程式現在支援指定自訂 TrustManager 加入 「 trustManagerClass 」 與 「 trustManagerConstructorArg"連接屬性。 這可讓每個連線為基礎而不需修改 JVM 環境的全域設定信任憑證的一組動態的規格。

**已新增的支援 datetime/smallDatetime 中資料表值參數 (TVP)**

使用資料表值參數 (TVP) 時，驅動程式現在支援 DATETIME 和 SMALLDATETIME 資料型別。

**已新增的支援 sql_variant 資料類型**

JDBC 驅動程式現在支援 sql_variant 資料類型，搭配 SQL Server。 Sql_variant 也被支援的功能，例如資料表值參數 (TVP) 和大量複製具有以下限制：

1. 對於日期值： 當使用 TVP 來擴展資料表，其中包含儲存在 sql_variant 資料行中的日期/datetime/smalldatetime 值時，結果集上呼叫 getDateTime()/getSmallDateTime()/getDate() 方法會無法運作，而擲回下列例外狀況：
    ```
    java.lang.String cannot be cast to java.sql.Timestamp
    ```
    因應措施： 請改用"Sr"或"getObject() 」 方法。

2. 使用 null 值一起 SQL Variant TVP

如果您使用 TVP 擴展資料表，並將 NULL 值傳送至 sql_variant 資料行類型，就會發生例外狀況，因為目前不支援與 sql_variant 資料行類型中 TVP 的插入 NULL 值。

**實作備妥的陳述式中繼資料快取**

JDBC 驅動程式已實作備妥的陳述式中繼資料快取以改進效能。 驅動程式現在支援 「 disableStatementPooling"和"statementPoolingCacheSize"連接屬性與驅動程式中的快取的已備妥的陳述式中繼資料。 此功能預設為停用。 可以找到更多資訊[這裡](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)

**加入的 AAD Linux/Mac 上的整合式驗證的支援**

JDBC 驅動程式現在也支援 Azure Active Directory 整合式驗證的所有支援作業系統 (Windows/Linux/Mac) Kerberos。 此外，Windows 作業系統上，使用者可以向 sqljdbc_auth.dll。

**更新的 1.4.0 ADAL4J 版本**

JDBC 驅動程式已更新為版本 1.4.0 的 maven 相依於 azure-activedirectory-程式庫-如-java (ADAL4J)。 如需相依性的詳細資訊，請參閱[這裡](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)

## <a name="updates-in-microsoft-jdbc-driver-62-for-sql-server"></a>Microsoft JDBC Driver for SQL Server 6.2 中的更新
SQL Server 的 Microsoft JDBC 驅動程式 6.2 是完全符合 JDBC 規格 4.1 和 4.2。 （每瓶） 6.0 套件中包含的命名為準 Java 版本相容性。 例如，mssql-jdbc-6.2.1.jre8.jar 檔案從 6.2 套件建議搭配 Java 8。 

> [!NOTE]  
>  已於 2017 年 6 月 29，發行 JDBC 6.2 RTW 中找不到中繼資料快取改進的問題。 改進已回復，而且新 （每瓶） （版本 6.2.1） 上發行的 2017 年 7 月 17， [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=852460)， [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1)，和[Maven 中央](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.sqlserver%22%20AND%20a%3A%22mssql-jdbc%22)。 請更新您的專案以使用 6.2.1 版本 （每瓶）。 請檢視[版本資訊](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1)如需詳細資訊。

**適用於 Linux 的 azure Active Directory (AAD) 支援**

您 Linux 應用程式連接至 Azure SQL Database 使用 AAD 驗證透過使用者名稱/密碼與存取語彙基元的方法。

**聯邦資訊處理標準 (FIPS) 啟用 JVMs**

JDBC 驅動程式現在可以用於 JVMs FIPS 140 以符合美國聯邦標準與相容性的相容性模式中執行。 

**Kerberos 驗證的增強功能** 

JDBC 驅動程式現在可支援： 
* 其中 Kerberos 設定不能修改或無法擷取新的權杖或 keytab 應用程式的主體/密碼方法。 這個方法可以用於驗證 SQL Server，只允許 Kerberos 驗證。 
* 跨領域驗證使用 Kerberos 整合式驗證未明確設定伺服器的 SPN。 驅動程式現在會自動計算之領域即使未提供。
* 接受 Kerberos 限制委派會模擬使用者認證當做資料來源透過 GSS 認證物件。 此模擬的認證然後用來建立 Kerberos 連接。 

**增加逾時**

JDBC 驅動程式現在支援可設定逾時將會根據您的應用程式需求： 
* 若要控制執行查詢時發生逾時之前要等候的秒數的查詢逾時。 
* 若要指定讀取通訊端上發生逾時之前要等候的毫秒數，或接受通訊端逾時。 

## <a name="updates-in-microsoft-jdbc-driver-61-for-sql-server"></a>Microsoft JDBC Driver 6.1 for SQL Server 中的更新

SQL Server 的 Microsoft JDBC 驅動程式 6.1 是完全符合 JDBC 規格 4.1 和 4.2。 這是 JDBC 驅動程式的初始的開放原始碼版本，並包含 mssql-jdbc-6.1.0.jre8.jar mssql-jdbc-6.1.0.jre7.jar 檔案，其對應至 Java 版本相容性。 

## <a name="updates-in-microsoft-jdbc-driver-60-for-sql-server"></a>Microsoft JDBC Driver 6.0 for SQL Server 中的更新

Microsoft JDBC Driver 6.0 for SQL Server 會完全符合 JDBC 規格 4.1 和 4.2。 （每瓶） 6.0 套件中包含的命名為準相容性的 JDBC API 版本。 例如，6.0 套件中的 sqljdbc42.jar 檔案是 JDBC API 4.2 相容。 同樣地，sqljdbc41.jar 檔案會符合 JDBC API 4.1。

若要確保您擁有正確的 sqljdbc42.jar 或 sqljdbc41.jar，執行下列程式碼。 如果輸出，則 「 驅動程式版本： 6.0.7507.100"，JDBC Driver 6.0 封裝。
```
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```  
 **永遠加密**  
  
 在 SQL Server 2016，新的安全性功能，可確保敏感性資料永遠不會看到以純文字的 SQL Server 執行個體中的最近發行永遠加密功能的支援。 永遠加密的運作方式為明確加密應用程式中的資料，如此 SQL Server 就只會處理加密的資料和非純文字的值。 即使 SQL 執行個體或主機電腦遭到入侵，攻擊者可以得到的也只是敏感性資料。 如需詳細資訊，請參閱[使用一律加密與 JDBC 驅動程式](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)。  
  
 **國際化的網域名稱 (IDN)**  
  
 支援伺服器名稱使用國際化網域名稱 (IDN)。 如需詳細資訊，請參閱使用國際化網域名稱上[JDBC driver 的國際功能](../../connect/jdbc/international-features-of-the-jdbc-driver.md)頁面。  
  
 **參數型的查詢**  
  
 現在支援針對子查詢及 (或) 聯結等複雜查詢，使用備妥陳述式來擷取參數中繼資料。 請注意，只有使用 SQL Server 2012 及更新版本時，才可使用這項改進功能。  
  
 **Azure Active Directory (AAD)**  
  
 AAD 驗證是連接到 Azure SQL Database v12 的一種機制使用 AAD 中識別。 使用 AAD 驗證集中管理身分識別的資料庫使用者，以及 SQL Server 驗證的替代方案。 JDBC Driver 6.0 可讓您連接到 Azure SQL DB JDBC 連接字串中指定您的 AAD 認證。  如需詳細資訊，請參閱 [驗證] 屬性上[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)頁面。  
  
 **資料表值參數**  
  
 資料表值參數會提供簡單的方法，而不需多次來回存取或特殊的伺服器端邏輯來處理資料，從 SQL Server 用戶端應用程式資料的多個資料列封送處理。 您可以使用資料表值參數，是爲用戶端應用程式中的資料列，並將資料傳送至單一參數化命令中的伺服器。 可以再由使用 TRANSACT-SQL 資料表變數中儲存內送資料列。 如需詳細資訊，請參閱[Using Table-Valued 參數](../../connect/jdbc/using-table-valued-parameters.md)。  
  
 **AlwaysOn 可用性群組 (AG)**  
  
 驅動程式現在支援 AlwaysOn 可用性群組的透明連接。 驅動程式快速探索伺服器基礎結構目前的 AlwaysOn 拓撲，並以透明的方式連接到目前作用中的伺服器。  
  
## <a name="updates-in-microsoft-jdbc-driver-42-for-sql-server-and-later"></a>Microsoft JDBC Driver 4.2 for SQL Server 及更新版本的更新  
Microsoft JDBC Driver 4.2 for SQL Server 會完全符合 JDBC 規格 4.1 和 4.2。 （每瓶） 4.2 套件中包含的命名為準相容性的 JDBC API 版本。 例如，從 4.2 套件 sqljdbc42.jar 檔案是 JDBC API 4.2 相容。 同樣地，sqljdbc41.jar 檔案會符合 JDBC API 4.1。

若要確保您擁有正確的 sqljdbc42.jar 或 sqljdbc41.jar，執行下列程式碼。 如果輸出，則 「 驅動程式版本： 4.2.6420.100 」，您具有 JDBC Driver 4.2 套件。
```
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```
 **支援 JDK 8**  
  
 支援 JDK 7.0、6.0 與 5.0 以外的 Java Development Kit (JDK) 8.0 版。  
  
 **JDBC 4.1 和 4.2 相容性**  
  
 除了 Java 資料庫連線 API 4.0 規格之外，也支援 Java 資料庫連線 API 4.1 和 4.2 規格。 如需詳細資訊，請參閱[JDBC 驅動程式的 JDBC 4.1 相容性](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md)和[JDBC 驅動程式的 JDBC 4.2 相容性](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)。  
  
 **大量複製**  
  
 大量複製功能可用來快速將大量資料複製到 SQL Server 資料庫中的資料表或檢視。 如需詳細資訊，請參閱[JDBC 驅動程式使用大量複製](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)。  
  
 **XA 交易復原選項**  
  
 對於已取消準備交易的現有自動回復，加入新的逾時選項。 如需詳細資料請參閱[了解 XA 交易](../../connect/jdbc/understanding-xa-transactions.md)。  
  
 **新的 Kerberos 主體連接屬性**  
  
 加入新的連接屬性，藉此讓 Kerberos 連線更具彈性。 如需詳細資料請參閱[使用 Kerberos 整合式驗證來連接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。  
  
## <a name="updates-in-microsoft-jdbc-driver-41-for-sql-server-and-later"></a>Microsoft JDBC Driver 4.1 for SQL Server 及更新版的更新  
 **JDK 7 支援**  
  
 JDK 6.0 與 5.0 以外的 Java Development Kit (JDK) 7.0 版支援  
  
## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>JDBC Driver 6.4、 6.0、 4.2 與 4.1 應用程式不支援 Itanium  
  
 6.4、 6.0、 4.2 與 4.1 for SQL Server 應用程式的 Microsoft JDBC Driver 不支援在 Itanium 電腦上執行。  
  
## <a name="see-also"></a>另請參閱  
 [JDBC Driver 概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

