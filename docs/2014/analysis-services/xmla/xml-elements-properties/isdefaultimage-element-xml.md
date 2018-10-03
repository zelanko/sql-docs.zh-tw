---
title: IsDefaultImage 元素 (XML) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: e29cd137-af82-4753-a681-0d3e705513f3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0821c2dfaa25f3d9a557663046db0405aca0cb24
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48201368"
---
# <a name="isdefaultimage-element-xml"></a>IsDefaultImage 元素 (XML)
  表示可以透過此關聯性導覽至另一個資料表以及提取具有屬性 IsDefaultImage 的成員，取得此實體的預設影像。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <IsDefaultImage>...</IsDefaultImage>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|false|  
|基數|0-1：只出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[RelationshipEndVisualizationProperties](../../scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 對於 `RelationshipEndVisualizationProperties` 元素，`IsDefaultImage` 元素表示可透過導覽至此關聯性的另一端，取得此實體的預設影像。 預設值 `false` 表示沒有要取得的預設影像。  
  
  
