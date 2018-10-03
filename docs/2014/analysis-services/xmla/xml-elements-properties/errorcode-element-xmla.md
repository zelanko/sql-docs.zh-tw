---
title: ErrorCode 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ErrorCode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#ErrorCode
- microsoft.xml.analysis.errorcode
- http://schemas.microsoft.com/analysisservices/2003/engine#ErrorCode
helpviewer_keywords:
- ErrorCode element
ms.assetid: da187661-b15e-4b95-8b49-7820ebcced40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5a86a27d9eebd0cd683bf58e0a302f1b947f9b9f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48133414"
---
# <a name="errorcode-element-xmla"></a>ErrorCode 元素 (XMLA)
  包含父代的數值傳回碼[錯誤](error-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Error>  
   ...  
   <ErrorCode>...</ErrorCode>  
   ...  
</Error>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|UnsignedInt|  
|預設值|None|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[錯誤](error-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
