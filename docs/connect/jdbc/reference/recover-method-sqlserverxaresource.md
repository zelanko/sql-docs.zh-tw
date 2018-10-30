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
manager: craigg
ms.openlocfilehash: 8ec96cd3f56b1710268ae951e39e98866fe1bd54
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47826816"
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
  
 **Int**值可接受下列值之一： XAResource.TMSTARTRSCAN 或 XAResource.TMENDRSCAN 或 XAResource.TMNOFLAGS XAResource.TMSTARTTRSCAN |XAResource.TMENDRSCAN。  
  
## <a name="return-value"></a>傳回值  
 Xid 物件。  
  
## <a name="exceptions"></a>例外狀況  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 這個 recover 方法是由 javax.transaction.xa.XAResource 介面中的 recover 方法指定。  
  
 如果參數**旗標**XAResource.TMSTARTRSCAN 或 XAResource.TMSTARTRSCAN |XAResource.TMENDRSCAN，則表示復原掃描必須正在進行中。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成員](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 類別](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
