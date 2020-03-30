---
title: 功能相依性設定檔要求選項 (資料分析工作) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 6eb853aa-8016-490c-be4f-06ab8d7f5021
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6cf3c23908b3ec391afc7b9073796ab4c2f47100
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71298271"
---
# <a name="functional-dependency-profile-request-options-data-profiling-task"></a>功能相依性設定檔要求選項 (資料分析工作)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  您可以使用 [設定檔要求]  頁面的 [要求屬性]  窗格，針對要求窗格中選取的 [功能相依性設定檔要求]  設定選項。 功能相依性設定檔會報告某個資料行 (相依資料行) 中的值相依於另一個資料行或資料行集合 (行列式資料行) 中之值的程度。 這個設定檔也可協助您識別資料中的問題，例如無效的值。 舉例來說，您分析了「郵遞區號」資料行與「美國州名」資料行之間的相依性。 在這個設定檔中，相同的郵遞區號應該永遠具有相同的州名，但是此設定檔卻發現了相依性的違規。  
  
> [!NOTE]  
>  本主題所描述的選項會顯示在 **[資料分析工作編輯器]** 的 **[設定檔要求]** 頁面上。 如需此編輯器頁面的詳細資訊，請參閱[資料分析工作編輯器 &#40;設定檔要求頁面&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)。  
  
 如需如何使用資料分析工作的詳細資訊，請參閱 [資料分析工作的設定](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)。 如需如何使用資料設定檔檢視器來分析資料分析工作輸出的詳細資訊，請參閱 [資料設定檔檢視器](../../integration-services/control-flow/data-profile-viewer.md)。  
  
## <a name="understanding-the-selection-of-determinant-and-dependent-columns"></a>了解行列式和相依資料行的選擇  
 [功能相依性設定檔要求]  會計算行列式端資料行或資料行集合 (在 **DeterminantColumns** 屬性中指定) 決定相依端資料行值 (在 **DependentColumn** 屬性中指定) 的程度。 例如，美國州名資料行應該在功能上相依於美國郵遞區號資料行。 也就是說，如果郵遞區號 (行列式資料行) 是 98052，州名 (相依資料行) 應該永遠是華盛頓。  
  
 您可以針對行列式端，在 **DeterminantColumns** 屬性中指定資料行或資料行集合。 例如，假設有一個包含 A、B 和 C 資料行的範例資料表。您針對 **DeterminantColumns** 屬性進行下列選擇：  
  
-   當您選取 **(\*)** 萬用字元時，資料分析工作會測試每個資料行，當做相依性的行列式端。  
  
-   當您選取 **(\*)** 萬用字元和其他資料行時，資料分析工作會測試每個資料行的組合，當做相依性的行列式端。 例如，假設有一個包含 A、B 和 C 資料行的範例資料表。如果您指定 **(\*)** 和 C 資料行當做 **DeterminantColumns** 屬性的值，資料分析工作會測試 (A, C) 和 (B, C) 組合，當做相依性的行列式端。  
  
 您可以針對相依端，在 **DependentColumn\* 屬性中指定單一資料行或** ( **)** 萬用字元。 當您選取 **(\*)** 時，資料分析工作會針對每個資料行測試行列式端資料行或資料行集合。  
  
> [!NOTE]  
>  如果您選取 **(\*)** ，這個選項可能會產生大量計算並降低工作的效能。 不過，如果此工作找到滿足功能相依性臨界值的子集，它就不會分析其他組合。 例如，在上述範例資料表中，如果此工作決定 C 資料行是行列式資料行，它就不會繼續分析複合候選。  
  
## <a name="request-properties-options"></a>要求屬性選項  
 [要求屬性]  窗格會針對 [功能相依性設定檔要求]  顯示下列選項群組：  
  
-   [資料]  ，其中包括 **DeterminantColumns** 和 **DependentColumn** 選項  
  
-   **一般**  
  
-   **選項**  
  
### <a name="data-options"></a>資料選項  
 **ConnectionManager**  
 選取現有的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員，以便使用 .NET Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) 來連線至包含要分析之資料表或檢視表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。  
  
 **[TableOrView]**  
 選取要分析的現有資料表或檢視表。  
  
 **DeterminantColumns**  
 選取行列式資料行或資料行集合。 也就是說，您可以選取其值可決定相依資料行之值的資料行或資料行集合。  
  
 如需詳細資訊，請參閱本主題的「了解行列式和相依資料行的選擇」和「DeterminantColumns 和 DependentColumn 選項」章節。  
  
 **)**  
 選取相依資料行。 也就是說，您可以選取其值由行列式端資料行或資料行集合之值決定的資料行。  
  
 如需詳細資訊，請參閱本主題的「了解行列式和相依資料行的選擇」和「DeterminantColumns 和 DependentColumn 選項」章節。  
  
#### <a name="determinantcolumns-and-dependentcolumn-options"></a>DeterminantColumns 和 DependentColumn 選項  
 下列選項會呈現給在 **DeterminantColumns** 和 **DependentColumn**中選取待分析的每個資料行。  
  
 如需詳細資訊，請參閱本主題前面的「了解行列式和相依資料行的選擇」章節。  
  
 **IsWildCard**  
 指定是否已經選取 **(\*)** 萬用字元。 如果您已選取 **(** ) **來分析所有資料行，這個選項會設定為 [True]\*** 。 如果您已選取要分析的個別資料行，它就會設定為 **[False]** 。 此選項是唯讀的。  
  
 **ColumnName**  
 顯示所選取資料行的名稱。 如果您已選取 **(\*)** 來分析所有資料行，這個選項就是空白的。 此選項是唯讀的。  
  
 **StringCompareOptions**  
 選取比較字串值的選項。 這個屬性具有下表中所列的選項。 這個選項的預設值為 **預設值**頁面上。  
  
> [!NOTE]  
>  當您針對 **ColumnName\* 使用** ( **)** 萬用字元時，**CompareOptions** 就是唯讀的，而且它會設定為 [預設值]  設定。  
  
|值|描述|  
|-----------|-----------------|  
|**預設值**|根據來源資料表中的資料行定序來排序和比較資料。|  
|**BinarySort**|根據針對每個字元所定義的位元模式來排序和比較資料。 二進位排序順序為區分大小寫和區分腔調字。 二進位也是最快的排序順序。|  
|**DictionarySort**|根據相關聯之語言或字母字典中所定義的排序和比較規則來排序和比較資料。|  
  
 如果您選取 [DictionarySort]  ，也可以選取下表中所列的任何選項組合。 根據預設，系統不會選取這些額外的選項。  
  
|值|描述|  
|-----------|-----------------|  
|**IgnoreCase**|指定比較是否區分大寫與小寫字母。 如果設定此選項，則字串比較會忽略大小寫。 例如，「ABC」與「abc」視為一樣。|  
|**IgnoreNonSpace**|指定比較是否區分空格字元與變音。 如果設定此選項，則比較會忽略變音符號。 例如，"Ã¥" 等於 "a"。|  
|**IgnoreKanaType**|指定比較是否區分兩類日文的假名字元：平假名與片假名。 如果設定此選項，則字串比較會忽略假名類型。|  
|**IgnoreWidth**|指定比較是否區分單一位元組字元和表示為雙位元組字元的相同字元。 如果設定此選項，則字串比較會將同一字元的單一位元組表示法和雙位元組表示法視為一樣。|  
  
### <a name="general-options"></a>一般選項  
 **RequestID**  
 輸入描述性名稱，以便識別這個設定檔要求。 一般而言，您不需要變更自動產生的值。  
  
### <a name="options"></a>選項。  
 **ThresholdSetting**  
 指定臨界值設定。 這個屬性的預設值為 [已指定]  。  
  
|值|描述|  
|-----------|-----------------|  
|**None**|沒有指定臨界值。 不論功能相依性強度為何，系統都會報告此值。|  
|**已指定**|使用 **FDStrengthThreshold**中指定的臨界值。 只有當功能相依性強度大於臨界值時，系統才會報告此值。|  
|**精確**|沒有指定臨界值。 只有當選取之資料行之間的功能相依性為精確時，系統才會報告此值。|  
  
 **FDStrengthThreshold**  
 指定臨界值 (使用介於 0 與 1 之間的值)，而且超過此值就應該報告功能相依性強度。 這個屬性的預設值為 0.95。 只有當 [已指定]  選取成為 [ThresholdSetting]  時，這個選項才會啟用。  
  
 **MaxNumberOfViolations**  
 指定可在輸出中報告的功能相依性違規數目上限。 這個屬性的預設值為 100。 當 [精確]  選取成為 [ThresholdSetting]  時，這個選項會停用。  
  
## <a name="see-also"></a>另請參閱  
 [資料分析工作編輯器 &#40;一般頁面&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [單一資料表快速分析表單 &#40;資料分析工作&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
