---
title: 群組元素 (ASSL) |Microsoft 文件
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
- Group Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- GROUP
helpviewer_keywords:
- Group element
ms.assetid: 7df4ba90-b39f-4d8a-8db1-b73639a522a6
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6b10e557c91a27305ca0b9bff1d989e327b3b6f7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030877"
---
# <a name="group-element-assl"></a>Group 元素 (ASSL)
  定義繫結至屬性的成員群組。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Groups>  
   <Group>  
      <Name>...</Name>  
      <Members>...</Members>  
   </Group>  
<Groups/>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-n：出現一次以上的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[群組](../collections/groups-element-assl.md)|  
|子元素|[Members](../collections/members-element-assl.md)、[Name](../properties/name-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.Group>。  
  
## <a name="see-also"></a>另請參閱  
 [UserDefinedGroupBinding 資料類型&#40;ASSL&#41;](../data-type/binding-data-type-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  