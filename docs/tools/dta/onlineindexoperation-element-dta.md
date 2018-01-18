---
title: "OnlineIndexOperation 元素 (DTA) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: dta
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: OnlineIndexOperation element
ms.assetid: 7c5614cd-09aa-4a59-9591-347aa7d36473
caps.latest.revision: "13"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 399763df5f0ee05db8d0058bf70f146873119952
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="onlineindexoperation-element-dta"></a>OnlineIndexOperation 元素 (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]指定是否索引、 索引檢視表或 Database Engine Tuning Advisor 建議的資料分割可以在線上建立。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <OnlineIndexOperation>...</OnlineIndexOperation>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|**資料類型和長度**|**字串**，沒有最大長度。|  
|**允許的值**|**OFF**<br /> 不能在線上建立任何建議的實體設計結構。<br /><br /> **ON**<br /> 可以在線上建立所有建議的實體設計結構。<br /><br /> **MIXED**<br /> Database Engine Tuning Advisor 嘗試建議在可能的情況下，能夠在線上建立的實體設計結構。<br /><br /> 這個元素使用這些值的其中之一。 如果在線上建立索引，就會在它的物件定義上附加關鍵字 **ONLINE = ON** 。|  
|**預設值**|無。|  
|**出現次數**|選擇性。 如果使用這個元素的話， **TuningOptions** 元素只能使用這個元素一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素 &#40; Dta& &#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**子元素**|無。|  
  
## <a name="example"></a>範例  
 如需此元素的使用範例，請參閱[簡單 XML 輸入檔範例 &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
