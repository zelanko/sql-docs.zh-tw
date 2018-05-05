---
title: ReadWriteMode 元素 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ReadWriteMode command
ms.assetid: 379bcaca-bb7e-4934-a9e7-21f8ede2fdc7
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 695cf49a79bebe5540cb07c28f474d9b73cbb669
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
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
  
  
