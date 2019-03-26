---
title: 單一資料表快速分析表單 (資料分析工作) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataprofilingtask.quickprofile.f1
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: d2fac9ce-730e-474e-961a-69406b633778
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 74bfa46a09968549ef8b11dd21230f8da2e7714f
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58274128"
---
# <a name="single-table-quick-profile-form-data-profiling-task"></a>單一資料表快速分析表單 (資料分析工作)
  您可以使用 **[單一資料表快速分析表單]** 來快速地設定資料分析工作，以便使用預設設定分析單一資料表或檢視表。  
  
 如需如何使用資料分析工作的詳細資訊，請參閱 [資料分析工作的設定](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)。 如需如何使用資料設定檔檢視器來分析資料分析工作輸出的詳細資訊，請參閱 [資料設定檔檢視器](../../integration-services/control-flow/data-profile-viewer.md)。  
  
## <a name="options"></a>選項。  
 **[連接]**  
 選取現有的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員，以便使用 .NET Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) 來連接至包含要分析之資料表或檢視表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。  
  
 **[資料表或檢視表]**  
 選取選定連接管理員所連接之資料庫中的現有資料表或檢視表。  
  
 **計算**  
 選取要計算的設定檔。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**資料行 Null 比例設定檔**|使用選取之資料表或檢視表中所有適用資料行的預設設定來計算資料行 Null 比例設定檔。<br /><br /> 這個設定檔會報告選取之資料行中 Null 值的百分比。 這個設定檔可協助您識別資料中的問題，例如某個資料行中 Null 值的比例過高。 如需設定此設定檔的詳細資訊，請參閱[資料行 Null 比例設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/column-null-ratio-profile-request-options-data-profiling-task.md)。|  
|**資料行統計資料設定檔**|使用選取之資料表或檢視表中所有適用資料行的預設設定來計算資料行統計資料設定檔。<br /><br /> 這個設定檔會報告數值資料行的最小值、最大值、平均和標準差，以及 **datetime** 資料行的最小值和最大值等統計資料。 這個設定檔可協助您識別資料中的問題，例如無效的日期。 如需設定此設定檔的詳細資訊，請參閱[資料行統計資料設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/column-statistics-profile-request-options-data-profiling-task.md)。|  
|**資料行值散發設定檔**|使用選取之資料表或檢視表中所有適用資料行的預設設定來計算資料行值散發設定檔。<br /><br /> 這個設定檔會報告選取之資料行中的所有相異值，以及該資料表中每個值所代表之資料列的百分比。 這個設定檔也可以報告代表超過資料表中指定之資料列百分比的值。 這個設定檔可協助您識別資料中的問題，例如某個資料行中相異值的數目不正確。 如需此設定檔的詳細資訊，請參閱[資料行值散發設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/column-value-distribution-profile-request-options-data-profiling-task.md)。|  
|**資料行長度散發設定檔**|使用選取之資料表或檢視表中所有適用資料行的預設設定來計算資料行長度散發設定檔。<br /><br /> 這個設定檔會報告選取之資料行中字串值的所有相異長度，以及該資料表中每個長度所代表之資料列的百分比。 這個設定檔可協助您識別資料中的問題，例如無效的值。 如需設定此設定檔的詳細資訊，請參閱[資料行長度散發設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/column-length-distribution-profile-request-options-data-profiling-task.md)。|  
|**資料行模式設定檔**|使用選取之資料表或檢視表中所有適用資料行的預設設定來計算資料行模式設定檔。<br /><br /> 這個設定檔會報告一組規則運算式，其中涵蓋了字串資料行中的值。 這個設定檔可協助您識別資料中的問題，例如無效的字串。 這個設定檔也可以建議未來可用於驗證新值的規則運算式。 如需設定此設定檔的詳細資訊，請參閱[資料行模式設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/column-pattern-profile-request-options-data-profiling-task.md)。|  
|**候選索引鍵設定檔**|針對包含最多可達到在 **[最多可達 N 個資料行索引鍵]** 中指定之資料行數目的資料行組合，計算候選索引鍵設定檔。<br /><br /> 這個設定檔會報告資料行或資料行集合是否適合當做選取之資料表的索引鍵。 這個設定檔也可協助您識別資料中的問題，例如潛在索引鍵資料行中重複的值。 如需設定此設定檔的詳細資訊，請參閱[候選索引鍵設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/candidate-key-profile-request-options-data-profiling-task.md)。|  
|**[最多可達 N 個資料行索引鍵]**|選取要在可能的組合中當做資料表或檢視表之索引鍵進行測試的資料行數目上限。 預設值是 1。 最大值為 1000。 例如，選取 3 種測試：一個資料行、兩個資料行和三個資料行的索引鍵組合。|  
|**功能相依性設定檔**|針對包含最多可達到在 **[最多可達 N 個資料行當做行列式資料行]** 中指定之資料行數目的行列式資料行組合，計算功能相依性設定檔。<br /><br /> 這個設定檔會報告某個資料行 (相依資料行) 中的值相依於另一個資料行或資料行集合 (行列式資料行) 中之值的程度。 這個設定檔也可協助您識別資料中的問題，例如無效的值。 如需設定此設定檔的詳細資訊，請參閱[功能相依性設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/functional-dependency-profile-request-options-data-profiling-task.md)。|  
|**[最多可達 N 個資料行當做行列式資料行]**|選取要在可能的組合中當做行列式資料行進行測試的資料行數目上限。 預設值是 1。 最大值為 1000。 ˥Ƃ，選取 2 種測試組合，其中單一資料行或兩個資料行組合是另一個 (相依) 資料行的行列式資料行。|  
  
> [!NOTE]  
>  您無法在 [單一資料表快速分析表單] 中使用值包含設定檔類型。  
  
## <a name="see-also"></a>另請參閱  
 [資料分析工作編輯器 &#40;一般頁面&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [資料分析工作編輯器 &#40;設定檔要求頁面&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)  
  
  
