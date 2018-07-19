---
title: ContextualNameRule 元素 (XML) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: eb567ef8-f412-4d34-837a-75e53b88b3ce
caps.latest.revision: 7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c93e14e122dbe3e0905e25e56570c67c3fa769a1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37193898"
---
# <a name="contextualnamerule-element-xml"></a>ContextualNameRule 元素 (XML)
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|-1|  
|基數|0-1：只出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[RelationshipEndVisualizationProperties](../../scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 向用戶端應用程式提供有關如何為此屬性建立明確名稱的提示。  
  
 `ContextualNameRule` 元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*無*|使用屬性的名稱。|  
|*內容*|使用內送關聯性的名稱。|  
|*合併式*|按照應用程式語言的規則，串連內送關聯性的名稱和屬性名稱。|  
  
  
