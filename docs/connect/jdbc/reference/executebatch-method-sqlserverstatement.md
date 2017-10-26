---
title: "executeBatch 方法 (SQLServerStatement) |Microsoft 文件"
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
- SQLServerStatement.executeBatch
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fb034f63-2532-4da8-a1b0-bc125734585a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 47f455ba7df88636de5ae9ecfc59a15827adf7d8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="executebatch-method-sqlserverstatement"></a>executeBatch 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將命令批次提交到要執行的資料庫。 如果所有命令都成功執行，則傳回更新計數陣列。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int[] executeBatch()  
```  
  
## <a name="return-value"></a>傳回值  
 陣列**int**的更新計數。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
 java.sql.BatchUpdateException  
  
## <a name="remarks"></a>備註  
 這個 executeBatch 方法是由 java.sql.Statement 介面中的 executeBatch 方法指定。  
  
 將命令提交到資料庫以後，這個方法會清除批次中的任何命令。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

