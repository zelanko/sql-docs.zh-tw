---
title: SQLServerException 建構函式 (java.lang.String，SQLState，DriverError，java.lang.Throwable) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 33f7b15a2f4dd8e83c7e703e96812f29691e6bd6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverexception-constructor-javalangstring-sqlstate-drivererror-javalangthrowable"></a>SQLServerException 建構函式 (java.lang.String，SQLState，DriverError，java.lang.Throwable)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  初始化的新執行個體[SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)類別時指定**字串**物件**sqlstate**物件**drivererror**物件，和**throwable**物件。

## <a name="syntax"></a>語法  
  
```  
public SQLServerException(java.lang.String errText,
            SQLState sqlState,
            DriverError driverError,
            java.lang.Throwable cause)
            
```  
  
#### <a name="parameters"></a>參數  
 *errText*  
  
 字串，包含錯誤文字。
  
 *sqlState*  
  
 列舉物件保存 SQL 狀態。
 
 *driverError*  
  
 存放驅動程式錯誤列舉物件。
 
 *可能的原因*  
  
 Throwable 物件保留造成例外狀況。
  
## <a name="see-also"></a>另請參閱  
 [SQLServerException 建構函式](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 成員](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 類別](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
