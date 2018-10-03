---
title: 命令元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Commands Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Commands
helpviewer_keywords:
- Commands element
ms.assetid: c9f69fe8-2221-469b-b5b0-08563aaa01dc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 14287d7479af8a34e8394b878436bd2ed812d763
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48184748"
---
# <a name="commands-element-assl"></a>Commands 元素 (ASSL)
  包含與 [MdxScript](../objects/mdxscript-element-assl.md) 元素相關聯之 [Command](../objects/command-element-assl.md) 元素的集合。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MdxScript>  
   ...  
   <Commands>  
      <Command>...</Command>  
...</Commands>  
   ...  
</MdxScript>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MdxScript](../objects/mdxscript-element-assl.md)|  
|子元素|[Command](../objects/command-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.CommandCollection>。  
  
## <a name="see-also"></a>另請參閱  
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
