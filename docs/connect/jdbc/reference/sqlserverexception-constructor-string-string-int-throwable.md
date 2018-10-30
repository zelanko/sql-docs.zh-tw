---
title: SQLServerException 建構函式 （java.lang.String、 java.lang.String、 int、 java.lang.Throwable） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f596056d830ae3fa3462095e5a17a112c8f641f2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47759256"
---
# <a name="sqlserverexception-constructor-javalangstring-javalangstring-int-javalangthrowable"></a>SQLServerException 建構函式 （java.lang.String、 java.lang.String、 int、 java.lang.Throwable）
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  初始化的新執行個體[SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)類別時指定**字串**物件**字串**物件， **int**，以及**throwable**物件。

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
  
 整數，包含例外狀況的錯誤碼。
 
 *cause*  
  
 Throwable 的物件，其中包含造成此例外狀況。
  
## <a name="see-also"></a>另請參閱  
 [SQLServerException 建構函式](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 成員](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 類別](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
