---
title: 值包含設定檔要求選項 (資料分析工作) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: ca94da82-a4c9-4e87-9cba-c2d85bd31f01
author: chugugrace
ms.author: chugu
ms.openlocfilehash: aa6215e3fafbbf962c687daf329f6781f466342d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71293806"
---
# <a name="value-inclusion-profile-request-options-data-profiling-task"></a>值包含設定檔要求選項 (資料分析工作)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  您可以使用 [設定檔要求] 頁面的 [要求屬性] 窗格，針對要求窗格中選取的 [值包含設定檔要求] 設定選項。 值包含設定檔會計算兩個資料行或資料行集合之間值的重疊。 因此，它也可以判斷資料行或資料行集合是否適合當做選取之資料表之間的外部索引鍵。 這個設定檔也可協助您識別資料中的問題，例如無效的值。 舉例來說，您使用了值包含設定檔來分析 Sales 資料表的 ProductID 資料行。 此設定檔發現該資料行包含在 Products 資料表之 ProductID 資料行中找不到的值。  
  
> [!NOTE]  
>  本主題所描述的選項會顯示在 **[資料分析工作編輯器]** 的 **[設定檔要求]** 頁面上。 如需此編輯器頁面的詳細資訊，請參閱[資料分析工作編輯器 &#40;設定檔要求頁面&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)。  
  
 如需如何使用資料分析工作的詳細資訊，請參閱 [資料分析工作的設定](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)。 如需如何使用資料設定檔檢視器來分析資料分析工作輸出的詳細資訊，請參閱 [資料設定檔檢視器](../../integration-services/control-flow/data-profile-viewer.md)。  
  
## <a name="understanding-the-selection-of-columns-for-the-inclusioncolumns-property"></a>了解 InclusionColumns 屬性之資料行的選擇  
 [值包含設定檔要求]  會計算某個子集中的所有值是否都會出現在超集中。 超集通常是查閱或參考資料表。 例如，地址資料表中的州名資料行就是子集資料表。 這個資料行中的每個二字元州名代碼也應該可在美國郵遞服務州名代碼的資料表 (超集資料表) 中找到。  
  
 當您使用 (*) 萬用字元當做子集資料行或超集資料行的值時，資料分析工作會比較該端的每個資料行與另一端指定的資料行。  
  
> [!NOTE]  
>  如果您選取 (*)，這個選項可能會產生大量計算並降低工作的效能。  
  
## <a name="understanding-the-threshold-settings"></a>了解臨界值設定  
 您可以使用兩個不同的臨界值設定來精簡值包含設定檔要求的輸出。  
  
 當您針對 [InclusionThresholdSetting]  指定 **None** 以外的值時，只有在下列其中一項條件底下，此設定檔才會報告超集中子集的包含強度：  
  
-   當包含強度超過 [InclusionStrengthThreshold]  中指定的臨界值時。  
  
-   當包含強度具有 1.0 的值，而且 [InclusionStrengthThreshold]  設定為 [精確]  時。  
  
 您可以透過篩選出超集資料行並非超集資料表之適當索引鍵的組合 (因為非唯一的值)，進一步精簡輸出。 當您針對 [SupersetColumnsKeyThresholdSetting] 指定 **None** 以外的值時，只有在下列其中一項條件底下，此設定檔才會報告超集中子集的包含強度：  
  
-   當超集資料行當作超集資料表之索引鍵的適合性超過 [SupersetColumnsKeyThreshold]  中指定的臨界值時  
  
-   當包含強度具有 1.0 的值，而且 [SupersetColumnsKeyThreshold]  設定為 [精確]  時。  
  
## <a name="request-properties-options"></a>要求屬性選項  
 [要求屬性] 窗格會針對 [值包含設定檔要求] 顯示下列選項群組：  
  
-   [資料]  ，其中包括 [SubsetTableOrView]  、[SupersetTableOrView]  和 [InclusionColumns]  選項  
  
-   **一般**  
  
-   **選項**  
  
### <a name="data-options"></a>資料選項  
 **ConnectionManager**  
 選取現有的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員，以便使用 .NET Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) 來連線至包含要分析之資料表或檢視表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。  
  
 **SubsetTableOrView**  
 選取要分析的現有資料表或檢視表。  
  
 如需詳細資訊，請參閱這個主題中的「SubsetTableOrView 和 SupersetTableOrView 選項」一節。  
  
 **SupersetTableOrView**  
 選取要分析的現有資料表或檢視表。  
  
 如需詳細資訊，請參閱這個主題中的「SubsetTableOrView 和 SupersetTableOrView 選項」一節。  
  
 **InclusionColumns**  
 從子集和超集資料表中選取資料行或資料行集合。  
  
 如需詳細資訊，請參閱本主題的「了解 InclusionColumns 屬性之資料行的選擇」和「InclusionColumns 選項」章節。  
  
#### <a name="subsettableorview-and-supersettableorview-options"></a>SubsetTableOrView 和 SupersetTableOrView 選項  
 **結構描述**  
 指定選取之資料表所屬的結構描述。 此選項是唯讀的。  
  
 **[TableOrView]**  
 顯示選取之資料表的名稱。 此選項是唯讀的。  
  
#### <a name="inclusioncolumns-options"></a>InclusionColumns 選項  
 下列選項會呈現給在 **[InclusionColumns]** 中選取待分析的每個資料行集合。  
  
 如需詳細資訊，請參閱本主題前面的「了解 InclusionColumns 屬性之資料行的選擇」一節。  
  
 **IsWildcard**  
 指定是否已經選取 **(\*)** 萬用字元。 如果您已選取 **(\*)** 來分析所有資料行，這個選項會設定為 [True]。 如果您已選取要分析的個別資料行，它就會設定為 **[False]** 。 此選項是唯讀的。  
  
 **ColumnName**  
 顯示所選取資料行的名稱。 如果您已選取 **(\*)** 來分析所有資料行，這個選項就是空白的。 此選項是唯讀的。  
  
 **StringCompareOptions**  
 選取比較字串值的選項。 這個屬性具有下表中所列的選項。 這個選項的預設值為 **預設值**頁面上。  
  
> [!NOTE]  
>  當您針對 **ColumnName** 使用 **(\*)** 萬用字元時，**CompareOptions** 就是唯讀的，而且它會設定為 [預設值] 設定。  
  
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
 **InclusionThresholdSetting**  
 選取臨界值設定，以便精簡設定檔的輸出。 這個屬性的預設值為 [已指定]  。 如需詳細資訊，請參閱本主題前面的「了解臨界值設定」一節。  
  
|值|描述|  
|-----------|-----------------|  
|**None**|沒有指定臨界值。 不論索引鍵強度為何，系統都會報告此值。|  
|**已指定**|使用 **InclusionStrengthThreshold**中指定的臨界值。 只有當包含強度大於臨界值時，系統才會報告此值。|  
|**精確**|沒有指定臨界值。 只有當子集值完全包含在超集值中時，系統才會報告包含強度。|  
  
 **InclusionStrengthThreshold**  
 指定臨界值 (使用介於 0 與 1 之間的值)，而且超過此值就應該報告包含強度。 這個屬性的預設值為 0.95。 只有當 [已指定]  選取成為 [InclusionThresholdSetting]  時，這個選項才會啟用。  
  
 如需詳細資訊，請參閱本主題前面的「了解臨界值設定」一節。  
  
 **SupersetColumnsKeyThresholdSetting**  
 指定超集臨界值。 這個屬性的預設值為 [已指定]  。 如需詳細資訊，請參閱本主題前面的「了解臨界值設定」一節。  
  
|值|描述|  
|-----------|-----------------|  
|**None**|沒有指定臨界值。 不論超集資料行的索引鍵強度為何，系統都會報告包含強度。|  
|**已指定**|使用 **SupersetColumnsKeyThreshold**頁面上。 只有當超集資料行的索引鍵強度大於臨界值時，系統才會報告包含強度。|  
|**精確**|沒有指定臨界值。 只有當超集資料行是超集資料表中的精確索引鍵時，系統才會報告包含強度。|  
  
 **SupersetColumnsKeyThreshold**  
 指定臨界值 (使用介於 0 與 1 之間的值)，而且超過此值就應該報告包含強度。 這個屬性的預設值為 0.95。 只有當 [已指定]  選取成為 [SupersetColumnsKeyThresholdSetting]  時，這個選項才會啟用。  
  
 如需詳細資訊，請參閱本主題前面的「了解臨界值設定」一節。  
  
 **MaxNumberOfViolations**  
 指定可在輸出中報告的包含違規數目上限。 這個屬性的預設值為 100。 當 [精確]  選取成為 [InclusionThresholdSetting]  時，這個選項會停用。  
  
## <a name="see-also"></a>另請參閱  
 [資料分析工作編輯器 &#40;一般頁面&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [單一資料表快速分析表單 &#40;資料分析工作&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
