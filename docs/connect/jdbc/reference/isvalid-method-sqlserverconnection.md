---
title: "isValid 方法 (SQLServerConnection) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3b0a8bbf-9369-4456-9ab8-1434ccacdd7e
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ed5a2cb3da3fd5ac503f002f3da3dd4dd90a3e77
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="isvalid-method-sqlserverconnection"></a>isValid 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指出是否此[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件尚未關閉，而且仍然有效。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean isValid(int timeout)  
```  
  
#### <a name="parameters"></a>參數  
 *逾時*  
  
 **Int** ，指定等候驗證連接的秒數。  
  
## <a name="return-value"></a>傳回值  
 **true**連線是否有效。**false**如果連接無效，或逾時到期前，無法判斷連線的有效性。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 IsValid 方法 java.sql.Connection 介面中所指定此 isValid 方法。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

