---
title: Subscribe 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Subscribe Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Subscribe
- microsoft.xml.analysis.subscribe
- http://schemas.microsoft.com/analysisservices/2003/engine#Subscribe
helpviewer_keywords:
- Subscribe command
ms.assetid: aad50dd7-44d4-4d83-a973-187f9aed35ec
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cf88b3e4e2fd990ad786b8e505c908f96f53ce6e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079338"
---
# <a name="subscribe-element-xmla"></a>Subscribe 元素 (XMLA)
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[物件](../xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 `Subscribe`命令會訂閱和資料流將從指定的追蹤資料列集上[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。 如果在指定追蹤以外的物件`Object`項目，則會發生錯誤。  
  
 如果您沒有指定 `Object` 元素，系統就會在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體上定義工作階段追蹤並進行訂閱。 此工作階段追蹤會從目前的工作階段傳回固定的追蹤事件集合。  
  
 如果用戶端應用程式關閉的連接，便會終止此命令傳回的資料列集資料流[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體，或如果工作階段`Subscribe`執行命令終止。  
  
## <a name="see-also"></a>另請參閱  
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
