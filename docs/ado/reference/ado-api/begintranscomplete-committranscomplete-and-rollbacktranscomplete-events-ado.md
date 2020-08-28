---
description: 'BeginTransComplete、CommitTransComplete 和 RollbackTransComplete 事件 (ADO) '
title: BeginTrans、CommitTrans、RollbackTrans 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 91f5d573d62ef5000cdd6ed85a52866a0ee7f544
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975869"
---
# <a name="begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado"></a>BeginTransComplete、CommitTransComplete 和 RollbackTransComplete 事件 (ADO) 
在 [連接](./connection-object-ado.md) 物件上的相關聯作業完成執行之後，將會呼叫這些事件。  
  
-   在[BeginTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md)作業之後，會呼叫**BeginTransComplete** 。  
  
-   在[CommitTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md)作業之後，會呼叫**CommitTransComplete** 。  
  
-   在[RollbackTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md)作業之後，會呼叫**RollbackTransComplete** 。  
  
## <a name="syntax"></a>語法  
  
```  
  
BeginTransComplete TransactionLevel, pError, adStatus, pConnection  
CommitTransComplete pError, adStatus, pConnection  
RollbackTransComplete pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>參數  
 *TransactionLevel*  
 **長**值，包含造成這個事件的**BeginTrans**的新交易層級。  
  
 *pError*  
 [Error](./error-object.md)物件。 描述 EventStatusEnum 的值為 **adStatusErrorsOccurred**時所發生的錯誤;否則未設定。  
  
 *adStatus*  
 [EventStatusEnum](./eventstatusenum.md)狀態值。 當呼叫這些事件中的任何一個時，如果造成事件的作業成功，則此參數會設定為 **adStatusOK** ，或在作業失敗時 **adStatusErrorsOccurred** 。  
  
 這些事件可在事件傳回之前將此參數設定為 **adStatusUnwantedEvent** ，以防止後續的通知。  
  
 *pConnection*  
 發生此事件的 **連接** 物件。  
  
## <a name="remarks"></a>備註  
 在 Visual C++ 中，多個 **連接** 可以共用相同的事件處理方法。 方法會使用傳回的 **連接** 物件，判斷哪個物件造成事件。  
  
 如果 [ [屬性](./attributes-property-ado.md) ] 屬性設定為 [ **adXactCommitRetaining** ] 或 [ **adXactAbortRetaining**]，則會在認可或回復交易後啟動新的交易。 使用 **BeginTransComplete** 事件，以忽略第一個交易開始事件以外的所有專案。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 (VC + +) ](./ado-events-model-example-vc.md)   
 [BeginTrans、CommitTrans 和 RollbackTrans 方法範例 (VB) ](./begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [ADO 事件處理常式摘要](../../guide/data/ado-event-handler-summary.md)   
 [BeginTrans、CommitTrans 和 RollbackTrans 方法 (ADO)](./begintrans-committrans-and-rollbacktrans-methods-ado.md)