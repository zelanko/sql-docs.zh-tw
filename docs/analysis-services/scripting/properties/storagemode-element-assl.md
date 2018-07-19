---
title: StorageMode 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 72b2963293c6c59338ad23f8e4f4f5c0e9d19001
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34038652"
---
# <a name="storagemode-element-assl"></a>StorageMode 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  決定父元素的儲存模式。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Cube> <!-- or Dimension, MeasureGroup, Partition -->  
   ...  
   <StorageMode>...</StorageMode>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*MOLAP*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Cube 元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)，[維度項目&#40;ASSL&#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [MeasureGroup 元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)，[磁碟分割項目&#40;ASSL&#41;](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|Description|  
|-----------|-----------------|  
|*MOLAP*|父系使用多維度 OLAP (MOLAP) 儲存。|  
|*ROLAP*|父系使用關聯式 OLAP (ROLAP) 儲存。|  
|*HOLAP*|父系使用混合式 OLAP (HOLAP) 儲存。<br /><br /> 注意： 此值不是有效的[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)父元素。|  
|*InMemory*|父系使用 IMBI 儲存。|  
  
 列舉型別對應至允許的值**StorageMode**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.StorageMode>。  
  
 對應至父系的項目**StorageMode**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Cube>， <xref:Microsoft.AnalysisServices.Dimension>， <xref:Microsoft.AnalysisServices.MeasureGroup>，和<xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
