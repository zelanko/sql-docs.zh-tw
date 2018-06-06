---
title: BeginTrans，CommitTrans，RollbackTrans 事件 (ADO) |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CommitTransComplete
- Connection::BeginTransComplete
- Connection::RollbackTransComplete
- Connection::CommitTransComplete
- RollbackTransComplete
- BeginTransComplete
helpviewer_keywords:
- CommitTransComplete event [ADO]
- RollbackTransComplete event [ADO]
- BeginTransComplete event [ADO]
ms.assetid: ec4e4b38-e9c6-4757-b2ef-4e468ae5f1d8
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f9754baa574a21916e981c91aad56385adfb16e0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado"></a>BeginTransComplete、 CommitTransComplete 和 RollbackTransComplete 事件 (ADO)
這些事件將在上呼叫相關聯的作業之後[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件完成執行。  
  
-   **BeginTransComplete**之後呼叫[BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)作業。  
  
-   **CommitTransComplete**之後呼叫[CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)作業。  
  
-   **RollbackTransComplete**之後呼叫[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)作業。  
  
## <a name="syntax"></a>語法  
  
```  
  
BeginTransComplete TransactionLevel, pError, adStatus, pConnection  
CommitTransComplete pError, adStatus, pConnection  
RollbackTransComplete pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>參數  
 *TransactionLevel*  
 A**長**值，包含新的交易等級的**BeginTrans**導致此事件。  
  
 *pError*  
 [錯誤](../../../ado/reference/ado-api/error-object.md)物件。 它描述 EventStatusEnum 值時所發生的錯誤**adStatusErrorsOccurred**; 否則為未設定。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。 當呼叫這些事件時，這個參數會設定為**adStatusOK**如果造成事件的作業成功，或**adStatusErrorsOccurred**作業失敗。  
  
 這些事件可以將這個參數設定以防止後續通知**adStatusUnwantedEvent**事件會傳回之前。  
  
 *pConnection*  
 **連接**發生此事件的物件。  
  
## <a name="remarks"></a>備註  
 在 Visual c + + 中，多個**連線**可以共用相同的事件處理方法。 此方法會使用傳回**連接**來判斷哪些物件造成事件的物件。  
  
 如果[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)屬性設定為**adXactCommitRetaining**或**adXactAbortRetaining**，新的交易開始之後認可或回復交易。 使用**BeginTransComplete**略過所有事件，但第一個交易的開始事件。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [BeginTrans、 CommitTrans 和 RollbackTrans 方法範例 (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [BeginTrans、CommitTrans 和 RollbackTrans 方法 (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)
