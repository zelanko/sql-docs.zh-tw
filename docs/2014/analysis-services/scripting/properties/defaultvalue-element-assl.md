---
title: DefaultValue 元素 (ASSL) |Microsoft 文件
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
- DefaultValue Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DefaultValue
helpviewer_keywords:
- DefaultValue element
ms.assetid: 87e964a3-f317-46c3-98c7-b3621765c77b
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a319f22dc353f860ca3b0fa3a8e4b0cf60f421ee
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134810"
---
# <a name="defaultvalue-element-assl"></a>DefaultValue 元素 (ASSL)
  包含相關聯的唯讀預設值[ServerProperty](../objects/serverproperty-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ServerProperty>  
   ...  
   <DefaultValue>   </DefaultValue>  
   ...  
</ServerProperty>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|任何 simpleType|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ServerProperty](../objects/serverproperty-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個項目包含的唯讀安裝預設值`ServerProperty`目前執行個體[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 預設值是由此執行個體提供，而且通常無法變更。  
  
 對應目的父代的項目`DefaultValue`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.ServerProperty>。  
  
## <a name="see-also"></a>另請參閱  
 [ServerProperties 元素&#40;ASSL&#41;](../collections/serverproperties-element-assl.md)   
 [Server 元素&#40;ASSL&#41;](../objects/server-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  