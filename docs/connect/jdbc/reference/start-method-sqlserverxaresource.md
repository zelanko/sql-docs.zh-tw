---
title: start 方法 (SQLServerXAResource) |Microsoft 文件
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
- SQLServerXAResource.start
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 33c90213-92f7-416b-b2fa-67a1afe64e97
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 64b9df7990ca1017b77a6e81d470c5c52984ea97
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32846723"
---
# <a name="start-method-sqlserverxaresource"></a>start 方法 (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表 Xid 物件中指定的交易分支開始工作。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void start(javax.transaction.xa.Xid xid,  
                  int flags)  
```  
  
#### <a name="parameters"></a>參數  
 *xid*  
  
 Xid 物件。  
  
 *flags*  
  
 **Int**值。  
  
## <a name="exceptions"></a>例外狀況  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>備註  
 此開始方法是由 javax.transaction.xa.XAResource 介面中的 start 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成員](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 類別](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
