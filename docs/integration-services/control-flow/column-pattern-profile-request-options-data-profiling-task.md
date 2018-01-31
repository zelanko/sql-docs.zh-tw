---
title: "資料行模式設定檔要求選項 (資料分析工作) | Microsoft Docs"
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
ms.assetid: 9ccb8fc5-f65e-41a2-9511-7fa55586eb8b
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 154dc4da51c19363cb9fd41616e9e89ea3d3ded8
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="column-pattern-profile-request-options-data-profiling-task"></a>資料行模式設定檔要求選項 (資料分析工作)
  您可以使用 [設定檔要求] 頁面的 [要求屬性] 窗格，針對要求窗格中選取的 [資料行模式設定檔要求] 設定選項。 資料行模式設定檔會報告一組規則運算式，其中涵蓋了字串資料行中值的指定百分比。 這個設定檔可協助您識別資料中的問題，例如無效的字串，而且可以建議未來可用於驗證新值的規則運算式。 例如，「美國郵遞區號」資料行的模式設定檔可能會產生規則運算式 \d{5}-\d{4}、\d{5} 和 \d{9}。 如果您看見其他規則運算式，表示您的資料可能包含無效或格式錯誤的值。  
  
> [!NOTE]  
>  本主題所描述的選項會顯示在 **[資料分析工作編輯器]** 的 **[設定檔要求]**頁面上。 如需此編輯器頁面的詳細資訊，請參閱[資料分析工作編輯器 &#40;設定檔要求頁面&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)。  
  
 如需如何使用資料分析工作的詳細資訊，請參閱[資料分析工作的設定](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)。 如需如何使用資料設定檔檢視器來分析資料分析工作輸出的詳細資訊，請參閱 [資料設定檔檢視器](../../integration-services/control-flow/data-profile-viewer.md)。  
  
## <a name="understanding-the-use-of-delimiters-and-symbols"></a>了解分隔符號和符號的使用方式  
 針對 [資料行模式設定檔要求] 計算模式之前，資料分析工作會 Token 化資料。 也就是說，此工作會將字串值分隔成名為 Token 的較小單位。 此工作會根據您針對 [分隔符號] 和 [符號] 屬性指定的分隔符號和符號，將字串分隔成 Token：  
  
-   **分隔符號**：根據預設，分隔符號清單包含下列字元：空格、水平定位字元 (\t)、新行字元 (\n) 和歸位字元 (\r)。 雖然您可以指定其他分隔符號，但是無法移除預設的分隔符號。  
  
-   **符號**：根據預設，[符號] 清單包含下列字元：`,.;:-"'~=&/@!?()<>[]{}|#*^%` 以及刻度標記。 例如，如果這些符號是 "`()-`"，"(425) 123-4567" 值就會 Token 化成為 ["(", "425", ")", "123", "-", "4567", ")"]。  
  
 一個字元無法同時屬於分隔符號和符號。  
  
 所有分隔符號都會在 Token 化程序中正規化成為單一空格，而符號則會保留。  
  
## <a name="understanding-the-use-of-the-tag-table"></a>了解標記資料表的使用方式  
 您可以將標記和相關的詞彙儲存在您於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中建立的特殊資料表中，藉以選擇性地以單一標記將相關 Token 組成群組。 標記資料表必須具有兩個字串資料行：一個名為「標記」，而另一個名為「詞彙」。 這些資料行的類型可以是 **char**、 **nchar**、 **varchar**或 **nvarchar**，但不得為 **text** 或 **ntext**。 您可以在單一資料表中結合多個標記和對應的詞彙。 一個資料行模式設定檔要求只能使用一份標記資料表。 您可以使用個別的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員來連接至標記資料表。 因此，標記資料表可以位於不同的資料庫中或與來源資料位於不同的伺服器上。  
  
 例如，您可以使用單一標記「方向」，將可能顯示在街道地址中的「東」、「西」、「北」和「南」值組成群組。 下表是這類標記資料表的範例。  
  
|標記|詞彙|  
|---------|----------|  
|方向|東|  
|方向|西|  
|方向|北|  
|方向|南|  
  
 您可以使用另一個標記，將在街道地址中表示「街道」概念的不同字詞組成群組：  
  
|標記|詞彙|  
|---------|----------|  
|街|街|  
|街|道|  
|街|大街|  
|街|路|  
  
 根據這種標記的組合，街道地址的產生模式可能會類似於下列模式：  
  
 `\d+\ LookupTag=Direction \d+\p{L}+\ LookupTag=Street`  
  
> [!NOTE]  
>  使用標記資料表會降低資料分析工作的效能。 請勿使用超過 10 個標記或使用超過 100 個詞彙 (每個標記)。  
  
 相同的詞彙可以屬於多個標記。  
  
## <a name="request-properties-options"></a>要求屬性選項  
 [要求屬性] 窗格會針對 [資料行模式設定檔要求] 顯示下列選項群組：  
  
-   **[資料]**，其中包括 **[TableOrView]** 和 **[資料行]** 選項。  
  
-   **一般**  
  
-   **Options**  
  
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
 指定是否已經選取 **(\*)** 萬用字元。 如果您已選取 **(\*)** 來分析所有資料行，這個選項會設定為 [True]。 如果您已選取要分析的個別資料行，它就會設定為 **[False]** 。 此選項是唯讀的。  
  
 **ColumnName**  
 顯示所選取資料行的名稱。 如果您已選取 **(\*)** 來分析所有資料行，這個選項就是空白的。 此選項是唯讀的。  
  
 **StringCompareOptions**  
 這個選項不會套用至資料行模式設定檔。  
  
### <a name="general-options"></a>一般選項  
 **RequestID**  
 輸入描述性名稱，以便識別這個設定檔要求。 一般而言，您不需要變更自動產生的值。  
  
### <a name="options"></a>選項。  
 **MaxNumberOfPatterns**  
 指定您想讓設定檔計算的模式數目上限。 這個選項的預設值為 10。 最大值為 100。  
  
 **PercentageDataCoverageDesired**  
 指定您想讓計算模式涵蓋的資料百分比。 這個選項的預設值為 95 (%)。  
  
 **CaseSensitive**  
 指出模式是否應該區分大小寫。 此選項的預設值是 **[False]**。  
  
 **分隔符號**  
 列出在 Token 化文字時應該視為字詞之間空格對等項目的字元。 根據預設，[分隔符號] 清單包含下列字元：空格、水平定位字元 (\t)、新行字元 (\n) 和歸位字元 (\r)。 雖然您可以指定其他分隔符號，但是無法移除預設的分隔符號。  
  
 如需詳細資訊，請參閱本主題前面的「了解分隔符號和符號的使用方式」。  
  
 **Symbols**  
 列出應該保留成為模式一部分的符號。 範例可能包括 "/" (代表日期)、":" (代表時間) 和 "@" (代表電子郵件地址)。 根據預設，[符號] 清單包含下列字元：`,.;:-"'~=&/@!?()<>[]{}|#*^%`。  
  
 如需詳細資訊，請參閱本主題前面的「了解分隔符號和符號的使用方式」。  
  
 **TagTableConnectionManager**  
 選取現有的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員，以便使用 .NET Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) 來連接至包含標記資料表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。  
  
 如需詳細資訊，請參閱本主題前面的「了解標記資料表的使用方式」。  
  
 **TagTableName**  
 選取現有的標記資料表，其中必須具有兩個分別名為「標記」和「詞彙」的資料行。  
  
 如需詳細資訊，請參閱本主題前面的「了解標記資料表的使用方式」。  
  
## <a name="see-also"></a>另請參閱  
 [資料分析工作編輯器 &#40;一般頁面&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [單一資料表快速分析表單 &#40;資料分析工作&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
