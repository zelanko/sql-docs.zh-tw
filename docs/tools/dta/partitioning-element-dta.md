---
title: "Partitioning 元素 (DTA) |Microsoft 文件"
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
- Partitioning element
ms.assetid: 9bc5d1d5-27a7-4434-966f-c3935794af27
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f1937f32556c442460ee0ed051ae5aed7b14b13b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="partitioning-element-dta"></a>Partitioning 元素 (DTA)
  包含在分析期間，Database Engine Tuning Advisor 所要使用的資料分割配置。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <Partitioning>...</Partitioning>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|**資料類型和長度**|**字串**，沒有最大長度。|  
|**允許的值**|**NONE**<br /> 沒有資料分割。<br /><br /> **FULL**<br /> 完整的資料分割。 (增強效能。)<br /><br /> **ALIGNED**<br /> 只有對齊的資料分割。 (增強管理功能。)<br /><br /> 這個元素只能使用這些值的其中之一。<br /><br /> **ALIGNED** 表示在 Database Engine Tuning Advisor 所產生的建議中，每個提出的索引都完全依照索引定義基礎資料表的相同方式來分割。 索引檢視表中的非叢集索引會對齊索引檢視表。|  
|**預設值**|**NONE**|  
|**出現次數**|**TuningOptions** 元素需要出現一次，除非使用 **DropOnlyMode** 元素。 如果使用 **DropOnlyMode** ，您不能使用 **Partitioning**。 這些元素互斥。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素 &#40; Dta& &#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**子元素**|無。|  
  
## <a name="example"></a>範例  
 如需此元素的使用範例，請參閱[簡單 XML 輸入檔範例 &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  

