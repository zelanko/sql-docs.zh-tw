---
title: 屬性元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Attribute Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Attribute
- microsoft.xml.analysis.attribute
- urn:schemas-microsoft-com:xml-analysis#Attribute
helpviewer_keywords:
- Attribute element
ms.assetid: 0df9cf44-dc5f-4234-8a5a-daac8aabc0d6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b7baad7e154cda5ce52e67f08af46e7344f6af1b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48128208"
---
# <a name="attribute-element-xmla"></a>Attribute 元素 (XMLA)
  定義或篩選中之屬性的成員父代[插入](../xml-elements-commands/insert-element-xmla.md)，[更新](../xml-elements-commands/update-element-xmla.md)，或[卸除](../xml-elements-commands/drop-element-xmla.md)命令會執行。  
  
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[屬性](attributes-element-xmla.md)|  
  
 **項目子系**  
  
|||  
|-|-|  
|**上階或父系**|**子項目**|  
|[卸除](../xml-elements-commands/drop-element-xmla.md)，[何處](name-element-xmla.md)，[金鑰](keys-element-xmla.md)|  
|[插入](../xml-elements-commands/insert-element-xmla.md)，[更新](../xml-elements-commands/update-element-xmla.md)|[AttributeName](name-element-xmla.md)， [CustomRollup](customrollup-element-xmla.md)， [CustomRollupProperties](properties-element-xmla.md)，[金鑰](keys-element-xmla.md)，[名稱](name-element-xmla.md)， [SkippedLevels](skippedlevels-element-xmla.md)，[翻譯](translations-element-xmla.md)， [UnaryOperator](unaryoperator-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 `Attribute`項目定義之屬性成員插入、 更新或刪除，分別由`Insert`， `Update`，或`Drop`命令。 因為這些命令只會針對單一屬性成員運作一次[屬性](attributes-element-xmla.md)的集合`Insert`， `Update`，並`Drop`命令只能包含一個`Attribute`項目。 不過，`Attributes` 和 `Where` 命令之 `Drop` 元素的 `Update` 集合可以包含一個以上的 `Attribute` 元素，如此您就可以篩選要在可寫入維度中卸除或更新的屬性。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)   
 [可寫入維度](../../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
