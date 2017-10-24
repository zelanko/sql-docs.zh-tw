---
title: "StorageBoundInMB 元素 (DTA) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- StorageBoundInMB element
ms.assetid: a8374910-bf68-4edb-b464-53a3a705e7f4
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9be01bd27f8a3ad4a878e8b5340f2a4e0aead79e
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="storageboundinmb-element-dta"></a>StorageBoundInMB 元素 (DTA)
  指定 Database Engine Tuning Advisor 微調建議 (索引和資料分割集) 所能取用的最大空間 (MB)。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <StorageBoundInMB>...</ StorageBoundInMB >  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|**資料類型和長度**|**unsignedInt**，沒有長度限制。|  
|**預設值**|無。|  
|**出現次數**|選擇性。 **TuningOptions** 元素只能使用這個元素一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素 &#40; Dta& &#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**子元素**|無|  
  
## <a name="remarks"></a>備註  
 微調多個資料庫時，所有資料庫的建議內容都考量了空間的計算。 依預設，Database Engine Tuning Advisor 會採用下列中較小的儲存體大小：  
  
-   目前的原始資料大小的三倍，其中包括各資料表的堆積和叢集索引的總大小。  
  
-   所有相連硬碟的可用空間，加上原始資料大小。  
  
 預設儲存體大小不包括非叢集索引和索引檢視。  
  
 如果指定給 **StorageBoundInMB** 元素的值超出實際的磁碟大小，Database Engine Tuning Advisor 會傳回錯誤，但會繼續微調。 微調完成之後，如果您決定實作建議，您可以增加磁碟空間。  
  
## <a name="example"></a>範例  
  
## <a name="description"></a>說明  
 下列程式碼範例顯示如何將 1500 MB 的限制設為微調建議所能取用的最大磁碟空間：  
  
## <a name="code"></a>程式碼  
  
```  
<DTAInput>  
  <Server>...</Server>  
  <Workload>...</Workload>  
  <TuningOptions>  
    <StorageBoundInMB>1500</StorageBoundInMB>  
...code removed here...  
</DTAInput>  
```  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  

