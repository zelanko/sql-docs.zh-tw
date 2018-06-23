---
title: Exception 元素 (XMLA) |Microsoft 文件
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
- Exception Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Exception
- urn:schemas-microsoft-com:xml-analysis#Exception
- microsoft.xml.analysis.exception
helpviewer_keywords:
- Exception element
ms.assetid: 0be4cc2f-c03e-490a-a6f7-8b1ede5d09ba
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 824743a3e8aeb7d735d6844dd1b025de06e09e9d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033959"
---
# <a name="exception-element-xmla"></a>Exception 元素 (XMLA)
  表示例外狀況傳回從[探索](../xml-elements-methods-discover.md)或[Execute](../xml-elements-methods-execute.md)方法呼叫。  
  
 **命名空間** http://schemas.microsoft.com/analysisservices/2003/exception  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<root>  
   ...  
   <Exception />  
   ...  
</root>  
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
|父元素|[根](root-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如果在執行 `Discover` 方法呼叫或 `Execute` 方法呼叫中的單一 XMLA 命令期間發生讓方法或命令無法完成的錯誤，該命令或方法的 `root` 元素就會包含 `Exception` 元素和 `Messages` 元素。 `Exception` 元素表示發生了讓方法或命令無法順利執行的錯誤，而 `Messages` 元素則包含與錯誤相關的錯誤或警告訊息清單。  
  
## <a name="see-also"></a>另請參閱  
 [郵件項目&#40;XMLA&#41;](messages-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  