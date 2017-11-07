---
title: "SkippedLevelsColumn 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- SkippedLevelsColumn Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- SkippedLevelsColumn
helpviewer_keywords:
- SkippedLevelsColumn element
ms.assetid: 6b00a288-99c1-4735-9e6b-cd13ed4fa346
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 181e93110f5e482a04940ee5fe66bbba99b6c073
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="skippedlevelscolumn-element-assl"></a>SkippedLevelsColumn 元素 (ASSL)
    
> [!NOTE]  
>  這項功能在這個 Microsoft SQL Server 版本中已經停止。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。  
  
 提供儲存每個成員與其父系之間略過 (空白) 之層級數目的資料行詳細資料。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <SkippedLevelsColumn xsi:type="DataItem">...</SkippedLevelsColumn>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **SkippedLevelsColumn**項目是只適用於父屬性 (換言之，值[使用量](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md)元素**DimensionAttribute**父設定若要*父*)。 **SkippedLevelsColumn**元素包含資料行或儲存每個成員與其父成員之間略過層級數目的父屬性的屬性。 這可讓以父屬性為基礎的父子式階層略過成員之間的層級。 這個資料行或屬性中包含的值必須為非負整數，否則就會發生處理錯誤。 如果**SkippedLevelsColumn**項目未指定，或不含任何值，目前成員的層級深度一低於父成員。  
  
 如需有關**DataItem**型別，包括 Analysis Services 指令碼語言 (ASSL) 物件和屬性的資料表**DataItem**資料表，請參閱[DataItem 資料類型&#40;ASSL &#41;](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 對應目的父代的項目**SkippedLevelsColumn**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>另請參閱  
 [Attributes 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/attributes-element-assl.md)   
 [Dimension 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [物件 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

