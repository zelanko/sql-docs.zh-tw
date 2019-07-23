---
title: getObject 方法 (int, java.util.Map) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getObject (int, java.util.Map)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: df85a514-ab43-4bf6-98dd-f7f37fad1850
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b66ef3388d8536ca4299891ec24f57fff41a3610
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67981267"
---
# <a name="getobject-method-int-javautilmap-sqlserverresultset"></a>getObject 方法 (int, java.util.Map) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 Java 程式設計語言，並透過指定的 Map 物件，從這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件目前資料列中取得指定的資料行索引值來當作物件。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 目前不支援這個方法。 因此，使用這個方法時一定會傳回預設對應。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.Object getObject(int i,  
                                  java.util.Map map)  
```  
  
#### <a name="parameters"></a>參數  
 *i*  
  
 指出資料行索引的 **int**。  
  
 *map*  
  
 Map 物件。  
  
## <a name="return-value"></a>傳回值  
 **Object** 值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getObject 方法是由 java.sql.ResultSet 介面中的 getObject 方法指定。  
  
 這個方法將傳回給定資料行的值來當做 Java 物件。 此 Java 物件將會是預設的 Java 物件類型，此種類型會對應到資料行的 SQL 類型，並且會對應於 JDBC 規格中所指定的內建類型。 如果該值為 SQL NULL，則驅動程式會傳回 Java null。  
  
 這個方法也可以用來讀取資料庫特性抽象資料類型。 在 JDBC 2.0 API 中，會延伸 getObject 方法的行為，以具體化 SQL 使用者定義型別的資料。 當資料行包含結構化或相異的值，這個方法的行為會如同對 `getObject(columnIndex, this.getStatement().getConnection().getTypeMap())` 的呼叫。  
  
 從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 驅動程式 3.0 開始：  
  
-   將會以 java.sql.Date 物件的形式傳回 date 型別的值。  
  
-   將會以 java.sql.Time 物件的形式傳回 time 型別的值。  
  
-   將會以 java.sql.Timestamp 物件的形式傳回 datetime2 型別的值。  
  
-   將會以 microsoft.sql.DateTimeOffset 物件的形式傳回 datetimeoffset 型別的值。  
  
## <a name="see-also"></a>另請參閱  
 [getObject 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
