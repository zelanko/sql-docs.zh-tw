---
title: 執行 Integration Services (SSIS) 套件 | Microsoft Docs
ms.custom: ''
ms.date: 06/04/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.ispackageexecute.f1
- sql13.ssis.ssms.executepackage.f1
helpviewer_keywords:
- Integration Services packages, running
- SSIS packages, running
- packages [Integration Services], running
- SQL Server Integration Services packages, running
- executing packages [Integration Services]
- running packages [Integration Services]
- Integration Services, (See also Integration Services packages)
ms.assetid: c5fecc23-6f04-4fb2-9a29-01492ea41404
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b46ed84db9ad5339639119a8d5f29644c7be8fc7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47757336"
---
# <a name="run-integration-services-ssis-packages"></a>執行 Integration Services (SSIS) 封裝
  若要執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，您可以根據這些封裝的儲存位置使用數種工具的其中一種。 工具會列在下表中。  

> [!NOTE]
> 本文描述如何在一般情況下執行 SSIS 套件，以及如何在內部部署執行套件。 您也可以在下列平台上執行 SSIS 套件：
> - **Microsoft Azure 雲端**。 如需詳細資訊，請參閱[將 SQL Server Integration Services 工作負載隨即轉移至雲端](../lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)和[在 Azure 中執行 SSIS 套件](../lift-shift/ssis-azure-run-packages.md)。
> - **Linux**。 如需詳細資訊，請參閱[使用 SSIS 在 Linux 上擷取、轉換和載入資料](../../linux/sql-server-linux-migrate-ssis.md)。
  
 若要將封裝儲存於 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器，您可使用專案部署模型將專案部署到伺服器上。 如需資訊，請參閱[部署 Integration Services (SSIS) 專案和套件](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)。  
  
 若要將封裝儲存在 SSIS 封裝存放區、msdb 資料庫或是檔案系統中，您可使用封裝部署模型。 如需詳細資訊，請參閱[舊版封裝部署 &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)。  
  
|工具|儲存在 Integration Services 伺服器上的封裝|儲存在 SSIS 封裝存放區或是 msdb 資料庫中的封裝|儲存在檔案系統中，但不在 SSIS 封裝存放區中的封裝|  
|----------|-----------------------------------------------------------------|--------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|  
|**SQL Server Data Tools**|否|否<br /><br /> 但是，您可以將 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區中現有的封裝加入專案，其中包括 msdb 資料庫。 用這種方式來將現有封裝加入專案，會在檔案系統中建立封裝的本機複本。|是|  
|**SQL Server Management Studio (當您連接到主控 Integration Services 伺服器的 Database Engine 執行個體時)**<br /><br /> 如需詳細資訊，請參閱 [執行封裝對話方塊](#execute_package_dialog)|是|否<br /><br /> 但是，您可以將封裝從這些位置匯入伺服器。|否<br /><br /> 但是，您可以將封裝從檔案系統匯入伺服器。|
|**SQL Server Management Studio (當您連接到主控已啟用為相應放大主機之 Integration Services 伺服器的 Database Engine 執行個體時)**<br /><br /> 如需詳細資訊，請參閱[在 [相應放大] 中執行套件](../../integration-services/scale-out/run-packages-in-integration-services-ssis-scale-out.md)|是|否|否|
|**SQL Server Management Studio (當連接到管理 SSIS 套件存放區的 Integration Services 服務時)**|否|是|否<br /><br /> 但是，您可以從檔案系統將封裝匯入 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區。|  
|**dtexec**<br /><br /> 如需詳細資訊，請參閱 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)。|是|是|是|  
|**dtexecui**<br /><br /> 如需詳細資訊，請參閱[執行封裝公用程式 &#40;DtExecUI&#41; UI 參考](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md)|否|是|是|  
|**SQL Server Agent**<br /><br /> 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業排程封裝。<br /><br /> 如需詳細資訊，請參閱 [封裝的 SQL Server Agent 作業](../../integration-services/packages/sql-server-agent-jobs-for-packages.md)。|是|是|是|  
|**內建預存程序**<br /><br /> 如需詳細資訊，請參閱 [catalog.start_execution &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)|是|否|否|  
|**Managed API (使用** <xref:Microsoft.SqlServer.Management.IntegrationServices> 命名空間中的類型和成員)|是|否|否|  
|**Managed API (使用** <xref:Microsoft.SqlServer.Dts.Runtime> 命名空間中的類型和成員)|非目前|是|是|  

## <a name="execution-and-logging"></a>執行與記錄  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝可以啟用記錄功能，您可以在記錄檔中擷取執行階段資訊。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
 您可以使用作業報表監視部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器並在其中執行的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中可提供此報告。 如需詳細資訊，請參閱 [Reports for the Integration Services Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports)。  
  
## <a name="run-a-package-in-sql-server-data-tools"></a>在 SQL Server Data Tools 中執行套件
  在開發、偵錯和測試封裝期間，您通常會在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中執行封裝。 當您從「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」執行封裝時，封裝一定會立即執行。  
  
 封裝執行時， [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師會在 **[進度]** 索引標籤上顯示封裝執行的進度。您可以檢視封裝的開始和結束時間、它的工作和容器，以及封裝中任何失敗之工作或容器的相關資訊。 在完成執行封裝後，執行階段資訊會在 [執行結果] 索引標籤上保持可用。如需詳細資訊，請參閱＜ [Debugging Control Flow](../../integration-services/troubleshooting/debugging-control-flow.md)＞主題中的＜進度報表＞一節。  
  
 **設計階段部署**。 當您在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中執行封裝時，會建立封裝，然後部署至資料夾。 在執行封裝之前，您可以指定要用來部署封裝的資料夾。 如果未指定資料夾，預設將會使用 **bin** 資料夾。 這種類型的部署稱為設計階段部署。  
  
### <a name="to-run-a-package-in-sql-server-data-tools"></a>若要在 SQL Server Data Tools 中執行封裝  
  
1.  在方案總管中，如果您的方案包含多個專案，請以滑鼠右鍵按一下包含封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案，然後按一下 [設定為啟始物件] 以設定啟始物件。  
  
2.  在方案總管中，如果您的專案包含多個封裝，請以滑鼠右鍵按一下封裝，然後按一下 [設定為啟始物件] 以設定啟始封裝。  
  
3.  若要執行封裝，請使用下列其中一個程序：  
  
    -   開啟您要執行的封裝，然後按一下功能表列上的 **[啟動偵錯]** ，或按下 F5。 在封裝完成執行後，按下 Shift+F5 以返回設計模式。  
  
    -   在方案總管中，以滑鼠右鍵按一下封裝，然後按一下 [執行封裝]。  
  
### <a name="to-specify-a-different-folder-for-design-time-deployment"></a>若要為設計階段部署指定不同的資料夾  
  
1.  在方案總管中，以滑鼠右鍵按一下包含您要執行之封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案資料夾，然後按一下 [屬性]。  
  
2.  在 [\<專案名稱> 屬性頁] 對話方塊中，按一下 [建置]。  
  
3.  更新 OutputPath 屬性中的值，以指定要用於設計階段部署的資料夾，然後按一下 [確定]。  


## <a name="run-a-package-on-the-ssis-server-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 在 SSIS 伺服器上執行套件
  將專案部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器之後，即可在伺服器上執行封裝。  
  
 您可以使用作業報表，檢視已在伺服器上執行過或目前正在執行之封裝的相關資訊。 如需詳細資訊，請參閱 [Reports for the Integration Services Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports)。  
  
### <a name="to-run-a-package-on-the-server-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 在伺服器上執行封裝  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 並連接至包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目錄的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 執行個體。  
  
2.  依序展開 [物件總管] 中的 **[Integration Services 目錄]** 節點和 **[SSISDB]** 節點，然後導覽至已部署之專案中包含的封裝。  
  
3.  以滑鼠右鍵按一下封裝名稱，然後選取 [執行]。  
  
4.  使用 **[執行封裝]** 對話方塊中， **[參數]**、 **[連線管理員]** 和 **[進階]** 標籤上的設定，設定封裝執行。  
  
5.  按一下 **[確定]** 以執行封裝。  
  
     -或-  
  
     使用預存程序來執行封裝。 按一下 [指令碼]，產生用以建立執行之執行個體與啟動執行之執行個體的 Transact-SQL 陳述式。 此陳述式包含了對 catalog.create_execution、catalog.set_execution_parameter_value 和 catalog.start_execution 預存程序的呼叫。 如需這些預存程序的詳細資訊，請參閱 [catalog.create_execution &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)、[catalog.set_execution_parameter_value &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) 和 [catalog.start_execution &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)。  

## <a name="execute_package_dialog"></a> 執行封裝對話方塊
  使用 **[執行封裝]** 對話方塊，即可執行儲存在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器上的封裝。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝可能會包含參考儲存在環境變數中之值的參數。 在執行這種封裝前，您必須指定要使用何種環境來提供環境變數值。 專案可能包含多個環境，但是執行期間只能使用一個環境來繫結環境變數值。 如果封裝中沒有使用環境變數，就不需要環境。  
  
 您想要做什麼事？  
  
-   [開啟 [執行封裝] 對話方塊](#open_dialog)  
  
-   [設定 [一般] 頁面上的 [選項]](#general)  
  
-   [設定 [參數] 索引標籤上的 [選項]](#parameters)  
  
-   [設定[連接管理員] 索引標籤上的 [選項]](#connection)  
  
-   [設定 [進階] 索引標籤上的 [選項]](#advanced)  
  
-   [編寫執行封裝對話方塊中之選項的指令碼](#script)  
  
###  <a name="open_dialog"></a> 開啟 [執行封裝] 對話方塊  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，連接至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器。  
  
     您正在連接到主控 SSISDB 資料庫之 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體。  
  
2.  在 [物件總管] 中，展開樹狀目錄以顯示 **[Integration Services 目錄]** 節點。  
  
3.  展開 **[SSISDB]** 節點。  
  
4.  展開包含您要執行之封裝的資料夾。  
  
5.  以滑鼠右鍵按一下封裝，然後按一下 [執行]。  
  
###  <a name="general"></a> 設定 [一般] 頁面上的 [選項]  
 選取 **[環境]** 來指定適用於執行執行封裝的環境。  
  
###  <a name="parameters"></a> 設定 [參數] 索引標籤上的 [選項]  
 使用 **[參數]** 索引標籤來修改封裝執行時所使用的參數值。  
  
###  <a name="connection"></a> 設定[連接管理員] 索引標籤上的 [選項]  
 使用 [連接管理員] 索引標籤設定封裝連接管理員的屬性。  
  
###  <a name="advanced"></a> 設定 [進階] 索引標籤上的 [選項]  
 使用 [進階] 索引標籤管理屬性和其他封裝設定。  
  
 [加入]、[編輯]、[移除]  
 按一下可加入、編輯或移除屬性。  
  
 **記錄層級**  
 選取用於執行封裝的記錄層級。 如需詳細資訊，請參閱 [catalog.set_execution_parameter_value &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)。  
  
 **在發生錯誤時傾印**  
 指定在封裝執行期間發生錯誤時是否建立傾印檔。 如需相關資訊，請參閱 [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)。  
  
 **32 位元執行階段**  
 指定封裝將會在 32 位元系統上執行。  
  
###  <a name="script"></a> 編寫執行封裝對話方塊中之選項的指令碼  
 當您位於 **[執行封裝]** 對話方塊時，也可以使用工具列上的 **[指令碼]** 按鈕來為您撰寫 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼。 產生的指令碼會使用您在 [執行封裝] 對話方塊中已選取的相同選項來呼叫預存程序 [catalog.start_execution &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)。 指令碼會出現在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]的新指令碼視窗中。  

## <a name="see-also"></a>另請參閱  
 [dtexec 公用程式](../../integration-services/packages/dtexec-utility.md)   
[啟動 SQL Server 匯入和匯出精靈](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)
  
  
