---
title: ModelingFlag 元素 (ASSL) |Microsoft Docs
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
- ModelingFlag Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ModelingFlag
helpviewer_keywords:
- ModelingFlag element
ms.assetid: c9af1b9a-506f-4cc1-acd7-e57698cb672c
caps.latest.revision: 31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 611a93a27e5f668c9b367eb35d5df9eb454743b8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37275434"
---
# <a name="modelingflag-element-assl"></a>ModelingFlag 元素 (ASSL)
  包含採礦結構或採礦模型中某個資料行的模型旗標。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ModelingFlags>  
   <ModelingFlag xsi:type="MiningModelingFlag">...</ModelingFlag>  
</ModelingFlags>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|[MiningModelingFlag](../data-type/miningmodelingflag-data-type-assl.md)|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ModelingFlags](../collections/modelingflags-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 在「分析管理物件」(AMO) 物件模型中緊密相關的元素是 <xref:Microsoft.AnalysisServices.MiningModelingFlags>。  
  
## <a name="see-also"></a>另請參閱  
 [MiningModel 元素&#40;ASSL&#41;](miningmodel-element-assl.md)   
 [MiningStructure 元素&#40;ASSL&#41;](miningstructure-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
