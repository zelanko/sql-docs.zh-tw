---
title: "Power Pivot 使用量資料收集 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9057cb89-fb17-466e-a1ce-192c8ca20692
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 55ce7a5604bac4871942a281313a853d9477a974
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="power-pivot-usage-data-collection"></a>PowerPivot 使用量資料收集
  使用量資料收集是伺服陣列層級的 SharePoint 功能。 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] for SharePoint 會使用並擴充此系統來支援 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 管理儀表板中的報表，以便顯示 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 資料與服務的使用方式。 根據您安裝 SharePoint 的方式而定，可能會關閉伺服陣列的使用量資料收集。 伺服器陣列管理員必須啟用使用量記錄，以建立會顯示在 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 管理儀表板中的使用量資料。  
  
 如需 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 管理儀表板中使用量資料的相關資訊，請參閱 [Power Pivot 管理儀表板和使用量資料](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)。  
  
  
##  <a name="usagearch"></a> 使用量資料收集和報告架構  
 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)]收集使用量資料，儲存和管理使用來自 SharePoint 基礎結構和 Powerpivot 伺服器元件功能的組合。 SharePoint 基礎結構會提供集中式使用量服務以及內建的計時器工作。 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] for SharePoint 會針對您在 SharePoint 管理中心內檢視的 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 使用量資料和報表，加入較長期的儲存體。  
  
 在使用量資料收集系統中，事件資訊會進入應用程式伺服器或 Web 前端上的使用量收集系統。 使用量資料會在系統中移動以回應計時器工作，這些計時器工作會造成資料從實體伺服器上的暫存資料檔，移動到資料庫伺服器上的持續性儲存體 (Persistent Storage)。 下圖說明透過資料收集和報告系統，移動使用量資料的元件和處理序。  
  
 **注意** ：請確認使用量資料收集已啟用。 若要確認，請移至 [SharePoint 管理中心] 的 **[監視]** 。 如需詳細資訊，請參閱 [設定使用量資料收集的對象 &#40;Power Pivot for SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)。  
  
 ![元件和處理序的使用量資料收集。](../../analysis-services/power-pivot-sharepoint/media/gmni-usagedata.gif "元件和處理序的使用量資料收集。")  
  
|階段|說明|  
|-----------|-----------------|  
|1|使用量資料收集是由 SharePoint 部署中之 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 元件和 [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] 資料提供者所產生的事件來觸發。 可以開啟或關閉的可設定事件，包括由應用程式伺服器上的 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服務所監視的連接要求、載入和卸載要求，以及查詢回應計時事件。 僅由伺服器管理且無法關閉的其他事件。 這些包括資料重新整理與伺服器健全狀況事件。<br /><br /> 一開始，使用量資料是使用 SharePoint 系統的資料收集功能來收集並儲存在本機記錄檔中。 這些檔案及其位置屬於 SharePoint 中標準使用量資料收集系統的一部分。 檔案的位置在伺服器陣列中的每部伺服器上都是相同的。 若要檢視或變更記錄目錄的位置，請移至 SharePoint 管理中心的 **[監視]** ，然後按一下 **[設定 Usage and Health Data Collection]**。|  
|2|Microsoft SharePoint Foundation 使用量資料匯入計時器工作會依照排程的間隔 (預設是每小時)，將使用量資料從記錄檔移到 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服務應用程式資料庫。 如果在伺服器陣列中有多個 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服務應用程式，則每一個都會有其專屬資料庫。 事件包含識別產生事件之 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服務應用程式的內部資訊。 應用程式識別碼可確保使用量資料繫結至建立該資料的應用程式。|  
|3|資料會複製到可供 [管理中心] 內 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 管理儀表板使用的內部報告資料庫。|  
|4|資料來源是您可以存取以便在 Excel 中建立自訂報表的 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 活頁簿。 來源活頁簿只有一個執行個體。 當地語系化報表都是以同一份來源活頁簿為基礎。|  
|5|系統會為管理伺服器效能和可用性的系統管理員，在 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服務應用程式的報表中顯示使用量資料。 活頁簿的當地語系化執行個體是針對支援的 SharePoint 語言建立的。 如需詳細資訊，請參閱本主題中的＜ [使用量資料的報告](#reporting) ＞。|  
  
##  <a name="sources"></a> 使用量資料的來源  
 當已啟用使用量資料收集時，就會為下列伺服器事件產生資料。  
  
|事件|說明|可設定|  
|-----------|-----------------|------------------|  
|連接|伺服器連接是以在 Excel 活頁簿中查詢 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 資料的使用者身分來建立。 連接事件會識別開啟 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 活頁簿連接的使用者。 在報表中，這項資訊是用來識別最常見的使用者，由相同的使用者存取的 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 資料來源，以及一段時間內連接的趨勢。|您可以啟用和停用 [設定使用量資料收集的對象 &#40;Power Pivot for SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)。|  
|查詢回應時間|根據完成查詢的時間來分類查詢的回應統計資料。 查詢回應的統計資料會顯示伺服器回應查詢要求所需時間的模式。|您可以啟用和停用 [設定使用量資料收集的對象 &#40;Power Pivot for SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)。|  
|資料載入|由 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]載入的資料作業。 資料載入事件會識別最常使用的資料來源。|您可以啟用和停用 [設定使用量資料收集的對象 &#40;Power Pivot for SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)。|  
|資料卸載|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服務應用程式的資料卸載作業。 如果 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 資料來源未在使用中，或者伺服器有記憶體不足的壓力，或需要額外的記憶體來執行資料重新整理作業時， [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 會卸載非使用中的資料來源。|您可以啟用和停用 [設定使用量資料收集的對象 &#40;Power Pivot for SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)。|  
|伺服器健全狀況|表示伺服器健全狀況的伺服器作業，是以 CPU 和記憶體使用量來表示。 此資料是歷程記錄。 它並未提供在伺服器上目前處理負載的相關即時資訊。|資料分割 這個事件永遠都會收集使用量資料。|  
|資料重新整理|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服務為已排程的資料更新所起始的資料重新整理作業。 在應用程式層級會為可操作的報表收集資料重新整理的使用量記錄，而且會反映在個別活頁簿的 [管理資料重新整理] 頁面。<br /><br /> **注意** ：對於 [!INCLUDE[ssSQL11SP1_md](../../includes/sssql11sp1-md.md)] 和 SharePoint 2013 部署而言，資料重新整理是由 Excel Services 所管理，而非 Analysis Services 伺服器。|資料分割 如果您啟用 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服務應用程式的資料重新整理，一律都會收集資料重新整理使用量資料。|  
  
##  <a name="servicesjobs"></a> 服務與計時器工作  
 下表描述在使用量資料收集系統中的服務和資料收集存放區。 如需如何覆寫計時器工作排程以強制在伺服器健全狀況與使用量資料的資料重新整理的指示[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)]管理儀表板報告，請參閱[輸入連結描述](../../analysis-services/power-pivot-sharepoint/power-pivot-data-refresh-with-sharepoint-2013.md)。 您可以在 SharePoint 管理中心內查看計時器工作。 移至 **[監視]**，然後按一下 **[檢查工作狀態]**。 按一下 **[檢閱工作定義]**。  
  
|元件|預設排程|說明|  
|---------------|----------------------|-----------------|  
|SharePoint 計時器服務 (SPTimerV4)||這項 Windows 服務會在伺服陣列中每一部成員電腦上的本機執行，並處理在伺服陣列層級所定義的所有計時器工作。|  
|Microsoft SharePoint Foundation 使用量資料匯入|在 SharePoint 2010 中，每隔 30 分鐘。 在 SharePoint 2013 中，每隔 5 分鐘。|此計時器工作是在伺服陣列層級以全域方式設定。 它會將使用量資料從本機使用量記錄檔，移到中央的使用量資料收集資料庫。 您可以用手動方式來執行此計時器工作，以強制資料匯入作業。|  
|Microsoft SharePoint Foundation 使用量資料處理計時器工作|每天上午 3:00 點|從 SQL Server 2012 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] for SharePoint 開始，此計時器工作支援 SharePoint 使用量資料庫仍有舊版使用量資料的升級或移轉案例。 從 SQL Server 2012 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] for SharePoint 開始，SharePoint 使用量資料庫不會用於 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 使用量收集和管理儀表板工作流程。 您可以手動執行此計時器工作，將 SharePoint 使用量資料庫中任何剩餘的 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 相關資料移到 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服務應用程式資料庫。<br /><br /> 此計時器工作是在伺服陣列層級以全域方式設定。 它會檢查中央使用量資料收集資料庫中過期的使用量資料 (也就是，30 天之前的任何記錄)。 對於伺服陣列中的 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 伺服器，此計時器工作會為 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 使用量資料執行額外的檢查。 偵測到 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 使用量資料時，計時器工作就會使用應用程式識別碼來尋找正確的資料庫，以便將資料移至服務應用程式資料庫。<br /><br /> 您可以手動執行這項計時器作業來強制到期資料的檢查，或是強制將 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 使用量資料匯入 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服務應用程式資料庫。|  
|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 管理儀表板處理計時器工作|每天上午 3:00 點|此計時器工作會更新提供系統管理資料給 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 管理儀表板的內部 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 活頁簿。 它會取得 SharePoint 所管理的更新資訊，包括伺服器名稱、使用者名稱、應用程式名稱，以及出現在儀表板報表或 Web 組件中的檔案名稱。|  
  
##  <a name="reporting"></a> 使用量資料的報告  
 若要檢視 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 資料的使用量資料，您可以檢視 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 管理儀表板中的內建報表。 內建報表會合併從服務應用程式資料庫中的報告資料結構，所擷取的使用量資料。 因為基礎報表資料會每天更新，所以內建的使用量報表只會在 Microsoft SharePoint Foundation 使用量資料處理計時器工作將資料複製到 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服務應用程式資料庫後，才會顯示更新的資訊。 根據預設，這個工作每天進行一次。  
  
 如需有關如何檢視報表的詳細資訊，請參閱＜ [Power Pivot Management Dashboard and Usage Data](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)＞。  
  
## <a name="see-also"></a>請參閱＜  
 [Power Pivot 管理儀表板和使用量資料](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)   
 [組態設定參考 &#40;Power Pivot for SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [設定使用量資料收集的對象 &#40;Power Pivot for SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  

