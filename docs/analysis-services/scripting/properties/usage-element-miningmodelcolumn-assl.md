---
title: Usage 元素 (MiningModelColumn) (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: fbe265861a16e28e9244261a26a253f78adc9dba
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="usage-element-miningmodelcolumn-assl"></a>Usage 元素 (MiningModelColumn) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  描述如何與父系相關聯的資料行[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)用。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningModelColumn>  
   ...  
   <Usage>...</Usage>  
   ...  
</MiningModelColumn>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|Description|  
|-----------|-----------------|  
|*索引鍵*|此資料行為索引鍵資料行。|  
|*輸入*|此資料行為輸入資料行。|  
|*Predict*|此資料行為預測資料行。|  
|*PredictOnly*|此資料行只能為預測資料行。|  
|*無*|模型不會使用此資料行。<br /><br /> **\*\* 警告\* \*** 時使用的值是"None"，Analysis Services 不會將傳送的任何值到伺服器預設值; 因此，使用方式 屬性不包含要求/回應中。|  
  
 列舉型別對應至允許的值**使用量**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.MiningModelColumnUsages>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
