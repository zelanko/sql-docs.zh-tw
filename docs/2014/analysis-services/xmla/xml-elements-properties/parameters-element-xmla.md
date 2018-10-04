---
title: Parameters 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Parameters Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Parameters
- urn:schemas-microsoft-com:xml-analysis#Parameters
- microsoft.xml.analysis.parameters
helpviewer_keywords:
- Parameters element
ms.assetid: d46454a1-a1d1-4aa8-95ea-54be22a53e83
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3b9c3d0d642ad7248d87e7cc17aaa17953bf6aec
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48134048"
---
# <a name="parameters-element-xmla"></a>Parameters 元素 (XMLA)
  包含的集合[參數](parameter-element-xmla.md)所使用的項目[Execute](../xml-elements-methods-execute.md)方法。  
  
 **命名空間：** `urn:schemas-microsoft-com:xml-analysis`  
  
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[執行](../xml-elements-methods-execute.md)|  
|子元素|[參數](parameter-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 某些 XML for Analysis (XMLA) 命令，例如[程序](../xml-elements-commands/process-element-xmla.md)命令，可能需要其他資訊。 `Parameters` 元素會提供一項機制，讓您提供其他資訊 (包括區塊資訊) 給 XMLA 命令。  
  
 如果 XMLA 命令並未使用 `Parameters` 元素，在呼叫 `Execute` 方法時就可以省略此元素。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
