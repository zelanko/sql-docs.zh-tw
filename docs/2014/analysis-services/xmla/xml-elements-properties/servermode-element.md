---
title: ServerMode 元素 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: c2f8cb39-dad7-433b-b7b7-fb1625f76a84
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6e714c9f5bbc7626030d83faa7d0058c7aa13752
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140178"
---
# <a name="servermode-element"></a>ServerMode 元素
  `ServerMode` 伺服器元素指定伺服器的作業模式。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Server>  
...  
   <ddl300:ServerMode>...</ddl300:ServerMode>  
...  
</Server>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|(無)|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Server](../../scripting/objects/server-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 伺服器以下列其中一個模式運作：  
  
|[值]|描述|  
|-----------|-----------------|  
|*多維度*|多維度和資料採礦模式|  
|*表格式*|表格式模式|  
|*SharePoint*|SharePoint 模式|  
  
## <a name="see-also"></a>另請參閱  
 [Server](../../scripting/objects/server-element-assl.md)  
  
  
