---
title: Configuration 元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Configuration element
ms.assetid: 1478e56f-57c4-4441-bac9-1ac91453839b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7a394a390c691b5558b4ecb9036e28d457393b6d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48076644"
---
# <a name="configuration-element-dta"></a>Configuration 元素 (DTA)
  指定由現有的實體設計結構和假設的實體設計結構所組成，供 Database Engine Tuning Advisor 在微調工作負載時進行分析的使用者指定組態。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DTAInput>  
    <Server>...</Server>  
    <Workload>...</Workload>  
    <TuningOptions>...</TuningOptions  
    <Configuration [SpecificationMode="Relative" | "Absolute"]>  
    ...code removed here...  
    </Configuration>  
</DTAInput>  
```  
  
## <a name="element-attributes"></a>元素屬性  
  
|組態屬性|描述|  
|-----------------------------|-----------------|  
|`SpecificationMode`|選擇性。 指定 Database Engine Tuning Advisor 應該關聯於目前現有的組態來分析指定的組態，或將它當作全新的獨立組態來進行分析。 請利用 **string** 資料類型和下列其中一個允許的值，來指定這個屬性：<br /><br /> `Relative`： <br />                  關聯於正在微調的資料庫其中之實體設計結構 (索引、索引檢視、資料分割) 目前現有的組態來評估指定的組態。 例如： <br />`<Configuration SpecificationMode="Relative">`<br /><br /> `Absolute`： <br />                  將指定的組態當作獨立組態來評估。 當指定 Absolute 時，Database Engine Tuning Advisor 不會考慮現有的組態。 例如：<br />`<Configuration SpecificationMode="Absolute">`|  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|選擇性。 可以為每一次使用`DTAInput`項目。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[DTAInput 元素&#40;DTA&#41;](dtainput-element-dta.md)|  
|**子元素**|[組態的 server 元素&#40;DTA&#41;](server-element-for-configuration-dta.md)|  
  
## <a name="example"></a>範例  
 如需此元素的使用範例，請參閱[含使用者指定組態的 XML 輸入檔範例 &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
