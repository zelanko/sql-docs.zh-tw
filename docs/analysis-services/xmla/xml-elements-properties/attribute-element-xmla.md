---
title: "屬性元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Attribute Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Attribute
- microsoft.xml.analysis.attribute
- urn:schemas-microsoft-com:xml-analysis#Attribute
helpviewer_keywords: Attribute element
ms.assetid: 0df9cf44-dc5f-4234-8a5a-daac8aabc0d6
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b2100479529d5d7ca15bd8b6dcf0600088617c02
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="attribute-element-xmla"></a>Attribute 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]定義或篩選中之屬性的成員父[插入](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)，[更新](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)，或[卸除](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)命令會執行。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Attributes>  
   ...  
   <Attribute>  
      <AttributeName>...</AttributeName>  
      <Keys>...</Keys>  
      <!-- The following elements are included only for attributes contained in the Attributes element of a parent Insert or Update command -->  
      <Name>...</Name>  
      <Translations>...</Translations>  
      <CustomRollup>...</CustomRollup>  
      <CustomRollupProperties>...</CustomRollupProperties>  
      <UnaryOperator>...</UnaryOperator>  
      <SkippedLevels>...</SkippedLevels>  
   </Attribute>  
   ...  
</Attributes>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[屬性](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md)|  
|子元素|請參閱下表。|  
  
|上階或父系|子元素|  
|------------------------|-------------------|  
|[卸除](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)，[位置](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)|[AttributeName](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md)，[金鑰](../../../analysis-services/xmla/xml-elements-properties/keys-element-xmla.md)|  
|[插入](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)，[更新](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|[AttributeName](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md)， [CustomRollup](../../../analysis-services/xmla/xml-elements-properties/customrollup-element-xmla.md)， [CustomRollupProperties](../../../analysis-services/xmla/xml-elements-properties/customrollupproperties-element-xmla.md)，[金鑰](../../../analysis-services/xmla/xml-elements-properties/keys-element-xmla.md)，[名稱](../../../analysis-services/xmla/xml-elements-properties/name-element-xmla.md)， [SkippedLevels](../../../analysis-services/xmla/xml-elements-properties/skippedlevels-element-xmla.md)，[翻譯](../../../analysis-services/xmla/xml-elements-properties/translations-element-xmla.md)， [UnaryOperator](../../../analysis-services/xmla/xml-elements-properties/unaryoperator-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **Attribute** 元素會定義分別由 **Insert**、 **Update**或 **Drop** 命令插入、更新或刪除的屬性成員。 因為只能針對單一屬性成員運作這些命令一次[屬性](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md)集合**插入**，**更新**，和**卸除**命令只能包含一個**屬性**項目。 不過， **Attributes** 和 **Where** 命令之 **Drop** 元素的 **Update** 集合可以包含一個以上的 **Attribute** 元素，如此您就可以篩選要在可寫入維度中卸除或更新的屬性。  
  
## <a name="see-also"></a>請參閱  
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)   
 [可寫入維度](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
