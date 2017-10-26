---
title: "absolute 方法 (SQLServerResultSet) |Microsoft 文件"
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
- SQLServerResultSet.absolute
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 638e8148-8ca0-4e1f-9ec2-04a11bc9809b
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c952c24cfab1a36715d98cf0aad6caad7212a601
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="absolute-method-sqlserverresultset"></a>absolute 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將游標移至指定的資料列，在這個[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean absolute(int row)  
```  
  
#### <a name="parameters"></a>參數  
 *資料列*  
  
 **Int** ，指出移至資料列數目。 可以為正數、負數或 0。  
  
## <a name="return-value"></a>傳回值  
 **true**如果將游標移至指定的位置。 **false**如果它是第一個資料列之前或之後的最後一個資料列。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個絕對的方法是由 java.sql.ResultSet 介面中的絕對方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

