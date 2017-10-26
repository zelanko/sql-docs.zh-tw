---
title: "commit 方法 (SQLServerConnection) |Microsoft 文件"
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
- SQLServerConnection.commit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c7346165-51bf-4844-b64c-29833c147236
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bf9cc3b66c0d8b5e9eca015dd5e62fdd7541a9c2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="commit-method-sqlserverconnection"></a>commit 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使從上一次認可或復原後成為永久狀態的所有變更，並且釋放目前由這個保留的任何資料庫鎖定[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void commit()  
```  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 commit 方法是由 java.sql.Connection 介面中的認可方法指定。  
  
 只有當已經停用自動認可模式時，才應該使用這個方法。  
  
 請注意，如果用戶端開始手動交易，然後 SQL Server 基於某個原因回復此手動交易，這個方法將會失敗並擲回例外狀況。 例如，如果用戶端呼叫預存程序會明確呼叫 ROLLBACK TRANSACTION，會擲回例外狀況，然後用戶端呼叫 commit 方法。 此外，如果 SQL Server 就會引發錯誤回復足夠的嚴重性 （16 或更高） 的用戶端起始的手動交易。commit 方法的後續呼叫會擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

