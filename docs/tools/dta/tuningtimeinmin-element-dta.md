---
title: TuningTimeInMin 元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- TuningTimeInMin element
ms.assetid: 4973d9ac-20fd-4ac3-bc9f-5d60e39fdb7d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 46d2ff64c5dd91f2e58f57c5f745a37e93efb0f4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47835486"
---
# <a name="tuningtimeinmin-element-dta"></a>TuningTimeInMin 元素 (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  指定微調工作階段的最長時間 (分鐘)。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <TuningTimeInMin>...</TuningTimeInMin>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|Description|  
|--------------------|-----------------|  
|**資料類型和長度**|**unsignedInt**，沒有長度限制。|  
|**預設值**|480 分鐘 (8 小時)。|  
|**出現次數**|除非指定了 **NumberOfEvents** 元素值，否則，需要這個元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素 &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**子元素**|None|  
  
## <a name="example"></a>範例  
  
## <a name="description"></a>Description  
 下列程式碼範例顯示如何設定 12 小時作為最大微調時間：  
  
## <a name="code"></a>程式碼  
  
```  
<DTAInput>  
  <Server>...</Server>  
  <Workload>...</Workload>  
  <TuningOptions>  
    <TuningTimeInMin>720</TuningTimeInMin>  
...code removed here...  
</DTAInput>  
```  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
