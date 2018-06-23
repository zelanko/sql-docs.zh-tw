---
title: root 元素 (XMLA) |Microsoft 文件
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
caps.latest.revision: 16
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 481947e1d58fe5da34b29f43405bfff48583b8c9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133777"
---
# <a name="root-element-xmla"></a>root 元素 (XMLA)
  包含所傳回的結果[探索](../xml-elements-methods-discover.md)方法或 XML for Analysis (XMLA) 命令，使用執行[Execute](../xml-elements-methods-execute.md)方法。  
  
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
|預設值|無|  
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
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `root`項目包含在傳回的資訊[DiscoverResponse](../xml-elements-objects-discoverresponse.md)傳回單一項目`Discover`方法呼叫，或在[ExecuteResponse](../xml-elements-objects-executeresponse.md)項目所執行的是單一的單一 XMLA 命令傳回`Execute`方法呼叫。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  