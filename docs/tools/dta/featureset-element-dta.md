---
title: FeatureSet 元素 (DTA) |Microsoft Docs
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
- FeatureSet element
ms.assetid: f2070c53-4a5c-4c11-ac38-96ee200c84f0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 24e136b862956d6862e2cfa998ff529a27c02595
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47839746"
---
# <a name="featureset-element-dta"></a>FeatureSet 元素 (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  包含在分析期間，Database Engine Tuning Advisor 所要使用的實體設計結構 (索引或索引檢視)。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <FeatureSet>...</FeatureSet>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|Description|  
|--------------------|-----------------|  
|**資料類型和長度**|**字串**，沒有最大長度。|  
|**允許的值**|**IDX_IV**<br /> 索引和索引檢視表。<br /><br /> **IDX**<br /> 只有索引。<br /><br /> **IV**<br /> 只有索引檢視表。<br /><br /> **NCL_IDX**<br /> 只有非叢集索引。<br /><br /> 這個元素使用這些值的其中之一。|  
|**預設值**|**IDX**|  
|**出現次數**|每個 **TuningOptions** 元素都需要一次，除非使用 **DropOnlyMode** 元素。 如果使用 **DropOnlyMode** ，您不能使用 **FeatureSet**。 這些元素互斥。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素 &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**子元素**|無。|  
  
## <a name="example"></a>範例  
 如需此元素的使用範例，請參閱[簡單 XML 輸入檔範例 &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
