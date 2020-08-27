---
description: FetchComplete 事件 (ADO)
title: FetchComplete 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7ef8df9f6d4ea113d5cca9ad9ffba9c4888776d8
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973349"
---
# <a name="fetchcomplete-event-ado"></a>FetchComplete 事件 (ADO)
當冗長的非同步作業中的所有記錄都被抓取到[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)之後，就會呼叫**FetchComplete**事件。  
  
## <a name="syntax"></a>語法  
  
```  
  
FetchComplete pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *pError*  
 [Error](../../../ado/reference/ado-api/error-object.md)物件。 描述 **adStatus** 的值為 **adStatusErrorsOccurred**時所發生的錯誤;否則未設定。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。 當呼叫這個事件時，如果造成事件的作業成功，這個參數會設定為 **adStatusOK** ，如果作業失敗，則為 **adStatusErrorsOccurred** 。  
  
 在此事件傳回之前，請將此參數設定為 **adStatusUnwantedEvent** ，以防止後續的通知。  
  
 *pRecordset*  
 **記錄集**物件。 已抓取記錄的物件。  
  
## <a name="remarks"></a>備註  
 若要搭配 Microsoft Visual Basic 使用 **FetchComplete** ，需要 Visual Basic 6.0 或更新版本。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 (VC + +) ](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
