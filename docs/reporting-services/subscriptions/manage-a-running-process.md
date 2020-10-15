---
title: 管理執行中的處理序 | Microsoft Docs
description: 了解如何管理執行中的處理序，例如使用者作業或系統作業。 您可透過程式設計方式來檢視作業、取消作業或管理作業。
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- report processing [Reporting Services], status information
- jobs [Reporting Services]
- viewing jobs
- canceling jobs
- user jobs [Reporting Services]
- system jobs [Reporting Services]
- report processing [Reporting Services], managing running processes
- processes [Reporting Services]
- scanning processes [Reporting Services]
- status information [Reporting Services]
- report processing [Reporting Services]
- canceling subscriptions
- report servers [Reporting Services], jobs
- data-driven subscriptions
- displaying jobs
- subscriptions [Reporting Services], running processes
ms.assetid: 473e574e-f1ff-4ef9-bda6-7028b357ac42
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e382dc67cb0a04bafabbbf4a88c2695edba8472b
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987359"
---
# <a name="manage-a-running-process"></a>管理執行中的處理序
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會監視作業在報表伺服器上執行的狀態。 報表伺服器會以固定間隔執行進行中作業的掃描，並將狀態資訊寫入報表伺服器資料庫或服務應用程式資料庫 (如果是 SharePoint 模式)。 如果下列任一個處理序進行中，作業就是進行中：在遠端或本機資料庫伺服器上的查詢執行、報表處理，以及報表轉譯。  
  
 您可以管理 *使用者作業* 和 *系統作業*。  
  
-   使用者作業是由個別使用者或訂閱起始。 這包括視需要執行報表、要求報表記錄快照集、手動建立報表快照集，以及處理標準訂閱。  
  
-   系統作業不會由報表伺服器起始。 系統作業包括排程的報表執行快照集、排程的報表記錄快照集，以及資料驅動訂閱。  
  
 報表處理時間與資源的使用，會依報表、查詢複雜度、資料量，以及針對報表所指定的轉譯格式而大有不同。 針對本機資料來源進行簡單查詢的報表，通常會在幾毫秒內完成，並且不需要管理或微調。 相對地，以 PDF 或 Excel 轉譯的大型報表，則會依硬體資源、傳遞選項和是否同時執行其他處理序，而可能需要很長的處理時間。 在報表伺服器上，大多數長時間執行中的處理序，是等候查詢處理結束的報表轉譯作業和處理序。 偶爾您會因為要將電腦離線，或者停止要花太長時間完成的執行中作業，而必須取消報表處理序。  
  
 您可以取消下列處理序：  
  
-   視需要報表處理。  
  
-   排程報表處理。  
  
-   個別使用者所擁有的標準訂閱。  
  
 取消作業只會取消在報表伺服器上執行的處理序。 由於報表伺服器不會管理在其他電腦上進行的資料處理，因此您必須手動取消隨後在其他系統上遺棄的查詢處理序。 請考慮指定查詢逾時值，以自動關閉花太長時間執行的查詢。 如需詳細資訊，請參閱[設定報表和共用資料集處理的逾時值 &#40;SSRS&#41;](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)。 如需詳細資訊，請參閱 [停用或暫停報表與訂閱處理](../../reporting-services/subscriptions/disable-or-pause-report-and-subscription-processing.md)。  
  
> [!NOTE]  
>  很少數的情況下，您可能需要重新啟動伺服器才能取消處理序。 如果是 SharePoint 模式，您可能需要重新啟動裝載 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式的應用程式集區。 如需詳細資訊，請參閱 [啟動與停止報表伺服器服務](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)。  
  
 本主題內容：  
  
-   [檢視和取消作業 (原生模式)](#bkmk_native)  
  
-   [檢視和取消作業 (SharePoint 模式)](#bkmk_sharepoint)  
  
-   [以程式設計方式管理作業](#bkmk_programmatically)  
  
##  <a name="view-and-cancel-jobs-native-mode"></a><a name="bkmk_native"></a> 檢視和取消作業 (原生模式)  
 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 來檢視或取消在報表伺服器上執行的作業。 您必須重新整理頁面，以便擷取目前正在執行之作業的清單，或從報表伺服器資料庫取得最新的作業狀態。 當您在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中連接至報表伺服器時，可以開啟 [作業] 資料夾來檢視報表伺服器電腦上目前正在處理之報表的清單。 每項作業的狀態資訊都會顯示在 [作業屬性] 頁面中。 您可以透過開啟 [取消報表伺服器作業] 對話方塊，檢視所有作業的狀態資訊。  
  
 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 來檢視或取消在報表伺服器上執行的作業。 您必須重新整理頁面，以便擷取目前正在執行之作業的清單，或從報表伺服器資料庫取得最新的作業狀態。 當您在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中連接至報表伺服器時，可以開啟 [作業] 資料夾來檢視報表伺服器電腦上目前正在處理之報表的清單。 每項作業的狀態資訊都會顯示在 [作業屬性] 頁面中。 您可以透過開啟 [取消報表伺服器作業] 對話方塊，檢視所有作業的狀態資訊。  
  
 您無法使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 來列出或取消模型產生、模型處理或資料驅動訂閱。 Reporting Services 不會提供取消模型產生或處理的方式。 不過，您可以使用本主題所提供的指示來取消資料驅動訂閱。  
  
### <a name="how-to-cancel-report-processing-or-subscription"></a>如何取消報表處理或訂閱  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，連接至報表伺服器。 如需指示，請參閱 [連接到 Management Studio 中的報表伺服器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)。  
  
2.  開啟 **[作業]** 資料夾。  
  
3.  以滑鼠右鍵按一下報表，然後按一下 [取消作業]  。  
  
### <a name="how-to-cancel-a-data-driven-subscription"></a>如何取消資料驅動訂閱  
  
1.  在文字編輯器中開啟 RSReportServer.config 檔。  
  
2.  尋找 **IsNotificationService**。  
  
3.  將它設為 **False**。  
  
4.  儲存檔案。  
  
5.  在報表管理員中，從報表的 [訂閱] 索引標籤或 [我的訂閱]  中刪除資料驅動訂閱。  
  
6.  刪除訂閱之後，請在 RSReportServer.config 檔中，尋找 **IsNotificationService** ，然後將它設為 **True**。  
  
7.  儲存檔案。  
  
### <a name="configuring-frequency-settings-for-retrieving-job-status"></a>設定擷取作業狀態的頻率設定  
 執行中的作業會儲存在報表伺服器的暫存資料庫中。 您可以修改 RSReportServer.config 檔案中的組態設定，以控制報表伺服器掃描進行中作業的頻率，和執行中作業的狀態要等候多久才會從新的變更為執行中。 **RunningRequestsDbCycle** 設定會指定報表伺服器掃描執行中處理序的頻率。 依預設，每 60 秒就會記錄狀態資訊。 **RunningRequestsAge** 設定會指定作業從新的轉換為執行中的間隔。  
  
##  <a name="view-and-cancel-jobs-sharepoint-mode"></a><a name="bkmk_sharepoint"></a> 檢視和取消作業 (SharePoint 模式)  
 使用 SharePoint 管理中心，為每個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式完成 SharePoint 模式部署中的作業管理。  
  
#### <a name="to-manage-jobs-in-sharepoint-mode"></a>若要管理 SharePoint 模式下的作業  
  
1.  在 SharePoint 管理中心中，按一下 **[管理服務應用程式]** 。  
  
2.  找出並按一下 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式的名稱，以開啟 [管理應用程式] 頁面。  
  
3.  按一下 **[管理作業]**  
  
4.  按一下 **[作業識別碼]** 以查看作業的詳細資料。  
  
5.  或按一下適用於您作業的方塊，然後按一下 **[刪除]** 以取消作業。 刪除作業並不會刪除訂閱。  
  
##  <a name="managing-jobs-programmatically"></a><a name="bkmk_programmatically"></a> 以程式設計方式管理作業  
 您可以用程式設計方式或利用指令碼來管理作業。 如需詳細資訊，請參閱 <xref:ReportService2010.ReportingService2010.ListJobs%2A>和 <xref:ReportService2010.ReportingService2010.CancelJob%2A>。  
  
## <a name="see-also"></a>另請參閱  
 [取消報表伺服器作業 &#40;Management Studio&#41;](../../reporting-services/tools/cancel-report-server-jobs-management-studio.md)   
 [作業屬性 &#40;Management Studio&#41;](../../reporting-services/tools/job-properties-management-studio.md)   
 [修改 Reporting Services 組態檔 &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [報表管理員 &#40;SSRS 原生模式&#41;](../web-portal-ssrs-native-mode.md)   
 [監視報表伺服器效能](../../reporting-services/report-server/monitoring-report-server-performance.md)  
  
