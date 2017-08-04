---
title: "TuningOptions 元素 (DTA) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- TuningOptions element
ms.assetid: 58a22ba1-8e03-411f-bd46-85e4540f217a
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c8fcdfd21cdbc923bc92e06aca42c7495f5d35e9
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

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
  
|特性|說明|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|選擇性。 如果使用這個元素的話，每個 **DTAInput** 元素只能使用這個元素一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[DTAInput 元素 &#40; Dta& &#41;](../../tools/dta/dtainput-element-dta.md)|  
|**子元素**|**ReportSet** 元素。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](http://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> **TuningLogTable** 元素。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](http://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> **NumberOfEvents** 元素。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](http://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> [TuningTimeInMin 元素 &#40; Dta& &#41;](../../tools/dta/tuningtimeinmin-element-dta.md)<br /><br /> [StorageBoundInMB 元素 &#40;DTA&#41;](../../tools/dta/storageboundinmb-element-dta.md)<br /><br /> **MaxKeyColumnsInIndex** 元素。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](http://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> **MaxColumnsInIndex** 元素。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](http://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> **MinPercentageImprovement** 元素。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](http://go.microsoft.com/fwlink/?linkid=43100)＞<br /><br /> [TestServer 元素 &#40; Dta& &#41;](../../tools/dta/testserver-element-dta.md)<br /><br /> [FeatureSet 元素 &#40; Dta& &#41;](../../tools/dta/featureset-element-dta.md)<br /><br /> [資料分割元素 &#40; Dta& &#41;](../../tools/dta/partitioning-element-dta.md)<br /><br /> [DropOnlyMode 元素 &#40; Dta& &#41;](../../tools/dta/droponlymode-element-dta.md)<br /><br /> [KeepExisting 元素 &#40; Dta& &#41;](../../tools/dta/keepexisting-element-dta.md)<br /><br /> [OnlineIndexOperation 元素 &#40; Dta& &#41;](../../tools/dta/onlineindexoperation-element-dta.md)<br /><br /> [DatabaseToConnect 元素 &#40;DTA&#41;](../../tools/dta/databasetoconnect-element-dta.md)<br /><br /> **IgnoreConstantsInWorkload** 元素。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](http://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> **RetainShellDB** 元素。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](http://go.microsoft.com/fwlink/?linkid=43100)＞。|  
  
## <a name="example"></a>範例  
 如需 **TuningOptions** 元素的範例，請參閱 [XML 輸入檔範例 &#40;DTA&#41;](../../tools/dta/xml-input-file-samples-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
