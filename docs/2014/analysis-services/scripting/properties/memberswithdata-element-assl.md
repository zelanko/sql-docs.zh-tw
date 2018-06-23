---
title: MembersWithData 元素 (ASSL) |Microsoft 文件
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
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5c0311a774b225234aeb63d4d67680e12b693b0d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136494"
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
|子元素|無|  
  
## <a name="remarks"></a>備註  
 值`MembersWithData`項目僅供父屬性 (換言之，值的[使用量](usage-element-dimensionattribute-assl.md)元素`DimensionAttribute`父項目設定為*父*) 來判斷是否若要在父屬性中顯示非分葉成員的資料成員。 如需資料成員的詳細資訊，請參閱 [父子式階層中的屬性](../../multidimensional-models/parent-child-dimension-attributes.md)。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*NonLeafDataHidden*|隱藏非分葉資料。|  
|*NonLeafDataVisible*|顯示非分頁資料。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `MembersWithData` 允許值的列舉是 <xref:Microsoft.AnalysisServices.MembersWithData>。  
  
## <a name="see-also"></a>另請參閱  
 [MembersWithDataCaption 元素&#40;ASSL&#41;](caption-element-assl.md)   
 [DimensionAttribute 資料類型&#40;ASSL&#41;](../data-type/dimensionattribute-data-type-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  