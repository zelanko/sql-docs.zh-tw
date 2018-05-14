---
title: ServerMode 元素 |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bcbd6e0315fc8a418ccff20fe5c2a69eebe4490b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="servermode-element"></a>ServerMode 元素
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
  
  
