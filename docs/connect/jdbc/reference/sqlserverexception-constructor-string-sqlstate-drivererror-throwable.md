---
title: SQLServerException 建構函式 (java.lang.String、 SQLState、 DriverError、 java.lang.Throwable) |Microsoft Docs
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
ms.openlocfilehash: dc7608582a5ed146b656d41714853ba4c3b21b00
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47679976"
---
# <a name="sqlserverexception-constructor-javalangstring-sqlstate-drivererror-javalangthrowable"></a>SQLServerException 建構函式 (java.lang.String、 SQLState、 DriverError、 java.lang.Throwable)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  初始化的新執行個體[SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)類別，在給定**字串**物件**sqlstate**物件， **drivererror**物件，並**throwable**物件。

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
  
 列舉物件，持有的驅動程式錯誤。
 
 *cause*  
  
 會保留造成例外狀況 throwable 物件。
  
## <a name="see-also"></a>另請參閱  
 [SQLServerException 建構函式](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 成員](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 類別](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
