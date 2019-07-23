---
title: SQLServerException 的構造函式 (JAVA.lang.throwable) |Microsoft Docs
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
ms.openlocfilehash: 14984450507b5eea63d2fbe88bb2e7f957f61868
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67971072"
---
# <a name="sqlserverexception-constructor-javalangstring-javalangthrowable"></a>SQLServerException 的構造函式 (JAVA.lang.throwable)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定**字串**物件和**java.lang.throwable**物件時, 初始化[SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)類別的新實例。

## <a name="syntax"></a>語法  
  
```  
public SQLServerException(java.lang.String errText,
            java.lang.Throwable cause)
            
```  
  
#### <a name="parameters"></a>參數  
 *errText*  
  
 包含錯誤文字的字串。
 
 *cause*  
  
 包含例外狀況原因的 java.lang.throwable 物件。
  
## <a name="see-also"></a>另請參閱  
 [SQLServerException 建構函式](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 成員](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 類別](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
