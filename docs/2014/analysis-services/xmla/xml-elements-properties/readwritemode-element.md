---
title: ReadWriteMode 元素 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ReadWriteMode command
ms.assetid: 379bcaca-bb7e-4934-a9e7-21f8ede2fdc7
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 88ebc7e23fc3ec4aad0d8273464636354958217a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146817"
---
# <a name="readwritemode-element"></a>ReadWriteMode 元素
  `ReadWriteMode` 資料庫屬性會指定資料庫處於 `ReadWrite` 模式或 `ReadOnly` 模式。 此屬性只有這兩種可能的值。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Database>  
...  
   <ddlns_100_0:ReadWriteMode>...</ddlns_100_0:ReadWriteMode>  
...  
</Database>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|ReadWrite|  
|基數|0-1：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[[資料庫]](database-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 您只能在 `ReadWrite` 模式中建立資料庫， 無法在 `ReadOnly` 模式中建立資料庫。  
  
 `ReadWriteMode` 元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*ReadOnly*|您就無法將任何變更或更新套用至該資料庫。|  
|*ReadWrite*|您可以將變更或更新套用至該資料庫。|  
  
## <a name="see-also"></a>另請參閱  
 [Attach 元素](../xml-elements-commands/attach-element.md)   
 [附加和卸離 Analysis Services 資料庫](../../multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [移動 Analysis Services 資料庫](../../multidimensional-models/move-an-analysis-services-database.md)   
 [資料庫 Readwritemode](../../multidimensional-models/database-readwritemodes.md)   
 [切換 ReadOnly 和 ReadWrite 模式之間的 Analysis Services 資料庫](../../multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
  