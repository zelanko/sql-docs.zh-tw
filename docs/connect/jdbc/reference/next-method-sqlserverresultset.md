---
title: "next 方法 (SQLServerResultSet) |Microsoft 文件"
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
apiname:
- SQLServerResultSet.next
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 60248447-6908-4036-a779-a501453cd553
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5fe62919bd765d83e2d3a38a9cdda33d88312e29
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="next-method-sqlserverresultset"></a>next 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  從資料指標的目前位置，將資料指標向下移動到下一個資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean next()  
```  
  
## <a name="return-value"></a>傳回值  
 **true**新的目前資料列是否有效。 **false**如果沒有要處理多個資料列。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個下一個的方法是由 java.sql.ResultSet 介面中的下一個方法所指定。  
  
 結果集資料指標一開始位於第一個資料列的前面。 第一個呼叫下一個方法讓第一個資料列的目前資料列，第二次呼叫第二個資料列目前的資料列，依此類推。  
  
 如果輸入資料流已開啟的目前資料列下, 一個方法的呼叫會以隱含方式關閉它。 警告鏈結[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)讀取新的資料列時，會清除物件。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

