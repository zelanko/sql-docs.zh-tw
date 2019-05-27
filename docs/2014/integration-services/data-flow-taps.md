---
title: 資料流程點選 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 2d847adf-4b3d-4949-a195-ef43de275077
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a1938f2389f64d7a869ae924690b8b22fa209f82
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66059911"
---
# <a name="data-flow-taps"></a>資料流程點選
  [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 導入了一項新功能，可讓您在執行階段於封裝的資料流程路徑上加入資料點選，然後從資料點選將輸出導向至外部檔案。 若要使用此功能，您必須使用專案部署模型將 SSIS 專案部署至 SSIS 伺服器。 將封裝部署至伺服器之後，您需要對 SSISDB 資料庫執行 T-SQL 指令碼先加入資料點選，然後再執行該封裝。 範例狀況如下：  
  
1.  使用 [catalog.create_execution &#40;SSISDB Database&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database) 預存程序建立封裝的執行執行個體。  
  
2.  使用 [catalog.add_data_tap](/sql/integration-services/system-stored-procedures/catalog-add-data-tap) 或 [catalog.add_data_tap_by_guid](/sql/integration-services/system-stored-procedures/catalog-add-data-tap-by-guid) 預存程序加入資料點選。  
  
3.  使用 [catalog.start_execution &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database) 啟動封裝的執行執行個體。  
  
 以下是執行上述狀況各個步驟的範例 SQL 指令碼：  
  
```  
  
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
  
 當您執行指令碼時，輸出檔會儲存於 \<Program Files>\Microsoft SQL Server\110\DTS\DataDumps。 如果已有同名的檔案存在，則將建立附帶尾碼的新檔案 (例如：output[1].txt)。  
  
 如先前所述，您也可以使用 [catalog.add_data_tap_by_guid](/sql/integration-services/system-stored-procedures/catalog-add-data-tap-by-guid)預存程序，而不是使用 add_data_tap 預存程序。 此預存程序接受資料流程工作的識別碼當做參數，而非 task_package_path。 您可以從 Visual Studio 屬性視窗取得資料流程工作的識別碼。  
  
## <a name="removing-a-data-tap"></a>移除資料點選  
 您可以使用 [catalog.remove_data_tap](/sql/integration-services/system-stored-procedures/catalog-remove-data-tap) 預存程序，在啟動執行之前移除資料點選。 此預存程序接受資料點選的識別碼當做參數，而識別碼可透過 add_data_tap 預存程序的輸出取得。  
  
```  
  
DECLARE @tap_id bigint  
EXEC [SSISDB].[catalog].add_data_tap @execution_id = @execid, @task_package_path = '\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[Flat File Source.Flat File Source Output]', @data_filename = 'output.txt' @data_tap_id=@tap_id OUTPUT  
EXEC [SSISDB].[catalog].remove_data_tap @tap_id  
  
```  
  
## <a name="listing-all-data-taps"></a>列出所有資料點選  
 您也可以使用 catalog.execution_data_taps 檢視表，列出所有資料點選。 下列範例會擷取規格執行之執行個體的資料點選 (識別碼：54)。  
  
```  
select * from [SSISDB].[catalog].execution_data_taps where execution_id=@execid  
```  
  
## <a name="performance-consideration"></a>效能考量  
 啟用詳細資訊記錄層次和加入資料點選會致使資料整合方案執行更多 I/O 作業。 因此，建議您只有在進行疑難排解時才加入資料點選。  
  
## <a name="video"></a>視訊  
 這部 [TechNet 上的影片](https://technet.microsoft.com/sqlserver/dn600163) 示範了如何在 SQL Server 2012 SSISDB 目錄中加入/使用資料點選，協助您以程式設計方式對封裝進行偵錯及在執行階段擷取部分結果。 該影片也將討論如何列出/移除這些資料點選，以及在 SSIS 封裝中使用資料點選的最佳作法。  
  
## <a name="related-tasks"></a>相關工作  
 [偵錯資料流程](troubleshooting/debugging-data-flow.md)  
  
 [套件執行的疑難排解工具](troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
  
