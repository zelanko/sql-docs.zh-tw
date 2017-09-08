---
title: "Excel 目的地，|Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.exceldest.f1
- sql13.dts.designer.exceldestadapter.connection.f1
- sql13.dts.designer.exceldestadapter.mappings.f1
- sql13.dts.designer.exceldestadapter.erroroutput.f1
helpviewer_keywords:
- destinations [Integration Services], Excel
- Excel [Integration Services]
ms.assetid: 37c07446-1264-4814-b4f5-9c66d333bb24
caps.latest.revision: 49
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 7d5bc198ae3082c1b79a3a64637662968b0748b2
ms.openlocfilehash: 69a0a8b907fcb45cf6ecd0576fb6fba04775d237
ms.contentlocale: zh-tw
ms.lasthandoff: 08/17/2017

---
# <a name="excel-destination"></a>Excel 目的地
  Excel 目的地會將資料載入至 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 活頁簿中的工作表或範圍。  
  
## <a name="access-modes"></a>存取模式  
 Excel 目的地提供三種不同的資料存取模式用於載入資料：  
  
-   資料表或檢視。  
  
-   在變數中指定的資料表或檢視。  
  
-   SQL 陳述式的結果。 查詢可以是參數化查詢。  
  
> [!IMPORTANT]  
>  在 Excel 中，工作表或範圍相當於資料表或檢視。 「Excel 來源」及「Excel 目的地」編輯器中的可用資料表清單，僅會顯示現有工作表 (以附加到工作表名稱的 $ 符號識別，例如 Sheet1$) 及具名範圍 (以沒有 $ 符號的方式識別，例如 MyRange)。  
  
## <a name="usage-considerations"></a>使用狀況的考量  
 Excel 連線管理員會使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet 4.0 及其支援的 Excel ISAM (Indexed Sequential Access Method，索引循序存取方法) 驅動程式，連接和讀寫資料至 Excel 資料來源。  
  
 許多現有的「 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知識庫」文件都有記錄此提供者和驅動程式的行為，而即使這些文件並非 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或其前置的「資料轉換服務」專用，您仍會想了解可能導致未預期結果的特定行為。 如需有關 Excel 驅動程式之使用與行為的一般資訊，請參閱＜ [如何從 Visual Basic 或 VBA 搭配使用 ADO 與 Excel 資料](http://support.microsoft.com/kb/257819)＞。  
  
 在將資料儲存至 Excel 目的地時，下列隨附於 Excel 驅動程式之 Jet 提供者的行為可能會導致非預期的結果。  
  
-   **儲存文字資料**。 將文字資料值儲存至 Excel 目的地時，Excel 驅動程式會在每個資料格的文字前面加上單引號字元 (')，以確保儲存的值會被解譯為文字值。 如果您擁有或開發讀取或處理儲存值的其他應用程式，您可能必須包含加在每個文字值前面的單引號字元的特殊處理。  
  
     如需如何避免包含單引號的資訊，請參閱 msdn.com 上的此篇部落格文章 [使用 SSIS 封裝中 Excel 資料流程目的地元件將資料轉換至 Excel 時，附加至所有字串的單引號](http://go.microsoft.com/fwlink/?LinkId=400876)(英文)。  
  
-   **正在儲存備忘 (ntext) 資料**。 在 Excel 資料行中成功儲存長於 255 個字元的字串之前，驅動程式必須能將目的地資料行的資料類型辨識為 **備忘** ，而不是 **字串**。 如果目的地資料表已包含資料列，則驅動程式所取樣的前幾個資料列必須在備忘資料行中至少包含一個值長於 255 個字元的執行個體。 如果目的地資料表是在封裝設計期間或在執行階段建立，則 CREATE TABLE 陳述式必須使用 LONGTEXT (或其同義字之一) 做為備忘資料行的資料類型。  
  
-   **資料類型**。 Excel 驅動程式只能辨識有限的一組資料類型。 例如，所有的數值資料行都會被解譯為倍整數 (DT_R8)，而所有的字串資料行 (備忘錄資料行除外) 全都會被解譯成 255 個字元的 Unicode 字串 (DT_WSTR)。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 對應 Excel 資料類型的情況如下：  
  
    -   數值 - 雙精確度浮點數 (DT_R8)  
  
    -   貨幣 - 貨幣 (DT_CY)  
  
    -   布林值 - 布林值 (DT_BOOL)  
  
    -   日期/時間 -     **datetime** (DT_DATE)  
  
    -   字串 - Unicode 字串，長度 255 (DT_WSTR)  
  
    -   備忘錄 - Unicode 文字資料流 (DT_NTEXT)  
  
-   **資料類型和長度轉換**： [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 不會隱含地轉換資料類型。 因此，您可能必須使用衍生的資料行轉換或資料轉換，在將 Excel 資料載入到非 Excel 目的地之前明確轉換 Excel 資料，或是在將非 Excel 資料載入到 Excel 目的地之前轉換資料。 在這種情況下，使用「匯入和匯出精靈」建立初始封裝可能很有用，因為這個精靈會為您設定必要的轉換。 某些轉換範例可能必須包含下列各項：  
  
    -   Unicode Excel 字串資料行與具有特定字碼頁之非 Unicode 字串資料行之間的轉換。  
  
    -   255 個字元之 Excel 字串資料行與不同長度之字串資料行之間的轉換。  
  
    -   雙精確度 Excel 數值資料行與其他類型之數值資料行之間的轉換。  
  
## <a name="configuration-of-the-excel-destination"></a>設定 Excel 目的地  
 Excel 目的地會使用 Excel 連接管理員，以連接到資料來源，而連接管理員會指定要使用的活頁簿檔案。 如需詳細資訊，請參閱 [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md)。  
  
 Excel 目的地擁有一個規則輸入與一個錯誤輸出。  
  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之所有屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Excel 自訂屬性](../../integration-services/data-flow/excel-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
-   [連接至 Excel 活頁簿](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
-   [使用 Foreach 迴圈容器來循環使用 Excel 檔案和資料表](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
-   [設定資料流程元件的屬性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>相關內容  
  
-   dougbert.com 上的部落格文章： [Integration Services 中的 Excel (第一部分，共三部分)：連接與元件](http://go.microsoft.com/fwlink/?LinkId=217674)   
  
-   dougbert.com 上的部落格文章： [Integration Services 中的 Excel (第二部分，共三部分)：資料表與資料類型](http://go.microsoft.com/fwlink/?LinkId=217675)。  
  
-   dougbert.com 上的部落格文章： [Integration Services 中的 Excel (第三部分，共三部分)：問題與替代方案](http://go.microsoft.com/fwlink/?LinkId=217676)。  
  
## <a name="excel-destination-editor-connection-manager-page"></a>Excel 目的地編輯器 (連接管理員頁面)
  使用 **[Excel 目的地編輯器]** 對話方塊的 **[連接管理員]** 頁面，來指定資料來源資訊，以及預覽結果。 Excel 目的地會將資料載入 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 活頁簿中的工作表或具名範圍。  
  
> [!NOTE]  
>  在 **[Excel 目的地編輯器]** 中無法使用 Excel 目的地的 **CommandTimeout**屬性，但可使用 **[進階編輯器]**來設定這個屬性。 此外， **[進階編輯器]**中只會有特定的快速載入選項。 如需有關這個屬性的詳細資訊，請參閱＜ [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md)＞的＜Excel 目的地＞一節。  
  
### <a name="static-options"></a>靜態選項  
 **Excel 連接管理員**  
 從清單中選取現有的 Excel 連線管理員，或按一下 [新增] 建立新的連線管理員。  
  
 **新**  
 使用 [Excel 連線管理員] 對話方塊來建立新的連線管理員。  
  
 **資料存取模式**  
 從來源中指定選取資料的方法。  
  
|選項|說明|  
|------------|-----------------|  
|資料表或檢視|將資料載入 Excel 資料來源中的工作表或具名範圍。|  
|資料表名稱或檢視名稱變數|在變數中指定工作表或範圍名稱。<br /><br /> **相關資訊：**[在封裝中使用變數](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|SQL (命令)|使用 SQL 查詢將資料載入 Excel 目的地。|  
  
 **Excel 工作表的名稱**  
 從下拉式清單中選取 Excel 目的地。 如果此清單為空，請按一下 **[新增]**。  
  
 **新**  
 按一下 [新增] 以啟動 [建立工資料表] 對話方塊。 按一下 **[確定]**時，對話方塊會建立 **[Excel 連接管理員]** 指向的 Excel 檔案。  
  
 **檢視現有的資料**  
 使用 [預覽查詢結果] 對話方塊來預覽結果。 預覽最多可顯示 200 個資料列。  
  
> [!WARNING]  
>  如果您選取的 [Excel 連線管理員] 指向不存在的 Excel 檔，則在您按一下此按鈕時將看到一條錯誤消息。  
  
### <a name="data-access-mode-dynamic-options"></a>資料存取模式動態選項  
  
#### <a name="data-access-mode--table-or-view"></a>資料存取模式 = 資料表或檢視  
 **Excel 工作表的名稱**  
 從資料來源裡可用的資訊清單中，選取工作表或具名範圍的名稱。  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>資料存取模式 = 資料表名稱或檢視名稱變數  
 **變數名稱**  
 選取包含工作表名稱或具名範圍的變數。  
  
#### <a name="data-access-mode--sql-command"></a>資料存取模式 = SQL 命令  
 **SQL 命令文字**  
 輸入 SQL 查詢的文字，按一下 [建立查詢] 來建立查詢，或是按一下 [瀏覽] 以找出包含查詢文字的檔案。  
  
 **建立查詢**  
 使用 [查詢產生器] 對話方塊，以視覺化的方式來建構 SQL 查詢。  
  
 **瀏覽**  
 使用 [開啟] 對話方塊來找出包含 SQL 查詢文字的檔案。  
  
 **剖析查詢**  
 請確認查詢文字的語法。  
  
## <a name="excel-destination-editor-mappings-page"></a>Excel 目的地編輯器 (對應頁面)
  使用 **[Excel 目的地編輯器]** 對話方塊的 **[對應]** 頁面，將輸入資料行對應至目的地資料行。  
  
### <a name="options"></a>選項  
 **可用的輸入資料行**  
 檢視可用的輸入資料行清單。 使用拖放作業，即可將資料表中的可用輸入資料行對應到目的地資料行。  
  
 **可用的目的地資料行**  
 檢視可用的目的地資料行清單。 使用拖放作業，即可將資料表中的可用目的地資料行對應到輸入資料行。  
  
 **輸入資料行**  
 從上述資料表檢視選取的輸入資料行。 您可以使用 **[可用的輸入資料行]**清單來變更對應。  
  
 **目的地資料行**  
 檢視每個可用的目的地資料行，不論是否已經對應。  
  
## <a name="excel-destination-editor-error-output-page"></a>Excel 目的地編輯器 (錯誤輸出頁面)
  使用 [Excel 目的地編輯器] 對話方塊的 [進階] 頁面，即可指定錯誤處理的選項。  
  
### <a name="options"></a>選項  
 **輸入或輸出**  
 檢視資料來源的名稱。  
  
 **[資料行]**  
 檢視您在 [Excel 來源編輯器] 對話方塊的 [連線管理員] 節點中所選取的外部 (來源) 資料行。  
  
 **錯誤**  
 指定錯誤發生時要採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **相關主題** [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **截斷**  
 指定截斷發生時要採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **說明**  
 檢視錯誤的描述。  
  
 **將這個值設定到選取的資料格**  
 指定發生錯誤或截斷時要對所有選取之資料格採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **套用**  
 將錯誤處理選項套用至選取的資料格。  
  
## <a name="see-also"></a>另請參閱  
 [Excel 來源](../../integration-services/data-flow/excel-source.md)   
 [Integration Services &#40;SSIS &#41;變數](../../integration-services/integration-services-ssis-variables.md)   
 [資料流程](../../integration-services/data-flow/data-flow.md)   
 [使用 with the Script Task Excel 檔案](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
  
  
