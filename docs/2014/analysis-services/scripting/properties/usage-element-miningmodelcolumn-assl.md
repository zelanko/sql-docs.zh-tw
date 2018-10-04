---
title: Usage 元素 (MiningModelColumn) (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Usage Element (MiningModelColumn)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Usage
helpviewer_keywords:
- Usage element
ms.assetid: 435a857e-37a9-434e-9de1-354f1ff2993f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 220f59e5e342f61f30d0f94bc9f9728982105986
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48090295"
---
# <a name="usage-element-miningmodelcolumn-assl"></a>Usage 元素 (MiningModelColumn) (ASSL)
  描述如何在父代相關聯的資料行[MiningStructure](../objects/miningstructure-element-assl.md)用。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningModelColumn>  
   ...  
   <Usage>...</Usage>  
   ...  
</MiningModelColumn>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*索引鍵*|此資料行為索引鍵資料行。|  
|*輸入*|此資料行為輸入資料行。|  
|*Predict*|此資料行為預測資料行。|  
|*PredictOnly*|此資料行只能為預測資料行。|  
|*無*|模型不會使用此資料行。 **警告：** 時使用的值為"None"，Analysis Services 不會傳送任何值給伺服器依預設，因此，使用方式 屬性不包含在要求/回應。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `Usage` 允許值的列舉是 <xref:Microsoft.AnalysisServices.MiningModelColumnUsages>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
