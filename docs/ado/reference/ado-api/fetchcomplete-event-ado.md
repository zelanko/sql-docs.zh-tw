---
title: "FetchComplete 事件 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset::ExecuteComplete
- ExecuteComplete
helpviewer_keywords: FetchComplete event [ADO]
ms.assetid: a28d3858-566c-468d-b070-d1de4339fbea
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1754cb26eb381e056ba818958593cda40722c7c8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="fetchcomplete-event-ado"></a>FetchComplete 事件 (ADO)
**FetchComplete**冗長的非同步作業中的所有記錄到都擷取之後，呼叫事件[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
FetchComplete pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *pError*  
 [錯誤](../../../ado/reference/ado-api/error-object.md)物件。 它描述如果發生之錯誤的值**adStatus**是**adStatusErrorsOccurred**; 否則它不會設定。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。 當呼叫這個事件時，這個參數會設定為**adStatusOK**如果造成事件的作業成功，或**adStatusErrorsOccurred**作業失敗。  
  
 這個事件會傳回之前，請將此參數設定為**adStatusUnwantedEvent**以避免後續的通知。  
  
 *pRecordset*  
 A**資料錄集**物件。 記錄已為其擷取的物件。  
  
## <a name="remarks"></a>備註  
 若要使用**FetchComplete**搭配 Microsoft Visual Basic 中，Visual Basic 6.0 或更新版本為必要。  
  
## <a name="see-also"></a>請參閱＜  
 [ADO 事件模型範例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
