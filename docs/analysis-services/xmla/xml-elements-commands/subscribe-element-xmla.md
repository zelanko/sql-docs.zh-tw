---
title: Subscribe 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 548336f5e891cc41c485bed4047c1223d0f9344c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="subscribe-element-xmla"></a>Subscribe 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  訂閱追蹤並傳回包含追蹤事件的資料列集[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <Subscribe>  
      <Object>...</Object>  
   </Subscribe>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[物件](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **訂閱**命令訂閱和資料流將從指定的追蹤資料列集上[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。 如果您在 **Object** 元素中指定追蹤以外的物件，就會發生錯誤。  
  
 如果**物件**未指定項目、 定義及訂閱的工作階段追蹤[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。 此工作階段追蹤會從目前的工作階段傳回固定的追蹤事件集合。  
  
 當用戶端應用程式關閉的連接，就會結束此命令傳回的資料列集資料流[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體，或如果所在工作階段**訂閱**命令執行已終止。  
  
## <a name="see-also"></a>另請參閱  
 [命令 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
