---
title: Slice 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d76e4434a31e35ec4900a5f94f603d31059c7a3c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="slice-element-assl"></a>Slice 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含定義資料分割中包含之配量的多維度運算式 (MDX) 運算式。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Partition>  
      ...  
   <Slice>...</Slice>  
   ...  
</Partition>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[資料分割](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **配量**元素包含 MDX tuple 運算式或集合運算式，可識別資料分割，會儲存資訊的 cube 部分。 MDX 運算式是類似於[StrToSet](../../../mdx/strtoset-mdx.md) MDX 函數與含有 CONSTRAINED 關鍵字，因為此運算式無法包含 MDX 或使用者定義函數。  
  
 對應目的父代的項目**配量**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
