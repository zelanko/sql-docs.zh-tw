---
title: getXAResource 方法 (SQLServerXAConnection) |Microsoft 文件
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
- SQLServerXAConnection.getXAResource
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e1d2828f-fd20-44b0-b796-dc70f77c5b03
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc93f1b4ee29d25893c64c7334c8ce6458354624
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
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
  
  
