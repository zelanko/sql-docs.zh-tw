---
title: DefaultDetailsPosition 元素 (XML) |Microsoft 文件
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
ms.assetid: 851ad331-aefd-4277-a5e5-e32a8f5c5e22
caps.latest.revision: 6
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 296c8f5229a7b5996c8b53319a26999590f9e75e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031980"
---
# <a name="defaultdetailsposition-element-xml"></a>DefaultDetailsPosition 元素 (XML)
  包含有關元素在元素集合中的位置資訊。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <DefaultDetailsPosition>...</DefaultDetailsPosition>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|Integer|  
|預設值|-1|  
|基數|0-1：只出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[RelationshipEndVisualizationProperties](../../scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對於 `RelationshipEndVisualizationProperties` 元素，`DefaultDetailsPosition` 元素包含預設詳細資料元素在詳細資料集合中的位置。 預設值 `false` 表示沒有要使用的預設詳細資料。  
  
  