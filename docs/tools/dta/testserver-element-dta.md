---
title: "TestServer 元素 (DTA) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: dta
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: TestServer element
ms.assetid: caa3547a-2cd5-47ad-ace2-a36752835cfe
caps.latest.revision: "11"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8b0d3bce0b200207f12527b639d259a723ececa7
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="testserver-element-dta"></a>TestServer 元素 (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]指定測試伺服器微調實際伺服器時使用。  
  
## <a name="syntax"></a>語法  
  
```  
  
<TuningOptions>  
  <TestServer>...</TestServer>  
   ...code removed here...  
</TuningOptions>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|**資料類型和長度**|**string**，沒有長度限制。|  
|**預設值**|無。|  
|**出現次數**|選擇性。 每個 **TuningOptions** 元素可以使用這個元素一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素 &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**子元素**|無。|  
  
## <a name="example"></a>範例  
 如需此元素的使用範例，請參閱 [降低生產伺服器的微調負載](../../relational-databases/performance/reduce-the-production-server-tuning-load.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
