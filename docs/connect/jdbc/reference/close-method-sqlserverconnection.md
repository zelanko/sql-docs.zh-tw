---
title: "close 方法 (SQLServerConnection) |Microsoft 文件"
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
- SQLServerConnection.close
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f0f26585-bdf7-4737-b434-8c7e115c8e94
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e9f7dc84edb37bde6242be79830198ab565547e0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="close-method-sqlserverconnection"></a>close 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  釋放這個[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件的資料庫和 JDBC 資源，立即而非等待它們由系統自動釋放。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void close()  
```  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 此 close 方法是由 java.sql.Connection 介面中之關閉方法指定。  
  
 呼叫交易中間之關閉方法，會導致回復交易。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
