---
title: CDC 來源 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.cdcsource.f1
- sql13.ssis.designer.cdcsource.connection.f1
- sql13.ssis.designer.cdcsource.columns.f1
- sql13.ssis.designer.cdcsource.errorhandling.f1
ms.assetid: 99775608-e177-44ed-bb44-aaccb0f4f327
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c487852af232224304e0d746f0ab32bf0fe90dbe
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58290534"
---
# <a name="cdc-source"></a>CDC 來源
  CDC 來源會從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 變更資料表中讀取變更資料的範圍，並將這些變更向下游傳遞至其他 SSIS 元件。  
  
 CDC 來源所讀取的變數資料範圍稱為 CDC 處理範圍，並且由目前資料流程啟動之前執行的 CDC 控制工作所決定。 CDC 處理範圍衍生自維護資料表群組之 CDC 處理狀態的封裝變數值。  
  
 CDC 來源會使用資料庫資料表、檢視或 SQL 陳述式，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中擷取資料。  
  
 CDC 來源使用下列組態：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ADO.NET 連接管理員，用以存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 資料庫。 如需設定 CDC 來源連接的詳細資訊，請參閱 [CDC 來源編輯器 &#40;連線管理員頁面&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)。  
  
-   啟用 CDC 的資料表。  
  
-   所選資料表的擷取執行個體名稱 (如果 more-than-one 存在)。  
  
-   變更處理模式。  
  
-   做為決定 CDC 處理範圍之依據的 CDC 狀態封裝變數名稱。 CDC 來源不會修改該變數。  
  
 CDC 來源傳回的資料與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 函式 **cdc.fn_cdc_get_all_changes_\<擷取執行個體名稱>** 或 **cdc.fn_cdc_get_net_changes_\<擷取執行個體名稱>** (如果有) 傳回的資料相同。 唯一的選擇性附加資料行是 **__$initial_processing** ，表示目前處理範圍是否可與資料表的初始載入重疊。 如需初始處理的詳細資訊，請參閱 [CDC 控制工作](../../integration-services/control-flow/cdc-control-task.md)。  
  
 CDC 來源有一個一般輸出和一個錯誤輸出。  
  
## <a name="error-handling"></a>錯誤處理  
 CDC 來源有錯誤輸出。 此元件的錯誤輸出包含下列輸出資料行：  
  
-   **錯誤碼**：此值一律為 -1。  
  
-   **錯誤資料行**：造成錯誤 (用於轉換錯誤) 的來源資料行。  
  
-   **錯誤資料列資料行**：造成錯誤的記錄資料。  
  
 根據錯誤行為設定，CDC 來源支援在錯誤輸出中傳回擷取程序期間發生的錯誤 (資料轉換、截斷)。  
  
## <a name="data-type-support"></a>資料類型支援  
 Microsoft 的 CDC 來源元件支援所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型，這些資料類型都會對應至正確的 SSIS 資料類型。  
  
## <a name="troubleshooting-the-cdc-source"></a>CDC 來源的疑難排解  
 以下包含 CDC 來源的疑難排解資訊。  
  
### <a name="use-this-script-to-isolate-problems-and-reproduce-them-in-sql-server-management-studio"></a>使用此指令碼來隔離問題，並在 SQL Server Management Studio 中重現問題。  
 CDC 來源作業是由叫用 CDC 來源之前執行的 CDC 控制工作作業所控制。 CDC 控制工作會準備 CDC 狀態封裝變數的值，以包含開始和結束 LSN。 它所執行的功能相當於下列指令碼：  
  
```sql
use <cdc-enabled-database-name>  
               declare @start_lsn binary(10), @end_lsn binary(10)  
               set @start_lsn = sys.fn_cdc_increment_lsn(  
                       convert(binary(10),'0x' + '<value-from-state-cs>', 1))  
               set @end_lsn =   
                       convert(binary(10),'0x' + '<value-from-state-ce>', 1)  
               select * from cdc.fn_cdc_get_net_changes_dbo_Table1(@start_lsn,  
@end_lsn, '<mode>')  
```  
  
 其中：  
  
-   \<cdc-enabled-database-name> 是包含變更資料表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫名稱。  
  
-   \<value-from-state-cs> 是在 CDC 狀態變數中顯示為 CS/\<value-from-state-cs>/ 的值 (CS 代表 Current-processing-range-Start)。  
  
-   \<value-from-state-ce> 是在 CDC 狀態變數中顯示為 CE/\<value-from-state-cs>/ 的值 (CE 代表 Current-processing-range-End)。  
  
-   \<模式> 是 CDC 處理模式。 處理模式有下列其中一個值：[全部]、[全部 (含舊值)]、[淨]、[淨 (含更新遮罩)]、[淨 (含合併)]。  
  
 此指令碼會在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中重現問題，協助您輕鬆重現及識別錯誤以隔離問題。  
  
#### <a name="sql-server-error-message"></a>SQL Server 錯誤訊息  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可能會傳回下列訊息：  
  
 **提供給程序或函式 cdc.fn_cdc_get_net_changes_\<..>** 的引數數量不足。  
  
 此錯誤並不表示缺少引數。 它表示 CDC 狀態變數中的開始或結束 LSN 值無效。  
  
## <a name="configuring-the-cdc-source"></a>設定 CDC 來源  
 您可以透過程式設計方式或 SSIS 設計師來設定 CDC 來源。  
  
 如需詳細資訊，請參閱下列其中一個主題：  
  
-   [CDC 來源編輯器 &#40;連線管理員頁面&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)  
  
-   [CDC 來源編輯器 &#40;資料行頁面&#41;](../../integration-services/data-flow/cdc-source-editor-columns-page.md)  
  
-   [CDC 來源編輯器 &#40;錯誤輸出頁面&#41;](../../integration-services/data-flow/cdc-source-editor-error-output-page.md)  
  
 **[進階編輯器]** 對話方塊包含可以程式設計方式設定的屬性。  
  
 若要開啟 **[進階編輯器]** 對話方塊：  
  
-   在 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 專案的 [資料流程] 畫面中，以滑鼠右鍵按一下 CDC 來源，然後選取 [顯示進階編輯器]。  
  
 如需可在 [進階編輯器] 對話方塊中設定之屬性的詳細資訊，請參閱 [CDC 來源自訂屬性](../../integration-services/data-flow/cdc-source-custom-properties.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [CDC 來源自訂屬性](../../integration-services/data-flow/cdc-source-custom-properties.md)  
  
-   [使用 CDC 來源擷取變更資料](../../integration-services/data-flow/extract-change-data-using-the-cdc-source.md)  
  
## <a name="cdc-source-editor-connection-manager-page"></a>CDC 來源編輯器 (連接管理員頁面)
  使用 [CDC 來源編輯器] 對話方塊的 [連線管理員] 頁面，即可針對 CDC 來源從中讀取變更資料列的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 資料庫 (CDC 資料庫) 選取 ADO.NET 連線管理員。 一旦選取 CDC 資料庫之後，您就必須在資料庫中選取擷取的資料表。  
  
 如需 CDC 來源的詳細資訊，請參閱 [CDC 來源](../../integration-services/data-flow/cdc-source.md)。  
  
### <a name="task-list"></a>工作清單  
 **若要開啟 CDC 來源編輯器的連接管理員頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，開啟具有 CDC 來源的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 封裝。  
  
2.  在 [資料流程] 索引標籤中，按兩下 CDC 來源。  
  
3.  在 [CDC 來源編輯器] 中，按一下 [連線管理員]。  
  
### <a name="options"></a>選項。  
 **ADO.NET 連接管理員**  
 從清單中選取現有的連接管理員，或按一下 [新增] 建立新的連接。 此連接必須指向啟用 CDC 而且包含選取之變更資料表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。  
  
 **新增**  
 按一下 **[新增]**。 [設定 ADO.NET 連線管理員編輯器] 對話方塊隨即開啟，讓您能夠建立新的連線管理員。  
  
 **CDC 資料表**  
 選取 CDC 來源資料表，其中包含您想要讀取並饋送至下游 SSIS 元件進行處理的擷取變更。  
  
 **擷取執行個體**  
 選取或輸入包含要讀取之 CDC 資料表的 CDC 擷取執行個體名稱。  
  
 擷取的來源資料表可以具有一個或兩個擷取執行個體，以便透過結構描述變更處理資料表定義的流暢轉換。 如果針對所擷取的來源資料表定義了多個擷取執行個體，請在此選取您想要使用的擷取執行個體。 [schema].[table] 資料表的預設擷取執行個體名稱是 \<結構描述>_\<資料表>，但是使用中的實際擷取執行個體名稱可能有所不同。 實際讀取的資料表是 CDC 資料表 **cdc .\<capture-instance>_CT**。  
  
 **CDC 處理模式**  
 選取可有效處理處理需求的處理模式。 可能的選項包括：  
  
-   **全部**：傳回目前 CDC 範圍中的變更，不含 [更新之前] 值。  
  
-   **全部 (含舊值)**：傳回目前 CDC 處理範圍中的變更，包括舊值 ([更新前])。 每個更新作業都有兩個資料列：一個包含更新之前的值，另一個則包含更新之後的值。  
  
-   **淨**：只針對目前 CDC 處理範圍中修改的每個來源資料列傳回一項變更。 如果來源資料列更新了許多次，就會產生結合的變更 (例如，插入+更新會產生為單一更新，而更新+刪除則產生為單一刪除)。 在淨變更處理模式中工作時，您可以將變更分割成刪除、插入和更新輸出，並且以平行方式處理它們，因為單一來源資料列會出現在多個輸出中。  
  
-   **淨 (含更新遮罩)**：這種模式與一般的淨模式很相似，但還新增了名稱模式為 **__$\<資料行名稱>\__Changed** 的布林資料行，表示目前變更資料列中的變更資料行。  
  
-   **淨 (含合併)**：這種模式與一般的淨模式很相似，但是插入和更新作業會合併成單一合併作業 (UPSERT)。  
  
> [!NOTE]  
>  對於所有淨變更選項而言，來源資料表必須具有主索引鍵或唯一索引。 如果資料表沒有主索引鍵或唯一索引，您就必須使用 [全部] 選項。  
  
 **包含 CDC 狀態的變數**  
 選取針對目前 CDC 內容維護 CDC 狀態的 SSIS 字串封裝變數。 如需 CDC 狀態變數的詳細資訊，請參閱 [定義狀態變數](../../integration-services/data-flow/define-a-state-variable.md)。  
  
 **包含重新處理指標資料行**  
 選取此核取方塊即可建立名為 **__$reprocessing**的特殊輸出資料行。  
  
 當 CDC 處理範圍與初始處理範圍 (對應至初始載入週期之 LSN 的範圍) 重疊，或者上一次執行發生錯誤之後重新處理 CDC 處理範圍時，這個資料行的值就是 **true** 。 這個指標資料行可讓 SSIS 開發人員在重新處理變更時以不同的方式處理錯誤 (例如，可以忽略刪除不存在的資料列以及在重複索引鍵上失敗的插入等動作)。  
  
 如需詳細資訊，請參閱 [CDC 來源自訂屬性](../../integration-services/data-flow/cdc-source-custom-properties.md)。  
  
## <a name="cdc-source-editor-columns-page"></a>CDC 來源編輯器 (資料行頁面)
  使用 [CDC 來源編輯器] 對話方塊的 [資料行] 頁面，即可將輸出資料行對應至每個外部 (來源) 資料行。  
  
### <a name="task-list"></a>工作清單  
 **若要開啟 CDC 來源編輯器的資料行頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，開啟具有 CDC 來源的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 封裝。  
  
2.  在 [資料流程] 索引標籤中，按兩下 CDC 來源。  
  
3.  在 **[CDC 來源編輯器]** 中，按一下 **[資料行]**。  
  
### <a name="options"></a>選項。  
 **可用的外部資料行**  
 資料來源中可用的外部資料行清單。 您無法使用此資料表來加入或刪除資料行。 請在來源中選取要使用的資料行。 選取的資料行就會依照選取的順序加入至 **[外部資料行]** 清單。  
  
 **[外部資料行]**  
 外部 (來源) 資料行的檢視，這些資料行會依照您在設定取用 CDC 來源資料之元件時所看見的順序列出。 若要變更此順序，請先清除 **[可用的外部資料行]** 清單中的選取資料行，然後依照不同的順序，從清單選取外部資料行。 選取的資料行就會依照您選取的順序加入至 **[外部資料行]** 清單。  
  
 **輸出資料行**  
 為每個輸出資料行輸入唯一的名稱。 預設值為選取之外部 (來源) 資料行的名稱。不過，您也可以選擇任何唯一的描述性名稱。 輸入的名稱就會顯示在 SSIS 設計師中。  
  
## <a name="cdc-source-editor-error-output-page"></a>CDC 來源編輯器 (錯誤輸出頁面)
  使用 [CDC 來源編輯器] 對話方塊的 [錯誤輸出] 頁面，即可選取錯誤處理選項。  
  
### <a name="task-list"></a>工作清單  
 **若要開啟 CDC 來源編輯器的錯誤輸出頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，開啟具有 CDC 來源的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 封裝。  
  
2.  在 [資料流程] 索引標籤中，按兩下 CDC 來源。  
  
3.  在 [CDC 來源編輯器] 中，按一下 [錯誤輸出]。  
  
### <a name="options"></a>選項。  
 **輸入/輸出**  
 檢視資料來源的名稱。  
  
 **資料行**  
 檢視您在 [CDC 來源編輯器] 對話方塊的 [連線管理員] 頁面上所選取的外部 (來源) 資料行。  
  
 **錯誤**  
 選取 CDC 來源應該如何處理流程中的錯誤：忽略失敗、重新導向資料列，或使元件失效。  
  
 **截斷**  
 選取 CDC 來源應該如何處理流程中的截斷：忽略失敗、重新導向資料列，或使元件失效。  
  
 **說明**  
 未使用。  
  
 **將這個值設定到選取的資料格**  
 選取發生錯誤或截斷時 CDC 來源如何處理所有選取的資料格：忽略失敗、重新導向資料列，或使元件失效。  
  
 **套用**  
 將錯誤處理選項套用至選取的資料格。  
  
### <a name="error-handling-options"></a>錯誤處理選項  
 您可以使用下列選項來設定 CDC 來源處理錯誤和截斷的方式。  
  
 **失敗元件**  
 當發生錯誤或截斷時，資料流程工作將失敗。 這是預設行為。  
  
 **忽略失敗**  
 系統會忽略錯誤或截斷，並將資料列導向至 CDC 來源輸出。  
  
 **重新導向流程**  
 系統會將錯誤或截斷資料列導向至 CDC 來源的錯誤輸出。 在此情況中，就會使用 CDC 來源錯誤處理。 如需詳細資訊，請參閱 [CDC 來源](../../integration-services/data-flow/cdc-source.md)。  
  
## <a name="related-content"></a>相關內容  
  
-   mattmasson.com 上的部落格文章：[Processing Modes for the CDC Source](https://www.mattmasson.com/2012/01/processing-modes-for-the-cdc-source/)。  
  
  
