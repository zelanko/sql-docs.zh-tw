---
title: "Parameters 元素 (XMLA) |Microsoft 文件"
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
- Parameters Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Parameters
- urn:schemas-microsoft-com:xml-analysis#Parameters
- microsoft.xml.analysis.parameters
helpviewer_keywords:
- Parameters element
ms.assetid: d46454a1-a1d1-4aa8-95ea-54be22a53e83
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 27bf966c1a1fb44c547a74f38cc3cddd6399793c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="parameters-element-xmla"></a>Parameters 元素 (XMLA)
  包含集合[參數](../../../analysis-services/xmla/xml-elements-properties/parameter-element-xmla.md)元素所使用[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。  
  
 **命名空間：**`urn:schemas-microsoft-com:xml-analysis`  
  
## <a name="syntax"></a>語法  
  
```  
  
<Execute>  
...  
   <Parameters>  
      <Parameter>...</Parameter>  
   </Parameters>  
...  
</Execute>  
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
|父元素|[執行](../../../analysis-services/xmla/xml-elements-methods-execute.md)|  
|子元素|[參數](../../../analysis-services/xmla/xml-elements-properties/parameter-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 某些 XML for Analysis (XMLA) 命令，例如[程序](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)命令，可能需要其他資訊。 **參數**項目會提供一種機制，提供其他資訊，包括區塊的資訊，請為 XMLA 命令。  
  
 如果 XMLA 命令沒有使用**參數**項目，呼叫時，就可以省略此元素**Execute**方法。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

