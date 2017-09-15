---
title: "getXAResource 方法 (SQLServerXAConnection) |Microsoft 文件"
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
- SQLServerXAConnection.getXAResource
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e1d2828f-fd20-44b0-b796-dc70f77c5b03
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 78999ece74ad80f7d4ce107484d225cc1ab6f4f6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getxaresource-method-sqlserverxaconnection"></a>getXAResource 方法 (SQLServerXAConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)物件的交易管理員將會用來管理此[SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)物件的參與分散式交易中。  
  
## <a name="syntax"></a>語法  
  
```  
  
public javax.transaction.xa.XAResource getXAResource()  
```  
  
## <a name="return-value"></a>傳回值  
 XAResource 物件。  
  
## <a name="exceptions"></a>例外狀況  
 java.sql.SQLException  
  
## <a name="remarks"></a>備註  
 這個 getXAResource 方法是由 javax.sql.XAConnection 介面中 getXAResource 方法來指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXAConnection 方法](../../../connect/jdbc/reference/sqlserverxaconnection-methods.md)   
 [SQLServerXAConnection 成員](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [SQLServerXAConnection 類別](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)  
  
  
