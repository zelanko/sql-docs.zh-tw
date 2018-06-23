---
title: Parameters 元素 (XMLA) |Microsoft 文件
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
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 63d50c1b57691a9b4cdb76adb9edaa202388d15e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037753"
---
# <a name="parameters-element-xmla"></a>Parameters 元素 (XMLA)
  包含集合[參數](parameter-element-xmla.md)元素所使用[Execute](../xml-elements-methods-execute.md)方法。  
  
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
|資料類型和長度|無|  
|預設值|無|  
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
  
  