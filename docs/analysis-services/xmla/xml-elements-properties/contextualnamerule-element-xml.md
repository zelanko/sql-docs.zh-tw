---
title: ContextualNameRule 元素 (XML) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: beb58b21c88bf5500ba7c15c336b866df59b0c7e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="contextualnamerule-element-xml"></a>ContextualNameRule 元素 (XML)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  提供有關為屬性建構複合名稱的最佳方法提示。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <ContextualNameRule>...</ContextualNameRule>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|-1|  
|基數|0-1：只出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[RelationshipEndVisualizationProperties](../../../analysis-services/scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 向用戶端應用程式提供有關如何為此屬性建立明確名稱的提示。  
  
 值**ContextualNameRule**元素僅限於一個下表所列的字串。  
  
|Value|說明|  
|-----------|-----------------|  
|*無*|使用屬性的名稱。|  
|*內容*|使用內送關聯性的名稱。|  
|*合併式*|按照應用程式語言的規則，串連內送關聯性的名稱和屬性名稱。|  
  
  
