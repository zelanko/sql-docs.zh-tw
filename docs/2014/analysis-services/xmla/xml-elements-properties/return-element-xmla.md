---
title: return 元素 (XMLA) |Microsoft Docs
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
- return Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.return
- http://schemas.microsoft.com/analysisservices/2003/engine#return
- urn:schemas-microsoft-com:xml-analysis#return
helpviewer_keywords:
- return element
ms.assetid: 3cfe8b74-fec3-4987-a74a-5f731444e024
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4808372fbf80b2b3a79bc11e3f2423511eb717be
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37192400"
---
# <a name="return-element-xmla"></a>return 元素 (XMLA)
  包含所傳回的資訊[DiscoverResponse](../xml-elements-objects-discoverresponse.md)元素為了回應[Discover](../xml-elements-methods-discover.md)方法呼叫或有[ExecuteResponse](../xml-elements-objects-executeresponse.md)元素為了回應[Execute](../xml-elements-methods-execute.md)方法呼叫。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DiscoverResponse> <!-- or ExecuteResponse -->  
   <return>  
      <root>...</root>  
      <!-- or -->  
      <results>...</results> <!-- ExecuteResponse only -->  
   </return>  
</DiscoverResponse>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DiscoverResponse](../xml-elements-objects-discoverresponse.md)， [ExecuteResponse](../xml-elements-objects-executeresponse.md)|  
|上階：[DiscoverResponse](../xml-elements-objects-discoverresponse.md)|子元素： <br />                        [根目錄](root-element-xmla.md)|  
|上階： <br />                        [ExecuteResponse](../xml-elements-objects-executeresponse.md)|子元素：[根](root-element-xmla.md)或[結果](results-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 `return` 元素包含 `Discover` 和 `Execute` 方法所傳回的資料。 一般而言，`return` 元素包含單一 `root` 元素，其中包含 `Discover` 或 `Execute` 方法呼叫成功所傳回的資料或方法呼叫不成功所傳回的 XML for Analysis (XMLA) 例外狀況。 如果 `Execute` 方法包含執行多項作業的 `Batch` 命令，`return` 元素就會包含 `results` 元素，而此元素接著會針對 `root` 命令執行成功或不成功的每個命令包含一個 `Batch` 元素。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
