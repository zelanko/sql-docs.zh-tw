---
title: Database 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f874d72700646456fa046b820f0fdf29e4738d58
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="database-element-xmla"></a>Database 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  識別包含父代所代表之維度的資料庫[物件](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Object>  
   ...  
   <Database>...</Database>  
   ...  
</Object>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[物件](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **資料庫**元素是物件識別碼，其中包含含有所代表之維度的 Analysis Services 資料庫名稱**物件**項目。  
  
## <a name="see-also"></a>另請參閱  
 [Cube 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/cube-element-xmla.md)   
 [Dimension 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/dimension-element-xmla.md)   
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
