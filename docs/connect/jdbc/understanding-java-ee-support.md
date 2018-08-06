---
title: 了解 Java EE 支援 |Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a9448b80-b7a3-49cf-8bb4-322c73676005
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d5cc306a407e818a79d67cfc4c4340e1a9c2b22
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278859"
---
# <a name="understanding-java-ee-support"></a>了解 Java EE 支援
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  下列各節列出 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 如何提供 Java Platform Enterprise Edition (Java EE) 和 JDBC 3.0 選用 API 功能的支援。 本說明系統中提供的原始程式碼範例提供開始使用這些功能的良好參考。  
  
 首先，請確認您的 Java 環境 (JDK、JRE) 包含 javax.sql 封裝。 這是使用選用 API 的任何 JDBC 應用程式所需的封裝。 JDK 1.5 和更新版本已經包含此套件；因此，您不需要另外安裝該套件。  
  
## <a name="driver-name"></a>驅動程式名稱  
 驅動程式類別名稱為 **com.microsoft.sqlserver.jdbc.SQLServerDriver**。 針對 JDBC Drivers 4.1、4.2 和 6.0，驅動程式包含在 sqljdbc.jar、sqljdbc4.jar、sqljdbc41.jar 或 sqljdbc42.jar 檔案中。 JDBC Driver 6.2，驅動程式都包含在 mssql-jdbc-6.2.1.jre7.jar 或 mssql-jdbc-6.2.1.jre8.jar。 若是 JDBC Driver 6.4，驅動程式被包含在 mssql-jdbc-6.4.0.jre7.jar、 mssql jdbc 6.4.0.jre8.jar 或 mssql-jdbc-6.4.0.jre9.jar。
  
 每當您載入具有 JDBC DriverManager 類別的驅動程式時，便會使用此類別名稱。 每當您必須在任何驅動程式設定中指定驅動程式的類別名稱時，也會使用此類別名稱。 例如，在 Java EE 應用程式伺服器中設定資料來源可能需要您輸入驅動程式類別名稱。  
  
## <a name="data-sources"></a>資料來源  
 JDBC Driver 會提供 Java EE / JDBC 3.0 資料來源的支援。 JDBC 驅動程式 [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) 類別是由 **com.microsoft.sqlserver.jdbc.SQLServerXADataSource** 實作。  
  
### <a name="datasource-names"></a>Datasource 名稱  
 您可以使用資料來源建立資料庫的連接。 適用於 JDBC 驅動程式的資料來源詳述於下表中：  
  
|DataSource 類型|類別名稱和描述|  
|---------------|--------------------------|  
|DataSource|com.microsoft.sqlserver.jdbc.SQLServerDataSource <br/> <br/> 非共用資料來源。|  
|ConnectionPoolDataSource|com.microsoft.sqlserver.jdbc.SQLServerConnectionPoolDataSource <br/> <br/> 設定 JAVA EE 應用程式伺服器連接集區的資料來源。 一般用於應用程式在 JAVA EE 應用程式伺服器中執行時。|  
|XADataSource|com.microsoft.sqlserver.jdbc.SQLServerXADataSource <br/> <br/> 設定 JAVA EE XA 資料來源的資料來源。 一般用於應用程式在 JAVA EE 應用程式伺服器和 XA 交易管理員中執行時。|  
  
### <a name="data-source-properties"></a>資料來源屬性  
 所有資料來源都支援設定和取得與基礎驅動程式屬性集相關聯之任何屬性的能力。  
  
 範例:  
  
 `setServerName("localhost");`  
  
 `setDatabaseName("AdventureWorks");`  
  
 下列顯示應用程式如何使用資料來源連接：  
  
```java
initialize JNDI ..  
Context ctx = new InitialContext(System.getProperties());  
...  
DataSource ds = (DataSource) ctx.lookup("MyDataSource");  
Connection c = ds.getConnection("user", "pwd");  
```  
  
 如需詳細的資料來源屬性的詳細資訊，請參閱[設定的資料來源屬性](../../connect/jdbc/setting-the-data-source-properties.md)。  
  
## <a name="see-also"></a>另請參閱  
 [JDBC Driver 概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
