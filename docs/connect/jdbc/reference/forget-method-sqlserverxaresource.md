---
title: forget 方法 (SQLServerXAResource) |Microsoft 文件
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
- SQLServerXAResource.forget
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6d83138d-aa45-4d94-9da6-fdfe7ed28edc
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 13bd0144f69500998735b41b82b4a43f7a5e8e29
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32828133"
---
# <a name="forget-method-sqlserverxaresource"></a>forget 方法 (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  告知資源管理員要忘記以啟發方式完成的交易分支。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void forget(javax.transaction.xa.Xid xid)  
```  
  
#### <a name="parameters"></a>參數  
 *xid*  
  
 Xid 物件。  
  
## <a name="exceptions"></a>例外狀況  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>備註  
 此略過方法是由 javax.transaction.xa.XAResource 介面中略過方法中指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成員](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 類別](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
