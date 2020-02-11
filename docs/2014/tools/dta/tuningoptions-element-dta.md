---
title: TuningOptions 元素（DTA） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- TuningOptions element
ms.assetid: 58a22ba1-8e03-411f-bd46-85e4540f217a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3050ce285cc98386f6de6278bedd2520cb39ba36
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63061062"
---
# <a name="tuningoptions-element-dta"></a>TuningOptions 元素 (DTA)
  包含特定微調工作階段的微調選項。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DTAInput>  
    <Server>  
...code removed...  
    <Workload>...</Workload>  
    <TuningOptions>...</TuningOptions>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|選擇性。 如果使用這個元素的話，每個 `DTAInput` 元素只能使用這個元素一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[DTAInput 元素 &#40;DTA&#41;](dtainput-element-dta.md)|  
|**子元素**|`ReportSet`元素. 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](https://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> `TuningLogTable`元素. 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](https://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> `NumberOfEvents`元素. 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](https://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> [TuningTimeInMin 元素 &#40;DTA&#41;](tuningtimeinmin-element-dta.md)<br /><br /> [StorageBoundInMB 元素 &#40;DTA&#41;](storageboundinmb-element-dta.md)<br /><br /> `MaxKeyColumnsInIndex`元素. 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](https://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> `MaxColumnsInIndex`元素. 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](https://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> `MinPercentageImprovement`元素. 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](https://go.microsoft.com/fwlink/?linkid=43100)＞<br /><br /> [TestServer 元素 &#40;DTA&#41;](server-element-dta.md)<br /><br /> [FeatureSet 元素 &#40;DTA&#41;](featureset-element-dta.md)<br /><br /> [Partitioning 元素 &#40;DTA&#41;](partitioning-element-dta.md)<br /><br /> [DropOnlyMode 元素 &#40;DTA&#41;](droponlymode-element-dta.md)<br /><br /> [KeepExisting 元素 &#40;DTA&#41;](keepexisting-element-dta.md)<br /><br /> [OnlineIndexOperation 元素 &#40;DTA&#41;](onlineindexoperation-element-dta.md)<br /><br /> [DatabaseToConnect 元素 &#40;DTA&#41;](databasetoconnect-element-dta.md)<br /><br /> `IgnoreConstantsInWorkload`元素. 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](https://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> `RetainShellDB`元素. 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](https://go.microsoft.com/fwlink/?linkid=43100)＞。|  
  
## <a name="example"></a>範例  
 如需`TuningOptions`元素的範例，請參閱[&#40;DTA&#41;的 XML 輸入檔範例](xml-input-file-samples-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
