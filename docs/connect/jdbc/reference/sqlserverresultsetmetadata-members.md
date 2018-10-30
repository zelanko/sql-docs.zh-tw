---
title: SQLServerResultSetMetaData 成員 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 37587981-2979-49a3-a6ab-df4bfb9b8748
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 912bd276e9b80911e7dec71d7edbb68cd30676af
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47818596"
---
# <a name="sqlserverresultsetmetadata-members"></a>SQLServerResultSetMetaData 成員
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出由 [SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) 類別公開的成員。  
  
## <a name="constructors"></a>建構函式  
 無。  
  
## <a name="fields"></a>欄位  
 無。  
  
## <a name="inherited-fields"></a>繼承的欄位  
  
|[屬性]|Description|  
|----------|-----------------|  
|java.sql.ResultSetMetaData|columnNoNulls, columnNullable, columnNullableUnknown|  
  
## <a name="methods"></a>方法  
  
|[屬性]|Description|  
|----------|-----------------|  
|[getCatalogName](../../../connect/jdbc/reference/getcatalogname-method-sqlserverresultsetmetadata.md)|取得包含所指定之資料行之資料表的目錄名稱。|  
|[getColumnClassName](../../../connect/jdbc/reference/getcolumnclassname-method-sqlserverresultsetmetadata.md)|傳回 Java 類別的完整名稱，此類別執行個體會在呼叫 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 類別的 [getObject](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md) 方法來從資料行擷取值時進行製造。|  
|[getColumnCount](../../../connect/jdbc/reference/getcolumncount-method-sqlserverresultsetmetadata.md)|傳回結果集中的資料行數目。|  
|[getColumnDisplaySize](../../../connect/jdbc/reference/getcolumndisplaysize-method-sqlserverresultsetmetadata.md)|傳回所指定資料行的正常最大寬度，以字元為單位。|  
|[getColumnLabel](../../../connect/jdbc/reference/getcolumnlabel-method-sqlserverresultsetmetadata.md)|取得建議在指定之資料行之列印輸出和顯示中使用的標題。|  
|[getColumnName](../../../connect/jdbc/reference/getcolumnname-method-sqlserverresultsetmetadata.md)|取得所指定資料行的名稱。|  
|[getColumnType](../../../connect/jdbc/reference/getcolumntype-method-sqlserverresultsetmetadata.md)|擷取指定之資料行的 SQL 型別。|  
|[getColumnTypeName](../../../connect/jdbc/reference/getcolumntypename-method-sqlserverresultsetmetadata.md)|擷取所指定資料行的資料庫特性類型名稱。|  
|[getPrecision](../../../connect/jdbc/reference/getprecision-method-sqlserverresultsetmetadata.md)|取得所指定資料行的小數位數。|  
|[getScale](../../../connect/jdbc/reference/getscale-method-sqlserverresultsetmetadata.md)|取得指定之資料行小數點右邊的位數。|  
|[getSchemaName](../../../connect/jdbc/reference/getschemaname-method-sqlserverresultsetmetadata.md)|取得指定之資料行的資料表結構描述名稱。|  
|[getTableName](../../../connect/jdbc/reference/gettablename-method-sqlserverresultsetmetadata.md)|取得指定之資料行的資料表名稱。|  
|[isAutoIncrement](../../../connect/jdbc/reference/isautoincrement-method-sqlserverresultsetmetadata.md)|指出指定之資料行是否已自動編號而形成唯讀狀態。|  
|[isCaseSensitive](../../../connect/jdbc/reference/iscasesensitive-method-sqlserverresultsetmetadata.md)|指出資料行是否區分大小寫。|  
|[isCurrency](../../../connect/jdbc/reference/iscurrency-method-sqlserverresultsetmetadata.md)|指出指定的資料行是否為貨幣 (cash) 類型值。|  
|[isDefinitelyWritable](../../../connect/jdbc/reference/isdefinitelywritable-method-sqlserverresultsetmetadata.md)|指出寫入至所指定資料行的作業是否絕對會成功。|  
|[isNullable](../../../connect/jdbc/reference/isnullable-method-sqlserverresultsetmetadata.md)|指出指定之資料行中之值的 Null 屬性。|  
|[isReadOnly](../../../connect/jdbc/reference/isreadonly-method-sqlserverresultsetmetadata.md)|指出指定的資料行是否絕對不可寫入。|  
|[isSearchable](../../../connect/jdbc/reference/issearchable-method-sqlserverresultsetmetadata.md)|指出指定的資料行是否能用於 SQL WHERE 子句。|  
|[isSigned](../../../connect/jdbc/reference/issigned-method-sqlserverresultsetmetadata.md)|指出指定之資料行中的值是否為帶正負號的數值。|  
|[isSparseColumnSet](../../../connect/jdbc/reference/issparsecolumnset-method-sqlserverresultsetmetadata.md)|指出結果集中的資料行是否為疏鬆資料行集。|  
|[isWritable](../../../connect/jdbc/reference/iswritable-method-sqlserverresultsetmetadata.md)|指出寫入至指定之資料行的作業是否可能成功。|  
  
## <a name="inherited-methods"></a>繼承的方法  
  
|類別繼承自：|方法|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSetMetaData 類別](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
