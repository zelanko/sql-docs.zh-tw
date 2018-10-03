---
title: MembersWithData 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MembersWithData Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MembersWithData
helpviewer_keywords:
- MembersWithData element
ms.assetid: 845087a2-b12d-4344-a8be-85ca61155296
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 17a3fced7327c1fb2211b1c80f774ae859757952
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48089641"
---
# <a name="memberswithdata-element-assl"></a>MembersWithData 元素 (ASSL)
  決定是否要在父屬性中顯示非分葉成員的資料成員。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <MembersWithData>...</MembersWithData>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*NonLeafDataVisible*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 值`MembersWithData`項目僅供父屬性 (亦即的值[使用量](usage-element-dimensionattribute-assl.md)項目`DimensionAttribute`父項目設定為*父*) 來判斷是否若要在父屬性中顯示非分葉成員的資料成員。 如需資料成員的詳細資訊，請參閱 [父子式階層中的屬性](../../multidimensional-models/parent-child-dimension-attributes.md)。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*NonLeafDataHidden*|隱藏非分葉資料。|  
|*NonLeafDataVisible*|顯示非分頁資料。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `MembersWithData` 允許值的列舉是 <xref:Microsoft.AnalysisServices.MembersWithData>。  
  
## <a name="see-also"></a>另請參閱  
 [MembersWithDataCaption 元素&#40;ASSL&#41;](caption-element-assl.md)   
 [DimensionAttribute 資料類型&#40;ASSL&#41;](../data-type/dimensionattribute-data-type-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
