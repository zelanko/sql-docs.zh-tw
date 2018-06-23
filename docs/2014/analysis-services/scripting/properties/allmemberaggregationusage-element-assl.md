---
title: AllMemberAggregationUsage 元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- AllMemberAggregationUsage Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AllMemberAggregationUsage
helpviewer_keywords:
- AllMemberAggregationUsage element
ms.assetid: 264fe9d8-8e9a-4642-8cee-7c2804126926
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 1da20a067a1f293bafbca858623ab477aacac6b2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131798"
---
# <a name="allmemberaggregationusage-element-assl"></a>AllMemberAggregationUsage 元素 (ASSL)
  控制項如何在彙總設計師[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]設計彙總。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CubeDimension>  
   ...  
   <AllMemberAggregationUsage>...</AllMemberAggregationUsage>  
   ...  
</CubeDimension>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*預設值*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CubeDimension](../data-type/dimension-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*Full*|Cube 的每個彙總必須包含 (全部) 成員。|  
|*無*|Cube 的彙總都不應該包含 All 成員。|  
|*不受限制*|彙總設計師沒有任何限制。|  
|*預設值*|與相同*不受限制*。|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目`AllMemberAggregationUsage`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.CubeDimension>。  
  
## <a name="see-also"></a>另請參閱  
 [Cube 元素&#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [維度元素&#40;ASSL&#41;](../objects/dimension-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  