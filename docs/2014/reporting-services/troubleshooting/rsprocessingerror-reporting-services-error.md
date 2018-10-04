---
title: rsProcessingError - Reporting Services 錯誤 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rsProcessingError
ms.assetid: 414ee58a-8251-4367-9a8e-10c068d17280
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 68a2b5b9a48523193f263ae0bba1c8eaddc186c0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48207318"
---
# <a name="rsprocessingerror---reporting-services-error"></a>rsProcessingError - Reporting Services 錯誤
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|rsProcessingError|  
|事件來源|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings.resources|  
|元件|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|訊息文字|報表處理時發生錯誤。|  
  
## <a name="explanation"></a>說明  
 發行、處理、本機預覽、從報表伺服器檢視或建立報表的訂閱時，發生一個或多個錯誤。 這個錯誤訊息表示偵測到至少一個錯誤。  
  
### <a name="possible-causes"></a>可能的原因  
 可能的原因包括：  
  
-   報表伺服器上發生處理錯誤。  
  
-   在預覽報表時，於處理本機報表期間發生處理錯誤。  
  
-   群組運算式經判斷為不正確的資料類型。  
  
-   篩選定義指定了兩個運算式，而這兩個運算式判斷為無法比較的資料類型。  
  
-   運算式參考了欄位集合中不存在的欄位。  
  
-   運算式包含具有無效或衝突範圍的彙總函式呼叫。  
  
-   運算式參考了報表參數集合中不存在的參數。  
  
-   無法載入不正確部署的自訂組件或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組件。  
  
-   可為 Null 的屬性設定為參數`False`參數中偵測到 null 值。  
  
-   資料區域之 Hidden 屬性的運算式含有錯誤：物件參考未設定為物件的執行個體。  
  
-   運算式包含無效的函數呼叫或語法錯誤。  
  
## <a name="user-action"></a>使用者動作  
  
### <a name="finding-more-information"></a>尋找詳細資訊  
 執行下列其中一個或多個動作：  
  
-   如果要從報表伺服器檢視報表，或是將報表當做訂閱檢視，請查看錯誤訊息的全文。 全文中會提供其他資訊。  
  
-   如果您正在報表設計師中撰寫報表，並且在預覽或發行報表時看到這個錯誤，[錯誤清單] 視窗中會提供其他資訊。  
  
-   如果您正在「報表設計師預覽」中撰寫報表，請查看錯誤訊息的全文。 全文中會提供其他資訊。  
  
-   如果您在報表伺服器上檢視報表，並以本機管理員身分在報表伺服器上執行，只要以滑鼠右鍵按一下頁面，然後選取 [檢視來源]，即可檢視呼叫堆疊。 呼叫堆疊中會提供其他資訊。  
  
-   如果您正以本機管理員的身分在報表伺服器上執行，請搜尋 `ReportProcessingException`的記錄檔。 記錄項目會包含更多資訊。 報表伺服器記錄檔通常位於 \<磁碟機>:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\LogFiles\ReportServerService__<日期時間戳記>.log。 如需詳細資訊，請參閱 [Reporting Services 記錄檔和來源](../report-server/reporting-services-log-files-and-sources.md)。  
  
### <a name="failed-to-load-expression-host-assembly"></a>無法載入運算式主機組件  
 自訂組件必須以強式名稱簽署，並設定 AllowPartiallyTrustedCallers 屬性。 如需詳細資訊，請參閱 < [Using Custom Assemblies with Reports](../custom-assemblies/using-custom-assemblies-with-reports.md)並[Understanding Security Policies](../extensions/secure-development/understanding-security-policies.md)。  
  
### <a name="a-built-in-global-name-does-not-exist"></a>內建的全域名稱不存在  
 請檢查運算式中的拼字。 內建的全域、參數和欄位名稱都會區分大小寫。 在導致錯誤發生的運算式中，檢查此名稱是否確實存在報表中，而且它的拼字是否正確。 如需詳細資訊，請參閱[運算式中的內建集合 &#40;報表產生器及 SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md)。  
  
### <a name="parameter-properties-and-null"></a>參數屬性和 Null  
 多重值參數不可以是 Null。 如需詳細資訊，請參閱[報表參數 &#40;報表產生器和報表設計師&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)。  
  
### <a name="main-report-with-subreport-could-not-be-processed"></a>無法處理含有子報表的主報表  
 含有子報表的主報表必須由相同的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表處理器版本處理。 將報表升級至目前版本的報表定義結構描述時，主報表和子報表不一定會同時更新。 如果報表與子報表之間的版本不相容，就會顯示下列訊息：「無法處理子報表」。  
  
 您必須變更主報表或子報表，如此所有報表才能由相同的報表處理器版本處理。 如需為何報表無法升級的資訊，請參閱[升級報表](../install-windows/upgrade-reports.md)。  
  
### <a name="verify-function-calls-are-visual-basic-and-not-sql"></a>確認函數呼叫是 Visual Basic 而不是 SQL  
 在關聯式資料庫上，您可以在查詢文字中使用 SQL 函數。 您無法在查詢文字中使用 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 函數。  
  
 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，運算式可以使用 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 函數、System.Math 或 System.String 函數、完整 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 函數，或是自訂程式碼或自訂組件中提供的自訂函數。 您不能在運算式中使用 SQL 函數。  
  
 請確認查詢和運算式中的函數呼叫有效。  
  
### <a name="cannot-compare-data-types-for-a-filter"></a>無法比較篩選的資料類型  
 在篩選方程式中，定義篩選項目的篩選運算式與篩選值必須屬於相同的資料類型，才能進行比較。 如果您看見下列其中一個錯誤，請修改欄位運算式或篩選值，讓資料類型相符：  
  
-   無法處理 \<報表項目名稱> 的 \<報表項目類型>。 無法比較類型 \<類型> 與 \<類型> 的資料。 請檢查 \<報表項目名稱> 所傳回的資料類型。  
  
-   無法評估 \<屬性名稱>。  
  
-   無法評估 \<屬性名稱>。 它參考有錯誤的資料集欄位：\<錯誤字串>。  
  
 如需詳細資訊，請參閱[篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)。  
  
### <a name="invalid-or-conflicting-scope-specification-in-an-aggregate-function-call"></a>彙總函式呼叫中的無效或衝突範圍規格  
 當您在 Tablix 資料格中加入運算式的彙總函式呼叫時，報表處理器就會在該資料格所屬之最內部群組的範圍中評估運算式。  
  
 您也可以將特定範圍的名稱傳遞給彙總函式。 範圍可以參考資料集的名稱、資料區域或在資料階層中較高範圍的名稱。 這點適用於下列訊息：  
  
-   \<報表項目類型> '\<報表項目名稱>' 有無效的範圍 “\<範圍名稱>”。 範圍必須是目前的範圍，或包含在目前的範圍之內。  
  
-   \<報表項目類型> '\<報表項目名稱>' 的 \<屬性名稱> 運算式含有對彙總函式無效的範圍參數。 範圍參數必須設定為字串常數，此字串常數要和所包含的群組名稱、所包含的資料區域名稱或資料集名稱相同。  
  
 若為計算累加值的彙總函式 (`Previous`、`RunningValue` 或 `RowNumber`)，您可以指定屬於資料列群組名稱或資料行群組名稱的範圍參數，但不可同時屬於這兩者。 這點適用於下列錯誤訊息：  
  
-   `Previous``RunningValue`或是`RowNumber`彙總函式用於資料格中*\<報表項目類型 >* '*\<報表項目名稱 >*' 群組範圍，請參閱在 資料行和資料列*\<報表項目類型 >*。 所有的範圍參數`Previous`，`RunningValue`並`RowNumber`彙總函式內*\<報表項目類型 >* 資料列群組或資料行群組，但不能兩者都可以參考。  
  
 如需詳細資訊，請參閱[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md) 和[運算式中的內建集合 &#40;報表產生器及 SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md)。  
  
### <a name="default-dataset-scope-for-a-top-level-text-box"></a>最上層文字方塊的預設資料集範圍  
 當報表具有多個資料集時，請勿針對加入至報表設計介面的文字方塊使用預設範圍。 請使用包含資料集名稱當做範圍的運算式，以及彙總函式。 例如， `=First(Fields!FieldName.Value, "DataSet2")`。  
  
## <a name="see-also"></a>另請參閱  
 [運算式 &#40;報表產生器及 SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)   
 [彙總函式參考&#40;報表產生器及 SSRS&#41;](../report-design/report-builder-functions-aggregate-functions-reference.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](../report-design/expression-examples-report-builder-and-ssrs.md)   
 [將資料加入至報表&#40;報表產生器及 SSRS&#41;](../report-data/report-datasets-ssrs.md)   
 [常用的篩選 &#40;報表產生器及 SSRS&#41;](../report-design/commonly-used-filters-report-builder-and-ssrs.md)   
 [資料集欄位集合 &#40;報表產生器及 SSRS&#41;](../report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [報表設計師中運算式的自訂程式碼及組件參考 &#40;SSRS&#41;](../report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)   
 [參數集合參考&#40;報表產生器及 SSRS&#41;](../report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
