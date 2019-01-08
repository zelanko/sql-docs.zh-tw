---
title: 排程 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- schedules [Reporting Services]
- schedules [Reporting Services], about schedules
- published reports [Reporting Services], schedules
- reports [Reporting Services], scheduling
- subscriptions [Reporting Services], scheduling
- automatic report processing
ms.assetid: ecccd16b-eba9-4e95-b55d-f15c621e003f
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: b59f544894677c75f923c2dd6185c229495e42ea
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53372780"
---
# <a name="schedules"></a>[排程]
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會提供共用排程和報表特定排程來協助您控制報表的處理和散發。 這兩種排程類型之間的差異是定義、儲存和管理它們的方式。 兩種排程類型的內部建構則相同。 所有排程都會指定一個循環類型：每月、每週或每日。 在循環類型內，您可以設定發生事件之頻率的間隔和範圍。 不論您是建立共用排程還是報表特定排程，循環模式的類型和指定這些模式的方式相同。  
  
 本主題內容：  
  
-   [您可以執行排程](#bkmk_whatyoucando)  
  
-   [比較共用排程與報表特定排程](#bkmk_compare)  
  
-   [設定資料來源](#bkmk_configuredatasources)  
  
-   [儲存認證和處理帳戶](#bkmk_credentials)  
  
-   [如何排程與傳遞處理器的運作](#bkmk_how_scheduling_works)  
  
-   [伺服器相依性](#bkmk_serverdependencies)  
  
-   [停止 SQL Server Agent 的影響](#bkmk_stoppingagent)  
  
-   [停止報表伺服器服務的影響](#bkmk_stoppingservice)  
  
  
##  <a name="bkmk_whatyoucando"></a> 可以使用排程執行的工作  
 您可以在原生模式下使用報表管理員以及在 SharePoint 模式下使用 SharePoint 網站管理頁面，以建立及管理您的排程。 您可以：  
  
-   以標準訂閱或資料驅動訂閱的方式，排程報表的傳遞。  
  
-   排程報表記錄，好讓新的快照集能夠在固定的週期加入至報表記錄中。  
  
-   排程何時重新整理報表快照集的資料。  
  
-   排程何時重新整理共用資料集的資料  
  
-   排程在預先定義的時間讓快取報表或共用資料集過期，以便之後可以重新整理。  
  
 如果您想要針對許多報表或訂閱使用相同的排程資訊，可以建立共用排程。 共用排程是分開定義的，然後再從需要排程資訊的報表、共用資料集與訂閱中參考。  
  
 當您建立排程時，報表會將排程資訊儲存在報表伺服器資料庫中；如果是 SharePoint 模式，則會儲存在服務應用程式資料庫中。 報表伺服器也會建立用來觸發排程的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業。 排程的處理會依據包含該排程之報表伺服器的本地時間。 時間的格式會依照 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 作業系統的標準。  
  
 如需如何建立及管理排程的詳細資訊，請參閱＜ [Create, Modify, and Delete Schedules](create-modify-and-delete-schedules.md)＞。  
  
> [!NOTE]  
>  並非所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本都提供排程作業。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本支援的功能清單，請參閱 [SQL Server 2012 版本支援的功能](https://go.microsoft.com/fwlink/?linkid=232473) (https://go.microsoft.com/fwlink/?linkid=232473)。  
  
##  <a name="bkmk_compare"></a> 比較共用排程與報表特定排程  
 這兩種排程類型會產生相同的輸出：  
  
-   **共用排程** 是多用途的可攜式項目，包含立即可用的排程資訊。 因為共用排程是系統層級項目，所以建立共用排程需要系統層級權限。 基於這個原因，報表伺服器管理員或內容管理員一般會在您的報表伺服器上建立可以使用的共用排程。 共用排程是在報表伺服器上，使用報表管理員或 SharePoint 網站設定儲存及管理。  
  
     與您透過報表、共用資料集或訂閱屬性定義的特定排程相較之下，共用排程比較容易管理和維護，原因如下：  
  
    -   如果排程作業的執行間隔過短或與伺服器上的其他處理序發生衝突，您可以從中央位置管理共用排程，以便更容易比較排程屬性和調整頻率與循環模式。  
  
    -   允許您快速地適應運算環境的變更。 例如，假設您在重新整理資料倉儲後， 有一組在上午 4:00 執行的報表。 如果資料重新整理作業重新排程或延遲，您就可以透過更新單一共用排程中的排程資訊，輕易地配合該項變更。  
  
    -   如果您只有使用共用排程，就可以精確地知道進行排程作業的時間。 這可在發生效能問題之前，讓您更容易地預期和配合伺服器負載。 例如，如果您決定要以特定時間排程電腦備份，就可以調整共用排程，以便於不同的時間執行。  
  
-   **報表特定排程** 會定義在個別報表、訂閱或報表執行作業的內容中，用以決定快取過期或快照集更新。 當您定義訂閱或設定報表執行屬性時，會以內嵌的方式建立這些排程。 若共用排程未提供您需要的頻率或循環模式，您可以建立報表特定排程。 若要防止報表執行，您必須手動編輯報表特定排程。 報表特定排程可以由個別的使用者建立。  
  
##  <a name="bkmk_configuredatasources"></a> 設定資料來源  
 您必須先將報表資料來源設定成使用預存認證或自動報表處理帳戶，才能排程報表的資料或訂閱處理。 如果您使用預存認證，則只能儲存一組認證，而且該組認證將會由所有執行報表的使用者使用。 預存認證可以是 Windows 使用者帳戶或資料庫使用者帳戶。  
  
 自動報表處理帳戶是在報表伺服器上設定的特殊目的帳戶。 此帳戶是報表伺服器在排程的作業需要擷取外部檔案或處理時，用來連接遠端電腦的帳戶。 如果您設定此帳戶，即可用它來連接提供資料給報表的外部資料來源。  
  
 若要指定預存認證或自動報表處理帳戶，請編輯報表的資料來源屬性。 如果報表使用共用資料來源，則請改為編輯該共用資料來源。  
  
##  <a name="bkmk_credentials"></a> 儲存認證和處理帳戶  
 您使用排程的方式會視您的角色指派的工作而定。 如果您要使用預先定義的角色，屬於內容管理員和系統管理員的使用者就可以建立和管理任何排程。 如果您使用自訂角色指派，角色指派就必須包括支援排程作業的工作。  
  
|動作|包括這個工作|原生模式預先定義的角色|SharePoint 模式群組|  
|----------------|-----------------------|----------------------------------|----------------------------|  
|建立、修改或刪除共用排程|管理共用排程|系統管理員|擁有者|  
|選取共用排程|檢視共用排程|系統使用者|成員|  
|建立、修改或刪除使用者自訂訂閱中的報表特定排程|管理個別訂閱|瀏覽器、報表產生器、我的報表和內容管理員|訪客、成員|  
|建立、修改或刪除所有其他已排程之作業的報表特定排程|管理報表記錄、管理所有訂閱、管理報表|內容管理員|擁有者|  
  
 如需原生模式 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中安全性的詳細資訊，請參閱 [Predefined Roles](../security/role-definitions-predefined-roles.md)(預先定義的角色)、 [在原生模式報表伺服器上授與權限](../security/granting-permissions-on-a-native-mode-report-server.md) 和 [工作和權限](../security/tasks-and-permissions.md)。 如果是 SharePoint 模式，請參閱＜ [將 Reporting Services 中的角色和工作與 SharePoint 群組和權限做比較](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)＞  
  
##  <a name="bkmk_how_scheduling_works"></a> 排程與傳遞處理器的運作方式  
 排程與傳遞處理器提供下列功能：  
  
-   在報表伺服器資料庫中維護事件與通知的佇列。 在向外延展部署中，佇列會在部署中的所有報表伺服器間共用。  
  
-   呼叫報表處理器以執行報表、處理訂閱或清除快取報表。 因為排程事件而發生的所有報表處理都會當做都會當做背景處理來執行。 SharePoint 模式會使用計時器工作執行作業。  
  
-   呼叫在訂閱中指定的傳遞延伸模組，以便可以傳遞報表。  
  
 排程和傳遞作業的其他層面是由使用「排程與傳遞處理器」的其他元件和服務所處理。 明確地說，「排程與傳遞處理器」會在報表伺服器服務中執行，並使用 SQL Server Agent 做為計時器來產生排程的事件。 下列逐步描述會說明排程的作業如何在 Reporting Services 部署中運作：  
  
1.  當使用者建立排程時，會定義排程的作業。 排程會定義將用於觸發報表傳遞之訂閱、重新整理快照集，或是讓快取到期的日期和時間。  
  
2.  報表伺服器會將排程資訊儲存在報表伺服器資料庫中。  
  
3.  報表伺服器會在包含所提供之排程資訊的 SQL Server Agent 中，建立對應的工作。 系統會使用與報表伺服器資料庫之間的現有開啟連接，透過預存程序建立工作。  
  
4.  SQL Server Agent 會在排程中指定的日期和時間執行作業， 而此作業會建立一個事件，該事件會加入到由 Reporting Services 所維護的佇列中。  
  
5.  事件導致報表或訂閱程序執行。 在佇列中偵測到事件時會加以處理，而且會相對應地處理或傳遞報表。  
  
     處理事件前，排程與傳遞處理器會執行驗證步驟，以確認訂閱擁有者具有檢視報表的權限。  
  
 Reporting Services 會針對所有排程的作業維護事件佇列， 也會定期輪詢此佇列，以檢查是否有新的事件。 依預設，每隔 10 秒鐘會掃描一次佇列。 您可以變更此間隔，其方式是在 RSReportServer.config 檔中修改 `PollingInterval`、`IsNotificationService` 和 `IsEventService` 組態設定。 SharePoint 模式也會將 RSreporserver.config 用於這些設定，而且這些值會套用到所有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式。 如需詳細資訊，請參閱 [RSReportServer Configuration File](../report-server/rsreportserver-config-configuration-file.md)。  
  
##  <a name="bkmk_serverdependencies"></a> 伺服器相依性  
 排程與傳遞處理器需要啟動報表伺服器服務與 SQL Server Agent。 排程與傳遞處理功能必須透過啟用`ScheduleEventsAndReportDeliveryEnabled`的屬性**Reporting Services 的介面區組態**中原則式管理 facet。 SQL Server Agent 與報表伺服器服務都必須執行，排程的作業才會發生。  
  
> [!NOTE]  
>  您可以使用 **[Reporting Services 的介面區組態]** Facet，暫時或永久地停止排程的作業。 您可以建立與部署自訂傳遞擴充模組，但排程與傳遞處理器無法藉由本身擴充。 您無法變更它管理事件與通知的方式。 如需有關關閉功能的詳細資訊，請參閱＜ **Turn Reporting Services Features On or Off** ＞的＜ [排程的事件和傳遞](../report-server/turn-reporting-services-features-on-or-off.md)＞一節。  
  
###  <a name="bkmk_stoppingagent"></a> 停止 SQL Server Agent 的影響  
 依預設，排程的報表是使用 SQL Server Agent。 如果您停止服務，則除非您透過 <xref:ReportService2010.ReportingService2010.FireEvent%2A> 方法，以程式設計方式加入處理要求，否則不會有新處理要求加入佇列。 您重新啟動服務後，建立報表處理要求的作業就會繼續。 報表伺服器不會嘗試重新建立可能在 SQL Server Agent 離線期間所發生的報表處理作業。 如果您停止 SQL Server Agent 一個星期，那個星期內所有排程的作業都會遺失。  
  
> [!NOTE]  
>  SQL Server Agent 為 Reporting Services 提供的功能，可以由使用 <xref:ReportService2010.ReportingService2010.FireEvent%2A> 方法的自訂程式碼取代，來將排程事件加入佇列。  
  
###  <a name="bkmk_stoppingservice"></a> 停止報表伺服器服務的影響  
 如果停止報表伺服器服務，SQL Server Agent 會繼續將報表處理要求加入佇列。 SQL Server Agent 中的狀態資訊會指出作業成功。 但是，因為報表伺服器服務已停止，因此實際上沒有任何報表處理發生。 要求將繼續在佇列中累積，直到您重新啟動報表伺服器服務為止。 一旦您重新啟動報表伺服器服務之後，佇列中的所有報表處理要求都會依照順序處理。  
  
## <a name="see-also"></a>另請參閱  
 [建立、修改及刪除報表記錄中的快照集](../report-server/create-modify-and-delete-snapshots-in-report-history.md)   
 [訂閱與傳遞 &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [Data-Driven Subscriptions](data-driven-subscriptions.md)   
 [快取多個報表 &#40;SSRS&#41;](../report-server/caching-reports-ssrs.md)   
 [報表伺服器內容管理 &#40;SSRS 原生模式&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)   
 [快取共用資料集 &#40;SSRS&#41;](../report-server/cache-shared-datasets-ssrs.md)  
  
  
