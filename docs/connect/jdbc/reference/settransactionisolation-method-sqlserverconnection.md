---
title: "setTransactionIsolation 方法 (SQLServerConnection) |Microsoft 文件"
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
- SQLServerConnection.setTransactionIsolation
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6a8fa4d3-5237-40f8-8a02-b40a3d7a1131
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b91e33388706cabe7436259193f9b2c0bb446b25
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="settransactionisolation-method-sqlserverconnection"></a>setTransactionIsolation 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  嘗試將交易隔離等級變更這個[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)一個指定的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setTransactionIsolation(int level)  
```  
  
#### <a name="parameters"></a>參數  
 *層級*  
  
 **Int**包含下列隔離等級的其中一個值：  
  
 TRANSACTION_READ_UNCOMMITTED  
  
 TRANSACTION_READ_COMMITTED  
  
 TRANSACTION_REPEATABLE_READ  
  
 TRANSACTION_SERIALIZABLE  
  
 TRANSACTION_SNAPSHOT = 0x1000  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setTransactionIsolation 方法是由 java.sql.Connection 介面中的 setTransactionIsolation 方法指定。  
  
 如果在交易中間呼叫這個方法，便不會認可交易。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

