---
title: recover 方法 (SQLServerXAResource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.recover
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 840ecfcf-0dd3-4b7b-976f-dc9a96cd1464
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 92d7b0db997a6b77b43efb6d8104f629bb5507e3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67976018"
---
# <a name="recover-method-sqlserverxaresource"></a>recover 方法 (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  從資源管理員取得備妥的交易分支清單。  
  
## <a name="syntax"></a>語法  
  
```  
  
public javax.transaction.xa.Xid[] recover(int flags)  
```  
  
#### <a name="parameters"></a>參數  
 *flags*  
  
 **Int**值, 可以採用下列其中一個值: XARESOURCE. TMSTARTRSCAN 或 XARESOURCE. TMENDRSCAN 或 XAResource. TMNOFLAGS 或 XARESOURCE. TMSTARTTRSCAN |XAResource. TMENDRSCAN。  
  
## <a name="return-value"></a>傳回值  
 Xid 物件。  
  
## <a name="exceptions"></a>例外狀況  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 這個 recover 方法是由 javax.transaction.xa.XAResource 介面中的 recover 方法指定。  
  
 如果參數**旗**標不是 XARESOURCE. TMSTARTRSCAN 或 XARESOURCE. TMSTARTRSCAN |XAResource. TMENDRSCAN, 復原掃描必須正在進行中。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成員](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 類別](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
