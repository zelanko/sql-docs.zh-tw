---
title: Configuration 元素 (DTA) |Microsoft 文件
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Configuration element
ms.assetid: 1478e56f-57c4-4441-bac9-1ac91453839b
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e9e3fbf76ffab1eea6baf7ea5cc8d2f6972379a5
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="configuration-element-dta"></a>Configuration 元素 (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]指定使用者指定組態的 Database Engine Tuning Advisor 微調工作負載時進行分析的現有與假設實體設計結構所組成。  
  
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
  
|組態屬性|Description|  
|-----------------------------|-----------------|  
|**SpecificationMode**|選擇性。 指定 Database Engine Tuning Advisor 應該關聯於目前現有的組態來分析指定的組態，或將它當作全新的獨立組態來進行分析。 請利用 **string** 資料類型和下列其中一個允許的值，來指定這個屬性：<br /><br /> **Relative**：<br />                  關聯於正在微調的資料庫其中之實體設計結構 (索引、索引檢視、資料分割) 目前現有的組態來評估指定的組態。 例如：<br /><br /> `<Configuration SpecificationMode="Relative">`<br /><br /> **Absolute**：<br />                  將指定的組態當作獨立組態來評估。 當指定 Absolute 時，Database Engine Tuning Advisor 不會考慮現有的組態。 例如：<br /><br /> `<Configuration SpecificationMode="Absolute">`|  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|選擇性。 每個 **DTAInput** 元素可以使用這個元素一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[DTAInput 元素 &#40; Dta& &#41;](../../tools/dta/dtainput-element-dta.md)|  
|**子元素**|[伺服器項目組態 &#40; Dta& &#41;](../../tools/dta/server-element-for-configuration-dta.md)|  
  
## <a name="example"></a>範例  
 如需此元素的使用範例，請參閱[含使用者指定組態的 XML 輸入檔範例 &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
