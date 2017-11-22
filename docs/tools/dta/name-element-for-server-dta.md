---
title: "名稱伺服器 (DTA) 項目 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: Name element
ms.assetid: 4c94754d-6d62-4357-8ce7-f107ebf90c71
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9a5db241528d6fbb75a30af055b6a7682d3e465e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="name-element-for-server-dta"></a>伺服器的 Name 元素 (DTA)
  包含您要微調的資料庫所在的伺服器名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
...code removed here...  
<Server>  
    <Name>...</Name>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|**資料類型和長度**|**string**，在 1 和 255 個字元之間。|  
|**預設值**|無。|  
|**出現次數**|每個 **Server** 元素需要使用這個元素一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[Server 元素 &#40;DTA&#41;](../../tools/dta/server-element-dta.md)|  
|**子元素**|無。|  
  
## <a name="example"></a>範例  
 如需如何使用這個 **Name** 元素的範例，請參閱 [Server 元素 &#40;DTA&#41;](../../tools/dta/server-element-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
