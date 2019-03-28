---
title: 資料分析工作編輯器 (設定檔要求頁面) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataprofilingtask.profilerequests.f1
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: c72acb3d-380e-436e-8041-ed364eddfabd
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e3f98e88428c25c3ecf2af415c942c30a18e9cf1
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58273375"
---
# <a name="data-profiling-task-editor-profile-requests-page"></a>Data Profiling Task Editor (Profile Requests Page)
  您可以使用 **[資料分析工作編輯器]** 的 **[設定檔要求]** 頁面來選取並設定想要計算的設定檔。 在單一「資料分析」工作中，您可以針對多個資料表或檢視表中的多個資料行或資料行組合計算多個設定檔。  
  
 如需如何使用資料分析工作的詳細資訊，請參閱 [資料分析工作的設定](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)。 如需如何使用資料設定檔檢視器來分析資料分析工作輸出的詳細資訊，請參閱 [資料設定檔檢視器](../../integration-services/control-flow/data-profile-viewer.md)。  
  
 **開啟資料分析工作編輯器的設定檔要求頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟具有資料分析工作的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [控制流程] 索引標籤中，按兩下資料分析工作。  
  
3.  在 **[資料分析工作編輯器]** 中，按一下 **[設定檔要求]**。  
  
## <a name="using-the-requests-pane"></a>使用要求窗格  
 要求窗格是指顯示在頁面頂端的窗格。 這個窗格會列出已經針對目前資料分析工作設定的所有設定檔。 如果尚未設定任何設定檔，此要求窗格就是空的。 若要加入新的設定檔，請在 **[設定檔類型]** 資料行底下的任何區域中按一下，然後從清單中選取設定檔類型。 若要設定設定檔，請在要求窗格中選取設定檔，然後在 **[要求屬性]** 窗格中設定設定檔的屬性。  
  
### <a name="requests-pane-options"></a>要求窗格選項  
 此要求窗格具有下列選項：  
  
 **[檢視]**  
 選取要檢視已經針對此工作設定的所有設定檔，還是僅檢視其中一個設定檔。  
  
 要求窗格中的資料行會根據您所選取的 **[檢視]** 而變更。 如需有關每個資料行的詳細資訊，請參閱下一節「要求窗格資料行」。  
  
### <a name="requests-pane-columns"></a>要求窗格資料行  
 要求窗格所顯示的資料行會根據您所選取的 **[檢視]** 而不同：  
  
-   如果您選取檢視 [所有要求]，要求窗格就會有兩個資料行：[設定檔類型] 和 [要求識別碼]。  
  
-   如果您選取檢視五個資料行設定檔的其中一個，要求窗格就會有四個資料行：[設定檔類型]、[資料表或檢視表]、[資料行] 和 [要求識別碼]。  
  
-   如果您選取檢視候選索引鍵設定檔，要求窗格就會有四個資料行：[設定檔類型]、[資料表或檢視表]、[KeyColumns] 和 [要求識別碼]。  
  
-   如果您選取檢視功能相依性設定檔，要求窗格就會有五個資料行：[設定檔類型]、[資料表或檢視表]、[行列式資料行]、[相依資料行] 和 [要求識別碼]。  
  
-   如果您選取檢視值包含設定檔，要求窗格就會有六個資料行：[設定檔類型]、[子集資料表或檢視表]、[超集資料表或檢視表]、[子集資料行]、[超集資料行] 和 [要求識別碼]。  
  
 下列各節會分別描述每個資料行。  
  
#### <a name="columns-common-to-all-views"></a>所有檢視通用的資料行  
 **[設定檔類型]**  
 從下列選項中選取資料設定檔：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**候選索引鍵設定檔要求**|計算候選索引鍵設定檔。<br /><br /> 這個設定檔會報告資料行或資料行集合是否為選取之資料表的索引鍵或近似索引鍵。 這個設定檔也可協助您識別資料中的問題，例如潛在索引鍵資料行中重複的值。|  
|**資料行長度散發設定檔要求**|計算資料行長度散發設定檔。<br /><br /> 資料行長度散發設定檔會報告選取之資料行中字串值的所有相異長度，以及該資料表中每個長度所代表之資料列的百分比。 這個設定檔可協助您識別資料中的問題，例如無效的值。 舉例來說，您分析了美國州名二字元代碼的資料行並發現長度超過兩個字元的值。|  
|**資料行 Null 比例設定檔要求**|計算資料行 Null 比例設定檔。<br /><br /> 資料行 Null 比例設定檔會報告選取之資料行中 Null 值的百分比。 這個設定檔可協助您識別資料中的問題，例如某個資料行中 Null 值的比例過高。 舉例來說，您分析了「郵遞區號」資料行並發現遺漏郵遞區號的百分比過高。|  
|**資料行模式設定檔要求**|計算資料行模式設定檔。<br /><br /> 資料行模式設定檔會報告一組規則運算式，其中涵蓋了字串資料行中值的指定百分比。 這個設定檔可協助您識別資料中的問題，例如屬於無效字串的字串。 這個設定檔也可以建議未來可用於驗證新值的規則運算式。 舉例來說，「郵遞區號」的資料行模式設定檔可能會產生規則運算式：\d{5}-\d{4}、\d{5} 和 \d{9}。 如果您看見其他規則運算式，表示資料可能包含無效或格式錯誤的值。|  
|**資料行統計資料設定檔要求**|選取此選項，即可使用選取之資料表或檢視表中所有適用資料行的預設設定來計算資料行統計資料設定檔。<br /><br /> 資料行統計資料設定檔會報告數值資料行的最小值、最大值、平均和標準差，以及 **datetime** 資料行的最小值和最大值等統計資料。 這個設定檔可協助您識別資料中的問題，例如無效的日期。 舉例來說，您分析了歷程記錄日期的資料行，並發現屬於未來的最大日期。|  
|**資料行值散發設定檔要求**|計算資料行值散發設定檔。<br /><br /> 資料行值散發設定檔會報告選取之資料行中的所有相異值，以及該資料表中每個值所代表之資料列的百分比。 這個設定檔也可以報告代表超過資料表中指定之百分比的值。 這個設定檔可協助您識別資料中的問題，例如某個資料行中相異值的數目不正確。 舉例來說，您分析了包含美國州名的資料行並發現超過 50 個相異值。|  
|**功能相依性設定檔要求**|計算功能相依性設定檔。<br /><br /> 功能相依性設定檔會報告某個資料行 (相依資料行) 中的值相依於另一個資料行或資料行集合 (行列式資料行) 中之值的程度。 這個設定檔也可協助您識別資料中的問題，例如無效的值。 舉例來說，您分析了「美國郵遞區號」資料行與「美國州名」資料行之間的相依性。 相同的郵遞區號應該永遠具有相同的州名，但是此設定檔卻發現了這個相依性的違規。|  
|**值包含設定檔要求**|計算值包含設定檔。<br /><br /> 值包含設定檔會計算兩個資料行或資料行集合之間值的重疊。 這個設定檔也可以判斷資料行或資料行集合是否適合當做選取之資料表之間的外部索引鍵。 這個設定檔也可協助您識別資料中的問題，例如無效的值。 舉例來說，您分析了 Sales 資料表的 ProductID 資料行，並發現此資料行包含在 Products 資料表之 ProductID 資料行中找不到的值。|  
  
 **RequestID**  
 顯示要求的識別碼。 一般而言，您不需要變更自動產生的值。  
  
#### <a name="columns-common-to-all-individual-profiles"></a>所有個別設定檔通用的資料行  
 **連線管理員**  
 顯示連接至來源資料庫的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員。  
  
 **[要求識別碼]**  
 顯示要求的識別碼。 一般而言，您不需要變更自動產生的值。  
  
#### <a name="columns-common-to-the-five-individual-column-profiles"></a>五個個別資料行設定檔通用的資料行  
 **[資料表或檢視表]**  
 顯示包含選取之資料行的資料表或檢視表。  
  
 **[資料行]**  
 顯示選取以便分析的資料行。  
  
#### <a name="columns-specific-to-the-candidate-key-profile"></a>候選索引鍵設定檔特有的資料行  
 **[資料表或檢視表]**  
 顯示包含選取之資料行的資料表或檢視表。  
  
 **索引鍵資料行**  
 顯示選取以便分析的資料行。  
  
#### <a name="columns-specific-to-the-functional-dependency-profile"></a>功能相依性設定檔特有的資料行  
 **[資料表或檢視表]**  
 顯示包含選取之資料行的資料表或檢視表。  
  
 **[行列式資料行]**  
 顯示選取以便分析成為行列式資料行的資料行。 在美國郵遞區號決定美國州名的範例中，行列式資料行就是郵遞區號資料行。  
  
 **Dependent column**  
 顯示選取以便分析成為相依資料行的資料行。 在美國郵遞區號決定美國州名的範例中，相依資料行就是州名資料行。  
  
#### <a name="columns-specific-to-the-value-inclusion-profile"></a>值包含設定檔特有的資料行  
 **[子集資料表或檢視表]**  
 顯示包含選取成為子集資料行之資料行的資料表或檢視表。  
  
 **[超集資料表或檢視表]**  
 顯示包含選取成為超集資料行之資料行的資料表或檢視表。  
  
 **[子集資料行]**  
 顯示選取以便分析成為子集資料行的資料行。 舉例來說，如果您想要確認美國州名資料行中的值可在二字元美國州名代碼的參考資料表中找到，子集資料行就是來源資料表中的州名資料行。  
  
 **[超集資料行]**  
 顯示選取以便分析成為超集資料行的資料行。 舉例來說，如果您想要確認美國州名資料行中的值可在二字元美國州名代碼的參考資料表中找到，超集資料行就是參考資料表中的州名代碼資料行。  
  
## <a name="using-the-request-properties-pane"></a>使用要求屬性窗格  
 **[要求屬性]** 窗格會顯示在要求窗格底下。 這個窗格會針對您已在要求窗格中選取的設定檔顯示選項。  
  
> [!NOTE]  
>  在您選取 [設定檔類型]之後，您必須選取 [要求識別碼] 欄位，才能在 [要求屬性] 窗格中查看設定檔要求的屬性。  
  
 這些選項會因選取的設定檔而不同。 如需有關個別設定檔類型之選項的詳細資訊，請參閱下列主題：  
  
-   [候選索引鍵設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/candidate-key-profile-request-options-data-profiling-task.md)  
  
-   [資料行 Null 比例設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/column-null-ratio-profile-request-options-data-profiling-task.md)  
  
-   [資料行統計資料設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/column-statistics-profile-request-options-data-profiling-task.md)  
  
-   [資料行值散發設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/column-value-distribution-profile-request-options-data-profiling-task.md)  
  
-   [資料行長度散發設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/column-length-distribution-profile-request-options-data-profiling-task.md)  
  
-   [資料行模式設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/column-pattern-profile-request-options-data-profiling-task.md)  
  
-   [功能相依性設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/functional-dependency-profile-request-options-data-profiling-task.md)  
  
-   [值包含設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/value-inclusion-profile-request-options-data-profiling-task.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料分析工作編輯器 &#40;一般頁面&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [單一資料表快速分析表單 &#40;資料分析工作&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
