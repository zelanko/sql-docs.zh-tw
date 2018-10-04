---
title: CurrentStorageMode 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CurrentStorageMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CurrentStorageMode
helpviewer_keywords:
- CurrentStorageMode element
ms.assetid: 050c21e4-368b-4ff0-b0c5-349f93fe9747
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1d930292898f55736daea9e00893cd6e5f000a34
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48058768"
---
# <a name="currentstoragemode-element-assl"></a>CurrentStorageMode 元素 (ASSL)
  決定父元素的目前儲存模式。  
  
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
|父元素|[維度](../objects/dimension-element-assl.md)，[資料分割](../objects/partition-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 `CurrentStorageMode` 元素會指出目前針對主動式快取目的所用的儲存模式，並套用至父元素的所有屬性。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*MOLAP*|父系使用多維度 OLAP (MOLAP) 儲存。|  
|*ROLAP*|父系使用關聯式 OLAP (ROLAP) 儲存。|  
|*HOLAP*|父系使用混合式 OLAP (HOLAP) 儲存。 **注意︰** 這個值才適用於[磁碟分割](../objects/partition-element-assl.md)父項目。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `CurrentStorageMode` 允許值的列舉是 <xref:Microsoft.AnalysisServices.StorageMode>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
