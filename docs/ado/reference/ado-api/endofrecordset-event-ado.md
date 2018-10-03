---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1697197bf9450a6487e70b0257160221e59359f8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47822526"
---
# <a name="endofrecordset-event-ado"></a>EndOfRecordset 事件 (ADO)
**EndOfRecordset**嘗試移動超過結尾的資料列時，會呼叫事件[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
EndOfRecordset fMoreData, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *fMoreData*  
 A **VARIANT_BOOL**值，如果設定為 VARIANT_TRUE，表示已加入多個資料列**資料錄集**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 當**EndOfRecordset**是呼叫，此參數設為**adStatusOK**如果造成事件的作業已順利完成。 它會設定為**adStatusCantDeny**如果此事件無法要求取消作業造成此事件。  
  
 再**EndOfRecordset**傳回，這個參數設定為**adStatusUnwantedEvent**以避免後續的通知。  
  
 *pRecordset*  
 A**資料錄集**物件。 **資料錄集**如發生此事件。  
  
## <a name="remarks"></a>備註  
 **EndOfRecordset**可能會發生事件，如果[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)作業將會失敗。  
  
 嘗試移動超過的結尾時，呼叫此事件處理常式**Recordset**物件，可能是因為呼叫**MoveNext**。 不過，在此情況下，您可以從資料庫擷取較多的記錄並將它們附加至結尾**資料錄集**。 在此情況下，設定*fMoreData* VARIANT_TRUE 時，並傳回**EndOfRecordset**。 然後呼叫**MoveNext**以存取新擷取的記錄。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
