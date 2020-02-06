---
title: DropOnlyMode 元素 (DTA)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DropOnlyMode element
ms.assetid: 80960676-7581-4074-889b-80ee665963dd
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: a0cd0d9511e3a2791231f1cfa39aa4c8e5999eec
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75305595"
---
# <a name="droponlymode-element-dta"></a>DropOnlyMode 元素 (DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

指定在微調工作階段期間，Database Engine Tuning Advisor 只應考慮卸除現有的索引、索引檢視或資料分割。 當指定這個微調選項時，不考慮任何新的實體設計結構。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <DropOnlyMode>...</DropOnlyMode>  
```  
  
## <a name="element-characteristics"></a>元素特性  
 **資料類型和長度**  
  
 **預設值**  
  
 **出現次數**︰選擇性。 每個 **TuningOptions** 元素只能使用這個元素一次。 如果在 **TuningOptions** 元素中指定了下列元素，就不能使用這個元素：  
  
-   [FeatureSet 元素 &#40;DTA&#41;](../../tools/dta/featureset-element-dta.md)  
  
-   [Partitioning 元素 &#40;DTA&#41;](../../tools/dta/partitioning-element-dta.md)  
  
-   [KeepExisting 元素 &#40;DTA&#41;](../../tools/dta/keepexisting-element-dta.md) 設為 **ALL**  
  
## <a name="element-relationships"></a>元素關聯性  
 **父元素**：[TuningOptions 元素 &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)  
  
 **子元素**  
  
## <a name="example"></a>範例  
 下例顯示指定 **DropOnlyMode** 之 Database Engine Tuning Advisor XML 輸入檔的 **TuningOptions** 區段。 在這個範例中，微調時間只限 24 小時 (1440 分鐘)，所有現有的叢集和非叢集索引都將考慮卸除：  
  
```xml  
<TuningOptions  
  <TuningTimeInMin>1440</Name>  
  <KeepExisting>ALIGNED</KeepExisting>  
  <DropOnlyMode />  
</TuningOptions>  
```  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
