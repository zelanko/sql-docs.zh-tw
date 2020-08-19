---
description: EndOfRecordset 事件 (ADO)
title: EndOfRecordset 事件 (ADO) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: d96d11333c47aeb190cd2842a5a65a832642eb8b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444030"
---
# <a name="endofrecordset-event-ado"></a>EndOfRecordset 事件 (ADO)
嘗試移到[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)結尾之後的資料列時，就會呼叫**EndOfRecordset**事件。  
  
## <a name="syntax"></a>語法  
  
```  
  
EndOfRecordset fMoreData, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *fMoreData*  
 **VARIANT_BOOL**值，如果設為 VARIANT_TRUE，表示已將更多資料列加入至**記錄集**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 當呼叫 **EndOfRecordset** 時，如果造成事件的作業成功，這個參數會設定為 **adStatusOK** 。 如果此事件無法要求取消導致此事件的作業，則會將它設定為 **adStatusCantDeny** 。  
  
 在 **EndOfRecordset** 傳回之前，請將此參數設定為 **adStatusUnwantedEvent** ，以防止後續的通知。  
  
 *pRecordset*  
 **記錄集**物件。 發生此事件的 **記錄集** 。  
  
## <a name="remarks"></a>備註  
 如果[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)作業失敗，可能會發生**EndOfRecordset**事件。  
  
 當嘗試移動超過 **記錄集** 物件的結尾（也許是因為呼叫 **MoveNext**）時，就會呼叫這個事件處理常式。 不過，在此事件中，您可以從資料庫抓取更多記錄，並將它們附加到 **記錄集**的結尾。 在此情況下，請將 *fMoreData* 設定為 VARIANT_TRUE，然後從 **EndOfRecordset**傳回。 然後再次呼叫 **MoveNext** 以存取新抓取的記錄。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 (VC + +) ](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
