---
title: AllowDuplicateNames 元素 (ASSL) |Microsoft 文件
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
- AllowDuplicateNames Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AllowDuplicateNames
helpviewer_keywords:
- AllowDuplicateNames element
ms.assetid: d0a80040-115f-4490-926f-4d64d8977e67
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e6fe55bdf9dde0906a43fa46745e22179dba9e74
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131578"
---
# <a name="allowduplicatenames-element-assl"></a>AllowDuplicateNames 元素 (ASSL)
  決定是否允許重複的名稱，以在[階層](../objects/hierarchy-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Hierarchy>  
      ...  
   <AllowDuplicateNames>...</AllowDuplicateNames>  
   ...  
</Hierarchy>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|`True`|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Hierarchy](../objects/hierarchy-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目`AllowDuplicateNames`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Hierarchy>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  