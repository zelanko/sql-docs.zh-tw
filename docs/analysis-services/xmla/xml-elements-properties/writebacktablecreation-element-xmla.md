---
title: WritebackTableCreation 元素 (XMLA) |Microsoft 文件
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
- WritebackTableCreation Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#WritebackTableCreation
- microsoft.xml.analysis.writebacktablecreation
- http://schemas.microsoft.com/analysisservices/2003/engine#WritebackTableCreation
helpviewer_keywords:
- WritebackTableCreation element
ms.assetid: e9579d63-e28c-4d4e-9f4a-21c5da24c276
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6a6258d7b0679af52839e2fa88a5764efb47d6d1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="writebacktablecreation-element-xmla"></a>WritebackTableCreation 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]決定是否要將回寫資料表建立期間[程序](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)作業。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Process>  
...  
   <WritebackTableCreation>...</WritebackTableCreation>  
...  
</Process>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
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
 Analysis Services 執行個體上物件可用處理選項的相關資訊，請參閱[處理多維度模型 &#40;Analysis Services &#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 值**WritebackTableCreation**元素僅限於一個下表所列的字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*建立*|建立新的回寫資料表 (如果回寫資料表不存在的話)。 如果回寫資料表已經存在，就會發生錯誤。|  
|*[Createalways]*|建立新的回寫資料表，並覆寫任何現有的回寫資料表。|  
|*UseExisting*|使用現有的回寫資料表 (如果回寫資料表已經存在的話)。 如果回寫資料表不存在，就會發生錯誤。|  
  
## <a name="see-also"></a>請參閱  
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
