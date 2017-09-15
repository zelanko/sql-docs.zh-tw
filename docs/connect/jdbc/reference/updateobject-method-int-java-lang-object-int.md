---
title: "updateObject 方法 （int，java.lang.Object，int） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSet.updateObject (int, java.lang.Object, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9d33571b-4887-49d3-96df-8abda7b5a904
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c7274ddfc4e4ca34df58699fb79b0f97cec6dcb1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="updateobject-method-int-javalangobject-int"></a>updateObject 方法 (int, java.lang.Object, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  更新指定的資料行與**物件**給定的資料行索引和小數位數的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateObject(int index,  
                         java.lang.Object x,  
                         int scale)  
```  
  
#### <a name="parameters"></a>參數  
 *索引*  
  
 **Int** ，指出資料行索引。  
  
 *obj*  
  
 **物件**值。  
  
 *scale*  
  
 如果是 java.sql.Types.DECIMAL 或 java.sql.Types.NUMERIC 型別，這就是小數點後面的位數。 如果是所有其他型別，則會忽略這個值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>另請參閱  
 [updateObject 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/updateobject-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
