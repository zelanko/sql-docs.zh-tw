---
title: ODBC 目的地 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.odbcdest.f1
- sql13.ssis.designer.odbcdest.connection.f1
- sql13.ssis.designer.odbcdest.columns.f1
- sql13.ssis.designer.odbcdest.errorhandling.f1
ms.assetid: bffa63e0-c737-4b54-b4ea-495a400ffcf8
author: janinezhang
ms.author: janinez
ms.openlocfilehash: bb521fa88cdfe5bc95cacceb7f5c0ebf521e337f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031285"
---
# <a name="odbc-destination"></a>ODBC 目的地

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  ODBC 目的地會將資料大量載入到 ODBC 支援的資料庫資料表。 ODBC 目的地使用 ODBC 連接管理員來連接到資料來源。  
  
 ODBC 目的地包含輸入資料行與目的地資料來源中資料行之間的對應。 您不一定要將輸入資料行對應到所有目的地資料行，但因目的地資料行屬性的不同，如果輸入資料行未對應到目的地資料行，則可能發生錯誤。 例如，如果目的地資料行不允許 Null 值，則輸入資料行必須對應到該資料行。 此外，雖然可對應不同類型的資料行，但是如果輸入資料與目的地資料行類型不相容，在執行階段會發生錯誤。 根據錯誤行為設定，錯誤會被忽略，導致失敗，或者資料列會傳送至錯誤輸出。  
  
 ODBC 目的地具有一個一般輸出和一個錯誤輸出。  
  
##  <a name="BKMK_odbcdestination_loadoptions"></a> 載入選項  
 ODBC 目的地可以使用兩種存取載入模組其中之一。 您會在 [ODBC 來源編輯器 &#40;連線管理員頁面&#41;](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md) 設定模式。 兩種模式為：  
  
-   **批次**：在此模式中，ODBC 目的地會根據所見的 ODBC 提供者功能，嘗試使用最有效率的插入方法。 對於最新的 ODBC 提供者，這表示準備含有參數的 INSERT 陳述式，然後使用資料列取向的陣列參數繫結 (陣列大小是由 **BatchSize** 屬性所控制)。 如果您選取 [批次]  ，而提供者不支援此方法，ODBC 目的地會自動切換為**逐列**模式。  
  
-   **逐列**：在此模式中，ODBC 目的地會準備含有參數的 INSERT 陳述式，然後使用 **SQL Execute**，一次插入一個資料列。  
  
## <a name="error-handling"></a>錯誤處理  
 ODBC 目的地有錯誤輸出。 此元件的錯誤輸出包含下列輸出資料行：  
  
-   **錯誤碼**：對應至目前錯誤的編號。 如需錯誤清單，請參閱來源資料庫的文件集。 如需 SSIS 錯誤碼清單，請參閱＜SSIS 錯誤碼和訊息參考＞。  
  
-   **錯誤資料行**：造成錯誤 (用於轉換錯誤) 的來源資料行。  
  
-   標準輸出資料行。  
  
 根據錯誤行為設定，ODBC 目的地支援在錯誤輸出中傳回擷取程序期間發生的錯誤 (資料轉換、截斷)。 如需詳細資訊，請參閱 [ODBC 來源編輯器 &#40;錯誤輸出頁面&#41;](../../integration-services/data-flow/odbc-source-editor-error-output-page.md)。  
  
## <a name="parallelism"></a>平行處理原則  
 可針對相同電腦或不同電腦上的相同資料表或不同資料表平行執行的 ODBC 目的地元件數目不受限制 (除了一般全域工作階段限制之外)。  
  
 然而，所使用的 ODBC 提供者的限制可能會限制透過提供者的並行連接數目。 這些限制會限制 ODBC 目的地支援的平行執行個體數目。 SSIS 開發人員必須知道所使用的任何 ODBC 提供者的限制，並在建立 SSIS 封裝時將這些限制納入考量。  
  
 您還必須知道同時載入到相同資料表可能會因為標準記錄鎖定而降低效能。 這取決於正在載入的資料和資料表組織。  
  
## <a name="troubleshooting-the-odbc-destination"></a>ODBC 目的地疑難排解  
 您可以記錄 ODBC 來源對外部資料提供者所執行的呼叫。 您可以使用這項記錄功能，針對 ODBC 目的地所執行之將資料儲存至外部資料來源的作業進行疑難排解。 若要記錄 ODBC 目的地對外部資料提供者執行的呼叫，請啟用 ODBC 驅動程式管理員追蹤。 如需詳細資訊，請參閱 Microsoft 文件集＜如何使用 ODBC 資料來源管理員產生 ODBC 追蹤＞。   
  
## <a name="configuring-the-odbc-destination"></a>設定 ODBC 目的地  
 您可以透過程式設計方式或 SSIS 設計師來設定 ODBC 目的地。  
  
 如需詳細資訊，請參閱下列其中一個主題：  
  
-   [ODBC 目的地編輯器 &#40;連線管理員頁面&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)  
  
-   [ODBC 目的地編輯器 &#40;對應頁面&#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)  
  
-   [ODBC 目的地編輯器 &#40;錯誤輸出頁面&#41;](../../integration-services/data-flow/odbc-destination-editor-error-output-page.md)  
  
 **[進階編輯器]** 對話方塊包含可以程式設計方式設定的屬性。  
  
 若要開啟 **[進階編輯器]** 對話方塊：  
  
-   在 **專案的** [資料流程] [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 畫面中，以滑鼠右鍵按一下 ODBC 目的地，然後選取 **[顯示進階編輯器]** 。  
  
 如需有關可在 [進階編輯器] 對話方塊中設定之屬性的詳細資訊，請參閱＜ [ODBC Destination Custom Properties](../../integration-services/data-flow/odbc-destination-custom-properties.md)＞。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [使用 ODBC 目的地來載入資料](../../integration-services/data-flow/load-data-by-using-the-odbc-destination.md)  
  
-   [ODBC 目的地自訂屬性](../../integration-services/data-flow/odbc-destination-custom-properties.md)  
  
## <a name="odbc-destination-editor-connection-manager-page"></a>ODBC 目的地編輯器 (連接管理員頁面)
  使用 **[ODBC 目的地編輯器]** 對話方塊的 **[連接管理員]** 頁面，即可選取目的地的 ODBC 連接管理員。 這個頁面也可以讓您從資料庫中選取資料表或檢視表。  
  
 **若要開啟 ODBC 目的地編輯器的連接管理員頁面**  
  
### <a name="task-list"></a>工作清單  
  
-   在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，開啟具有 ODBC 目的地的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 封裝。  
  
-   在 [資料流程]  索引標籤中，按兩下 ODBC 目的地。  
  
-   在 **[ODBC 目的地編輯器]** 中，按一下 **[連接管理員]** 。  
  
### <a name="options"></a>選項。  
  
#### <a name="connection-manager"></a>[ODBC 來源編輯器]  
 從清單中選取現有的 ODBC 連接管理員，或按一下 [新增] 建立新的連接。 此連接可以指向任何 ODBC 支援的資料庫。  
  
#### <a name="new"></a>新增  
 按一下 **[新增]** 。 **[設定 ODBC 連接管理員編輯器]** 對話方塊隨即開啟，讓您能夠建立新的連接管理員。  
  
#### <a name="data-access-mode"></a>資料存取模式  
 選取將資料載入目的地的方法。 下表將顯示這些選項：  
  
|選項|Description|  
|------------|-----------------|  
|資料表名稱 - 批次|若要將 ODBC 目的地設定成以批次模式運作，請選取此選項。 當您選取此選項時，可以使用下列選項：|  
||**資料表或檢視表的名稱**：從清單中選取資料表或檢視。<br /><br /> 此清單只包含前 1000 個資料表。 如果您的資料庫包含超過 1000 個資料表，您可以輸入資料表名稱的開頭或使用 (\*) 萬用字元來輸入名稱的任何部分，以便顯示您想要使用的資料表。<br /><br /> **批次大小**：輸入大量載入的批次大小。 這是當做批次載入的資料列數目。|  
|資料表名稱 - 逐列|若要將 ODBC 目的地設定成插入每個資料列至目的地資料表 (一次一個)，請選取此選項。 當您選取此選項時，可以使用下列選項：|  
||**資料表或檢視表的名稱**：從清單中的資料庫選取資料表或檢視。<br /><br /> 此清單只包含前 1000 個資料表。 如果您的資料庫包含超過 1000 個資料表，您可以輸入資料表名稱的開頭或使用 (*) 萬用字元來輸入名稱的任何部分，以便顯示您想要使用的資料表。|  
  
#### <a name="preview"></a>預覽  
 按一下 **[預覽]** ，最多可檢視您所選取之資料表的 200 個資料列。  
  
## <a name="odbc-destination-editor-mappings-page"></a>ODBC 目的地編輯器 (對應頁面)
  使用 [ODBC 目的地編輯器]  對話方塊的 [對應]  頁面，即可將輸入資料行對應至目的地資料行。  
  
### <a name="options"></a>選項。  
  
#### <a name="available-input-columns"></a>可用的輸入資料行  
 可用輸入資料行的清單。 將輸入資料行拖放至可用的目的地資料行，即可對應資料行。  
  
#### <a name="available-destination-columns"></a>可用的目的地資料行  
 可用目的地資料行的清單。 將目的地資料行拖放至可用的輸入資料行，即可對應資料行。  
  
#### <a name="input-column"></a>輸入資料行  
 檢視所選取的輸入資料行。 您可以選取 [\<忽略>]  移除對應，排除輸出的資料行。  
  
#### <a name="destination-column"></a>目的地資料行  
 檢視所有可用的目的地資料行，包括對應和取消對應的資料行。  
  
## <a name="odbc-destination-editor-error-output-page"></a>ODBC 目的地編輯器 (錯誤輸出頁面)
  使用 **[ODBC 目的地編輯器]** 對話方塊的 **[錯誤輸出]** 頁面，即可選取錯誤處理選項。  
  
 **若要開啟 ODBC 目的地編輯器的錯誤輸出頁面**  
  
### <a name="task-list"></a>工作清單  
  
-   在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，開啟具有 ODBC 目的地的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 封裝。  
  
-   在 [資料流程]  索引標籤中，按兩下 ODBC 目的地。  
  
-   在 **[ODBC 目的地編輯器]** 中，按一下 **[錯誤輸出]** 。  
  
### <a name="options"></a>選項。  
  
#### <a name="inputoutput"></a>輸入/輸出  
 檢視資料來源的名稱。  
  
#### <a name="column"></a>「資料行」  
 未使用。  
  
#### <a name="error"></a>錯誤  
 選取 ODBC 目的地應該如何處理流程中的錯誤：忽略失敗、重新導向資料列，或使元件失效。  
  
#### <a name="truncation"></a>截斷  
 選取 ODBC 目的地應該如何處理流程中的截斷：忽略失敗、重新導向資料列，或使元件失效。  
  
#### <a name="description"></a>Description  
 檢視錯誤的描述。  
  
#### <a name="set-this-value-to-selected-cells"></a>將這個值設定到選取的資料格  
 選取發生錯誤或截斷時 ODBC 目的地如何處理所有選取的資料格：忽略失敗、重新導向資料列，或使元件失效。  
  
#### <a name="apply"></a>套用  
 將錯誤處理選項套用至選取的資料格。  
  
### <a name="error-handling-options"></a>錯誤處理選項  
 您可以使用下列選項來設定 ODBC 目的地處理錯誤和截斷的方式。  
  
#### <a name="fail-component"></a>失敗元件  
 當發生錯誤或截斷時，資料流程工作將失敗。 這是預設行為。  
  
#### <a name="ignore-failure"></a>忽略失敗  
 忽略錯誤或截斷。  
  
#### <a name="redirect-flow"></a>重新導向流程  
 導致錯誤或截斷的資料列會導向至 ODBC 目的地的錯誤輸出。 如需詳細資訊，請參閱＜ODBC 目的地＞。  
  
