---
title: "FetchProgress 事件 (ADO) |Microsoft 文件"
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
- FetchProgress
- Recordset::FetchProgress
helpviewer_keywords: FetchProgress event [ADO]
ms.assetid: 301716fd-81fc-40eb-8a04-221ef7ab410e
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 990e5bbe3a203cd48c34c6153a9ee0ca8e678758
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="fetchprogress-event-ado"></a>FetchProgress 事件 (ADO)
**FetchProgress**回報到目前已擷取多個資料列數目的長時間非同步作業期間定期呼叫事件[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
FetchProgress Progress, MaxProgress, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *進度*  
 A**長**值，指出目前已經擷取擷取作業的記錄數目。  
  
 *MaxProgress*  
 A**長**預期要擷取的值，指出最大記錄數目。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 *pRecordset*  
 A**資料錄集**擷取記錄物件的物件。  
  
## <a name="remarks"></a>備註  
 使用時**FetchProgress**含有子系**資料錄集**，請注意，*進度*和*MaxProgress*衍生參數值從基礎[指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)資料列集。 傳回的值代表在基礎資料列集，不只是在目前的章節中的記錄數目的記錄總數。  
  
> [!NOTE]
>  若要使用**FetchProgress**搭配 Microsoft Visual Basic 中，Visual Basic 6.0 或更新版本為必要。  
  
## <a name="see-also"></a>請參閱＜  
 [ADO 事件模型範例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
