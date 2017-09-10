---
title: "查詢元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Query Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Query
- microsoft.xml.analysis.query
- http://schemas.microsoft.com/analysisservices/2003/engine#Query
helpviewer_keywords:
- Query element
ms.assetid: 5a4544e4-012f-4a47-942c-23596400ea16
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b3b6b989932fcb37fba1c137c30658238a0c05df
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="query-element-xmla"></a>Query 元素 (XMLA)
  包含查詢內[查詢](../../../analysis-services/xmla/xml-elements-properties/queries-element-xmla.md)集合所使用[DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)命令在基於使用方式的最佳化。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Queries>  
   ...  
   <Query>...</Query>  
   ...  
</Queries>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[查詢](../../../analysis-services/xmla/xml-elements-properties/queries-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **DesignAggregations** 命令會在命令的 **Query** 集合中包含一個或多個 **Queries** 元素，藉以支援基於使用方式的最佳化。 每個 **Query** 元素都代表一個目標查詢，而且設計處理序會使用此查詢來定義以最常用查詢為目標的彙總。 您可以指定您自己的目標查詢，或者您可以使用執行個體所儲存的資訊[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]擷取有關最常用的資訊的查詢記錄中使用查詢。  
  
 如果您反覆設計彙總，您只需要將目標查詢傳入第一個**DesignAggregations**指令，因為[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體儲存這些目標查詢，並在後續期間使用這些查詢**DesignAggregations**命令。 當您將目標查詢傳入反覆處理序的第一個 **DesignAggregations** 命令之後，任何在 **DesignAggregations** 屬性中包含目標查詢的後續 **Queries** 命令就會產生錯誤。  
  
 **Query** 元素包含具有下列引數的逗號分隔值：  
  
 *Frequency*,*Dataset*[,*Dataset*...]  
  
 *頻率*  
 對應至查詢先前執行次數的加權因數。 如果 **Query** 元素代表新的查詢， *Frequency* 值就代表設計處理序用來評估查詢的加權因數。 當頻率值變大時，在設計處理序期間放置於查詢的加權就會增加。  
  
 *資料集*  
 指定維度的哪些屬性要包含在查詢中的數值字串。 這個字串必須與維度中的屬性數目具有相同的字元數目。 零 (0) 表示指定之序數位置中的屬性沒有包含在指定維度的查詢中，而一 (1) 則表示指定之序數位置中的屬性已包含在指定維度的查詢中。  
  
 例如，字串 "011" 是指涉及含有三個屬性之維度的查詢，其中第二和第三個屬性包含在查詢中。  
  
> [!NOTE]  
>  某些屬性會從資料集的考量中排除。 如需有關排除屬性的詳細資訊，請參閱[屬性 (XMLA)](../../../analysis-services/xmla/xml-elements-properties/query-element-xmla.md)。  
  
 量值群組中包含彙總設計的每個維度是由 *Query* 元素中的 **Dataset** 值代表。 *Dataset* 值的順序必須與量值群組中包含維度的順序相符。  
  
## <a name="see-also"></a>另請參閱  
 [設計彙總 &#40;XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/designing-aggregations-xmla.md)   
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
