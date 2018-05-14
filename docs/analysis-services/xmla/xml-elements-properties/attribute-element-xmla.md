---
title: 屬性元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 68283f4d51bb01ed8b531b4d49e059b742663c26
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="attribute-element-xmla"></a>Attribute 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  定義或篩選屬性中 [Insert](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)、 [Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)或 [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) 父命令在上面執行的成員。  
  
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
|[Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)、 [Where](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)|[AttributeName](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md)、 [Keys](../../../analysis-services/xmla/xml-elements-properties/keys-element-xmla.md)|  
|[Insert](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)、 [Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|[AttributeName](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md)、 [CustomRollup](../../../analysis-services/xmla/xml-elements-properties/customrollup-element-xmla.md)、 [CustomRollupProperties](../../../analysis-services/xmla/xml-elements-properties/customrollupproperties-element-xmla.md)、 [Keys](../../../analysis-services/xmla/xml-elements-properties/keys-element-xmla.md)、 [Name](../../../analysis-services/xmla/xml-elements-properties/name-element-xmla.md)、 [SkippedLevels](../../../analysis-services/xmla/xml-elements-properties/skippedlevels-element-xmla.md)、 [Translations](../../../analysis-services/xmla/xml-elements-properties/translations-element-xmla.md)、 [UnaryOperator](../../../analysis-services/xmla/xml-elements-properties/unaryoperator-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **Attribute** 元素會定義分別由 **Insert**、 **Update**或 **Drop** 命令插入、更新或刪除的屬性成員。 因為只能針對單一屬性成員運作這些命令一次[屬性](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md)集合**插入**，**更新**，和**卸除**命令只能包含一個**屬性**項目。 不過， **Attributes** 和 **Where** 命令之 **Drop** 元素的 **Update** 集合可以包含一個以上的 **Attribute** 元素，如此您就可以篩選要在可寫入維度中卸除或更新的屬性。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)   
 [啟用寫入的維度](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
