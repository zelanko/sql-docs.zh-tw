---
title: UnknownMemberName 元素 (ASSL) |Microsoft Docs
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
api_name:
- UnknownMemberName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- UnknownMemberName
helpviewer_keywords:
- UnknownMemberName element
ms.assetid: 54271336-ea9b-4270-ac3a-9658a5cff77b
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2c788574586a20ef44f0206d07bb21389cfd0308
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37306488"
---
# <a name="unknownmembername-element-assl"></a>UnknownMemberName 元素 (ASSL)
  包含維度之未知成員的標題，而這個標題會以維度的預設語言顯示。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Dimension>  
      ...  
   <UnknownMemberName>...</UnknownMemberName>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|*Unknown*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Dimension](../objects/dimension-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `UnknownMemberName` 元素的值會提供用於未知成員的標題。 未知的成員的成員識別碼*維度*。UnknownMember，其中*維度*是維度的唯一名稱，且無法變更。  
  
 對應至父系的元素`UnknownMemberName`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Dimension>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
