---
title: "rollback 方法 （) |Microsoft 文件"
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
- SQLServerConnection.rollback ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7adb6772-4047-4d8e-931d-b3d20eec44b5
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6c913613419a1922cba3166c7d967eef9ef4d635
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="rollback-method-"></a>rollback 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  復原目前交易中所做的所有變更，並釋放目前由這個保留的任何資料庫鎖定[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void rollback()  
```  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 此復原的方法是由 java.sql.Connection 介面中的 rollBack 方法指定。  
  
 只有當已經停用自動認可模式時，才應該使用這個方法。  
  
## <a name="see-also"></a>另請參閱  
 [rollback 方法 &#40;SQLServerConnection &#41;](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)   
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

