---
title: FeatureSet 元素 (DTA)
description: 在 DTA 公用程式中，FeatureSet 元素會包含在分析期間 Database Engine Tuning Advisor 所使用的實體設計結構。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- FeatureSet element
ms.assetid: f2070c53-4a5c-4c11-ac38-96ee200c84f0
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: e7cf111f19344ae1364252d34801677c58326120
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85643869"
---
# <a name="featureset-element-dta"></a>FeatureSet 元素 (DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

包含在分析期間，Database Engine Tuning Advisor 所要使用的實體設計結構 (索引或索引檢視)。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <FeatureSet>...</FeatureSet>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
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
  
  
