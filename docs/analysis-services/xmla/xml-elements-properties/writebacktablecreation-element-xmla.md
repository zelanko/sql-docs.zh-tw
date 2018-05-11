---
title: WritebackTableCreation 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 54969f1710a4abcd079fc3318f1d7c99abc3ce80
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="writebacktablecreation-element-xmla"></a>WritebackTableCreation 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  決定是否要將回寫資料表建立期間[程序](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)作業。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Process>  
...  
   <WritebackTableCreation>...</WritebackTableCreation>  
...  
</Process>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[處理](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 Analysis Services 執行個體上物件可用處理選項的相關資訊，請參閱[處理多維度模型&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
 值**WritebackTableCreation**元素僅限於一個下表所列的字串。  
  
|Value|Description|  
|-----------|-----------------|  
|*建立*|建立新的回寫資料表 (如果回寫資料表不存在的話)。 如果回寫資料表已經存在，就會發生錯誤。|  
|*[Createalways]*|建立新的回寫資料表，並覆寫任何現有的回寫資料表。|  
|*UseExisting*|使用現有的回寫資料表 (如果回寫資料表已經存在的話)。 如果回寫資料表不存在，就會發生錯誤。|  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
