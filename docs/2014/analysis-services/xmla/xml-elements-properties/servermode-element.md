---
title: ServerMode 元素 |Microsoft 文件
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: c2f8cb39-dad7-433b-b7b7-fb1625f76a84
caps.latest.revision: 6
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 8448e5ac3111f4c1683ae3dd62dcaef992f3f0e7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022480"
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
|子元素|無|  
  
## <a name="remarks"></a>備註  
 伺服器以下列其中一個模式運作：  
  
|[值]|描述|  
|-----------|-----------------|  
|*多維度*|多維度和資料採礦模式|  
|*表格式*|表格式模式|  
|*SharePoint*|SharePoint 模式|  
  
## <a name="see-also"></a>另請參閱  
 [Server](../../scripting/objects/server-element-assl.md)  
  
  