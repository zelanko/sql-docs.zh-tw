---
title: close 方法 (SQLServerStatement) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerStatement.close
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 84a25d64-dd3e-4696-bb5f-4eaf391fab7e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 296b4551251913b9a8c8d2961bbf65d833390bb9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="close-method-sqlserverstatement"></a>close 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  釋放這個[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件的資料庫和 JDBC 資源，立即而非等待它們由系統自動釋放。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void close()  
```  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 此 close 方法是由 java.sql.Statement 介面中之關閉方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
