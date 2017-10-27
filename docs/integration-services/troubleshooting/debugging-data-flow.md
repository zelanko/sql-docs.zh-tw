---
title: "偵錯資料流程 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- progress reporting [Integration Services]
- data viewers [Integration Services]
- data flow [Integration Services], debugging
- debugging [Integration Services], data flow
- counting rows
ms.assetid: 1c574f1b-54f7-4c05-8e42-8620e2c1df0f
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: 7502a4c00ff680dd372114debbfc4d8de4067da3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/28/2017

---
# <a name="debugging-data-flow"></a>偵錯資料流程
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」提供許多功能和工具，讓您用來疑難排解 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝中的資料流程。  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」會提供資料檢視器。  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 轉換會提供資料列計數。  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」提供執行階段的進度報表。  
  
## <a name="data-viewers"></a>資料檢視器  
 資料檢視器可以顯示資料流程中兩個元件之間的資料。 從資料來源擷取資料或資料第一次進入資料流程時、在轉換更新資料之前和之後，以及在資料載入其目的地之前，可以透過資料檢視器來顯示資料。  
  
 若要檢視資料，請將資料檢視器附加至連接兩個資料流程元件的路徑。 具有在不同資料流程元件之間檢視資料的能力，可讓您更容易識別非預期的資料值、檢視轉換變更資料行值的方式，以及探索轉換失敗的原因。 例如，如果您發現參考資料表中的查閱失敗，為了修正此問題，您可能希望加入為空白資料行提供預設資料的轉換。  
  
 資料檢視器可以在方格中顯示資料。 使用方格時，您需要選取要顯示的資料行。 選定資料行的值會以表格格式顯示。  
  
 您也可以在路徑上加入多個資料檢視器， 並以不同格式顯示相同資料，例如，建立資料的圖表檢視與方格檢視，或是為不同資料行建立不同的資料檢視器。  
  
 當您將資料檢視器加入至路徑時，「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」會在 **[資料流程]** 索引標籤之設計介面上的路徑旁邊，加入資料檢視器圖示。 具備多個輸出的轉換 (例如「條件式分割」轉換) 可以在每個路徑上加入資料檢視器。  
  
 在執行階段， **[資料檢視器]** 視窗會開啟，並顯示以資料檢視器格式所指定的資訊。 例如，使用方格格式的資料檢視器會顯示選定資料行的資料、傳遞至資料流程元件的輸出資料列數目，以及顯示的資料列數目。 資訊會以逐一緩衝區的方式顯示，且根據資料流程中的資料列寬度而定，緩衝區可能包含一或多個資料列。  
  
 在 **[資料檢視器]** 對話方塊中，您可以將資料複製到剪貼簿、從資料表清除所有資料、重新設定資料檢視器、繼續資料流程，以及卸離或附加資料檢視器。  
  
#### <a name="to-add-a-data-viewer"></a>若要加入資料檢視器  
  
-   [將資料檢視器加入資料流程](#add_viewer)  
  
## <a name="row-counts"></a>資料列計數  
 經過某個路徑傳送的資料列數目，會顯示在「 **設計師」中** [資料流程] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 索引標籤之設計介面上的該路徑旁邊。 隨著資料不斷經由路徑移動，該數目會定期更新。  
  
 您也可以將「資料列計數」轉換加入資料流程，以擷取變數中的最後資料列計數。 如需詳細資訊，請參閱 [Row Count Transformation](../../integration-services/data-flow/transformations/row-count-transformation.md)。  
  
## <a name="progress-reporting"></a>進度報表  
 當您執行封裝時，「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」會在 **[資料流程]** 索引標籤的設計介面上，使用指示狀態的色彩顯示每個資料流程元件，以描述進度。 當每個元件開始執行其工作時，會從無色彩變更為黃色，並在成功完成時變更為綠色， 紅色則表示該元件已失敗。  
  
 下表描述色彩編碼。  
  
|Color|說明|  
|-----------|-----------------|  
|無色彩|正在等候由資料流程引擎呼叫。|  
|黃色|正在執行轉換、擷取資料或載入資料。|  
|綠色|已成功執行。|  
|紅色|已執行但發生錯誤。|  

## <a name="analysis-of-data-flow"></a>資料流程分析
  您可以使用 [catalog.execution_data_statistics](../../integration-services/system-views/catalog-execution-data-statistics.md) **SSISDB** 資料庫檢視，分析封裝的資料流程。 每當資料流程元件傳送資料至下游元件，此檢視就會顯示一個資料列。 您可以使用這項資訊深入了解傳送至每個元件的資料列。  
  
> [!NOTE]  
>  您必須將記錄層次設定為 [詳細資訊]，以透過 catalog.execution_data_statistics 檢視來擷取資訊。  
  
 下列範例顯示在封裝元件之間傳送的資料列數。  
  
```sql
use SSISDB  
select package_name, task_name, source_component_name, destination_component_name, rows_sent  
from catalog.execution_data_statistics  
where execution_id = 132  
order by source_component_name, destination_component_name   
```  
  
 下列範例計算針對特定執行，每個元件每毫秒所傳送的資料列數目。 計算值包括：  
  
-   **total_rows** - 元件傳送的所有資料列總和  
  
-   **wall_clock_time_ms** – 每個元件經過的執行時間總計 (以毫秒為單位)  
  
-   **num_rows_per_millisecond** – 每個元件每毫秒傳送的資料列數  
  
 **HAVING** 子句可用來避免在計算中發生除以零的錯誤。  
  
```sql  
use SSISDB  
select source_component_name, destination_component_name,  
    sum(rows_sent) as total_rows,  
    DATEDIFF(ms,min(created_time),max(created_time)) as wall_clock_time_ms,  
    ((0.0+sum(rows_sent)) / (datediff(ms,min(created_time),max(created_time)))) as [num_rows_per_millisecond]  
from [catalog].[execution_data_statistics]  
where execution_id = 132  
group by source_component_name, destination_component_name  
having (datediff(ms,min(created_time),max(created_time))) > 0  
order by source_component_name desc  
```  

## <a name="configure-an-error-output-in-a-data-flow-component"></a>在資料流程元件中設定錯誤輸出
  許多資料流程元件都支援錯誤輸出，因元件的不同， [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師會以不同的方式設定錯誤輸出。 除了設定錯誤輸出以外，您也可以設定錯誤輸出的資料行。 其中包括設定此元件所加入的 **ErrorCode** 和 **ErrorColumn** 資料行。  
  
### <a name="configuring-an-error-output"></a>設定錯誤輸出  
 若要設定錯誤輸出，您有兩個選項：  
  
-   使用 [設定錯誤輸出] 對話方塊。 您可以使用此對話方塊，在支援錯誤輸出的任何資料流程元件中設定錯誤輸出。  
  
-   請針對此元件使用編輯器對話方塊。 某些元件可讓您直接從它們的編輯器對話方塊設定錯誤輸出； 但如果是 ADO NET 來源、匯入資料行轉換、OLE DB 命令轉換或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 目的地，您便無法從編輯器對話方塊設定錯誤輸出。  
  
 下列程序描述如何使用這些對話方塊來設定錯誤輸出。  
  
#### <a name="to-configure-an-error-output-using-the-configure-error-output-dialog-box"></a>若要使用 [設定錯誤輸出] 對話方塊設定錯誤輸出  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中，按一下 [資料流程] 索引標籤。  
  
4.  將錯誤輸出 (以紅色箭頭表示) 從錯誤來源元件拖曳到資料流程中的另一個元件。  
  
5.  在 [設定錯誤輸出] 對話方塊中，針對元件輸入中的每個資料行，在 [錯誤] 和 [截斷] 資料行中選取動作。  
  
6.  若要儲存已更新的封裝，請按一下 [檔案] 功能表上的 [儲存選取項目]。  
  
#### <a name="to-add-an-error-output-using-the-editor-dialog-box-for-the-component"></a>針對此元件使用編輯器對話方塊來加入錯誤輸出  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 中，按一下 [資料流程] 索引標籤。  
  
4.  按兩下要在其中設定錯誤輸出的資料流程元件，並依據此元件，執行下列其中一個步驟：  
  
    -   按一下 [設定錯誤輸出]。  
  
    -   按一下 [錯誤輸出]。  
  
5.  為每個資料行設定 [錯誤] 選項。  
  
6.  為每個資料行設定 [截斷] 選項。  
  
7.  按一下 **[確定]**。  
  
8.  若要儲存已更新的封裝，請按一下 [檔案] 功能表上的 [儲存選取項目]。  
  
### <a name="configuring-error-output-columns"></a>設定錯誤輸出資料行  
 若要設定錯誤輸出資料行，您必須使用 [進階編輯器] 對話方塊的 [輸入與輸出屬性] 索引標籤。  
  
#### <a name="to-configure-error-output-columns"></a>設定錯誤輸出資料行  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 中，按一下 [資料流程] 索引標籤。  
  
4.  以滑鼠右鍵按一下要設定其錯誤輸出資料行的元件，並按一下 [顯示進階編輯器]。  
  
5.  按一下**輸入與輸出屬性**索引標籤上，展開  **\<元件名稱 > 錯誤輸出**，然後展開 **輸出資料行**。  
  
6.  按一下資料行並更新其屬性。  
  
    > [!NOTE]  
    >  資料行的清單包括元件輸入中的資料行、上一個錯誤輸出加入的 **ErrorCode** 和 **ErrorColumn** 資料行，以及此元件加入的 **ErrorCode** 和 **ErrorColumn** 資料行。  
  
7.  按一下 **[確定].**  
  
8.  若要儲存已更新的封裝，請按一下 [檔案] 功能表上的 [儲存選取項目]。  

## <a name="add_viewer"></a> 將資料檢視器加入資料流程
  本主題描述如何在資料流程中加入和設定資料檢視器。 資料檢視器可以顯示在兩個資料流程元件之間移動的資料。 例如，在資料流程中的轉換修改從資料來源擷取的資料之前，資料檢視器可以先顯示該資料。  
  
 將一個資料流程元件的輸出與另一元件的輸入連接，路徑可連接資料流程中的元件。  
  
 在可以將資料檢視器加入封裝之前，該封裝必須包括「資料流程」工作和至少兩個連接的資料流程元件。  
  
 將資料檢視器加入錯誤輸出中，以查看錯誤描述以及發生錯誤的資料行名稱。 錯誤輸出預設只包含錯誤和資料行的數值識別碼。  
  
### <a name="to-add-a-data-viewer-to-a-data-flow"></a>若要將資料檢視器加入資料流程  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  如果 [控制流程] 索引標籤尚未處於使用中，請按一下該索引標籤。  
  
4.  按一下要將資料檢視器附加至其資料流程的 [資料流程] 工作，然後按一下 [資料流程] 索引標籤。  
  
5.  以滑鼠右鍵按一下兩個資料流程元件之間的路徑，然後按一下 [編輯]。  
  
6.  在 [一般] 頁面上，您可以檢視和編輯路徑屬性。 例如，您可以從 [PathAnnotation] 下拉式清單選取出現在路徑旁的註解。  
  
7.  在 [中繼資料] 頁面上，您可以檢視資料行中繼資料，並且將中繼資料複製到 [剪貼簿]。  
  
8.  在 [資料檢視器] 頁面上，按一下 [啟用資料檢視器]。  
  
9. 在 [要顯示的資料行] 區域中，選取要在資料檢視器中顯示的資料行。 根據預設，所有可用的資料行都會選取，並且在 [顯示的資料行] 清單中列出。 將不想使用的資料行移至 [未使用的資料行] 清單，方法是選取它們然後按一下向左箭號。  
  
    > [!NOTE]  
    >  在此方格中，代表 DT_DATE、DT_DBTIME2、DT_FILETIME、DT_DBTIMESTAMP、DT_DBTIMESTAMP2 和 DT_DBTIMESTAMPOFFSET 資料類型的值會以 ISO 8601 格式化字串的形式出現，而且空格分隔符號會取代 **T** 分隔符號。 代表 DT_DATE 和 DT_FILETIME 資料類型的值包括小數秒的七位數。 由於 DT_FILETIME 資料類型只會儲存小數秒的三位數，所以此方格會將其餘四位數顯示為零。 代表 DT_DBTIMESTAMP 資料類型的值包括小數秒的三位數。 如果是代表 DT_DBTIME2、DT_DBTIMESTAMP2 和 DT_DBTIMESTAMPOFFSET 資料類型的值，則小數秒的位數會對應到針對資料行資料類型指定的小數位數。 如需 ISO 8601 格式的詳細資訊，請參閱 [日期和時間格式](http://msdn.microsoft.com/library/bed6e2c1-791a-4fa1-b29f-cbfdd1fa8d39)。 如需有關資料類型的詳細資訊，請參閱＜ [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)＞。  
  
10. 按一下 **[確定]**。  

## <a name="data-flow-taps"></a>資料流程點選
 您可以在執行階段於封裝的資料流程路徑上加入資料點選，然後從資料點選將輸出導向至外部檔案。 若要使用此功能，您必須使用專案部署模型將 SSIS 專案部署至 SSIS 伺服器。 將封裝部署至伺服器之後，您需要對 SSISDB 資料庫執行 T-SQL 指令碼先加入資料點選，然後再執行該封裝。 範例狀況如下：  
  
1.  使用 [catalog.create_execution &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md) 預存程序建立封裝的執行執行個體。  
  
2.  使用 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md) 或 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md) 預存程序加入資料點選。  
  
3.  使用 [catalog.start_execution &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) 啟動封裝的執行執行個體。  
  
 以下是執行上述狀況各個步驟的範例 SQL 指令碼：  
  
```sql
Declare @execid bigint  
EXEC [SSISDB].[catalog].[create_execution] @folder_name=N'ETL Folder', @project_name=N'ETL Project', @package_name=N'Package.dtsx', @execution_id=@execid OUTPUT  
EXEC [SSISDB].[catalog].add_data_tap @execution_id = @execid, @task_package_path = '\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[Flat File Source.Flat File Source Output]', @data_filename = 'output.txt'  
EXEC [SSISDB].[catalog].[start_execution] @execid  
```  
  
 create_execution 預存程序的資料夾名稱、專案名稱和封裝名稱參數對應到 Integration Services 目錄中的資料夾、專案和封裝名稱。 您可以從 SQL Server Management Studio 取得 create_execution 呼叫所要使用的資料夾、專案和封裝名稱，如下圖所示。 如果您的 SSIS 專案沒有出現在此，表示您可能尚未將該專案部署至 SSIS 伺服器。 請在 Visual Studio 中以滑鼠右鍵按一下 SSIS 專案，然後按一下 [部署] 將專案部署至所需的 SSIS 伺服器。  
  
 除了輸入 SQL 陳述式之外，執行下列步驟也可以產生執行封裝指令碼：  
  
1.  以滑鼠右鍵按一下 [Package.dtsx]，然後按一下 [執行]。  
  
2.  按一下 **[指令碼]** 工具列按鈕以產生指令碼。  
  
3.  接著，在 start_execution 呼叫前面加入 add_data_tap 陳述式。  
  
 add_data_tap 預存程序的 task_package_path 參數對應到 Visual Studio 中，資料流程工作的 PackagePath 屬性。 在 Visual Studio 中，以滑鼠右鍵按一下 [資料流程工作]，然後按一下 [屬性] 啟動 [屬性] 視窗。  請記下 **PackagePath** 屬性的值，其將做為 add_data_tap 預存程序呼叫的 task_package_path 參數值使用。  
  
 add_data_tap 預存程序的 dataflow_path_id_string 參數對應到您要在其上加入資料點選之資料流程路徑的 IdentificationString 屬性。 若要取得 dataflow_path_id_string，請按一下資料流程路徑 (資料流程中位於工作之間的箭號)，並記下 [屬性] 視窗所示 **IdentificationString** 屬性的值。  
  
 當您執行指令碼時，輸出檔會儲存在\<程式檔案 > \Microsoft SQL Server\110\DTS\DataDumps。 如果已有同名的檔案存在，則將建立附帶尾碼的新檔案 (例如：output[1].txt)。  
  
 如先前所述，您也可以使用 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)預存程序，而不是使用 add_data_tap 預存程序。 此預存程序接受資料流程工作的識別碼當做參數，而非 task_package_path。 您可以從 Visual Studio 屬性視窗取得資料流程工作的識別碼。  
  
### <a name="removing-a-data-tap"></a>移除資料點選  
 您可以使用 [catalog.remove_data_tap](../../integration-services/system-stored-procedures/catalog-remove-data-tap.md) 預存程序，在啟動執行之前移除資料點選。 此預存程序接受資料點選的識別碼當做參數，而識別碼可透過 add_data_tap 預存程序的輸出取得。  
  
```sql
DECLARE @tap_id bigint  
EXEC [SSISDB].[catalog].add_data_tap @execution_id = @execid, @task_package_path = '\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[Flat File Source.Flat File Source Output]', @data_filename = 'output.txt' @data_tap_id=@tap_id OUTPUT  
EXEC [SSISDB].[catalog].remove_data_tap @tap_id  
```  
  
### <a name="listing-all-data-taps"></a>列出所有資料點選  
 您也可以使用 catalog.execution_data_taps 檢視表，列出所有資料點選。 下列範例會擷取規格執行之執行個體 (識別碼：54) 的資料點選。  
  
```sql 
select * from [SSISDB].[catalog].execution_data_taps where execution_id=@execid  
```  
  
### <a name="performance-consideration"></a>效能考量  
 啟用詳細資訊記錄層次和加入資料點選會致使資料整合方案執行更多 I/O 作業。 因此，建議您只有在進行疑難排解時才加入資料點選。  
  
### <a name="video"></a>視訊  
 這部 [TechNet 上的影片](http://technet.microsoft.com/sqlserver/dn600163) 示範了如何在 SQL Server 2012 SSISDB 目錄中加入/使用資料點選，協助您以程式設計方式對封裝進行偵錯及在執行階段擷取部分結果。 該影片也將討論如何列出/移除這些資料點選，以及在 SSIS 封裝中使用資料點選的最佳作法。  
 
## <a name="see-also"></a>另請參閱  
 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)  
  
  
