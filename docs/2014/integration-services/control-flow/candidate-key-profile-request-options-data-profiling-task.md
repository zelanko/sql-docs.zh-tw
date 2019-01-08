---
title: 候選索引鍵設定檔要求選項 (資料分析工作) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 8632dbc4-4394-4dc7-b19c-f9adeb21ba52
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 64975d3e249db13a956f6300d340ac77dfc29db8
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52767150"
---
# <a name="candidate-key-profile-request-options-data-profiling-task"></a>候選索引鍵設定檔要求選項 (資料分析工作)
  您可以使用 [設定檔要求] 頁面的 [要求屬性] 窗格，針對要求窗格中選取的 [候選索引鍵設定檔要求] 設定選項。 候選索引鍵設定檔會報告資料行或資料行集合是否為選取之資料表的索引鍵或近似索引鍵。 這個設定檔也可協助您識別資料中的問題，例如潛在索引鍵資料行中重複的值。  
  
> [!NOTE]  
>  本主題所描述的選項會顯示在 **[資料分析工作編輯器]** 的 **[設定檔要求]** 頁面上。 如需此編輯器頁面的詳細資訊，請參閱[資料分析工作編輯器 &#40;設定檔要求頁面&#41;](data-profiling-task-editor-profile-requests-page.md)。  
  
 如需如何使用資料分析工作的詳細資訊，請參閱[資料分析工作的設定](data-profiling-task.md)。 如需如何使用資料設定檔檢視器來分析資料分析工作輸出的詳細資訊，請參閱 [資料設定檔檢視器](data-profile-viewer.md)。  
  
## <a name="understanding-the-selection-of-columns-for-the-keycolumns-property"></a>了解 KeyColumns 屬性之資料行的選擇  
 每個 [候選索引鍵設定檔要求] 都會計算包含單一資料行或多個資料行之單一索引鍵候選的索引鍵強度：  
  
-   當您在 [KeyColumns] 中僅選取一個資料行時，此工作會計算該單一資料行的索引鍵強度。  
  
-   當您在 [KeyColumns] 中選取多個資料行時，此工作會計算包含所有選取資料行之複合索引鍵的索引鍵強度。  
  
-   當您在 [KeyColumns] 中選取 **(\*)** 萬用字元時，此工作會計算資料表或檢視表中每個資料行的索引鍵強度。  
  
 例如，假設有一個包含 A、B 和 C 資料行的範例資料表。您針對 [KeyColumns] 進行下列選擇：  
  
-   您在 [KeyColumns] 中選取了 (\*) 和 C 資料行。 此工作會計算 C 資料行的索引鍵強度，然後計算複合索引鍵候選 (A, C) 和 (B, C) 的強度。  
  
-   您在 [KeyColumns] 中選取了 (\*) 和 (\*)。 此工作會計算 A、B 和 C 個別資料行的索引鍵強度，然後計算複合索引鍵候選 (A, B)、(A, C) 和 (B, C) 的強度。  
  
> [!NOTE]  
>  如果您選取 (*)，這個選項可能會產生大量計算並降低工作的效能。 不過，如果此工作找到滿足索引鍵臨界值的子集，它就不會分析其他組合。 例如，在上述範例資料表中，如果此工作決定 C 資料行是索引鍵，它就不會繼續分析複合索引鍵候選。  
  
## <a name="request-properties-options"></a>要求屬性選項  
 [要求屬性] 窗格會針對 [候選索引鍵設定檔要求] 顯示下列選項群組：  
  
-   [資料]，其中包括 [TableOrView] 和 [KeyColumns] 選項  
  
-   **一般**  
  
-   **Options**  
  
### <a name="data-options"></a>資料選項  
 **ConnectionManager**  
 選取現有的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員，以便使用 .NET Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) 來連線至包含要分析之資料表或檢視表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。  
  
 **TableOrView**  
 選取要分析的現有資料表或檢視表。  
  
 如需詳細資訊，請參閱本主題中的「TableorView 選項」一節。  
  
 **KeyColumns**  
 選取要分析的現有資料行。 您可以選取 **(\*)** 來分析所有資料行。  
  
 如需詳細資訊，請參閱本主題的「了解 KeyColumns 屬性之資料行的選擇」和「KeyColumns 選項」章節。  
  
#### <a name="tableorview-options"></a>TableOrView 選項  
 **結構描述**  
 指定選取之資料表所屬的結構描述。 此選項是唯讀的。  
  
 **Table**  
 顯示選取之資料表的名稱。 此選項是唯讀的。  
  
#### <a name="keycolumns-options"></a>KeyColumns 選項  
 下列選項會呈現給在 [KeyColumns] 中選取待分析的每個資料行或 **(\*)** 選項。  
  
 如需詳細資訊，請參閱本主題前面的「了解 KeyColumns 屬性之資料行的選擇」章節。  
  
 **IsWildcard**  
 指定是否已經選取 **(\*)** 萬用字元。 如果您已選取 **(\*)** 來分析所有資料行，這個選項會設定為 [True]。 如果您已選取要分析的個別資料行，它就會設定為 **[False]** 。 此選項是唯讀的。  
  
 **ColumnName**  
 顯示所選取資料行的名稱。 如果您已選取 **(\*)** 來分析所有資料行，這個選項就是空白的。 此選項是唯讀的。  
  
 **StringCompareOptions**  
 選取比較字串值的選項。 這個屬性具有下表中所列的選項。 這個選項的預設值為 **預設值**頁面上。  
  
> [!NOTE]  
>  當您針對 [ColumnName] 使用 **(\*)** 萬用字元時，[CompareOptions] 就是唯讀的，而且它會設定為 [預設值] 設定。  
  
|值|描述|  
|-----------|-----------------|  
|**預設值**|根據來源資料表中的資料行定序來排序和比較資料。|  
|**BinarySort**|根據針對每個字元所定義的位元模式來排序和比較資料。 二進位排序順序為區分大小寫和區分腔調字。 二進位也是最快的排序順序。|  
|**DictionarySort**|根據相關聯之語言或字母字典中所定義的排序和比較規則來排序和比較資料。|  
  
 如果您選取 [DictionarySort]，也可以選取下表中所列的任何選項組合。 根據預設，系統不會選取這些額外的選項。  
  
|值|描述|  
|-----------|-----------------|  
|**IgnoreCase**|指定比較是否區分大寫與小寫字母。 如果設定此選項，則字串比較會忽略大小寫。 例如，「ABC」與「abc」視為一樣。|  
|**IgnoreNonSpace**|指定比較是否區分空格字元與變音。 如果設定此選項，則比較會忽略變音符號。 例如，"å" 等於 "a"。|  
|**IgnoreKanaType**|指定比較是否區分兩類日文的假名字元：平假名與片假名。 如果設定此選項，則字串比較會忽略假名類型。|  
|**IgnoreWidth**|指定比較是否區分單一位元組字元和表示為雙位元組字元的相同字元。 如果設定此選項，則字串比較會將同一字元的單一位元組表示法和雙位元組表示法視為一樣。|  
  
### <a name="general-options"></a>一般選項  
 **RequestID**  
 輸入描述性名稱，以便識別這個設定檔要求。 一般而言，您不需要變更自動產生的值。  
  
### <a name="options"></a>選項。  
 **ThresholdSetting**  
 這個屬性具有下表中所列的選項。 這個屬性的預設值為 [已指定]。  
  
|值|描述|  
|-----------|-----------------|  
|**無**|沒有指定臨界值。 不論索引鍵強度為何，系統都會報告此值。|  
|**已指定**|臨界值是在 [KeyStrengthThreshold] 中指定的。 只有當索引鍵強度大於臨界值時，系統才會報告此值。|  
|**精確**|沒有指定臨界值。 只有當選取的資料行是精確索引鍵時，系統才會報告索引鍵強度。|  
  
 **KeyStrengthThreshold**  
 指定臨界值 (使用介於 0 與 1 之間的值)，而且超過此值就應該報告索引鍵強度。 這個屬性的預設值為 0.95。 只有當 [已指定] 選取成為 [KeyStrengthThresholdSetting] 時，這個選項才會啟用。  
  
 **MaxNumberOfViolations**  
 指定可在輸出中報告的候選索引鍵違規數目上限。 這個屬性的預設值為 100。 當 [精確] 選取成為 [KeyStrengthThresholdSetting] 時，這個選項會停用。  
  
## <a name="see-also"></a>另請參閱  
 [資料分析工作編輯器 &#40;一般頁面&#41;](../general-page-of-integration-services-designers-options.md)   
 [單一資料表快速分析表單 &#40;資料分析工作&#41;](single-table-quick-profile-form-data-profiling-task.md)  
  
  
