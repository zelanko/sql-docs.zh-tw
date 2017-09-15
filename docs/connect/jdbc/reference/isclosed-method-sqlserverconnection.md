---
title: "isClosed 方法 (SQLServerConnection) |Microsoft 文件"
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
- SQLServerConnection.isClosed
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3560ab18-4350-4d02-9716-439f0c2f7142
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 634a402f06005c7235755988adf1435d38da0313
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="isclosed-method-sqlserverconnection"></a>isClosed 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指出是否此[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件已遭關閉。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean isClosed()  
```  
  
## <a name="return-value"></a>傳回值  
 **true**如果連接已關閉， **false**如果不是。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 IsClosed 方法 java.sql.Connection 介面中所指定此 isClosed 方法。  
  
 驗證呼叫的 SQLServerConnection 物件的狀態。 如果關閉連線[關閉](../../../connect/jdbc/reference/close-method-sqlserverconnection.md)已經呼叫方法，或發生某些嚴重錯誤。 這個方法會傳回**true**只有當呼叫它呼叫 close 方法之後。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
