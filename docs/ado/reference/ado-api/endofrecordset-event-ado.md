---
title: EndOfRecordset 事件（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EndOfRecordset
- Recordset::EndOfRecordset
helpviewer_keywords:
- EndOfRecordset event [ADO]
ms.assetid: 475de5e2-f634-4954-9edf-0027a6ba38d6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a83f101d46a94a4ea43a85424677fc1c8da08be
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918944"
---
# <a name="endofrecordset-event-ado"></a>EndOfRecordset 事件 (ADO)
當嘗試移到超過[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)結尾的資料列時，會呼叫**EndOfRecordset**事件。  
  
## <a name="syntax"></a>語法  
  
```  
  
EndOfRecordset fMoreData, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *fMoreData*  
 **VARIANT_BOOL**值，如果設定為 [VARIANT_TRUE]，表示已將更多的資料列加入至**記錄集**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 當呼叫**EndOfRecordset**時，如果造成事件的作業成功，此參數會設定為**adStatusOK** 。 如果這個事件無法要求取消造成此事件的作業，則會設定為**adStatusCantDeny** 。  
  
 在**EndOfRecordset**傳回之前，請將此參數設定為**adStatusUnwantedEvent** ，以防止後續的通知。  
  
 *pRecordset*  
 **記錄集**物件。 發生此事件的**記錄集**。  
  
## <a name="remarks"></a>備註  
 如果[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)作業失敗，可能會發生**EndOfRecordset**事件。  
  
 當嘗試移動超過**記錄集**物件的結尾時（或許是呼叫**MoveNext**的結果），會呼叫此事件處理常式。 不過，在此事件中，您可以從資料庫中抓取更多記錄，並將它們附加到**記錄集**的結尾。 在此情況下，請將*fMoreData*設定為 VARIANT_TRUE，並從**EndOfRecordset**傳回。 然後再次呼叫**MoveNext**來存取新抓取的記錄。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
