---
title: "setAutoCommit 方法 (SQLServerConnection) |Microsoft 文件"
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
- SQLServerConnection.setAutoCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: db1e22d2-e53f-474e-8c99-cb1fff7f491a
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f1549693ac6b4e558c2fc86b29dc6aaa6122c235
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# setAutoCommit 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定這個自動認可模式[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)處於指定狀態的物件。  
  
## 語法  
  
```  
  
public void setAutoCommit(boolean value)  
```  
  
#### 參數  
 *value*  
  
 **true**若要啟用自動認可模式進行連接， **false**停用此功能。  
  
## 例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## 備註  
 這個 setAutoCommit 方法是由 java.sql.Connection 介面中的 setAutoCommit 方法指定。  
  
 如果連接處於自動認可模式，則它的所有 SQL 陳述式都會當做個別交易來執行及認可。 否則，其 SQL 陳述式的分組呼叫結束的交易[認可](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md)方法或[復原](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)方法。 根據預設，新的連接會處於自動認可模式。  
  
 當陳述式完成或下一次執行時 (以先發生者為準)，就會進行認可。 在傳回的陳述式的情況下[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件，此陳述式完成時擷取結果集的最後一個資料列，或已關閉結果集。 在進階案例中，除了輸出參數值以外，單一陳述式也可能會傳回多個結果。 在這些案例中，當擷取了所有結果和輸出參數值時，就會發生認可。  
  
 當自動認可模式是**false**，JDBC 驅動程式會以隱含方式開始新的交易，每次認可之後。  
  
> [!NOTE]  
>  如果在交易期間呼叫這個方法，便會認可交易。  
  
## 另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

