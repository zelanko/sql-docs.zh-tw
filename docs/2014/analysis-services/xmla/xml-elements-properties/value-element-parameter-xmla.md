---
title: 值元素 (Parameter) (XMLA) |Microsoft Docs
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
- Value Element (Parameter)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.value
- urn:schemas-microsoft-com:xml-analysis#Value
- http://schemas.microsoft.com/analysisservices/2003/engine#Value
helpviewer_keywords:
- Value element
ms.assetid: e590d189-91aa-40c7-8669-09c87812f4ce
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 05535bb119ce20334b5681ea001e4e8528a507f3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37302698"
---
# <a name="value-element-parameter-xmla"></a>Value 元素 (Parameter) (XMLA)
  包含所代表之參數的值[參數](parameter-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```  
  
<Parameter>  
   ...  
   <Value>...</Value>  
   ...  
</Parameter>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|任意|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[參數](parameter-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `Value`項目可以儲存任何簡單 XML 類型，以及 XML for Analysis (XMLA) 所`Rowset`資料類型，在 XMLA 命令所使用的參數[Execute](../xml-elements-methods-execute.md)方法。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
