---
title: EndOfRecordset 事件 (ADO) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EndOfRecordset
- Recordset::EndOfRecordset
helpviewer_keywords:
- EndOfRecordset event [ADO]
ms.assetid: 475de5e2-f634-4954-9edf-0027a6ba38d6
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 62f0b1837765101ca5aa6c45f51e5bd9a1506913
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="endofrecordset-event-ado"></a>EndOfRecordset 事件 (ADO)
**EndOfRecordset**嘗試將移到超過結尾的資料列時，會呼叫事件[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
EndOfRecordset fMoreData, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *fMoreData*  
 A **VARIANT_BOOL**值，如果設定為 VARIANT_TRUE，表示已加入多個資料列**資料錄集**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 當**EndOfRecordset**是呼叫，此參數設為**adStatusOK**如果造成事件的作業是否成功。 設定為**adStatusCantDeny**如果此事件不可以要求取消作業造成此事件。  
  
 之前**EndOfRecordset**傳回時，會將此參數設定為**adStatusUnwantedEvent**以避免後續的通知。  
  
 *pRecordset*  
 A**資料錄集**物件。 **資料錄集**如發生此事件。  
  
## <a name="remarks"></a>備註  
 **EndOfRecordset**如果，可能會發生事件[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)作業將會失敗。  
  
 嘗試移動超過的結尾時，這個事件處理常式的呼叫**資料錄集**物件，可能是因為呼叫**MoveNext**。 不過，在此事件，無法從資料庫擷取更多記錄，然後將它們附加至結尾**資料錄集**。 在此情況下，設定*fMoreData*為 VARIANT_TRUE，並從的傳回**EndOfRecordset**。 然後呼叫**MoveNext**以存取新擷取的記錄。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
