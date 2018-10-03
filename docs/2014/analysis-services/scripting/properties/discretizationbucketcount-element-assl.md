---
title: DiscretizationBucketCount 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DiscretizationBucketCount Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DiscretizationBucketCount
helpviewer_keywords:
- DiscretizationBucketCount element
ms.assetid: 551a73ae-59e1-4079-a2d9-988df96b5e07
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5fea5841750555185cbeb40f99b9dc5d312be490
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48202158"
---
# <a name="discretizationbucketcount-element-assl"></a>DiscretizationBucketCount 元素 (ASSL)
  包含要進行離散化的值區數目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DimensionAttribute> <!-- or ScalarMiningStructureColumn -->  
   ...  
   <DiscretizationBucketCount>...</DiscretizationBucketCount>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|Integer|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)， [ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 `DiscretizationBucketCount` 元素的值會決定當 `DimensionAttribute` 或 `ScalarMiningStructureColumn` 的值離散化或組織成特定群組集合時，要建立多少群組或「值區」。 如果未指定的項目，則元素的值，指定為零[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]建立適當數目的群組，根據離散化方法。 如需有關離散化方法的詳細資訊，請參閱[離散化方法&#40;資料採礦&#41;](../../data-mining/discretization-methods-data-mining.md)。  
  
 對應至父系的元素`DiscretizationBucketCount`在 「 分析管理物件 (AMO) 物件模型所<xref:Microsoft.AnalysisServices.DimensionAttribute>和<xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>另請參閱  
 [DiscretizationMethod 元素&#40;ASSL&#41;](discretizationmethod-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
