---
title: IsDefaultMeasure 元素 (XML) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 523cf3d7-9df0-4f9d-8486-9109de8d3cca
caps.latest.revision: 6
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: a4229507c856d511b805a249b162516d8b11feb6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031298"
---
# <a name="isdefaultmeasure-element-xml"></a>IsDefaultMeasure 元素 (XML)
  表示可以透過此關聯性導覽至另一個資料表以及提取具有屬性 DefaultMeasure 的成員，取得此實體的預設量值。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <IsDefaultMeasure>...</IsDefaultMeasure>  
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
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對於 `RelationshipEndVisualizationProperties` 元素，`IsDefaultMeasure` 元素表示可透過導覽至此關聯性的另一端，取得此實體的預設量值。 預設值 `false` 表示沒有要取得的預設量值。  
  
  