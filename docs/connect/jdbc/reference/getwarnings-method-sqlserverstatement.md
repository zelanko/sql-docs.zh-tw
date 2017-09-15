---
title: "getWarnings 方法 (SQLServerStatement) |Microsoft 文件"
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
- SQLServerStatement.getWarnings
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3d6decae-2570-4ca5-8ff6-57a2cc3e921f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1242bc3bd6e96e42e4b40936882b3f445c55ba59
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getwarnings-method-sqlserverstatement"></a>getWarnings 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取由呼叫所報告的第一個警告[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final java.sql.SQLWarning getWarnings()  
```  
  
## <a name="return-value"></a>傳回值  
 SQLWarning 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getWarnings 方法是由 java.sql.Statement 介面中的 getWarnings 方法來指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
