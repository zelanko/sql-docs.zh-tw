---
title: "end 方法 (SQLServerXAResource) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerXAResource.end
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: e6418b27-793b-4b36-8dfb-756aec7bcbba
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2228ac4825056e4c9733b479f4daf02ec484df10
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="end-method-sqlserverxaresource"></a>end 方法 (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  結束代表交易分支執行的工作。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void end(javax.transaction.xa.Xid xid,  
                int flags)  
```  
  
#### <a name="parameters"></a>參數  
 *xid*  
  
 Xid 物件。  
  
 *旗標*  
  
 **Int**值。  
  
## <a name="exceptions"></a>例外狀況  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>備註  
 這個一般方法是由 javax.transaction.xa.XAResource 介面中的結束方法指定。  
  
## <a name="see-also"></a>請參閱＜  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成員](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 類別](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
