---
title: "MemberUniqueNameStyle 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MemberUniqueNameStyle Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MemberUniqueNameStyle element
ms.assetid: f0771c81-0127-4203-9501-ae4f864730fa
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 94e0ed38f78c485e3c0178ac4dcc02cd318d065b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="memberuniquenamestyle-element-assl"></a>MemberUniqueNameStyle 元素 (ASSL)
  決定如何唯一名稱內所包含的階層成員產生[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CubeDimension>  
   ...  
   <MemberUniqueNameStyle>...</MemberUniqueNameStyle>  
   ...  
</CubeDimension>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*原生*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|Description|  
|-----------|-----------------|  
|*原生*|此執行個體會自動決定成員的唯一名稱。|  
|*NamePath*|此執行個體會產生複合名稱，而這個名稱是由成員的每個層級和標題所組成。|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目**MemberUniqueNameStyle**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.CubeDimension>。  
  
## <a name="see-also"></a>另請參閱  
 [Cube 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Dimension 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [CubeDimension 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)  
  
  

