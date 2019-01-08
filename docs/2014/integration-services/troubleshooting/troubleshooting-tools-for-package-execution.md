---
title: 套件執行的疑難排解工具 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, troubleshooting
- SSIS packages, troubleshooting
- Integration Services, troubleshooting
- errors [Integration Services], troubleshooting
- packages [Integration Services], troubleshooting
ms.assetid: f18d6ff6-e881-444c-a399-730b52130e7c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ca170bbae969db8610e1e0ec6e61e3e68fa905f4
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53377630"
---
# <a name="troubleshooting-tools-for-package-execution"></a>封裝執行的疑難排解工具
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的功能與工具，可讓您在完成及部署封裝之後，用以疑難排解封裝的執行問題。  
  
 在設計階段， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會提供中斷點以暫停封裝的執行，並提供 [進度] 視窗及資料檢視器以監視通過資料流程的資料。 不過，如果您是執行已經部署的封裝，就無法使用這些功能。 以下列出用於疑難排解已部署之封裝的主要技術：  
  
-   使用事件處理常式擷取及處理封裝錯誤。  
  
-   使用錯誤輸出擷取不正確的資料。  
  
-   使用記錄功能追蹤執行封裝的步驟。  
  
 您也可以使用下列秘訣與技巧，避免在執行封裝時發生問題  
  
-   **使用交易協助確保資料的完整性**。 如需詳細資訊，請參閱 [Integration Services 交易](../integration-services-transactions.md)。  
  
-   **使用檢查點從失敗點重新啟動封裝**。 如需詳細資訊，請參閱 [使用檢查點來重新啟動封裝](../packages/restart-packages-by-using-checkpoints.md)。  
  
## <a name="catch-and-handle-package-errors-by-using-event-handlers"></a>使用事件處理常式擷取及處理封裝錯誤  
 您可以使用事件處理常式，回應封裝以及封裝中的物件所引發的許多事件。  
  
-   **建立 OnError 事件的事件處理常式**。 在事件處理常式中，您可以使用傳送郵件工作通知管理員有關失敗的消息，使用指令碼工作與自訂邏輯取得系統資訊以進行疑難排解，或是清除暫存資源或不完全的輸出。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 事件處理常式](../integration-services-ssis-event-handlers.md)。  
  
## <a name="troubleshoot-bad-data-by-using-error-outputs"></a>使用錯誤輸出針對不正確的資料進行疑難排解  
 您可以使用可用於許多資料流程元件的錯誤輸出，將包含錯誤的資料列導向不同目的地，以便稍後進行分析。  
  
-   **使用錯誤輸出擷取不正確的資料**。 將包含錯誤的資料列傳送到不同目的地，例如錯誤資料表或文字檔。 錯誤輸出會自動加入兩個數值資料行，一個包含造成資料列遭到拒絕的錯誤編號，另一個包含發生錯誤之資料行的識別碼。 如需詳細資訊，請參閱 [處理資料中的錯誤](../data-flow/error-handling-in-data.md)。  
  
-   **將易懂資訊加入錯誤輸出**。 除了錯誤輸出所提供的兩個數值識別碼外，您還可以加入描述性的資訊，讓錯誤輸出更容易分析。  
  
     **新增錯誤的描述**。 使用指令碼元件可以很容易地查閱錯誤描述。 如需詳細資訊，請參閱 <<c0> [ 指令碼元件增強錯誤輸出](../extending-packages-scripting-data-flow-script-component-examples/enhancing-an-error-output-with-the-script-component.md)。  
  
     **將錯誤資料行名稱加入**。 在「指令碼」元件中，不容易以錯誤輸出所儲存之資料行識別碼，查閱相對應的資料行名稱，所以需要執行額外的步驟。 資料流程中的每一個資料行識別碼，在該資料流程工作內都是獨一無二的識別碼，並且在設計階段會保存於封裝中。 以下是將資料行名稱加入錯誤輸出的建議方法。 如需如何使用這種方法的範例，請參閱 <<c0> [ 將錯誤資料行名稱加入至錯誤輸出](https://go.microsoft.com/fwlink/?LinkId=261546)dougbert.com 上。  
  
    1.  **建立查閱資料表的資料行名稱**。 建立會使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] API 的個別應用程式，以便反覆查看每個儲存的封裝、封裝中的每個資料流程、資料流程中的每個物件，以及資料流程物件中的每個輸入與輸出。 此應用程式應該保存查閱資料表中的資料行識別碼以及每個資料行的名稱，以及保存父資料流程工作的識別碼與封裝識別碼。  
  
    2.  **將資料行名稱加入至輸出**。 將「查閱」轉換加入至錯誤輸出，以便查閱在先前步驟中所建立之查閱資料表中的資料行名稱。 查閱可以使用錯誤輸出中的資料行識別碼、封裝識別碼 (可在系統變數 System::PackageID 中找到)，以及資料流程工作識別碼 (可在系統變數 System::TaskID 中找到)。  
  
## <a name="troubleshoot-package-execution-by-using-operations-reports"></a>使用作業報表針對封裝執行進行疑難排解  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中提供標準作業報表，可協助您監視已部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。 這些封裝報表可協助您檢視封裝狀態及記錄，如有必要，也可協助您識別失敗原因。  
  
 如需詳細資訊，請參閱[疑難排解封裝執行的報表](troubleshooting-reports-for-package-execution.md)。  
  
## <a name="troubleshoot-package-execution-by-using-ssisdb-views"></a>使用 SSISDB 檢視疑難排解封裝執行  
 系統提供一些您可以查詢的 SSISDB 資料庫檢視，用以監視封裝執行以及其他作業資訊。 如需詳細資訊，請參閱 <<c0> [ 監視封裝執行和其他作業](../performance/monitor-running-packages-and-other-operations.md)。  
  
## <a name="troubleshoot-package-execution-by-using-logging"></a>使用記錄功能針對封裝執行進行疑難排解  
 您可以啟用記錄功能，追蹤執行中之封裝所發生的大部分事件。 記錄提供者會擷取指定之事件的相關資訊，以供稍後分析，並使用資料庫資料表、一般檔案、XML 檔案或其他支援的輸出格式儲存這項資訊。  
  
-   **啟用記錄功能**。 您可以只選取想要擷取其資訊的事件與項目，藉以精簡記錄輸出。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../performance/integration-services-ssis-logging.md)和 [Integration Services &#40;SSIS&#41; 記錄](../performance/integration-services-ssis-logging.md)。  
  
-   **選取封裝的 [診斷] 事件以疑難排解提供者問題。** 現在有可幫助您疑難排解封裝與外部資料來源之間互動的記錄訊息。 如需詳細資訊，請參閱 [Troubleshooting Tools Package Connectivity](troubleshooting-tools-for-package-connectivity.md)。  
  
-   **增強預設的記錄輸出**。 每次執行封裝時，記錄功能通常會將資料列附加至記錄目的地。 雖然記錄輸出的每一個資料列都會以封裝的名稱和唯一識別碼來識別封裝，並且以唯一的 ExecutionID 來識別封裝的執行，但單一清單中若有大量記錄輸出，分析就會變得很困難。  
  
     以下是用於增強預設記錄輸出的一個建議方法，讓您能夠輕鬆地產生報表：  
  
    1.  **建立可記錄封裝每次執行作業的父資料表**。 在這個父資料表中，封裝的各次執行作業只能分別記錄在單一資料列，並使用 ExecutionID 連結到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 記錄資料表中的子記錄。 您可以在每個封裝的開頭使用執行 SQL 工作，以建立這個新的資料列，並記錄開始時間； 接著再於封裝結尾使用另一個執行 SQL 工作，以結束時間、期間與狀態更新資料列。  
  
    2.  **將稽核資訊加入資料流程**。 您可以使用「稽核」轉換將建立或修改每一個資料列的封裝執行資訊，加入資料流程中的資料列。 「稽核」轉換可提供九項資訊，包括 PackageName 和 ExecutionInstanceGUID。 如需詳細資訊，請參閱[稽核轉換](../data-flow/transformations/audit-transformation.md)。 為了進行稽核，如果您有想要加入每個資料列的自訂資訊，便可以使用「衍生的資料行」轉換將這項資訊加入資料流程中的資料列。 如需詳細資訊，請參閱[衍生的資料行轉換](../data-flow/transformations/derived-column-transformation.md)。  
  
    3.  **考慮擷取資料列計數資料**。 請考慮另外建立資料表以存放資料列計數資訊，在此資料表中，是以封裝的 ExecutionID 識別封裝執行的每個執行個體。 使用「資料列計數」轉換，在資料流程的關鍵點將資料列計數儲存到一系列變數中。 資料流程結束後，請使用執行 SQL 工作將這一系列的值插入資料表中的資料列，以供稍後進行分析及製作報表。  
  
     更多這種方法的詳細資訊，請參閱 「 ETL 稽核和記錄 > 一節，在[!INCLUDE[msCoName](../../includes/msconame-md.md)]技術白皮書： [Project REAL:Business Intelligence ETL 設計練習](https://go.microsoft.com/fwlink/?LinkId=96602)。  
  
## <a name="troubleshoot-package-execution-by-using-debug-dump-files"></a>使用偵錯傾印檔案針對封裝執行進行疑難排解  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中，您可以建立偵錯傾印檔案，以便提供封裝執行的資訊。 如需相關資訊，請參閱 [產生封裝執行的傾印檔案](generating-dump-files-for-package-execution.md)。  
  
## <a name="troubleshoot-run-time-validation-issues"></a>疑難排解執行階段驗證的問題  
 有時候在尚未執行封裝中的優先工作之前，您可能無法連接到資料來源，或者無法驗證封裝的某些部分。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含下列功能，可協助您避免因這些狀況而造成的驗證錯誤：  
  
-   **設定載入封裝時無效之封裝元素的 DelayValidation 屬性**。 您可以將組態無效之封裝元素的 `DelayValidation` 設為 `True`，以避免載入封裝時發生驗證錯誤。 例如，您可能有一項會使用目的地資料表的資料流程工作，而這個目的地資料表卻要等到執行 SQL 工作在執行階段建立資料表後才會存在。 `DelayValidation` 屬性可以在封裝層級啟用，也可以在封裝所包含的個別工作和容器層級啟用。  
  
     您可以針對資料流程工作設定 `DelayValidation` 屬性，但無法針對個別資料流程元件設定這個屬性。 將個別資料流程元件的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> 屬性設為 `false`，也可以達到類似的效果。 不過，當這個屬性的值是 `false` 時，元件不會察覺對外部資料來源之中繼資料所做的變更。 設為 `true` 時，<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> 屬性可以協助避免因資料庫中的鎖定而造成的封鎖問題，尤其是在封裝使用交易時。  
  
## <a name="troubleshoot-run-time-permissions-issues"></a>疑難排解執行階段權限的問題  
 如果您嘗試使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 執行已部署封裝時發生錯誤，可能此代理程式所使用的帳戶沒有必要權限。 如需如何為您從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業執行的封裝進行疑難排解的資訊，請參閱[從 SQL Server Agent 作業步驟呼叫 SSIS 封裝時，SSIS 封裝未執行](https://support.microsoft.com/kb/918760)。 如需如何從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業執行封裝的詳細資訊，請參閱[封裝的 SQL Server Agent 作業](../packages/sql-server-agent-jobs-for-packages.md)。  
  
 若要連接至 Excel 或 Access 資料來源， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 需要使用在 TEMP 和 TMP 環境變數所指定之資料夾中有權讀取、寫入、建立和刪除暫存檔的帳戶。  
  
## <a name="troubleshoot-64-bit-issues"></a>疑難排解 64 位元的問題  
  
-   **在 64 位元平台上無法使用某些資料提供者**。 特別是，連接到 Excel 或 Access 資料來源所必須的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet OLE DB Provider 沒有 64 位元版本。  
  
## <a name="troubleshoot-errors-without-a-description"></a>疑難排解沒有隨附描述的錯誤  
 如果您遇到沒有隨附描述的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 錯誤，可以經由查閱錯誤的編號找出列在 [Integration Services 錯誤和訊息參考](../integration-services-error-and-message-reference.md)中的錯誤描述。 此清單這次沒有包含疑難排解資訊。  
  
## <a name="related-tasks"></a>相關工作  
 [在資料流程元件中設定錯誤輸出](../configure-an-error-output-in-a-data-flow-component.md)  
  
## <a name="related-content"></a>相關內容  
 位於 dougbert.com 的部落格項目： [Adding the error column name to an error output](https://go.microsoft.com/fwlink/?LinkId=261546)(將錯誤資料行名稱加入至錯誤輸出)。  
  
  
