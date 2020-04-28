---
title: FetchComplete 事件（ADO） |Microsoft Docs
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
ms.openlocfilehash: f3e5f5ae1c886f8d08d522fac19cee563efbb86c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932838"
---
# <a name="fetchcomplete-event-ado"></a>FetchComplete 事件 (ADO)
當冗長非同步作業中的所有記錄都已經抓取到[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)之後，就會呼叫**FetchComplete**事件。  
  
## <a name="syntax"></a>語法  
  
```  
  
FetchComplete pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *pError*  
 [錯誤](../../../ado/reference/ado-api/error-object.md)物件。 它會描述**adStatus**的值為**adStatusErrorsOccurred**時所發生的錯誤。否則不會設定。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。 呼叫這個事件時，如果造成事件的作業成功，此參數會設定為**adStatusOK** ，如果作業失敗，則為**adStatusErrorsOccurred** 。  
  
 在此事件傳回之前，請將此參數設定為**adStatusUnwantedEvent** ，以防止後續的通知。  
  
 *pRecordset*  
 **記錄集**物件。 抓取記錄的物件。  
  
## <a name="remarks"></a>備註  
 若要搭配使用**FetchComplete**與 Microsoft Visual Basic，需要 Visual Basic 6.0 或更新版本。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
