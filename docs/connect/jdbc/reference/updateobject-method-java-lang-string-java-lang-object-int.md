---
title: setObject 方法 (java.lang.String, java.lang.Object, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateObject (java.lang.String, java.lang.Object, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 27283ce1-637e-4e2c-91ee-8ad379114ac5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10959976eb6c3c9908d7f5953a8a2edb1c1328c8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654908"
---
# <a name="updateobject-method-javalangstring-javalangobject-int"></a>updateObject 方法 (java.lang.String, java.lang.Object, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根據指定的資料行索引和小數位數，使用 **Object** 值來更新指定的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateObject(java.lang.String columnName,  
                         java.lang.Object x,  
                         int scale)  
```  
  
#### <a name="parameters"></a>參數  
 *columnName*  
  
 包含資料行名稱的**字串**。  
  
 *obj*  
  
 **Object** 值。  
  
 *scale*  
  
 如果是 java.sql.Types.DECIMAL 或 java.sql.Types.NUMERIC 型別，這就是小數點後面的位數。 如果是所有其他型別，則會忽略這個值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 UpdateObject 方法 java.sql.ResultSet 介面中所指定這個 updateObject 方法。  
  
## <a name="see-also"></a>另請參閱  
 [updateObject 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateobject-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
