---
title: Partitioning 元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Partitioning element
ms.assetid: 9bc5d1d5-27a7-4434-966f-c3935794af27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: acf6d033595952186b411ef0e547858f8b59771b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62657233"
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
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|`string`，沒有最大長度。|  
|**允許的值**|**NONE**<br /> 沒有資料分割。<br /><br /> **FULL**<br /> 完整的資料分割。 (增強效能。)<br /><br /> **ALIGNED**<br /> 只有對齊的資料分割。 (增強管理功能。)<br /><br /> 這個元素只能使用這些值的其中之一。<br /><br /> **ALIGNED** 表示在 Database Engine Tuning Advisor 所產生的建議中，每個提出的索引都完全依照索引定義基礎資料表的相同方式來分割。 索引檢視表中的非叢集索引會對齊索引檢視表。|  
|**預設值**|**NONE**|  
|**出現次數**|除非使用 `TuningOptions` 元素，否則，`DropOnlyMode` 元素需要使用這個元素一次。 如果使用 `DropOnlyMode`，您便無法使用 `Partitioning`。 這些元素互斥。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素 &#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**子元素**|無。|  
  
## <a name="example"></a>範例  
 如需此元素的使用範例，請參閱[簡單 XML 輸入檔範例 &#40;DTA&#41;](simple-xml-input-file-sample-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
