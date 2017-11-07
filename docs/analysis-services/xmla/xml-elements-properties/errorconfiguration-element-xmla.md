---
title: "ErrorConfiguration 元素 (XMLA) |Microsoft 文件"
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
- ErrorConfiguration Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#ErrorConfiguration
- urn:schemas-microsoft-com:xml-analysis#ErrorConfiguration
- microsoft.xml.analysis.errorconfiguration
helpviewer_keywords:
- ErrorConfiguration element
ms.assetid: 5e350f5f-3a14-49b4-80c0-208c61f336d5
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 03107ab82e9190ae1e6860af8d13da589c05766e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="errorconfiguration-element-xmla"></a>ErrorConfiguration 元素 (XMLA)
  指定期間可能發生的錯誤處理設定[批次](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)或[程序](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)作業。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Batch> <!-- or Process -->  
   ...  
   <ErrorConfiguration>  
      <KeyErrorLimit>...</KeyErrorLimit>  
      <KeyErrorLogFile>...</KeyErrorLogFile>  
      <KeyErrorAction>...</KeyErrorAction>  
      <KeyErrorLimitAction>...</KeyErrorLimitAction>  
      <KeyNotFound>...</KeyNotFound>  
      <KeyDuplicate>...</KeyDuplicate>  
      <NullKeyConvertedToUnknown>...</NullKeyConvertedToUnknown>  
      <NullKeyNotAllowed>...<NullKeyNotAllowed>  
   </ErrorConfiguration>  
   ...  
</Batch>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[批次](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)，[程序](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
|子元素|[KeyDuplicate](../../../analysis-services/scripting/properties/keyduplicate-element-assl.md)， [KeyErrorAction](../../../analysis-services/scripting/properties/keyerroraction-element-assl.md)， [KeyErrorLimit](../../../analysis-services/scripting/properties/keyerrorlimit-element-assl.md)， [KeyErrorLimitAction](../../../analysis-services/scripting/properties/keyerrorlimitaction-element-assl.md)， [KeyErrorLogFile](../../../analysis-services/scripting/properties/keyerrorlogfile-element-assl.md)， [KeyNotFound](../../../analysis-services/scripting/properties/keynotfound-element-assl.md)， [NullKeyConvertedToUnknown](../../../analysis-services/scripting/properties/nullkeyconvertedtounknown-element-assl.md)， [NullKeyNotAllowed](../../../analysis-services/scripting/properties/nullkeynotallowed-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 這個項目之結構是相同的結構**ErrorConfiguration**項目在 Analysis Services 指令碼語言 (ASSL)。 如需有關**ErrorConfiguration**項目，請參閱[ErrorConfiguration 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md).  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

