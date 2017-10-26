---
title: "getUpdateCount 方法 (SQLServerStatement) |Microsoft 文件"
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
- SQLServerStatement.getUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e9570228-4500-44b6-b2f1-84ac050b5112
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 50d702db72b2d02cc52401d76cd289a3b21de81a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getupdatecount-method-sqlserverstatement"></a>getUpdateCount 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取目前結果當做更新計數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final int getUpdateCount()  
```  
  
## <a name="return-value"></a>傳回值  
 **Int** ，其中包含更新計數。 如果傳回的結果是結果集物件或者沒有其他結果，則會傳回 -1。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getUpdateCount 方法是由 java.sql.Statement 介面中 getUpdateCount 方法來指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

