---
title: TuningOptions 元素 (DTA)
description: 在 dta 公用程式中，TuningOptions 元素包含特定調整工作階段的調整選項。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- TuningOptions element
ms.assetid: 58a22ba1-8e03-411f-bd46-85e4540f217a
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: e23ba0eef792e64a9f2b8d6e6f95ec1b793b71fc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774976"
---
# <a name="tuningoptions-element-dta"></a>TuningOptions 元素 (DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
|**出現次數**|選擇性。 如果使用這個元素的話，每個 **DTAInput** 元素只能使用這個元素一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[DTAInput 元素 &#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)|  
|**子元素**|**ReportSet** 元素。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](https://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> **TuningLogTable** 元素。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](https://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> **NumberOfEvents** 元素。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](https://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> [TuningTimeInMin 元素 &#40;DTA&#41;](../../tools/dta/tuningtimeinmin-element-dta.md)<br /><br /> [StorageBoundInMB 元素 &#40;DTA&#41;](../../tools/dta/storageboundinmb-element-dta.md)<br /><br /> **MaxKeyColumnsInIndex** 元素。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](https://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> **MaxColumnsInIndex** 元素。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](https://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> **MinPercentageImprovement** 元素。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](https://go.microsoft.com/fwlink/?linkid=43100)＞<br /><br /> [TestServer 元素 &#40;DTA&#41;](../../tools/dta/testserver-element-dta.md)<br /><br /> [FeatureSet 元素 &#40;DTA&#41;](../../tools/dta/featureset-element-dta.md)<br /><br /> [Partitioning 元素 &#40;DTA&#41;](../../tools/dta/partitioning-element-dta.md)<br /><br /> [DropOnlyMode 元素 &#40;DTA&#41;](../../tools/dta/droponlymode-element-dta.md)<br /><br /> [KeepExisting 元素 &#40;DTA&#41;](../../tools/dta/keepexisting-element-dta.md)<br /><br /> [OnlineIndexOperation 元素 &#40;DTA&#41;](../../tools/dta/onlineindexoperation-element-dta.md)<br /><br /> [DatabaseToConnect 元素 &#40;DTA&#41;](../../tools/dta/databasetoconnect-element-dta.md)<br /><br /> **IgnoreConstantsInWorkload** 元素。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](https://go.microsoft.com/fwlink/?linkid=43100)＞。<br /><br /> **RetainShellDB** 元素。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](https://go.microsoft.com/fwlink/?linkid=43100)＞。|  
  
## <a name="example"></a>範例  
 如需 **TuningOptions** 元素的範例，請參閱 [XML 輸入檔範例 &#40;DTA&#41;](../../tools/dta/xml-input-file-samples-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
