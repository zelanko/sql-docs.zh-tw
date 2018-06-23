---
title: DisplayFlag 元素 (ASSL) |Microsoft 文件
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
api_name:
- DisplayFlag Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DisplayFlag
helpviewer_keywords:
- DisplayFlag element
ms.assetid: a6750477-0763-46da-9add-1f4448146a6b
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 43c797101826a614c67c7c4f213140a427b51395
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134701"
---
# <a name="displayflag-element-assl"></a>DisplayFlag 元素 (ASSL)
  包含指出使用者介面元件是否應該顯示相關聯的唯讀提示[ServerProperty](../objects/serverproperty-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ServerProperty>  
   ...  
   <DisplayFlag>...</DisplayFlag>  
   ...  
</ServerProperty>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ServerProperty](../objects/serverproperty-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應至父系的項目`DisplayFlag`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.ServerProperty>。  
  
## <a name="see-also"></a>另請參閱  
 [ServerProperties 元素&#40;ASSL&#41;](../collections/serverproperties-element-assl.md)   
 [Server 元素&#40;ASSL&#41;](../objects/server-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  