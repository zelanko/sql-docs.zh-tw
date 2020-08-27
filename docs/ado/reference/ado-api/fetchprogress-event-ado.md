---
description: FetchProgress 事件 (ADO)
title: FetchProgress 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: b84b963f42c83191c613dbb4849288fc862df474
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973329"
---
# <a name="fetchprogress-event-ado"></a>FetchProgress 事件 (ADO)
**FetchProgress**事件會在冗長的非同步作業期間定期呼叫，以報告目前已抓取到[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)的資料列數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
FetchProgress Progress, MaxProgress, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *Progress*  
 **長**數值，指出提取作業目前已抓取的記錄數目。  
  
 *MaxProgress*  
 **長**數值，指出預期要抓取的記錄數目上限。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 *pRecordset*  
 記錄所要抓取之物件的 **記錄集** 物件。  
  
## <a name="remarks"></a>備註  
 使用 **FetchProgress** 搭配子 **記錄集**時，請注意 *進度* 和 *MaxProgress* 參數值是衍生自基礎資料 [指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) 資料列集。 傳回的值代表基礎資料列集中的記錄總數，而不只是目前章節中的記錄數目。  
  
> [!NOTE]
>  若要搭配 Microsoft Visual Basic 使用 **FetchProgress** ，需要 Visual Basic 6.0 或更新版本。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 (VC + +) ](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
