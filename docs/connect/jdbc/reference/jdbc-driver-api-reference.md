---
title: "JDBC 驅動程式 API 參考 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e4e1ae9d-18a6-41db-8bd2-9cf0eee4cccb
caps.latest.revision: 46
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c19740d1247fa1fd7fe8036fa2aa557e01e74c82
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="jdbc-driver-api-reference"></a>JDBC Driver API 參考
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]提供的 API，可用於 Java 程式碼連接至並與其互動[!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料庫。  
  
> [!NOTE]  
>  如需使用 JDBC 驅動程式的概念資訊，請參閱[JDBC 驅動程式概觀](../../../connect/jdbc/overview-of-the-jdbc-driver.md)。  
  
> [!IMPORTANT]  
>  JDBC 4.1 和 4.2 相容性支援，請使用 Microsoft JDBC Driver 4.2 （或更新版本） for SQL Server。 先前的 Microsoft JDBC Drivers 4.1 和 4.0 版本不支援使用 JDBC 4.1 或 4.2 引進的新方法。  
>   
>  本章節未包含 JDBC 4.1 相容性的 API 詳細資訊。 請參閱[JDBC 4.1 相容性的 JDBC 驅動程式](../../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md)。  
>   
>  本章節未包含 JDBC 4.2 相容性的 API 詳細資料。 請參閱[JDBC 4.2 相容性的 JDBC 驅動程式](../../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)。  
>   
>  本節中找不到可從 Microsoft JDBC Driver 4.2 for SQL Server 的大量複製的 API 詳細資料。 請參閱[JDBC 驅動程式使用大量複製](../../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)。  
>   
>  本節中找不到應用程式開發介面的永遠加密，可從 Microsoft JDBC Driver 6.0 for SQL Server 的詳細資料。 請參閱[永遠加密的 JDBC 驅動程式 API 參考](../../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  
>   
>  本節中找不到可從 Microsoft JDBC Driver 6.0 for SQL Server 的 Using Table-Valued 參數的 API 詳細資料。 請參閱[使用資料表值參數](../../../connect/jdbc/using-table-valued-parameters.md)  
>   
>  Microsoft JDBC Drivers 6.0 與 4.2 支援 JDK 5.0、 6.0、 7.0 和 8.0 的編譯。  
>   
>  Microsoft JDBC Driver 4.1 支援 JDK 5.0、6.0 與 7.0 的編譯。  
>   
>  Microsoft JDBC Driver 4.0 支援 JDK 5.0 與 6.0 的編譯。  
  
## <a name="interfaces"></a>介面  
  
|介面名稱|Description|  
|--------------------|-----------------|  
|[ISQLServerCallableStatement 介面](../../../connect/jdbc/reference/isqlservercallablestatement-interface.md)|讓您指定要呼叫的預存程序名稱，連同輸入和輸出參數。|  
|[ISQLServerConnection 介面](../../../connect/jdbc/reference/isqlserverconnection-interface.md)|代表 JDBC 連接[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料庫。|  
|[SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)|代表特定屬性清單，來連接至[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料庫使用[ISQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件。|  
|[ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)|代表 JDBC 備妥之陳述式功能的基本實作。|  
|[ISQLServerResultSet](../../../connect/jdbc/reference/isqlserverresultset-interface.md)|代表 JDBC 結果集。|  
|[ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)|代表 JDBC 陳述式功能的基本實作。|  
  
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
|[SQLServerDataSource](../../../connect/jdbc/reference/isqlserverdatasource-interface.md)|代表特定屬性清單，來連接至[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料庫使用[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件。|  
|[SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)|代表可具體化來自 Java Naming and Directory Interface (JNDI) 之資料來源的物件 Factory。|  
|[SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)|代表 JDBC Driver。 這個類別包含方法，用於連接到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料庫，以及取得有關 JDBC 驅動程式的資訊。|  
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
|[SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)|表示 factory [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)為內部使用的物件。|  
|[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)|XAResource 代表 xa 分散式交易管理。|  
  
## <a name="see-also"></a>另請參閱  
 [JDBC 驅動程式概觀](../../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

