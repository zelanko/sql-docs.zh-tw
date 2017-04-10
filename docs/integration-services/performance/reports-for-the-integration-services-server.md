---
title: "Integration Services 伺服器的報表 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.SWB.SUMMARY.RENDER.CUSTOM.REPORT.F1"
ms.assetid: e976e7c0-a805-4370-bf73-356c8e3becfb
caps.latest.revision: 17
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 17
---
# Integration Services 伺服器的報表
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的目前版本中，[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中提供標準報表，協助您監視已部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。 這些報表可協助您檢視封裝狀態及記錄，如有必要，也可協助您識別封裝執行失敗的原因。  
  
 在每個報表頁面上方，上一步圖示可前往檢視的上一頁，重新整理圖示會重新整理頁面上顯示的資訊，而列印圖示可讓您列印目前頁面。  
  
 如需如何將封裝部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的相關資訊，請參閱[將專案部署至 Integration Services 伺服器](../../integration-services/packages/deploy-projects-to-integration-services-server.md)。  
  
## Integration Services 儀表板  
 [Integration Services 儀表板] 報表提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上所有封裝執行的概觀。 對於伺服器上已執行的每個封裝，儀表板可讓您放大報表，尋找可能發生之封裝執行錯誤的特定詳細資料。  
  
 此報表會顯示下列資訊區段。  
  
|章節|說明|  
|-------------|-----------------|  
|**執行資訊**|顯示在過去 24 小時內，處於不同狀態 (失敗、執行中、成功、其他) 的執行數目。|  
|**封裝資訊**|顯示在過去 24 小時內已經執行之封裝的總數。|  
|**連接資訊**|顯示在過去 24 小時內已經用於失敗執行的連接。|  
|**封裝詳細資訊**|顯示在過去 24 小時內所發生已完成執行的詳細資料。 例如，此區段會顯示失敗的執行數與執行總數、執行期間 (以秒為單位) 及過去三個月的平均值行期間的比較。<br /><br /> 您可以按一下 [概觀]、[所有訊息] 和 [執行效能]，檢視封裝的其他資訊。<br /><br /> [執行效能] 報表會顯示上一個執行個體的持續時間，以及開始和結束時間與套用的環境。<br /><br /> [執行效能] 報表中包含的圖表和相關資料表會顯示過去 10 次成功執行封裝的期間。 此資料表也會顯示過去三個月的平均執行期間。 在執行階段可能會對這 10 次成功的封裝執行套用不同的環境與不同的常值。<br /><br /> 最後，[執行效能] 報表會顯示封裝資料流程元件的 [啟用時間] 和 [總時間]。 [啟用時間] 是指元件在所有階段中執行所耗費的總時間，而 [總時間] 是指元件歷經的總時間。 報表只會在最後一個封裝執行作業的記錄層次設定為 [Performance] 或 [Verbose] 時，顯示封裝元件的這項資訊。<br /><br /> [概觀] 報表會顯示封裝工作的狀態。 [訊息] 報表會顯示封裝和工作的事件訊息和錯誤訊息，例如，回報開始和結束時間，以及寫入的資料列數目。<br /><br /> 您也可以按一下 [概觀] 報表中的 [檢視訊息]，導覽至 [訊息] 報表。 您同樣可以按一下 [訊息] 報表中的 [檢視概觀]，導覽至 [概觀] 報表。|  
  
 您可以按一下 [篩選]，然後選取 [篩選設定] 對話方塊中的準則，篩選任何頁面上顯示的資料表。 可用的篩選準則取決於顯示的資料。 您可以在 [篩選設定] 對話方塊中按一下排序圖示，以變更報表的排序次序。  
  
## 所有執行報表  
 [所有執行] 報表會顯示伺服器上已執行之所有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 執行的摘要。 範例封裝可能會有多個執行。 與 [Integration Services 儀表板] 報表不同的是，您可以設定 [所有執行] 報表以顯示某個日期範圍內開始的執行。 日期可以跨多天、數個月或數年。  
  
 此報表會顯示下列資訊區段。  
  
|章節|說明|  
|-------------|-----------------|  
|篩選|顯示目前套用至報表的篩選，例如 [開始時間範圍]。|  
|執行資訊|顯示每個封裝執行的開始時間、結束時間和期間。您可以檢視封裝執行使用的參數值清單，例如使用 [執行封裝] 工作傳遞至子封裝的值。 若要檢視參數清單，請按一下 [概觀]。|  
  
 如需使用「執行封裝」工作將值提供給子封裝的詳細資訊，請參閱[執行封裝工作](../../integration-services/control-flow/execute-package-task.md)。  
  
 如需參數的詳細資訊，請參閱 [Integration Services (SSIS) 封裝和專案參數](../../integration-services/integration-services-ssis-package-and-project-parameters.md)。  
  
## 所有連接  
 [所有連接] 報表會針對失敗的連接，以及在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上發生的執行提供下列資訊。  
  
 此報表會顯示下列資訊區段。  
  
|章節|說明|  
|-------------|-----------------|  
|篩選|顯示目前套用至報表的篩選，例如具有指定字串和 [上次失敗時間] 範圍的連接。<br /><br /> 設定 [上次失敗時間] 範圍，就可以只顯示某個日期範圍內發生的連接失敗。 範圍可以跨多天、數個月或數年。|  
|詳細資料|顯示連接字串、發生連接失敗的執行數目，以及上一次連接失敗的日期。|  
  
## 所有作業報表  
 [所有作業] 報表會顯示伺服器上已執行之所有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 作業的摘要，包括封裝部署、驗證和執行，以及其他管理作業。 就如同 Integration Services 儀表板一樣，您可以將篩選套用至資料表，以縮小顯示的資訊範圍。  
  
## 所有驗證報表  
 [所有驗證] 報表會顯示伺服器上已執行之所有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 驗證的摘要。 此摘要會顯示每個驗證的資訊，例如狀態、開始時間和結束時間。 每個摘要項目都包含一個指向驗證期間產生之訊息的連結。 就如同 Integration Services 儀表板一樣，您可以將篩選套用至資料表，以縮小顯示的資訊範圍。  
  
## 自訂報表  
 您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，將自訂報表 (.rdl 檔案) 加入 [Integration Services 目錄] 節點底下的 [SSISDB] 目錄節點。 加入報表之前，請確認您正在使用三部分命名慣例來完整限定您所參考的物件，例如來源資料表。 否則，[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 將會顯示錯誤。 此命名慣例是 \<資料庫>.\<擁有者>.\<物件>。 SSISDB.internal.executions 就是範例。  
  
> [!NOTE]  
>  當您將自訂報表加入 [資料庫] 節點底下的 [SSISDB] 節點時，不需要使用 SSISDB 前置詞。  
  
 如需如何建立和加入自訂報表的指示，請參閱[將自訂報表加入 Management Studio](../../ssms/object/add-a-custom-report-to-management-studio.md)。  
  
## 相關工作  
 [檢視 Integration Services 伺服器的報表](../../integration-services/performance/view-reports-for-the-integration-services-server.md)  
  
## 相關內容  
[監視執行封裝和其他作業](../../integration-services/performance/monitor-running-packages-and-other-operations.md)
  
  