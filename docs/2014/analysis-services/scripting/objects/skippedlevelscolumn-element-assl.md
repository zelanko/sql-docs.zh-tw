---
title: SkippedLevelsColumn 元素 (ASSL) |Microsoft 文件
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
- SkippedLevelsColumn Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- SkippedLevelsColumn
helpviewer_keywords:
- SkippedLevelsColumn element
ms.assetid: 6b00a288-99c1-4735-9e6b-cd13ed4fa346
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3ae469982f39e1274759eaaea992fe456330d8fb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032868"
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `SkippedLevelsColumn`項目是只適用於父屬性 (換言之，值[使用量](../properties/usage-element-dimensionattribute-assl.md)元素`DimensionAttribute`父代設定為*父*)。 `SkippedLevelsColumn` 元素包含儲存每個成員與其父成員之間略過之層級數目的父屬性的資料行或屬性。 這可讓以父屬性為基礎的父子式階層略過成員之間的層級。 這個資料行或屬性中包含的值必須為非負整數，否則就會發生處理錯誤。 如果您沒有指定 `SkippedLevelsColumn` 元素或者它並未包含任何值，目前成員的層級深度就會低於父成員一層。  
  
 如需有關`DataItem`型別，包括 Analysis Services 指令碼語言 (ASSL) 物件和屬性的資料表`DataItem`資料表，請參閱[DataItem 資料類型&#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md)。  
  
 對應目的父代的項目`SkippedLevelsColumn`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性項目&#40;ASSL&#41;](../collections/attributes-element-assl.md)   
 [維度元素&#40;ASSL&#41;](dimension-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  