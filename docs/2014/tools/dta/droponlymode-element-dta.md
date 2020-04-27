---
title: DropOnlyMode 元素（DTA） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DropOnlyMode element
ms.assetid: 80960676-7581-4074-889b-80ee665963dd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f1d449defa98112c87a4b5789f1cff6f764252e3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62659572"
---
# <a name="droponlymode-element-dta"></a>DropOnlyMode 元素 (DTA)
  指定在微調工作階段期間，Database Engine Tuning Advisor 只應考慮卸除現有的索引、索引檢視或資料分割。 當指定這個微調選項時，不考慮任何新的實體設計結構。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <DropOnlyMode>...</DropOnlyMode>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**次出現**|選擇性。 每個 `TuningOptions` 元素只能使用這個元素一次。 如果在 `TuningOptions` 元素中指定了下列元素，就不能使用這個元素：<br /><br /> [FeatureSet 元素 &#40;DTA&#41;](featureset-element-dta.md)<br /><br /> [Partitioning 元素 &#40;DTA&#41;](partitioning-element-dta.md)<br /><br /> [KeepExisting 元素 &#40;DTA&#41;](keepexisting-element-dta.md) 設為 **ALL**|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素 &#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**子元素**|無。|  
  
## <a name="example"></a>範例  
 下列範例顯示指定了 `TuningOptions` 的 Database Engine Tuning Advisor XML 輸入檔的 `DropOnlyMode` 區段。 在這個範例中，微調時間只限 24 小時 (1440 分鐘)，所有現有的叢集和非叢集索引都將考慮卸除：  
  
```xml  
<TuningOptions  
  <TuningTimeInMin>1440</Name>  
  <KeepExisting>ALIGNED</KeepExisting>  
  <DropOnlyMode />  
</TuningOptions>  
```  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
