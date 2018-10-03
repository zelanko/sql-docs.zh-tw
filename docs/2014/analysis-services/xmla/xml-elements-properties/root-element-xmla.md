---
title: root 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Root Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#root
- urn:schemas-microsoft-com:xml-analysis#root
- microsoft.xml.analysis.root
helpviewer_keywords:
- root element
ms.assetid: ecd9d6e8-b16c-4d62-9a87-107c413a0056
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 610ef2a3b332ec59e6ddf31d7f30acfe418549e5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48110248"
---
# <a name="root-element-xmla"></a>root 元素 (XMLA)
  包含所傳回的結果[Discover](../xml-elements-methods-discover.md)方法或 XML for Analysis (XMLA) 命令，使用執行[Execute](../xml-elements-methods-execute.md)方法。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<return> <!-- or results-->  
   ...  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">...</root> <!-- for Execute method only -->  
   <!-- or -->  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">...</root>  
   <!-- or -->  
   <root xmlns= xmlns="urn:schemas-microsoft-com:xml-analysis:empty">...</root>  
   ...  
</return>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|預設值|None|  
|基數|1-n：出現一次以上的必要元素。|  
  
## <a name="data-type-and-length"></a>資料類型和長度  
  
|Ancestor|資料類型|  
|--------------|---------------|  
|[DiscoverResponse](../xml-data-types/rowset-data-type-xmla.md)， [olapxmla_EmptyResult](../xml-data-types/emptyresult-data-type-xmla.md)|  
|[ExecuteResponse](../xml-data-types/mddataset-data-type-xmla.md)，[資料列集](../xml-data-types/rowset-data-type-xmla.md)， [olapxmla_EmptyResult](../xml-data-types/emptyresult-data-type-xmla.md)|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[結果](results-element-xmla.md)，[傳回](return-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 `root`項目包含在傳回的資訊[DiscoverResponse](../xml-elements-objects-discoverresponse.md)傳回單一項目`Discover`方法呼叫，或是在[ExecuteResponse](../xml-elements-objects-executeresponse.md)項目執行由單一的單一 XMLA 命令所傳回`Execute`方法呼叫。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
