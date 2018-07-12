---
title: 輸入元素 (PerspectiveCalculation) (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Type Element (PerspectiveCalculation)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: d7b87aea-3265-4f3c-a7ee-4f3e90f9a0b7
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d95f248e6991b8386ce9f6b4a2c012057c42ef4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37229568"
---
# <a name="type-element-perspectivecalculation-assl"></a>Type 元素 (PerspectiveCalculation) (ASSL)
  表示的型別[PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<PerspectiveCalculation>  
   ...  
   <Type>...</Type>  
   ...  
</PerspectiveCalculation>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*成員*|「導出成員」|  
|*設定*|命名集|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `Type` 允許值的列舉是 <xref:Microsoft.AnalysisServices.PerspectiveCalculationType>。  
  
 對應至父系的元素`Type`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.PerspectiveCalculation>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
