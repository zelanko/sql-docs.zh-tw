---
title: FetchProgress 事件 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab93d8117a5fb3d2bbc95ea33bbacdc7fba3f151
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932823"
---
# <a name="fetchprogress-event-ado"></a>FetchProgress 事件 (ADO)
**FetchProgress**冗長的非同步作業，以報告多個資料列數目目前已擷取到期間定期呼叫事件[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
FetchProgress Progress, MaxProgress, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *進度*  
 A**長**值，指出目前已經提取作業擷取的記錄數目。  
  
 *MaxProgress*  
 A**長**預期要擷取的值，指出最大記錄數目。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 *pRecordset*  
 A**資料錄集**是為其擷取記錄的物件的物件。  
  
## <a name="remarks"></a>備註  
 使用時**FetchProgress**含子系**資料錄集**，注意，*進度*並*MaxProgress*衍生參數值從基礎[資料指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)資料列集。 傳回的值代表在基礎資料列集，不只是在目前的章節中的記錄數目的記錄總數。  
  
> [!NOTE]
>  若要使用**FetchProgress**使用 Microsoft Visual Basic 中，Visual Basic 6.0 或更新版本是必要。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
