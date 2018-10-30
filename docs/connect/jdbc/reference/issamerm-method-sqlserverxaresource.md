---
title: isSameRM 方法 (SQLServerXAResource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.isSameRM
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bfa24c46-b7cf-470a-afa1-52301847a448
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0cbe71d1ff4d19da3baba87210a1444e83d4f98e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633772"
---
# <a name="issamerm-method-sqlserverxaresource"></a>isSameRM 方法 (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  判斷由目標物件表示之資源管理員執行個體是否與由所指定 XAResource 物件表示的資源管理員執行個體相同。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean isSameRM(javax.transaction.xa.XAResource xares)  
```  
  
#### <a name="parameters"></a>參數  
 *xares*  
  
 XAResource 物件。  
  
## <a name="return-value"></a>傳回值  
 如果執行個體相同，則為 **true**。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 這個 commit 方法是由 javax.transaction.xa.XAResource 介面中的 commit 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成員](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 類別](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
