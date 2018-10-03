---
title: TuningOptions 元素 (DTA) |Microsoft Docs
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
- TuningOptions element
ms.assetid: 58a22ba1-8e03-411f-bd46-85e4540f217a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a4630640d2d61685accdb26031b87aff2883b644
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48065838"
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
|**出現次數**|選擇性。 如果使用，可以只使用一次針對每個`DTAInput`項目。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[DTAInput 元素&#40;DTA&#41;](dtainput-element-dta.md)|  
|**子元素**|`ReportSet` 項目。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](http://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> `TuningLogTable` 項目。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](http://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> `NumberOfEvents` 項目。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](http://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> [TuningTimeInMin 元素&#40;DTA&#41;](tuningtimeinmin-element-dta.md)<br /><br /> [StorageBoundInMB 元素&#40;DTA&#41;](storageboundinmb-element-dta.md)<br /><br /> `MaxKeyColumnsInIndex` 項目。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](http://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> `MaxColumnsInIndex` 項目。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](http://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> `MinPercentageImprovement` 項目。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](http://go.microsoft.com/fwlink/?linkid=43100)＞<br /><br /> [TestServer 元素&#40;DTA&#41;](server-element-dta.md)<br /><br /> [FeatureSet 元素&#40;DTA&#41;](featureset-element-dta.md)<br /><br /> [Partitioning 元素&#40;DTA&#41;](partitioning-element-dta.md)<br /><br /> [DropOnlyMode 元素&#40;DTA&#41;](droponlymode-element-dta.md)<br /><br /> [KeepExisting 元素&#40;DTA&#41;](keepexisting-element-dta.md)<br /><br /> [OnlineIndexOperation 元素&#40;DTA&#41;](onlineindexoperation-element-dta.md)<br /><br /> [DatabaseToConnect 元素&#40;DTA&#41;](databasetoconnect-element-dta.md)<br /><br /> `IgnoreConstantsInWorkload` 項目。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](http://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> `RetainShellDB` 項目。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](http://go.microsoft.com/fwlink/?linkid=43100)＞。|  
  
## <a name="example"></a>範例  
 如需的範例`TuningOptions`項目，請參閱 < [XML 輸入檔範例&#40;DTA&#41;](xml-input-file-samples-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
