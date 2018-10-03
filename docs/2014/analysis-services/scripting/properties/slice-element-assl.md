---
title: Slice 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Slice Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Slice
helpviewer_keywords:
- Slice element
ms.assetid: 2c8c4107-c641-4724-bfa5-0c47e0ec8888
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 84bcab815ec93feae3b997c0341bb8c59012cb17
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48169728"
---
# <a name="slice-element-assl"></a>Slice 元素 (ASSL)
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[資料分割](../objects/partition-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 `Slice` 元素包含 MDX Tuple 運算式或集合運算式，可識別資料分割儲存資訊的 Cube 部分。 MDX 運算式是類似[StrToSet](/sql/mdx/strtoset-mdx) MDX 函數含有 CONSTRAINED 關鍵字，在於此運算式無法包含 MDX 或使用者定義函式。  
  
 對應至父系的元素`Slice`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
