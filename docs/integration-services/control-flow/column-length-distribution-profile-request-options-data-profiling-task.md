---
description: 資料行長度散發設定檔要求選項 (資料分析工作)
title: 資料行長度散發設定檔要求選項 (資料分析工作) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 1a4de41f-f38d-40ea-ba1b-6c0ef67ea52a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8eea376c7dc204b326f7ad4bb5ac41d0a76e4ee4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88496020"
---
# <a name="column-length-distribution-profile-request-options-data-profiling-task"></a>資料行長度散發設定檔要求選項 (資料分析工作)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  您可以使用 **[設定檔要求]** 頁面的 **[要求屬性]** 窗格，針對要求窗格中選取的 **[資料行長度散發設定檔要求]** 設定選項。 資料行長度散發設定檔會報告選取之資料行中字串值的所有相異長度，以及該資料表中每個長度所代表之資料列的百分比。 這個設定檔可協助您識別資料中的問題，例如無效的值。 舉例來說，您分析了美國州名二字元代碼的資料行並發現長度超過兩個字元的值。  
  
> [!NOTE]  
>  本主題所描述的選項會顯示在 **[資料分析工作編輯器]** 的 **[設定檔要求]** 頁面上。 如需此編輯器頁面的詳細資訊，請參閱[資料分析工作編輯器 &#40;設定檔要求頁面&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)。  
  
 如需如何使用資料分析工作的詳細資訊，請參閱 [資料分析工作的設定](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)。 如需如何使用資料設定檔檢視器來分析資料分析工作輸出的詳細資訊，請參閱 [資料設定檔檢視器](../../integration-services/control-flow/data-profile-viewer.md)。  
  
## <a name="request-properties-options"></a>要求屬性選項  
 **[要求屬性]** 窗格會針對 **[資料行長度散發設定檔要求]** 顯示下列選項群組：  
  
-   **[資料]**，其中包括 **[TableOrView]** 和 **[資料行]** 選項。  
  
-   **一般**  
  
-   **選項**  
  
### <a name="data-options"></a>資料選項  
 **ConnectionManager**  
 選取現有的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員，以便使用 .NET Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) 來連線至包含要分析之資料表或檢視表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。  
  
 **[TableOrView]**  
 選取包含要分析之資料行的資料表或檢視表。  
  
 如需詳細資訊，請參閱本主題中的「TableorView 選項」一節。  
  
 **資料行**  
 選取要分析的現有資料行。 您可以選取 **(\*)** 來分析所有資料行。  
  
 如需詳細資訊，請參閱本主題中的「資料行選項」一節。  
  
#### <a name="tableorview-options"></a>TableOrView 選項  
 **結構描述**  
 指定選取之資料表所屬的結構描述。 此選項是唯讀的。  
  
 **Table**  
 顯示選取之資料表的名稱。 此選項是唯讀的。  
  
#### <a name="column-options"></a>資料行選項  
 **IsWildCard**  
 指定是否已經選取 **(\*)** 萬用字元。 如果您已選取 **(\*)** 來分析所有資料行，這個選項會設定為 [True]****。 如果您已選取要分析的個別資料行，它就會設定為 **[False]** 。 此選項是唯讀的。  
  
 **ColumnName**  
 顯示所選取資料行的名稱。 如果您已選取 **(\*)** 來分析所有資料行，這個選項就是空白的。 此選項是唯讀的。  
  
 **StringCompareOptions**  
 這個選項不會套用至資料行長度散發設定檔。  
  
### <a name="general-options"></a>一般選項  
 **RequestID**  
 輸入描述性名稱，以便識別這個設定檔要求。 一般而言，您不需要變更自動產生的值。  
  
### <a name="options"></a>選項。  
 **IgnoreLeadingSpaces**  
 指出當設定檔比較字串值時是否要忽略開頭空白。 此選項的預設值是 **[False]**。  
  
 **IgnoreTrailingSpaces**  
 指出當設定檔比較字串值時是否要忽略尾端空白。 此選項的預設值是 **[True]**。  
  
## <a name="see-also"></a>另請參閱  
 [資料分析工作編輯器 &#40;一般頁面&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [單一資料表快速分析表單 &#40;資料分析工作&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
