---
title: Subscribe 元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f784cbe3c33eb6b2587b7b535668e793fac3b138
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37973070"
---
# <a name="subscribe-element-xmla"></a>Subscribe 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  訂閱追蹤，並傳回包含追蹤事件的 Analysis Services 執行個體的資料列集。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <Subscribe>  
      <Object>...</Object>  
   </Subscribe>  
</Command>  
```  
  
## <a name="element-characteristics"></a>項目特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>項目關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[物件](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **Subscribe**命令訂閱和資料流將從指定的追蹤資料列集上[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。 如果您在 **Object** 元素中指定追蹤以外的物件，就會發生錯誤。  
  
 如果**物件**項目未指定，是定義工作階段追蹤，並將其傳回[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。 此工作階段追蹤會從目前的工作階段傳回固定的追蹤事件集合。  
  
 如果用戶端應用程式關閉的連接，便會終止此命令傳回的資料列集資料流[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體，或如果工作階段**Subscribe**執行命令終止。  
  
## <a name="see-also"></a>另請參閱
 [命令&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
