---
title: 資料行值散發設定檔要求選項 (資料分析工作) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: c1e5f5de-04f5-4d00-a9f0-55817186bdf9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fd0f778495220f227e2dd1fca42c8f5104ea7d2b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71294226"
---
# <a name="column-value-distribution-profile-request-options-data-profiling-task"></a>資料行值散發設定檔要求選項 (資料分析工作)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  您可以使用 [設定檔要求]  頁面的 [要求屬性]  窗格，針對要求窗格中選取的 [資料行值散發設定檔要求]  設定選項。 資料行值散發設定檔會報告選取之資料行中的所有相異值，以及該資料表中每個值所代表之資料列的百分比。 此設定檔也可以報告代表超過資料表中指定之資料列百分比的值。 這個設定檔可協助您識別資料中的問題，例如某個資料行中相異值的數目不正確。 舉例來說，您分析了「美國州名」資料行並發現超過 50 個相異值。  
  
> [!NOTE]  
>  本主題所描述的選項會顯示在 **[資料分析工作編輯器]** 的 **[設定檔要求]** 頁面上。 如需此編輯器頁面的詳細資訊，請參閱[資料分析工作編輯器 &#40;設定檔要求頁面&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)。  
  
 如需如何使用資料分析工作的詳細資訊，請參閱 [資料分析工作的設定](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)。 如需如何使用資料設定檔檢視器來分析資料分析工作輸出的詳細資訊，請參閱 [資料設定檔檢視器](../../integration-services/control-flow/data-profile-viewer.md)。  
  
## <a name="request-properties-options"></a>要求屬性選項  
 [要求屬性]  窗格會針對 [資料行值散發設定檔要求]  顯示下列選項群組：  
  
-   **[資料]** ，其中包括 **[TableOrView]** 和 **[資料行]** 選項。  
  
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
 指定是否已經選取 **(\*)** 萬用字元。 如果您已選取 **(** ) **來分析所有資料行，這個選項會設定為 [True]\*** 。 如果您已選取要分析的個別資料行，它就會設定為 **[False]** 。 此選項是唯讀的。  
  
 **ColumnName**  
 顯示所選取資料行的名稱。 如果您已選取 **(\*)** 來分析所有資料行，這個選項就是空白的。 此選項是唯讀的。  
  
 **StringCompareOptions**  
 選取比較字串值的選項。 這個屬性具有下表中所列的選項。 這個選項的預設值為 **預設值**頁面上。  
  
> [!NOTE]  
>  如果您針對 **ColumnName\* 使用** ( **)** 萬用字元，**CompareOptions** 就是唯讀的，而且它會設定為 [預設值]  設定。  
  
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
 **ValueDistributionOption**  
 指定是否要計算所有資料行值的散發。 這個選項的預設值為 **FrequentValues**。  
  
|值|描述|  
|-----------|-----------------|  
|**AllValues**|計算所有資料行值的散發。|  
|**FrequentValues**|僅針對頻率超過 **FrequentValueThreshold**中指定之最小值的值計算散發。 輸出報表會排除不符合 **FrequentValueThreshold** 的值。|  
  
 **FrequentValueThreshold**  
 指定臨界值 (使用介於 0 與 1 之間的值)，而且超過此值就應該報告資料行值。 當您選取 **AllValues** 當作 **ValueDistributionOption**時，這個選項是停用的。 這個選項的預設值為 0.001。  
  
## <a name="see-also"></a>另請參閱  
 [資料分析工作編輯器 &#40;一般頁面&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [單一資料表快速分析表單 &#40;資料分析工作&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
