---
title: "SQLServerClob 建構函式 （SQLServerConnection，java.lang.String） |Microsoft 文件"
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
- SQLServerConnection.SQLServerClob (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7058f4f7-ef3e-4d62-90d1-79299708b1eb
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 028d7d4803ff53f518067d869fa192512209d723
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverclob-constructor-sqlserverconnection-javalangstring"></a>SQLServerClob 建構函式 (SQLServerConnection, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  初始化的新執行個體[SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)類別時指定[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件和資料的字串。  
  
> [!NOTE]  
>  這個方法在 JDBC Driver 2.0 版中已被取代。 請改用[createClob](../../../connect/jdbc/reference/createclob-method-sqlserverconnection.md)方法[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)類別。  
  
## <a name="syntax"></a>語法  
  
```  
  
public SQLServerClob(SQLServerConnection connection,  
                     java.lang.String data)  
```  
  
#### <a name="parameters"></a>參數  
 *連線*  
  
 
          SQLServerConnection 物件。  
  
 *資料*  
  
 CLOB 資料。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerClob 建構函式](../../../connect/jdbc/reference/sqlserverclob-constructors.md)   
 [SQLServerClob 成員](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 類別](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  

