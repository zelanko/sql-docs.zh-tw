---
title: ODBC 來源 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.odbcsource.f1
- sql13.ssis.designer.odbcsource.connection.f1
- sql13.ssis.designer.odbcsource.columns.f1
- sql13.ssis.designer.odbcsource.errorhandling.f1
ms.assetid: abcf34eb-9140-4100-82e6-b85bccd22abe
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7382675ca38ecaabd685d68e0dc31f09e94be6ad
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86914976"
---
# <a name="odbc-source"></a>ODBC 來源

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  ODBC 來源會使用資料庫資料表、檢視或 SQL 陳述式，從 ODBC 支援的資料庫中擷取資料。  
  
 ODBC 來源有下列資料存取模式可供擷取資料：  
  
-   資料表或檢視。  
  
-   SQL 陳述式的結果。  
  
 來源使用 ODBC 連接管理員，指定要使用的提供者。  
  
 ODBC 來源包含來源資料輸出資料行。 在 ODBC 目的地中將輸入資料行對應到目的地資料行時，如果沒有輸入資料行對應到目的地資料行，可能會發生錯誤。 可對應不同類型的資料行，但是如果輸出資料與目的地不相容，在執行階段會發生錯誤。 根據錯誤行為設定，錯誤會被忽略，導致失敗，或者資料列會傳送至錯誤輸出。  
  
 ODBC 來源有一個一般輸出和一個錯誤輸出。  
  
## <a name="error-handling"></a>錯誤處理  
 ODBC 來源有錯誤輸出。 此元件的錯誤輸出包含下列輸出資料行：  
  
-   **錯誤碼**：對應至目前錯誤的編號。 請參閱 ODBC 支援的資料庫的文件集，以取得錯誤清單。 如需 SSIS 錯誤碼清單，請參閱＜SSIS 錯誤碼和訊息參考＞。  
  
-   **錯誤資料行**：造成錯誤 (用於轉換錯誤) 的來源資料行。  
  
-   標準輸出資料行。  
  
 根據錯誤行為設定，ODBC 來源支援在錯誤輸出中傳回擷取程序期間發生的錯誤 (資料轉換、截斷)。 如需詳細資訊，請參閱 [ODBC 目的地編輯器 &#40;連線管理員頁面&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)。  
  
## <a name="data-type-support"></a>資料類型支援  
 如需有關 ODBC 來源支援之資料類型的資訊，請參閱＜Connector for Open Database Connectivity (ODBC)＞。  
  
## <a name="extract-options"></a>擷取選項  
 ODBC 來源以 [批次]  或 [逐列]  模式操作。 所用的模式是由 **FetchMethod** 屬性所決定。 下列清單描述這些模式。  
  
-   **批次**：元件會根據所見的 ODBC 提供者功能，嘗試使用最有效率的提取方法。 對於最新型的 ODBC 提供者，這是 SQLFetchScroll 與陣列繫結搭配使用 (陣列大小是由 **BatchSize** 屬性所決定)。 如果您選取 [批次]  ，而提供者不支援此方法，ODBC 目的地會自動切換為**逐列**模式。  
  
-   **逐列**：元件會使用 SQLFetch，一次擷取一個資料列。  
  
 如需有關 **FetchMethod** 屬性的詳細資訊，請參閱＜ [ODBC Source Custom Properties](../../integration-services/data-flow/odbc-source-custom-properties.md)＞。  
  
## <a name="parallelism"></a>平行處理原則  
 可針對相同電腦或不同電腦上的相同資料表或不同資料表平行執行的 ODBC 來源元件數目不受限制 (除了一般全域工作階段限制之外)。  
  
 然而，所使用的 ODBC 提供者的限制可能會限制透過提供者的並行連接數目。 這些限制會限制 ODBC 來源支援的平行執行個體數目。 SSIS 開發人員必須知道所使用的任何 ODBC 提供者的限制，並在建立 SSIS 封裝時將這些限制納入考量。  
  
## <a name="troubleshooting-the-odbc-source"></a>ODBC 來源的疑難排解  
 您可以記錄 ODBC 來源對外部資料提供者所執行的呼叫。 您可以使用這項記錄功能，疑難排解 ODBC 來源執行的從外部資料來源載入資料的作業。 若要記錄 ODBC 來源對外部資料提供者執行的呼叫，請啟用 ODBC 驅動程式管理員追蹤。 如需詳細資訊，請參閱 Microsoft 文件集＜如何使用 ODBC 資料來源管理員產生 ODBC 追蹤＞。   
  
## <a name="configuring-the-odbc-source"></a>設定 ODBC 來源  
 您可以透過程式設計方式或 SSIS 設計師來設定 ODBC 來源。  
  
 **[進階編輯器]** 對話方塊包含可以程式設計方式設定的屬性。  
  
 若要開啟 **[進階編輯器]** 對話方塊：  
  
-   在 **專案的** [資料流程] [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 畫面中，以滑鼠右鍵按一下 ODBC 來源，然後選取 **[顯示進階編輯器]** 。  
  
 如需有關可在 [進階編輯器] 對話方塊中設定之屬性的詳細資訊，請參閱＜ [ODBC Source Custom Properties](../../integration-services/data-flow/odbc-source-custom-properties.md)＞。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [使用 ODBC 來源來擷取資料](../../integration-services/data-flow/extract-data-by-using-the-odbc-source.md)  
  
-   [ODBC 來源自訂屬性](../../integration-services/data-flow/odbc-source-custom-properties.md)  
  
## <a name="odbc-source-editor-connection-manager-page"></a>ODBC 來源編輯器 (連接管理員頁面)
  使用 **[ODBC 來源編輯器]** 對話方塊的 **[連接管理員]** 頁面，即可選取來源的 ODBC 連接管理員。 這個頁面也可以讓您從資料庫中選取資料表或檢視。  
  
### <a name="task-list"></a>工作清單  
 **若要開啟 ODBC 來源編輯器的連接管理員頁面**  
  
-   在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，開啟具有 ODBC 來源的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 封裝。  
  
-   在 [資料流程]  索引標籤上，按兩下 ODBC 來源。  
  
### <a name="options"></a>選項。  
  
#### <a name="connection-manager"></a>[ODBC 來源編輯器]  
 從清單中選取現有的 ODBC 連接管理員，或按一下 **[新增]** 建立新的連接。 此連接可以指向任何 ODBC 支援的資料庫。  
  
#### <a name="new"></a>新增  
 按一下 **[新增]** 。 **[設定 ODBC 連接管理員編輯器]** 對話方塊隨即開啟，讓您能夠建立新的 ODBC 連接管理員。  
  
#### <a name="data-access-mode"></a>資料存取模式  
 選取從來源中選取資料的方法。 下表將顯示這些選項：  
  
|選項|描述|  
|------------|-----------------|  
|資料表名稱|從 ODBC 資料來源中的資料表或檢視表擷取資料。 當您選取此選項時，請從清單中選取下列項目的值：|  
||**資料表或檢視表的名稱**：從清單中選取可用的資料表或檢視表，或是輸入可識別資料表的規則運算式。|  
||此清單只包含前 1000 個資料表。 如果您的資料庫包含超過 1000 個資料表，您可以輸入資料表名稱的開頭或使用 (*) 萬用字元來輸入名稱的任何部分，以便顯示您想要使用的資料表。|  
|SQL (命令)|使用 SQL 查詢從 ODBC 資料來源中擷取資料。 您應該以目前所使用之來源資料庫的語法撰寫查詢。 當您選取此選項時，請用下列其中一種方式輸入查詢：|  
||在 **[SQL 命令文字]** 欄位中輸入 SQL 查詢的文字。|  
||按一下 **[瀏覽]** ，從文字檔載入 SQL 查詢。|  
||按一下 **[剖析查詢]** 驗證查詢文字的語法。|  
  
#### <a name="preview"></a>預覽  
 按一下 **[預覽]** ，最多可檢視從所選取之資料表或檢視表中擷取的前 200 個資料列。  
  
## <a name="odbc-source-editor-columns-page"></a>ODBC 來源編輯器 (資料行頁面)
  使用 [ODBC 來源編輯器]  對話方塊的 [資料行]  頁面，即可將輸出資料行對應至每個外部 (來源) 資料行。  
  
### <a name="task-list"></a>工作清單  
 **若要開啟 ODBC 來源編輯器的資料行頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，開啟具有 ODBC 來源的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 封裝。  
  
2.  在 [資料流程]  索引標籤上，按兩下 ODBC 來源。  
  
3.  在 **[ODBC 來源編輯器]** 中，按一下 **[資料行]** 。  
  
### <a name="options"></a>選項。  
  
#### <a name="available-external-columns"></a>可用的外部資料行  
 資料來源中可用的外部資料行清單。 您無法使用此資料表來加入或刪除資料行。 請從來源選取要使用的資料行。 選取的資料行就會依照選取的順序加入至 **[外部資料行]** 清單。  
  
 選取 **[全選]** 核取方塊，即可選取所有資料行。  
  
#### <a name="external-column"></a>外部資料行  
 外部 (來源) 資料行的檢視，這些資料行會依照您在設定取用 ODBC 來源資料之元件時所看見的順序列出。  
  
#### <a name="output-column"></a>輸出資料行  
 為每個輸出資料行輸入唯一的名稱。 預設值為選取的外部 (來源) 資料行的名稱；不過，您也可以選擇任何唯一的、描述性的名稱。 輸入的名稱就會顯示在 SSIS 設計師中。  
  
## <a name="odbc-source-editor-error-output-page"></a>ODBC 來源編輯器 (錯誤輸出頁面)
  使用 **[ODBC 來源編輯器]** 對話方塊的 **[錯誤輸出]** 頁面，即可選取錯誤處理選項。  
  
### <a name="task-list"></a>工作清單  
 **若要開啟 ODBC 來源編輯器的錯誤輸出頁面**  
  
-   在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，開啟具有 ODBC 來源的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 封裝。  
  
-   在 [資料流程]  索引標籤上，按兩下 ODBC 來源。  
  
-   在 **[ODBC 來源編輯器]** 中，按一下 **[錯誤輸出]** 。  
  
### <a name="options"></a>選項。  
  
#### <a name="inputoutput"></a>輸入/輸出  
 檢視資料來源的名稱。  
  
#### <a name="column"></a>資料行  
 未使用。  
  
#### <a name="error"></a>錯誤  
 選取 ODBC 來源應該如何處理流程中的錯誤：忽略失敗、重新導向資料列，或使元件失效。  
  
#### <a name="truncation"></a>截斷  
 選取 ODBC 來源應該如何處理流程中的截斷：忽略失敗、重新導向資料列，或使元件失效。  
  
#### <a name="description"></a>描述  
 未使用。  
  
#### <a name="set-this-value-to-selected-cells"></a>將這個值設定到選取的資料格  
 選取發生錯誤或截斷時 ODBC 來源如何處理所有選取的資料格：忽略失敗、重新導向資料列，或使元件失效。  
  
#### <a name="apply"></a>套用  
 將錯誤處理選項套用至選取的資料格。  
  
### <a name="error-handling-options"></a>錯誤處理選項  
 您可以使用下列選項來設定 ODBC 來源處理錯誤和截斷的方式。  
  
#### <a name="fail-component"></a>失敗元件  
 當發生錯誤或截斷時，資料流程工作將失敗。 此為預設行為。  
  
#### <a name="ignore-failure"></a>忽略失敗  
 忽略錯誤或截斷。  
  
#### <a name="redirect-flow"></a>重新導向流程  
 導致錯誤或截斷的資料列會導向至 ODBC 來源的錯誤輸出。  
  
  
