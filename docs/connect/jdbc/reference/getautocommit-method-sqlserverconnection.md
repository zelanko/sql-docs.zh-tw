---
title: "getAutoCommit 方法 (SQLServerConnection) |Microsoft 文件"
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
- SQLServerConnection.getAutoCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: af1f67f4-f568-4e58-abcc-5c809a89b547
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e2c8ee804ede53953f531fe945da39c7c0667cae
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# getAutoCommit 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取此目前自動認可模式[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件。  
  
## 語法  
  
```  
  
public boolean getAutoCommit()  
```  
  
## 傳回值  
 **true**啟用自動認可模式時，如果**false**如果不是。  
  
## 例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## 備註  
 這個 getAutoCommit 方法是由 java.sql.Connection 介面中的 getAutoCommit 方法指定。  
  
## 另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

