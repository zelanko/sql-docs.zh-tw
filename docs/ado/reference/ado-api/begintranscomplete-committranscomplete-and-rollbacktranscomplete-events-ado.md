---
title: BeginTrans、 CommitTrans RollbackTrans 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8239a5f9069212b9413216bc3535e3c90e2d5316
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66696361"
---
# <a name="begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado"></a>BeginTransComplete、 CommitTransComplete 和 RollbackTransComplete 事件 (ADO)
這些事件將在上呼叫相關聯的作業之後[連線](../../../ado/reference/ado-api/connection-object-ado.md)物件完成執行。  
  
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
 A**長**值，其中包含新的交易等級的**BeginTrans**導致此事件。  
  
 *pError*  
 [錯誤](../../../ado/reference/ado-api/error-object.md)物件。 它描述 EventStatusEnum 的值時，所發生的錯誤**adStatusErrorsOccurred**; 否則它不會設定。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。 當呼叫其中任何一個事件時，此參數設為**adStatusOK**造成事件的作業已順利完成，還是要**adStatusErrorsOccurred**如果作業失敗。  
  
 這些事件可透過此參數設定為防止後續通知**adStatusUnwantedEvent**事件會傳回之前。  
  
 *pConnection*  
 **連線**物件發生此事件。  
  
## <a name="remarks"></a>備註  
 在視覺效果C++、 多個**連線**可以共用相同的事件處理方法。 此方法會使用傳回**連線**來判斷哪些物件造成事件的物件。  
  
 如果[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)屬性設定為**adXactCommitRetaining**或是**adXactAbortRetaining**，新的交易開始之後認可或回復交易。 使用**BeginTransComplete**要略過所有的事件，但第一個交易的開始事件。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [BeginTrans、 CommitTrans 和 RollbackTrans 方法範例 (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [BeginTrans、CommitTrans 和 RollbackTrans 方法 (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)
