---
title: 結果元素 (XMLA) |Microsoft Docs
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
- results Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.results
- urn:schemas-microsoft-com:xml-analysis#results
- http://schemas.microsoft.com/analysisservices/2003/engine#results
helpviewer_keywords:
- results element
ms.assetid: 3249a17a-7bfa-4753-b605-8f611ba7ae2b
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1e42f6aa620b57630df690ee92bdbbd849ab100b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37165229"
---
# <a name="results-element-xmla"></a>results 元素 (XMLA)
  包含的集合[根](root-element-xmla.md)所傳回的項目[Execute](../xml-elements-methods-execute.md)方法使用[批次](../xml-elements-commands/batch-element-xmla.md)命令。  
  
 **命名空間** http://schemas.microsoft.com/analysisservices/2003/xmla-multipleresults  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<return>  
   <results>  
      <root>...</root>  
   </results>  
</return>  
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
|父元素|[傳回](return-element-xmla.md)|  
|子元素|[根目錄](root-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 如果 `Batch` 方法執行了 `Execute` 命令，`return` 元素就會包含單一 `results` 元素，而非單一 `root` 元素。 `results` 元素的內容取決於用來執行 `Batch` 命令的設定。  
  
 若為非交易式 `Batch` 命令，`results` 元素會針對 `root` 命令執行的每個命令包含一個 `Batch` 元素，不論命令成功或未成功完成都一樣。 若為交易式 `Batch` 命令，`results` 元素只會包含一個 `root` 元素，其中包含在 `Batch` 命令內部失敗之命令的錯誤資訊。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
