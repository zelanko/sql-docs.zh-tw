---
title: 特徵選取 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- feature selection, Setup
helpviewer_keywords:
- SQL Server Installation Wizard, Components to Install page
- Components to Install page [SQL Server Installation Wizard]
ms.assetid: 73182088-153b-4634-a060-d14d1fd23b70
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cedec01a7e8c7da94f75c00e377a2c965bd58c7d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087408"
---
# <a name="feature-selection"></a>特徵選取
  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈之 [特徵選取] 頁面上的核取方塊可選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝的元件。  
  
## <a name="installing-includessnoversionincludesssnoversion-mdmd-features"></a>安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能  
 在 [特徵選取] 頁面上，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能分成兩個主要部分：**執行個體功能**與**共用功能**。  
  
 **執行個體功能**指的是針對每個執行個體安裝一次，讓您擁有多個複本 (每個執行個體一個) 的元件。 每個執行個體都可以擁有不同修補程式等級的單獨版本。 當您安裝修補程式時，不論它是 Service Pack、Hotfix，還是累計更新，都只會針對給定機器上的一個執行個體更新檔案，如果尚未更新共用功能，也會一併更新。  
  
 **共用功能** 指的是給定機器上所有執行個體都通用的功能。 這些每一個共用功能的設計，都與支援且可並存安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本 (Service Pack、累計更新以及 Hotfix) 回溯相容。  
  
> [!NOTE]  
>  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集：**[!INCLUDE[ssDE](../../includes/ssde-md.md)] 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 元件是支援容錯移轉叢集的唯一 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 功能。 雖然您可以在容錯移轉叢集節點上安裝其他元件 (例如 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 或 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)])，但是這些元件無法感知叢集，而且如果容錯移轉叢集節點離線，這些元件的服務就不會容錯移轉。 如需詳細資訊，請參閱 [AlwaysOn 容錯移轉叢集執行個體 &#40;SQL Server&#41;](../failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)。  
  
### <a name="instance-features"></a>執行個體功能  
 當您選取元件時，每一個元件群組的描述會出現在 [描述] 窗格中。 您可以選取核取方塊的任何組合。 若要繼續，您必須做選擇。  
  
|功能|描述|  
|--------------|-----------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 服務|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 包含[!INCLUDE[ssDE](../../includes/ssde-md.md)]，來儲存、 處理和保護資料、 複寫、 全文檢索搜尋、 工具，來管理關聯式和 XML 資料的核心服務和[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)](DQS) 伺服器。 以下是 Database Engine的功能：<br /><br /> [!INCLUDE[ssDE](../../includes/ssde-md.md)] 是用來儲存、處理和保護資料安全的核心服務。<br /><br /> 複寫：(選擇性) 複寫是一組技術，用於將資料和資料庫物件從某個資料庫複製和散發到另一個資料庫，然後在兩個資料庫之間進行同步處理以維護一致性。<br /><br /> 全文檢索搜尋：(選擇性) 全文檢索搜尋提供一種功能，可針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中一般以字元為主的資料發出全文檢索查詢。<br /><br /> [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]：選擇性：[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) 是一種資料清除方案，可讓您在資料來源中探索不一致和不正確的資料，並提供電腦輔助及互動的方式以清理資料。 選取此核取方塊可安裝 DQS 伺服器。 在完成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝之後，您必須執行 DQSInstaller.exe 檔案才能「完成」 DQS 伺服器安裝。 如果您安裝 SQL server 的預設執行個體，這個檔案位於 C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12.<instancename>\。MSSQLSERVER\MSSQL\Binn。<br /><br /> <br /><br /> **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集：** 當您選取 Database Engine Services 時，複寫和全文檢索搜尋元件為必要項目，且安裝程式會自動選取這些元件進行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集安裝。|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包括用來建立及管理線上分析處理 (OLAP) 和資料採礦應用程式的工具。|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] – 原生|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式包括伺服器和用戶端元件，可用來建立、管理和部署表格式、矩陣、圖形化和自由形式報表。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 也是一個可延伸的平台，可讓您用來開發報表應用程式。|  
  
> [!IMPORTANT]  
>  1.  安裝程式不會為 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 向外延展部署中的多個節點，設定負載平衡和單一 URL 定址。 若要完成向外延展部署，您必須使用 Windows Server、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Application Center 或協力廠商叢集管理軟體。 如需有關設定 Web 伺服陣列部署的詳細資訊，請參閱 <<c0> [ 設定 Reporting Services 進行向外延展部署](http://go.microsoft.com/fwlink/?LinkId=199448)(http://go.microsoft.com/fwlink/?LinkId=199448)。  
> 2.  如需 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 元件的瀏覽器需求，請參閱 [規劃 Reporting Services 和 Power View 瀏覽器支援 &#40;Reporting Services 2014&#41;](../../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)。  
> 3.  同時在 64 位元平台以及在 64 位元伺服器的 32 位元子系統 (WOW64) 的並存組態中，不支援 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
### <a name="shared-features"></a>共用功能  
 單一電腦上供所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體共用的功能會安裝到單一目錄， 其中包括：  
  
|功能|描述|  
|-------------|-----------------|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -SharePoint|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式是伺服器應用程式，來建立、 管理和傳遞報表至電子郵件、 多個檔案格式和互動式 Web 格式。 SharePoint 模式會將報表檢視和報表管理經驗與 SharePoint 產品整合。 如需詳細資訊，請參閱 [Reporting Services 報表伺服器 &#40;原生模式&#41;](../../../2014/reporting-services/reporting-services-report-server-sharepoint-mode.md)。|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 適用於 SharePoint 產品的增益集|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集的 SharePoint 產品包括管理和使用者介面元件，可整合 SharePoint 產品與[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 模式報表伺服器。 如需詳細資訊，請參閱[尋找適用於 SharePoint 產品之 Reporting Services 增益集的位置](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)。|  
|Data Quality Client|Data Quality Client 是連接到 DQS 伺服器的獨立應用程式，提供了直覺式的圖形化使用者介面，可執行資料清理作業、資料比對作業，以及執行 DQS 的管理工作。|  
|用戶端工具連接性|用戶端工具包括用於用戶端和伺服器之間通訊的元件，包括 DB-Library、OLEDB for OLAP、ODBC、ADODB 和 ADOMD+ 的網路程式庫。|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 是一組圖形化工具和可程式化物件，用來移動、複製和轉換資料。|  
|用戶端工具回溯相容性|[用戶端工具回溯相容性] 包含下列元件：<br /><br /> SQL Distributed Management Objects (SQL-DMO)。 如需詳細資訊，請參閱[在 SQL Server 2014 中停止 SQL Server 的功能](../../../2014/getting-started/discontinued-sql-server-features-in-sql-server-2014.md)。<br /><br /> 決策支援物件 (DSO)。 如需詳細資訊，請參閱 [SQL Server 2014 中 Analysis Services 功能的重大變更](../../../2014/analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2014.md)。|  
|用戶端工具 SDK|包括內含供程式設計人員使用之資源的軟體開發套件。|  
|文件集元件|文件集文件包括檢視並管理說明內容的元件。|  
|管理工具 - 基本|**管理工具 – 基本** ：這包括下列元件：<br /><br /> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 支援[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]， [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]， **sqlcmd**公用程式，而[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]PowerShell 提供者<br /><br /> **管理工具 – 完整** ：除了基本版的元件以外，還包括下列元件：<br /><br /> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 支援<br /><br /> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]<br /><br /> Database Engine Tuning Advisor<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式管理|  
|Distributed Replay Controller|Distributed Replay Controller 可協調 Distributed Replay Client 的動作。 每個 Distributed Replay 環境都只能有一個 Controller 執行個體。 如需詳細資訊，請參閱 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)。|  
|Distributed Replay Client|Distributed Replay Client 會共同運作以模擬 SQL Server 執行個體的工作負載。 每個 Distributed Replay 環境中可以有一個或多個用戶端。 如需詳細資訊，請參閱 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)。|  
|SQL 用戶端連接性 SDK|包括用於資料庫應用程式開發的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (ODBC/OLE DB) SDK。|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 是一套平台，可針對精確度和稽核目的，將組織中不同系統的資料整合成單一主要資料來源。 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 選項會安裝 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]、組件、Windows PowerShell 嵌入式管理單元，以及 Web 應用程式與服務的資料夾和檔案。|  
  
 依預設，共用元件會安裝到 %Program Files%Microsoft SQL Server\\。 若要變更安裝路徑，請按一下 [瀏覽] 按鈕。 如果您變更某個共用元件的安裝路徑，您也會變更其他共用元件的安裝路徑。 後續安裝會將共用元件安裝到與原始安裝相同的位置。  
  
 **執行個體根目錄**-根據預設，執行個體根目錄為 C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\。 若要指定非預設的根目錄，請按一下 [瀏覽] 按鈕，或是提供路徑名稱。  
  
 在 x64 型作業系統上，您可以指定將要安裝 64 位元元件的位置，以及 32 位元元件將要安裝在 WOW64 子系統上的哪一個位置。  
  
## <a name="disk-space-requirements"></a>磁碟空間需求  
 使用 [磁碟空間摘要] 頁面，即可檢查您選取要安裝之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能的磁碟空間需求。  
  
### <a name="options"></a>選項。  
 如果所需的磁碟空間太高，請考慮下列選項：  
  
-   將安裝目錄變更為具有更多磁碟空間的磁碟機。  
  
-   變更要安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。  
  
-   在指定的磁碟機上，移動其他檔案或應用程式，藉以創造更多可用空間。  
  
## <a name="installing-adventureworks-sample-databases"></a>安裝 AdventureWorks 範例資料庫  
 根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程序中不會安裝範例資料庫和範例程式碼。 如需有關安裝範例資料庫和範例程式碼的詳細資訊，請參閱 < [Microsoft SQL Server 社群專案和範例](http://go.microsoft.com/fwlink/?LinkId=87843)(http://go.microsoft.com/fwlink/?LinkId=87843)。  
  
 在安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 之後，可使用有關範例的其他資訊。 從**啟動**功能表上，按一下**所有程式**，按一下**[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**，按一下**文件集和教學課程**然後按一下 **[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]範例概觀**。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 的版本和元件](../editions-and-components-of-sql-server-2016.md)  
  
  
