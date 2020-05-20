---
title: FetchProgress 事件（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FetchProgress
- Recordset::FetchProgress
helpviewer_keywords:
- FetchProgress event [ADO]
ms.assetid: 301716fd-81fc-40eb-8a04-221ef7ab410e
author: rothja
ms.author: jroth
ms.openlocfilehash: c5e75dd96a77261bfee44da0db9025fb02af6871
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82757114"
---
# <a name="fetchprogress-event-ado"></a>FetchProgress 事件 (ADO)
**FetchProgress**事件是在冗長的非同步作業期間定期呼叫，以報告目前已經抓取到[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)的多個資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
FetchProgress Progress, MaxProgress, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *進度*  
 **長**數值，指出提取作業目前已取得的記錄數目。  
  
 *MaxProgress*  
 **長**數值，指出預期要抓取的記錄數目上限。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 *pRecordset*  
 做為正在抓取記錄之物件的**記錄集**物件。  
  
## <a name="remarks"></a>備註  
 使用**FetchProgress**搭配子**記錄集**時，請注意，*進度*和*MaxProgress*參數值是衍生自基礎資料[指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)資料列集。 傳回的值代表基礎資料列集內的記錄總數，而不只是目前章節中的記錄數目。  
  
> [!NOTE]
>  若要搭配使用**FetchProgress**與 Microsoft Visual Basic，需要 Visual Basic 6.0 或更新版本。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
