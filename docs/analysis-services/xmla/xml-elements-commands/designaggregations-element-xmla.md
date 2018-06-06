---
title: DesignAggregations 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b32a7ecaf7c8268b88d3fc417cc1e41e024bfd2f
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34574130"
---
# <a name="designaggregations-element-xmla"></a>DesignAggregations 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Analysis Services 執行個體上建立的彙總設計的彙總。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <DesignAggregations>  
      <Object>...</Object>  
      <Time>...</Time>  
      <Steps>...</Steps>  
      <Optimization>...</Optimization>  
      <Storage>...</Storage>  
      <Materialize>...</Materialize>  
      <Queries>...</Queries>  
   </DesignAggregations>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[具體化](../../../analysis-services/xmla/xml-elements-properties/materialize-element-xmla.md)，[物件](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)，[最佳化](../../../analysis-services/xmla/xml-elements-properties/optimization-element-xmla.md)，[查詢](../../../analysis-services/xmla/xml-elements-properties/queries-element-xmla.md)，[步驟](../../../analysis-services/xmla/xml-elements-properties/steps-element-xmla.md)，[儲存體](../../../analysis-services/xmla/xml-elements-properties/storage-element-xmla.md)[時間](../../../analysis-services/xmla/xml-elements-properties/time-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **DesignAggregations**命令用來產生彙總設計所儲存的彙總定義。 然後，彙總設計可以用來具體化分割區的彙總而且可以在分割區之間重複使用。  
  
## <a name="see-also"></a>另請參閱
 [命令&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
