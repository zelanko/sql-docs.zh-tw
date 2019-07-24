---
title: JDBC 驅動程式 API 參考 |Microsoft Docs
ms.custom: ''
ms.date: 07/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e4e1ae9d-18a6-41db-8bd2-9cf0eee4cccb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 04cbe39698a99fbde43043b70bb9b1f0e5887f58
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977006"
---
# <a name="jdbc-driver-api-reference"></a>JDBC Driver API 參考

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 提供的 API，可用於 Java 程式碼中，以連接 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫，並與其互動。



### <a name="javadocio-website-is-primary"></a>JAVADoc.io 網站是主要的

Microsoft JDBC API 參考檔是在 JAVADoc.io 網站上進行您的觀看所主控。 JAVADoc.io 現在是我們的主要網站, 適用于 JDBC 參考檔。 您可以從下列直接連結取得 JAVADoc.io 的 JDBC 參考檔:

- [https://javadoc.io/doc/com.microsoft.sqlserver/mssql-jdbc/](https://javadoc.io/doc/com.microsoft.sqlserver/mssql-jdbc/)

JAVADoc.io 具有從6.0 版開始的 JDBC 參考檔。

#### <a name="only-legacy-jdbc-documentation-is-here-on-docs"></a>這裡只有舊版 JDBC 檔

當新版本的 jdbc 類別更新時 **https://docs.microsoft.com/sql/connect/jdbc/reference/** , 中的 jdbc API 參考檔文章已不再更新。 不過, 這裡的文章包含 JDBC 版本4.1 和4.2 的所有參考。

JDBC 6.0 版和更新版本的檔也在這裡。 但針對任何6.0 版或更新版本, 請使用 JAVADoc.io 網站。



### <a name="important-notes"></a>重要事項

> [!NOTE]  
>  如需有關使用 JDBC 驅動程式的概念性資訊, 請參閱[JDBC driver 的總覽](../../../connect/jdbc/overview-of-the-jdbc-driver.md)。  
  
> [!IMPORTANT]  
>  如需 JDBC 4.1 與 4.2 合規性支援，請使用 Microsoft JDBC Driver 4.2 for SQL Server (或更高版本)。 先前的 Microsoft JDBC Drivers 4.1 和 4.0 版本不支援使用 JDBC 4.1 或 4.2 引進的新方法。  
>   
>  本章節未包含 JDBC 4.1 相容性的 API 詳細資訊。 請參閱[適用於 JDBC 驅動程式的 JDBC 4.1 合規性](../../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md)。  
>   
>  本章節未包含 JDBC 4.2 相容性的 API 詳細資料。 請參閱[適用於JDBC 驅動程式的 JDBC 4.2 合規性](../../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)。  
>   
>  本節未包含從 Microsoft JDBC Driver 4.2 for SQL Server 起所提供的大量複製功能之 API 詳細資料。 請參閱[搭配 JDBC 驅動程式使用大量複製](../../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)。  
>   
>  本節未包含從 Microsoft JDBC Driver 6.0 for SQL Server 起所提供的 Always Encrypted 功能之 API 詳細資料。 請參閱[適用於 JDBC 驅動程式的 Always Encrypted API 參考](../../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  
>   
>  在本節中找不到使用資料表值參數的 API 詳細資料 (從 Microsoft JDBC Driver 6.0 for SQL Server 開始提供)。 請參閱[使用資料表值參數](../../../connect/jdbc/using-table-valued-parameters.md)  
>   
>  Microsoft JDBC Driver 6.4 支援 JDK 7.0、8.0 和 9.0 的編譯。  
>   
>  Microsoft JDBC Driver 6.2 支援 JDK 7.0 和 8.0 的編譯。  
>   
>  Microsoft JDBC Drivers 6.0 及 4.2 支援 JDK 5.0、6.0、7.0 和 8.0 的編譯。  
>   
>  Microsoft JDBC Driver 4.1 支援 JDK 5.0、6.0 與 7.0 的編譯。  



## <a name="interfaces"></a>介面  
  
|介面名稱|Description|  
|--------------------|-----------------|  
|[ISQLServerCallableStatement 介面](../../../connect/jdbc/reference/isqlservercallablestatement-interface.md)|讓您指定要呼叫的預存程序名稱，連同輸入和輸出參數。|  
|[ISQLServerConnection 介面](../../../connect/jdbc/reference/isqlserverconnection-interface.md)|代表與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的 JDBC 連接。|  
|[SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)|代表使用 [ISQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件，連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的特定屬性清單。|  
|[ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)|代表 JDBC 備妥之陳述式功能的基本實作。|  
|[ISQLServerResultSet](../../../connect/jdbc/reference/isqlserverresultset-interface.md)|代表 JDBC 結果集。|  
|[ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)|代表 JDBC 陳述式功能的基本實作。|
| &nbsp; | &nbsp; |


  
## <a name="classes"></a>類別  
  
|類別名稱|Description|  
|----------------|-----------------|  
|[DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)|代表 microsoft.sql.DateTimeOffset 型別的物件。|  
|[SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)|代表二進位大型物件 (BLOB)。|  
|[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)|實作 ISQLServerCallableStatement。|  
|[SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)|代表字元大型二進位物件 (CLOB)。|  
|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)|實作 ISQLServerConnectopn。|  
|[SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)|代表連接集區管理員的實體資料庫連接。|  
|[SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)|代表資料庫的中繼資料。|  
|[SQLServerDataSource](../../../connect/jdbc/reference/isqlserverdatasource-interface.md)|代表使用 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件，連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的特定屬性清單。|  
|[SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)|代表可具體化來自 Java Naming and Directory Interface (JNDI) 之資料來源的物件 Factory。|  
|[SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)|代表 JDBC Driver。 這個類別包含的方法可用來連線到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫，以及取得 JDBC 驅動程式的相關資訊。|  
|[SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)|代表 SQL 陳述式執行不成功或不完整。|  
|[SQLServerNClob 類別](../../../connect/jdbc/reference/sqlservernclob-class.md)|代表使用國家字元集 (National Character Set) 的字元大型二進位物件 (CLOB)。|  
|[SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)|代表準備陳述式參數的中繼資料。|  
|[SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)|代表連接集區中的實體資料庫連接。|  
|[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)|實作 ISQLServerPreparedStatement。|  
|[SQLServerResource](../../../connect/jdbc/reference/sqlserverresource-class.md)|代表當地語系化的錯誤字串資源。 這個類別僅供內部使用。|  
|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)|實作 ISQLServerResultSet。|  
|[SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)|代表結果集中所包含之資料行的中繼資料。|  
|[SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md)|代表可將交易回復至該處的檢查點。|  
|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)|實作 ISQLServerStatement。|  
|[SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)|代表可以參與分散式 (XA) 交易的 JDBC 連接。|  
|[SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)|代表內部使用之 [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) 物件的 Factory。|  
|[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)|代表 XA 分散式交易管理的 XAResource。|
| &nbsp; | &nbsp; |



## <a name="see-also"></a>另請參閱  
 [JDBC Driver 概觀](../../../connect/jdbc/overview-of-the-jdbc-driver.md)

