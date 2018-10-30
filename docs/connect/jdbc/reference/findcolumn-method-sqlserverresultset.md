---
title: findColumn 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.findColumn
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7c29994a-0b53-420b-8a9b-82a9eef08587
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a5ff2173990dabafab5297dd195e617825768aef
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47837726"
---
# <a name="findcolumn-method-sqlserverresultset"></a>findColumn 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取與這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中所指定資料行名稱相符的第一個資料行索引。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int findColumn(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>參數  
 *columnName*  
  
 **String**，包含資料行的名稱。  
  
## <a name="return-value"></a>傳回值  
 指出資料行索引的 **int**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 findColumn 方法是由 java.sql.ResultSet 介面中的 findColumn 方法指定。  
  
 如果有多個資料行同名，findColumn 方法會傳回第一個區分大小寫的相符項目。 如果沒有任何區分大小寫的相符項目，這個方法會傳回第一個不區分大小寫的相符項目。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
