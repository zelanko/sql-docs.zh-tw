---
title: "Resultset 資料類型 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Resultset Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Resultset
- urn:schemas-microsoft-com:xml-analysis#Resultset
- Resultset
helpviewer_keywords:
- Resultset data type
ms.assetid: 45e7d7d6-1f89-4dc8-b39d-9270ea2db541
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 30d8923c5e3e84c3e2f835caf160902c96c9bf4d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="resultset-data-type-xmla"></a>Resultset 資料類型 (XMLA)
  定義表示從傳回的資料的抽象基本資料類型[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)或[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法呼叫。  
  
 **命名空間**描述 urn:-microsoft-schemas-microsoft-com:-xml-analysis: resultset  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Resultset>  
   <Exception>...</Exception>  
   <Messages>...</Messages>  
</Resultset>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)， [olapxmla_EmptyResult](../../../analysis-services/xmla/xml-data-types/emptyresult-data-type-xmla.md)，[資料列集](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md)|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[例外狀況](../../../analysis-services/xmla/xml-elements-properties/exception-element-xmla.md)，[訊息](../../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md)|  
|衍生的元素|無|  
  
## <a name="remarks"></a>備註  
 **Resultset**資料類型是結構描述和資料，取決於要傳回資訊的類型可以包含自我描述 XML 結果集。  
  
## <a name="see-also"></a>另請參閱  
 [XML 資料類型 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)  
  
  

