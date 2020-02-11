---
title: BeginTrans、CommitTrans、RollbackTrans 事件（ADO） |Microsoft Docs
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
ms.openlocfilehash: 750e89e97eb916c7db23e71475b753a57a4d90e9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67920441"
---
# <a name="begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado"></a>BeginTransComplete、CommitTransComplete 和 RollbackTransComplete 事件（ADO）
當[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件上的相關聯作業完成執行之後，就會呼叫這些事件。  
  
-   **BeginTransComplete**是在[BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)作業之後呼叫。  
  
-   **CommitTransComplete**是在[CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)作業之後呼叫。  
  
-   **RollbackTransComplete**是在[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)作業之後呼叫。  
  
## <a name="syntax"></a>語法  
  
```  
  
BeginTransComplete TransactionLevel, pError, adStatus, pConnection  
CommitTransComplete pError, adStatus, pConnection  
RollbackTransComplete pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>參數  
 *TransactionLevel*  
 **長**數值，其中包含造成此事件之**BeginTrans**的新交易層級。  
  
 *pError*  
 [錯誤](../../../ado/reference/ado-api/error-object.md)物件。 它會描述 EventStatusEnum 的值為**adStatusErrorsOccurred**時所發生的錯誤。否則不會設定。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。 呼叫這些事件中的任何一個時，如果造成事件的作業成功，此參數會設定為**adStatusOK** ，如果作業失敗，則會**adStatusErrorsOccurred** 。  
  
 這些事件可以在事件傳回之前將此參數設定為**adStatusUnwantedEvent** ，以防止後續的通知。  
  
 *pConnection*  
 發生此事件的**連接**物件。  
  
## <a name="remarks"></a>備註  
 在 Visual C++ 中，多個**連接**可以共用相同的事件處理方法。 方法會使用傳回的**連接**物件來判斷造成事件的物件。  
  
 如果 [[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)] 屬性設定為**adXactCommitRetaining**或**adXactAbortRetaining**，新的交易就會在認可或回復交易之後啟動。 使用**BeginTransComplete**事件來忽略第一個交易啟動事件以外的所有專案。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [BeginTrans、CommitTrans 和 RollbackTrans 方法範例（VB）](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [BeginTrans、CommitTrans 和 RollbackTrans 方法 (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)
