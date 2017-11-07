---
title: "ServerMode 元素 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: c2f8cb39-dad7-433b-b7b7-fb1625f76a84
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8145c7090e1c172fe210202e55078cb4bd404fcb
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="servermode-element"></a>ServerMode 元素
  **ServerMode**伺服器項目會指定伺服器正在運作中的模式。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Server>  
...  
   <ddl300:ServerMode>...</ddl300:ServerMode>  
...  
</Server>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|(無)|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 伺服器以下列其中一個模式運作：  
  
|[值]|Description|  
|-----------|-----------------|  
|*多維度*|多維度和資料採礦模式|  
|*表格式*|表格式模式|  
|*SharePoint*|SharePoint 模式|  
  
## <a name="see-also"></a>另請參閱  
 [Server](../../../analysis-services/scripting/objects/server-element-assl.md)  
  
  

