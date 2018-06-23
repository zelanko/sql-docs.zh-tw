---
title: WritebackTableCreation 元素 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- WritebackTableCreation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#WritebackTableCreation
- microsoft.xml.analysis.writebacktablecreation
- http://schemas.microsoft.com/analysisservices/2003/engine#WritebackTableCreation
helpviewer_keywords:
- WritebackTableCreation element
ms.assetid: e9579d63-e28c-4d4e-9f4a-21c5da24c276
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 95b9639b34002aa69366f87cac48427624f7d0dd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131988"
---
# <a name="writebacktablecreation-element-xmla"></a>WritebackTableCreation 元素 (XMLA)
  決定是否要將回寫資料表建立期間[程序](../xml-elements-commands/process-element-xmla.md)作業。  
  
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
|父元素|[處理](../xml-elements-commands/process-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 Analysis Services 執行個體上物件可用處理選項的相關資訊，請參閱[多維度模型物件處理](../../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
 `WritebackTableCreation` 元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*建立*|建立新的回寫資料表 (如果回寫資料表不存在的話)。 如果回寫資料表已經存在，就會發生錯誤。|  
|*[Createalways]*|建立新的回寫資料表，並覆寫任何現有的回寫資料表。|  
|*UseExisting*|使用現有的回寫資料表 (如果回寫資料表已經存在的話)。 如果回寫資料表不存在，就會發生錯誤。|  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  