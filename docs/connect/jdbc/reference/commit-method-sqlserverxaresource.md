---
title: commit 方法 (SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.commit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1d0f8612-fb4a-4eca-bc37-8342e1419fd4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85bc4f123dd29025e906d57d64f21746df5f2e07
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67955550"
---
# <a name="commit-method-sqlserverxaresource"></a>commit 方法 (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  認可指定 XID 物件所指定的全域交易。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void commit(javax.transaction.xa.Xid xid,  
                   boolean onePhase)  
```  
  
#### <a name="parameters"></a>參數  
 *xid*  
  
 Xid 物件。  
  
 *onePhase*  
  
 **boolean** 值。  
  
## <a name="exceptions"></a>例外狀況  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>備註  
 這個 commit 方法是由 javax.transaction.xa.XAResource 介面中的 commit 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成員](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 類別](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
