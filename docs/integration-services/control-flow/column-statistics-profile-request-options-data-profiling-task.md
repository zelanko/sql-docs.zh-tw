---
title: "資料行統計資料設定檔要求選項 （資料分析工作） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 87205984-507a-49f3-b27c-36a0075c234d
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 10b9dd217872c27b6192bde49bfaf18fbd2f511b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/28/2017

---
# <a name="column-statistics-profile-request-options-data-profiling-task"></a>資料行統計資料設定檔要求選項 (資料分析工作)
  您可以使用 [設定檔要求] 頁面的 [要求屬性] 窗格，針對要求窗格中選取的 [資料行統計資料設定檔要求] 設定選項。 資料行統計資料設定檔會報告數值資料行的最小值、最大值、平均和標準差，以及 **datetime** 資料行的最小值和最大值等統計資料。 這個設定檔可協助您識別資料中的問題，例如無效的日期。 舉例來說，您分析了歷程記錄日期的資料行，並發現屬於未來的最大日期。  
  
> [!NOTE]  
>  本主題所描述的選項會顯示在 **[資料分析工作編輯器]** 的 **[設定檔要求]**頁面上。 如需此編輯器頁面的詳細資訊，請參閱[資料分析工作編輯器 &#40;設定檔要求頁面&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)。  
  
 如需如何使用資料分析工作的詳細資訊，請參閱[資料分析工作的設定](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)。 如需如何使用資料設定檔檢視器來分析資料分析工作輸出的詳細資訊，請參閱 [資料設定檔檢視器](../../integration-services/control-flow/data-profile-viewer.md)。  
  
## <a name="request-properties-options"></a>要求屬性選項  
 [要求屬性] 窗格會針對 [資料行統計資料設定檔要求] 顯示下列選項群組：  
  
-   **[資料]**，其中包括 **[TableOrView]** 和 **[資料行]** 選項。  
  
-   **一般**  
  
### <a name="data-options"></a>資料選項  
 **ConnectionManager**  
 選取現有的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員，以便使用 .NET Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) 來連線至包含要分析之資料表或檢視表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。  
  
 **[TableOrView]**  
 選取包含要分析之資料行的資料表或檢視表。  
  
 如需詳細資訊，請參閱本主題中的「TableorView 選項」一節。  
  
 **[資料行]**  
 選取要分析的現有資料行。 您可以選取 **(\*)** 來分析所有資料行。  
  
 如需詳細資訊，請參閱本主題中的「資料行選項」一節。  
  
#### <a name="tableorview-options"></a>TableOrView 選項  
 **結構描述**  
 指定選取之資料表所屬的結構描述。 此選項是唯讀的。  
  
 **Table**  
 顯示選取之資料表的名稱。 此選項是唯讀的。  
  
#### <a name="column-options"></a>資料行選項  
 **IsWildCard**  
 指定是否已經選取 **(\*)** 萬用字元。 如果您已選取 **(\*)** 來分析所有資料行，這個選項會設定為 [True]。 如果您已選取要分析的個別資料行，它就會設定為 **[False]** 。 此選項是唯讀的。  
  
 **ColumnName**  
 顯示所選取資料行的名稱。 如果您已選取 **(\*)** 來分析所有資料行，這個選項就是空白的。 此選項是唯讀的。  
  
 **StringCompareOptions**  
 這個選項不會套用至資料行統計資料設定檔。  
  
### <a name="general-options"></a>一般選項  
 **RequestID**  
 輸入描述性名稱，以便識別這個設定檔要求。 一般而言，您不需要變更自動產生的值。  
  
## <a name="see-also"></a>另請參閱  
 [資料分析工作編輯器 &#40;一般頁面&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [單一資料表快速分析表單 &#40; 資料分析工作 &#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  

