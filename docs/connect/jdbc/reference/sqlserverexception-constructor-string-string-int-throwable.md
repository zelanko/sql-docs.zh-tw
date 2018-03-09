---
title: "SQLServerException 建構函式 （java.lang.String，java.lang.String，int，java.lang.Throwable） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2018
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
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 98606e1dfa903c49ecd1152e49ca7d16406b167a
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2018
---
# <a name="sqlserverexception-constructor-javalangstring-javalangstring-int-javalangthrowable"></a>SQLServerException 建構函式 （java.lang.String，java.lang.String，int，java.lang.Throwable）
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  初始化的新執行個體[SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)類別時指定**字串**物件**字串**物件**int**，和**throwable**物件。

## <a name="syntax"></a>語法  
  
```  
public SQLServerException(java.lang.String errText,
            SQLState errState,
            int errNum,
            java.lang.Throwable cause)
            
```  
  
#### <a name="parameters"></a>參數  
 *errText*  
  
 字串，包含錯誤文字。
  
 *errState*  
  
 字串，包含錯誤的狀態。
 
 *errNum*  
  
 整數，其中包含例外狀況的錯誤碼。
 
 *cause*  
  
 Throwable 物件，其中包含造成此例外狀況。
  
## <a name="see-also"></a>另請參閱  
 [SQLServerException 建構函式](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 成員](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 類別](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
