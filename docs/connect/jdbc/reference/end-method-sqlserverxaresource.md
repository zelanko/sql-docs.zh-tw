---
title: end 方法 (SQLServerXAResource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.end
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e6418b27-793b-4b36-8dfb-756aec7bcbba
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8aa3da36a6bffbcaf223ea72d4adf5f9e541d90c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67955049"
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
  
 *flags*  
  
 **Int**值。  
  
## <a name="exceptions"></a>例外狀況  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 這個 end 方法是由 javax.transaction.xa.XAResource 介面中的 end 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成員](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 類別](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
