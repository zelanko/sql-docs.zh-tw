---
title: ErrorConfiguration 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ErrorConfiguration Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#ErrorConfiguration
- urn:schemas-microsoft-com:xml-analysis#ErrorConfiguration
- microsoft.xml.analysis.errorconfiguration
helpviewer_keywords:
- ErrorConfiguration element
ms.assetid: 5e350f5f-3a14-49b4-80c0-208c61f336d5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 730f48adee4d459c453f49f742f611f6d985771e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48191748"
---
# <a name="errorconfiguration-element-xmla"></a>ErrorConfiguration 元素 (XMLA)
  指定設定期間可能發生之錯誤的處理[批次](../xml-elements-commands/batch-element-xmla.md)或是[程序](../xml-elements-commands/process-element-xmla.md)作業。  
  
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[批次](../xml-elements-commands/batch-element-xmla.md)，[程序](../xml-elements-commands/process-element-xmla.md)|  
|子元素|[KeyDuplicate](../../scripting/properties/keyduplicate-element-assl.md)， [KeyErrorAction](../../scripting/objects/action-element-assl.md)， [KeyErrorLimit](../../scripting/properties/keyerrorlimit-element-assl.md)， [KeyErrorLimitAction](../../scripting/properties/keyerrorlimitaction-element-assl.md)， [KeyErrorLogFile](../../scripting/objects/file-element-assl.md)， [KeyNotFound](../../scripting/properties/keynotfound-element-assl.md)， [NullKeyConvertedToUnknown](../../scripting/properties/nullkeyconvertedtounknown-element-assl.md)， [NullKeyNotAllowed](../../scripting/properties/nullkeynotallowed-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 這個元素的結構與「Analysis Services 指令碼語言」(ASSL) 中 `ErrorConfiguration` 元素的結構完全相同。  如需詳細資訊`ErrorConfiguration`項目，請參閱 < [ErrorConfiguration 元素&#40;ASSL&#41;](../../scripting/objects/errorconfiguration-element-assl.md)。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
