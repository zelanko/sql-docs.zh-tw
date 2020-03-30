---
title: 監視執行中套件和其他作業 | Microsoft Docs
ms.custom: supportability
ms.date: 06/04/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.isoperations.executions.f1
- sql13.ssis.ssms.isoperations.general.f1
ms.assetid: cbbcd79f-ab9b-46ec-84cb-4821c1d16b99
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d7fd62f4f2f82e6dcc3921db7099b4f052db27b3
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "79287842"
---
# <a name="monitor-running-packages-and-other-operations"></a>監視執行封裝和其他作業

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  您可以使用下列其中一項或多項工具，監視 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 執行封裝、專案驗證及其他作業。 某些工具 (例如資料點選) 僅適用於部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的專案。  
  
-   記錄  
  
     如需詳細資訊，請參閱 [集成服務 &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
-   報表  
  
     如需詳細資訊，請參閱 [Reports for the Integration Services Server](#reports)。  
  
-   檢視  
  
     如需詳細資訊，請參閱[檢視 &#40;Integration Services 目錄&#41;](../../integration-services/system-views/views-integration-services-catalog.md)。  
  
-   效能計數器  
  
     如需相關資訊，請參閱 [Performance Counters](../../integration-services/performance/performance-counters.md)。  
  
-   資料點選  

> [!NOTE]
> 本文描述如何在一般情況下監視執行中的 SSIS 套件，以及如何在內部部署監視執行中的套件。 您也可以在 Azure SQL Database 中執行並監視 SSIS 套件。 如需詳細資訊，請參閱[將 SQL Server Integration Services 工作負載隨即轉移至雲端](../lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)。
>
> 雖然您也可以在 Linux 上執行 SSIS 套件，但 Linux 上未提供任何監視工具。 如需詳細資訊，請參閱[使用 SSIS 在 Linux 上擷取、轉換和載入資料](../../linux/sql-server-linux-migrate-ssis.md)。

## <a name="operation-types"></a>作業類型  
 **伺服器上的** SSISDB [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中會監視數個不同類型的作業。 每個作業都可以有多則與其相關聯的訊息。 每則訊息可以分類在數種不同的類型之一。 例如，訊息可以是資訊、警告或錯誤等類型。 如需訊息類型的完整清單，請參閱 Transact-SQL [catalog.operation_messages &#40;SSISDB Database&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md) 檢視的文件集。 如需作業類型的完整清單，請參閱 [catalog.operations &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)。  
  
 有九種不同的狀態類型可用來指示作業的狀態。 如需狀態類型的完整清單，請參閱 [catalog.operations &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md) 檢視。  

## <a name="active-operations-dialog-box"></a><a name="active_ops"></a> 作用中的作業對話方塊
  使用 **[作用中的作業]** 對話方塊檢視 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器上目前執行中之 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 作業 (例如，部署、驗證及封裝執行) 的狀態。 此資料儲存在 SSISDB 目錄中。  
  
 如需相關 [!INCLUDE[tsql](../../includes/tsql-md.md)] 檢視的詳細資訊，請參閱 [catalog.operations &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)、[catalog.validations &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-validations-ssisdb-database.md) 和 [catalog.executions &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md)  
  
###  <a name="open-the-active-operations-dialog-box"></a><a name="open_dialog"></a> 開啟 [作用中的作業] 對話方塊  
  
1.  開啟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
2.  連接 Microsoft SQL Server Database Engine  
  
3.  在 [物件總管] 中，展開 **[Integration Services]** 節點，再以滑鼠右鍵按一下 **[SSISDB]** ，然後按一下 **[作用中的作業]** 。  
  
### <a name="configure-the-options"></a>設定選項  
  
 **型別**  
 指定作業的類型。 下列是 **[類型]** 欄位的可能值，以及 Transact-SQL **catalog.operations** 檢視的 operations_type 資料行中的對應值。  
  
|||  
|-|-|  
|初始化 Integration Services|1|  
|作業清除 (SQL 代理程式作業)|2|  
|專案版本清理 (SQL 代理程式作業)|3|  
|部署專案|101|  
|還原專案|106|  
|建立及啟動封裝執行|200|  
|停止作業 (停止驗證或執行|202|  
|驗證專案|300|  
|驗證封裝|301|  
|設定目錄|1000|  
  
 **停止**  
 按一下即可停止目前執行中的作業。  

## <a name="viewing-and-stopping-packages-running-on-the-integration-services-server"></a>檢視及停止在 Integration Services 伺服器上執行的封裝
  **SSISDB** 資料庫會將執行記錄儲存在不會對使用者顯示的內部資料表中。 不過，它會透過可供您查詢的公用檢視來公開您需要的資訊。 另外，它也會提供預存程序，讓您可以加以呼叫，以執行與封裝相關的一般工作。  
  
 通常，您會在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中管理伺服器上的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]物件。 但您也可以直接查詢資料庫檢視並呼叫預存程序，或編寫可呼叫 Managed API 的自訂程式碼。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 Managed API 會查詢檢視並呼叫預存程序，以執行許多工作。 例如，您可以檢視目前正在伺服器上執行之 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的清單，並在需要時要求停止封裝。  
  
### <a name="viewing-the-list-of-running-packages"></a>檢視執行中封裝的清單  
 您可以在 **[作用中的作業]** 對話方塊中檢視目前正在伺服器上執行之封裝的清單。 如需詳細資訊，請參閱 [Active Operations Dialog Box](#active_ops)。  
  
 如需有關可用來檢視執行中封裝清單之其他方法的詳細資訊，請參閱下列主題。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] access  
 若要檢視正在伺服器上執行之封裝的清單，請針對狀態 2 的封裝查詢檢視 [catalog.executions &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md) 。  
  
 透過 Managed API 來以設計程式方式存取  
 請參閱 <xref:Microsoft.SqlServer.Management.IntegrationServices> 命名空間和其類別。  
  
### <a name="stopping-a-running-package"></a>停止執行中的封裝  
 您可以在 **[作用中的作業]** 對話方塊中要求執行中的封裝停止。 如需詳細資訊，請參閱 [Active Operations Dialog Box](#active_ops)。  
  
 如需有關可用來停止執行中封裝之其他方法的詳細資訊，請參閱下列主題。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] access  
 若要停止正在伺服器上執行的封裝，請呼叫預存程序 [catalog.stop_operation &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md)。  
  
 透過 Managed API 來以設計程式方式存取  
 請參閱 <xref:Microsoft.SqlServer.Management.IntegrationServices> 命名空間和其類別。  
  
### <a name="viewing-the-history-of-packages-that-have-run"></a>檢視已執行封裝的記錄  
 若要檢視已在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中執行之封裝的記錄，請使用 **[所有執行]** 報表。 如需 [所有執行]  報表和其他標準報表的詳細資訊，請參閱 [Reports for the Integration Services Server](#reports) (Integration Services 伺服器的報表)。  
  
 如需有關可用來檢視執行中封裝記錄之其他方法的詳細資訊，請參閱下列主題。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] access  
 若要檢視已執行封裝的資訊，請查詢檢視 [catalog.executions &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md)。  
  
 透過 Managed API 來以設計程式方式存取  
 請參閱 <xref:Microsoft.SqlServer.Management.IntegrationServices> 命名空間和其類別。  

## <a name="reports-for-the-integration-services-server"></a><a name="reports"></a> Reports for the Integration Services Server
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的目前版本中， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中提供標準報表，協助您監視已部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。 這些報表可協助您檢視封裝狀態及記錄，如有必要，也可協助您識別封裝執行失敗的原因。  
  
 在每個報表頁面上方，上一步圖示可前往檢視的上一頁，重新整理圖示會重新整理頁面上顯示的資訊，而列印圖示可讓您列印目前頁面。  
  
 如需如何將套件部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的資訊，請參閱[部署 Integration Services (SSIS) 專案和套件](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)。  
  
### <a name="integration-services-dashboard"></a>Integration Services 儀表板  
 [Integration Services 儀表板]  報表提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上所有封裝執行的概觀。 對於伺服器上已執行的每個封裝，儀表板可讓您放大報表，尋找可能發生之封裝執行錯誤的特定詳細資料。  
  
 此報表會顯示下列資訊區段。  
  
|區段|描述|  
|-------------|-----------------|  
|**執行資訊**|顯示在過去 24 小時內，處於不同狀態 (失敗、執行中、成功、其他) 的執行數目。|  
|**封裝資訊**|顯示在過去 24 小時內已經執行之封裝的總數。|  
|**連接資訊**|顯示在過去 24 小時內已經用於失敗執行的連接。|  
|**封裝詳細資訊**|顯示在過去 24 小時內所發生已完成執行的詳細資料。 例如，此區段會顯示失敗的執行數與執行總數、執行期間 (以秒為單位) 及過去三個月的平均值行期間的比較。<br /><br /> 您可以按一下 [概觀]  、[所有訊息]  和 [執行效能]  ，檢視封裝的其他資訊。<br /><br /> [執行效能]  報表會顯示上一個執行個體的持續時間，以及開始和結束時間與套用的環境。<br /><br /> [執行效能]  報表中包含的圖表和相關資料表會顯示過去 10 次成功執行封裝的期間。 此資料表也會顯示過去三個月的平均執行期間。 在執行階段可能會對這 10 次成功的封裝執行套用不同的環境與不同的常值。<br /><br /> 最後，[執行效能]  報表會顯示封裝資料流程元件的 [啟用時間] 和 [總時間]。 [啟用時間] 是指元件在所有階段中執行所耗費的總時間，而 [總時間] 是指元件歷經的總時間。 報表只會在最後一個封裝執行作業的記錄層次設定為 [Performance] 或 [Verbose] 時，顯示封裝元件的這項資訊。<br /><br /> [概觀]  報表會顯示封裝工作的狀態。 [訊息]  報表會顯示封裝和工作的事件訊息和錯誤訊息，例如，回報開始和結束時間，以及寫入的資料列數目。<br /><br /> 您也可以按一下 [概觀]  報表中的 [檢視訊息]  ，導覽至 [訊息]  報表。 您同樣可以按一下 [訊息]  報表中的 [檢視概觀]  ，導覽至 [概觀]  報表。|  
  
 您可以按一下 [篩選]  ，然後選取 [篩選設定]  對話方塊中的準則，篩選任何頁面上顯示的資料表。 可用的篩選準則取決於顯示的資料。 您可以在 [篩選設定]  對話方塊中按一下排序圖示，以變更報表的排序次序。  
  
### <a name="all-executions-report"></a>所有執行報表  
 [所有執行]  報表會顯示伺服器上已執行之所有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 執行的摘要。 範例封裝可能會有多個執行。 與 [Integration Services 儀表板]  報表不同的是，您可以設定 [所有執行]  報表以顯示某個日期範圍內開始的執行。 日期可以跨多天、數個月或數年。  
  
 此報表會顯示下列資訊區段。  
  
|區段|描述|  
|-------------|-----------------|  
|Filter|顯示目前套用至報表的篩選，例如 [開始時間範圍]。|  
|執行資訊|顯示每個封裝執行的開始時間、結束時間和期間。您可以檢視封裝執行使用的參數值清單，例如使用 [執行封裝] 工作傳遞至子封裝的值。 若要檢視參數清單，請按一下 [概觀]。|  
  
 如需使用「執行封裝」工作將值提供給子封裝的詳細資訊，請參閱 [執行封裝工作](../../integration-services/control-flow/execute-package-task.md)。  
  
 如需參數的詳細資訊，請參閱 [Integration Services (SSIS) 封裝和專案參數](../../integration-services/integration-services-ssis-package-and-project-parameters.md)。  
  
### <a name="all-connections"></a>所有連接  
 [所有連接]  報表會針對失敗的連接，以及在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上發生的執行提供下列資訊。  
  
 此報表會顯示下列資訊區段。  
  
|區段|描述|  
|-------------|-----------------|  
|Filter|顯示目前套用至報表的篩選，例如具有指定字串和 [上次失敗時間]  範圍的連接。<br /><br /> 設定 [上次失敗時間]  範圍，就可以只顯示某個日期範圍內發生的連接失敗。 範圍可以跨多天、數個月或數年。|  
|詳細資料|顯示連接字串、發生連接失敗的執行數目，以及上一次連接失敗的日期。|  
  
### <a name="all-operations-report"></a>所有作業報表  
 [所有作業]  報表會顯示伺服器上已執行之所有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 作業的摘要，包括封裝部署、驗證和執行，以及其他管理作業。 就如同 Integration Services 儀表板一樣，您可以將篩選套用至資料表，以縮小顯示的資訊範圍。  
  
### <a name="all-validations-report"></a>所有驗證報表  
 [所有驗證]  報表會顯示伺服器上已執行之所有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 驗證的摘要。 此摘要會顯示每個驗證的資訊，例如狀態、開始時間和結束時間。 每個摘要項目都包含一個指向驗證期間產生之訊息的連結。 就如同 Integration Services 儀表板一樣，您可以將篩選套用至資料表，以縮小顯示的資訊範圍。  
  
### <a name="custom-reports"></a>自訂報表  
 您可以在  **中，將自訂報表 (.rdl 檔案) 加入 [Integration Services 目錄]** **節點底下的 [SSISDB]** [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 目錄節點。 加入報表之前，請確認您正在使用三部分命名慣例來完整限定您所參考的物件，例如來源資料表。 否則， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 將會顯示錯誤。 此命名慣例是 \<資料庫>.\<擁有者>.\<物件>。 SSISDB.internal.executions 就是範例。  
  
> [!NOTE]  
>  當您將自訂報表加入 [資料庫]  節點底下的 [SSISDB]  節點時，不需要使用 SSISDB 前置詞。  
  
 如需如何建立和加入自訂報表的指示，請參閱 [將自訂報表加入 Management Studio](../../ssms/object/add-a-custom-report-to-management-studio.md)。  

## <a name="view-reports-for-the-integration-services-server"></a>檢視 Integration Services 伺服器的報表
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的目前版本中， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中提供標準報表，協助您監視已部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  如需報表的詳細資訊，請參閱 [Integration Services 伺服器的報表](#reports)。  
  
### <a name="to-view-reports-for-the-integration-services-server"></a>若要檢視 Integration Services 伺服器的報表  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，於物件總管中展開 [Integration Services 目錄]  節點。  
  
2.  以滑鼠右鍵按一下 [SSISDB]  ，按一下 [報表]  ，然後按一下 [標準報表]  。  
  
3.  按一下下列其中一項或多項，以檢視報表。  
  
    -   **Integration Services 儀表板**  
  
    -   **所有執行**  
  
    -   **所有驗證**  
  
    -   **所有作業**  
  
    -   **所有連接**  

## <a name="see-also"></a>另請參閱  
 [執行專案和套件](../packages/deploy-integration-services-ssis-projects-and-packages.md)   
 [套件執行的疑難排解報告](../troubleshooting/troubleshooting-reports-for-package-execution.md)  
