---
title: NamingTemplate 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- NamingTemplate Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NamingTemplate
helpviewer_keywords:
- NamingTemplate element
ms.assetid: d68d765c-f012-40c1-acd4-32741ee2eadf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2b1a167ffc7418d69b28e8436bb67238acc3284b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106308"
---
# <a name="namingtemplate-element-assl"></a>NamingTemplate 元素 (ASSL)
  定義從建構的父子式階層中如何命名層級[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)父項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DimensionAttribute>  
   ...  
      <NamingTemplate>...</NamingTemplate>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 值`NamingTemplate`項目僅供父屬性 (亦即的值[使用量](usage-element-dimensionattribute-assl.md)項目`DimensionAttribute`父項目設定為*父*)。  
  
 當父屬性用於建構階層時，階層的層級就會由父屬性所包含之成員之間的父子式關聯性決定。 因此，與其他維度不同的是，您無法從用於階層的屬性名稱中提取層級名稱。  
  
 不過，系統會使用命名範本來產生父子式階層的層級名稱。 定義於父屬性中的 `NamingTemplate` 元素包含用來定義層級名稱的字串運算式。 目前有兩種方式可定義父屬性的命名範本。 您可以設計命名模式，也可以指定一份名稱的清單。  
  
 命名模式會包含星號 (`*`) 當做計數器的預留位置字元，而此計數器會遞增並插入每個全新且更深層級的名稱。 例如，如果沒有定義任何 (全部) 層級，使用 `Level *` 就會產生 `Level 01`、`Level 02`、`Level 03` 等層級名稱。 如果命名模式沒有包含預留位置字元，系統會先依原狀使用它，接著後續層級名稱的構成方式是在模式的結尾附加一個空格和一個數字。 例如，使用 `Level` 就會產生 `Level`、`Level 01`、`Level 02` 等層級名稱。  
  
 若要使用特定名稱集合來命名，`NamingTemplate` 元素的值會設定為層級名稱的分號分隔清單。 清單中的每個名稱都會用於後續層級名稱。 如果層級的數目超過清單中名稱的數目，系統就會使用清單中的最後一個名稱當做任何其他層級名稱的範本，並且如先前所述，在最後一個名稱後面附加一個空格和一個序數。 例如，使用 `Division;Group;Unit` 就會產生 `Division`、`Group`、`Unit`、`Unit 01`、`Unit 02` 等層級名稱。 反之，使用 `Division;Group;Unit *` 則會產生`Division`、`Group`、`Unit 03`、`Unit 04` 等層級名稱。  
  
 清單中的每個名稱都會被視為範本，以便確保層級名稱的唯一性。 例如，使用 `Manager;Team Lead;Manager;Team Lead;Worker *` 就會產生 `Manager`、`Team Lead`、`Manager 01`、`Team Lead 01`、`Worker 05`、`Worker 06` 等層級名稱。  
  
 使用兩個星號 （*） 包含星號 (\*) 層級命名範本的一部分名稱中的字元。  
  
 對應至父系的元素`NamingTemplate`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>另請參閱  
 [NamingTemplateTranslations 元素&#40;ASSL&#41;](../collections/translations-element-assl.md)   
 [DimensionAttribute 資料類型&#40;ASSL&#41;](../data-type/dimensionattribute-data-type-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
