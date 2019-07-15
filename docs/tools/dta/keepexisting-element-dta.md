---
title: KeepExisting 元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- KeepExisting element
ms.assetid: e67aae61-d06d-4a03-85ba-6516c3502dce
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: fafd931dd05726285ee505f1d68ca59d28c0c59d
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727638"
---
# <a name="keepexisting-element-dta"></a>KeepExisting 元素 (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  指定在產生建議時，Database Engine Tuning Advisor 必須保留的實體設計結構 (索引、索引檢視或資料分割)。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <KeepExisting>...</KeepExisting>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|Description|  
|--------------------|-----------------|  
|**資料類型和長度**|**string**，伺服器強制實施長度限制。|  
|**允許的值**|**NONE**<br /> 無現有結構。<br /><br /> **ALL**<br /> 所有現有結構。<br /><br /> **ALIGNED**<br /> 所有資料分割對齊結構。<br /><br /> **CL_IDX**<br /> 資料表的所有叢集索引。<br /><br /> **IDX**<br /> 資料表的所有叢集和非叢集索引。<br /><br /> 這個元素只能使用這些值的其中之一。|  
|**預設值**|無。|  
|**出現次數**|選擇性。 每個 **TuningOptions** 元素只能使用這個元素一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素 &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**子元素**|無。|  
  
## <a name="example"></a>範例  
 如需此元素的使用範例，請參閱[簡單 XML 輸入檔範例 &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
