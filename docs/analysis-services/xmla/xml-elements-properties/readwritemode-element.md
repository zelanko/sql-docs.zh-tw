---
title: ReadWriteMode 元素 |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fde6410ac0f6932fe11e5486342e1d836dcc8000
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="readwritemode-element"></a>ReadWriteMode 元素
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  **ReadWriteMode**資料庫屬性會指定資料庫是否位在**ReadWrite**模式或**ReadOnly**模式。 此屬性只有這兩種可能的值。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Database>  
...  
   <ddlns_100_0:ReadWriteMode>...</ddlns_100_0:ReadWriteMode>  
...  
</Database>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|ReadWrite|  
|基數|0-1：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[資料庫](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 資料庫中建立**ReadWrite**僅限模式。 無法在建立資料庫**ReadOnly**模式。  
  
 值**ReadWriteMode**元素僅限於一個下表所列的字串。  
  
|Value|Description|  
|-----------|-----------------|  
|*ReadOnly*|您就無法將任何變更或更新套用至該資料庫。|  
|*ReadWrite*|您可以將變更或更新套用至該資料庫。|  
  
## <a name="see-also"></a>另請參閱  
 [Attach 元素](../../../analysis-services/xmla/xml-elements-commands/attach-element.md)   
 [附加和卸離 Analysis Services 資料庫](../../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [移動 Analysis Services 資料庫](../../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [資料庫 Readwritemode](../../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [切換 ReadOnly 和 ReadWrite 模式之間的 Analysis Services 資料庫](../../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
  
