---
title: 查詢元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Query Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Query
- microsoft.xml.analysis.query
- http://schemas.microsoft.com/analysisservices/2003/engine#Query
helpviewer_keywords:
- Query element
ms.assetid: 5a4544e4-012f-4a47-942c-23596400ea16
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 02feb5cb14e6b6acdc6100070495d0c84b89e483
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37293236"
---
# <a name="query-element-xmla"></a>Query 元素 (XMLA)
  包含查詢中的[查詢](queries-element-xmla.md)所使用的集合[DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md)命令在基於使用方式的最佳化期間。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Queries>  
   ...  
   <Query>...</Query>  
   ...  
</Queries>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[查詢](queries-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `DesignAggregations` 命令會在命令的 `Query` 集合中包含一個或多個 `Queries` 元素，藉以支援基於使用方式的最佳化。 每個`Query`項目代表一個目標查詢，使用定義目標最常用的查詢的彙總設計程序。 您可以指定您自己的目標查詢，或者您可以使用的執行個體所儲存的資訊[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]來擷取有關最常用的查詢記錄中使用的查詢。  
  
 如果您反覆設計彙總，您只需要將目標查詢傳入第一個`DesignAggregations`命令即可，因為[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體儲存這些目標查詢，並在後續的期間使用這些查詢`DesignAggregations`命令。 當您將目標查詢傳入反覆處理序的第一個 `DesignAggregations` 命令之後，任何在 `DesignAggregations` 屬性中包含目標查詢的後續 `Queries` 命令就會產生錯誤。  
  
 `Query` 元素包含具有下列引數的逗號分隔值：  
  
 *Frequency*,*Dataset*[,*Dataset*...]  
  
 *頻率*  
 對應至查詢先前執行次數的加權因數。 如果`Query`項目代表新的查詢中，*頻率*值代表設計處理序用來評估查詢的加權因數。 當頻率值變大時，在設計處理序期間放置於查詢的加權就會增加。  
  
 *資料集*  
 指定維度的哪些屬性要包含在查詢中的數值字串。 這個字串必須與維度中的屬性數目具有相同的字元數目。 零 (0) 表示指定之序數位置中的屬性沒有包含在指定維度的查詢中，而一 (1) 則表示指定之序數位置中的屬性已包含在指定維度的查詢中。  
  
 例如，字串 "011" 是指涉及含有三個屬性之維度的查詢，其中第二和第三個屬性包含在查詢中。  
  
> [!NOTE]  
>  某些屬性會從資料集的考量中排除。 如需有關排除屬性的詳細資訊，請參閱 <<c0> [ 屬性 (XMLA)](query-element-xmla.md)。  
  
 在包含彙總設計的量值群組中的每個維度由*資料集*中的值`Query`項目。 *Dataset* 值的順序必須與量值群組中包含維度的順序相符。  
  
## <a name="see-also"></a>另請參閱  
 [設計彙總&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/designing-aggregations-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
