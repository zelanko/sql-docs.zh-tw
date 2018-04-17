---
title: Database 元素 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Database Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.database
- http://schemas.microsoft.com/analysisservices/2003/engine#Database
- urn:schemas-microsoft-com:xml-analysis#Database
helpviewer_keywords:
- Database element
ms.assetid: 2ded06c4-4eaf-4ccb-a416-41ee51ced8bc
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 34d18aa3069da2d05be21059f07706a389f2939b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="database-element-xmla"></a>Database 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]識別包含父代所代表之維度的資料庫[物件](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Object>  
   ...  
   <Database>...</Database>  
   ...  
</Object>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[物件](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **資料庫**元素是物件識別碼，其中包含含有所代表之維度的 Analysis Services 資料庫名稱**物件**項目。  
  
## <a name="see-also"></a>請參閱  
 [Cube 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/cube-element-xmla.md)   
 [Dimension 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/dimension-element-xmla.md)   
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
