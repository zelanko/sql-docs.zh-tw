---
title: FetchComplete 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- FetchComplete event [ADO]
ms.assetid: a28d3858-566c-468d-b070-d1de4339fbea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 09ba18e3680579c7a09e4f51f3bfe3e083dda697
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63140198"
---
# <a name="fetchcomplete-event-ado"></a>FetchComplete 事件 (ADO)
**FetchComplete**冗長的非同步作業中的所有記錄都擷取到之後，會呼叫事件[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
FetchComplete pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *pError*  
 [錯誤](../../../ado/reference/ado-api/error-object.md)物件。 它說明如果發生錯誤的值**adStatus**是**adStatusErrorsOccurred**; 否則它不會設定。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。 呼叫此事件時，此參數設為**adStatusOK**造成事件的作業已順利完成，還是要**adStatusErrorsOccurred**如果作業失敗。  
  
 這個事件會傳回之前，請將此參數設定為**adStatusUnwantedEvent**以避免後續的通知。  
  
 *pRecordset*  
 A**資料錄集**物件。 物件，為其擷取記錄。  
  
## <a name="remarks"></a>備註  
 若要使用**FetchComplete**使用 Microsoft Visual Basic 中，Visual Basic 6.0 或更新版本是必要。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
