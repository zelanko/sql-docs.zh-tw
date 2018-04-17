---
title: CurrentStorageMode 元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- CurrentStorageMode Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CurrentStorageMode
helpviewer_keywords:
- CurrentStorageMode element
ms.assetid: 050c21e4-368b-4ff0-b0c5-349f93fe9747
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 83a958417136ca921714653492ffe118b1ff027c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="currentstoragemode-element-assl"></a>CurrentStorageMode 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]決定父元素的目前儲存模式。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Dimension> <!-- or Partition -->  
   <CurrentStorageMode>...</CurrentStorageMode>  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*ROLAP*|  
|基數|0-1：只能出現一次或完全不出現的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)，[磁碟分割](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **CurrentStorageMode**元素指出目前針對主動式快取的目的，使用中的儲存模式，並套用至父項目的所有屬性。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*MOLAP*|父系使用多維度 OLAP (MOLAP) 儲存。|  
|*ROLAP*|父系使用關聯式 OLAP (ROLAP) 儲存。|  
|*HOLAP*|父系使用混合式 OLAP (HOLAP) 儲存。<br /><br /> 注意： 這個值是唯一有效的[分割](../../../analysis-services/scripting/objects/partition-element-assl.md)父元素。|  
  
 列舉型別對應至允許的值**CurrentStorageMode**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.StorageMode>。  
  
## <a name="see-also"></a>請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
