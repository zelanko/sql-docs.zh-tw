---
title: SQL Server 服務安裝概觀 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 6a9fd19b-2367-4908-b638-363b1e929e1e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 65797fdf770196723a74510501d381fb608ad2ff
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53369060"
---
# <a name="overview-of-sql-server-servicing-installation"></a>SQL Server 服務安裝概觀
  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 服務更新，將更新套用至任何已安裝的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 元件。 如果現有 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 元件的版本層級比更新版本層級還新，則安裝程式會將其排除在更新作業外。 如需有關套用服務更新，請參閱[安裝 SQL Server 2014 服務更新](../../database-engine/install-windows/install-sql-server-servicing-updates.md)。  
  
 當您安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新時，應該進行下列考量：  
  
-   您必須同時更新屬於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的所有功能。 例如，更新 [!INCLUDE[ssDE](../../includes/ssde-md.md)]時，如果 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 元件與同一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體一起安裝，則您也必須更新這些元件。 共用功能 (例如管理工具、[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]) 一律必須更新為最新的更新。 如果未選取功能樹狀目錄中的元件或執行個體，便不會更新元件或執行個體。  
  
-   根據預設，[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]更新記錄檔會儲存到 %Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\LOG\\。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式現在可以整合更新與原始媒體，以便同時執行原始媒體及更新。 如需詳細資訊，請參閱 < [What's New in SQL Server 安裝](../../../2014/sql-server/install/what-s-new-in-sql-server-installation.md)。  
  
-   套用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 服務更新之前，建議您考慮將資料備份。  
  
-   您可以透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Update 取得 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新。 建議您定期掃描更新，讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體維持更新及安全的狀態。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1 會以完整的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝形式提供。 這個版本並非以標準修補可執行檔封裝的形式提供要套用至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RTM 執行個體的 Service Pack，而是提供安裝套件 (由 2 個檔案組成)。 執行時，將會安裝已預先安裝 SP1 的新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
## <a name="requirements-and-known-issues"></a>需求和已知問題  
 建議的磁碟空間需求大約是用於安裝、下載及擷取封裝之封裝大小的 2.5 倍。 安裝 Service Pack 之後，您可以移除下載的封裝。 任何暫存檔都會自動移除。  
  
 **檢閱已知的問題：** 如需有關目前版本已知問題的詳細資訊，請參閱這裡的對應版本資訊：[SQL Server 版本資訊](https://msdn.microsoft.com/f617a0af-92dd-47aa-82c3-f51b1346bcd8)。  
  
## <a name="installation-overview"></a>安裝概觀  
 本節將討論累計更新和 Service Pack 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝，包括如何執行下列作業：  
  
-   準備安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新  
  
-   安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新  
  
-   重新啟動服務及應用程式  
  
### <a name="prepare-for-a-includesscurrentincludessscurrent-mdmd-update-installation"></a>準備安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新  
 我們強烈建議您最好先執行以下作業再安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新：  
  
-   **備份您[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]系統資料庫**-在安裝之前[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]更新備份`master`， `msdb`，和`model`資料庫。 安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新會變更這些資料庫，而使它們無法與舊版 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]相容。 如果您決定要重新安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (不含這些更新)，則這些資料庫的備份就是必要項目。  
  
     您也必須備份使用者資料庫。  
  
    > [!IMPORTANT]  
    >  將更新套用至參與複寫拓撲的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，您必須先備份複寫資料庫以及系統資料庫，然後再套用更新。  
  
-   **備份您[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫、 組態檔和儲存機制**-更新的執行個體之前，先[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，您應該先備份下列：  
  
    -   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫。 根據預設，這些都會安裝在 C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS12。\<執行個體識別碼 > \OLAP\Data\\。 WOW 安裝，預設路徑為 C:\ProgramFiles (x86) \ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS12。\<執行個體識別碼 > \OLAP\Data\\。  
  
    -   msmdsrv.ini 組態檔中的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 組態設定。 根據預設，這位於 C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS12。\<執行個體識別碼 > \OLAP\Config\ 目錄。  
  
    -   (選擇性) 包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 儲存機制的資料庫。 只有在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 已設定成使用決策支援物件 (DSO) 程式庫時，才需要執行此步驟。  
  
    > [!NOTE]  
    >  如果備份 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫、組態檔和儲存機制時發生失敗，則無法將已更新的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體還原為舊版。  
  
-   **確認系統資料庫擁有足夠的可用空間**-如果自動成長選項未選取要`master`和`msdb`系統資料庫，每個資料庫都必須擁有至少 500 KB 的可用空間。 若要確認資料庫是否有足夠的空間，請在 `sp_spaceused` 和 `master` 資料庫上，執行 `msdb` 系統預存程序。 如果其中一個資料庫的未配置空間少於 500 KB，請增加該資料庫的大小。  
  
-   **停止服務和應用程式**-若要避免系統可能重新啟動，請先停止所有應用程式和服務的執行個體的連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在升級之，然後再安裝[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]更新。 這些包括 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。 如需詳細資訊，請參閱 [啟動、停止、暫停、繼續、重新啟動 Database Engine、SQL Server Agent 或 SQL Server Browser 服務](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)。  
  
    > [!NOTE]  
    >  您無法停止容錯移轉叢集環境中的服務。 如需詳細資訊，請參閱這個主題稍後的容錯移轉叢集安裝章節。  
  
-   為了排除在進行更新安裝之後重新啟動電腦的需求，安裝程式會顯示正在鎖定檔案之處理序的清單。 如果更新安裝程式必須在安裝時結束某項服務，它會在安裝完成之後重新啟動該服務。  
  
-   如果安裝程式判斷在安裝時鎖定了檔案，則在安裝完成之後可能必須重新啟動電腦。 如有必要，安裝程式會提示您重新啟動電腦。  
  
### <a name="install-includesscurrentincludessscurrent-mdmd-updates"></a>安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新  
 本節將說明安裝程序。  
  
> [!IMPORTANT]  
>  您必須在即將安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新的電腦上，使用具有管理權限的帳戶來安裝更新。 如果是本機安裝，您必須以管理員身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須使用對遠端共用位置具有讀取和執行權限的網域帳戶。  
  
#### <a name="starting-a-includesscurrentincludessscurrent-mdmd-update"></a>啟動 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新  
 若要安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新，請執行自動解壓縮封裝檔案。  
  
 累計更新封裝 (CU):\<SQLServer2014 >-KBxxxxxx-*PPP*.exe  
  
 Service pack 封裝 (PCU):\<SQLServer2014 >\<SPx >-KBxxxxxx-PPP-LLL.exe  
  
-   x 表示 Service Pack 號碼  
  
-   PPP 表示特定的平台  
  
-   LLL 表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 語言的字元縮寫，例如：英文的 LLL 為 ENU。  
  
 若要將更新套用至屬於容錯移轉叢集一部分的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 元件，請參閱容錯移轉叢集安裝的章節。 如需如何以自動模式中執行更新安裝的詳細資訊，請參閱[從命令提示字元安裝 SQL Server 2014](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)。  
  
####  <a name="Slipstream"></a> 中的產品更新[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]安裝  
 產品更新是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝程式中的功能。 它可以整合最新產品更新與主要產品安裝，因此主要產品及其適用的更新可以同時安裝。 產品更新可以搜尋 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update、Windows Server Update Services (WSUS)、本機資料夾，或可用更新的網路共用。  安裝程式找到最新版本的可用更新後，會使用目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程序進行下載與整合。 產品更新可以引入累計更新、Service Pack，或 Service Pack 加上累計更新。 產品更新功能是 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] PCU1 中可用之匯集功能的延伸模組。  
  
## <a name="updating-a-prepared-image-of-includessnoversionincludesssnoversion-mdmd"></a>更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的備妥映像  
 您可以將更新套用到已備妥但是未設定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，而不需完成已備妥之執行個體的組態。 將更新套用至已備妥之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的其他方式將於底下說明：  
  
-   更新之前已備妥的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體  
  
     已備妥之執行個體的更新可以在組態設定之前套用。 更新封裝會偵測到此執行個體位於備妥狀態，並將修補程式套用到備妥的執行個體，而不會完成組態設定。  
  
-   使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update 更新備妥的執行個體：  
  
     您可以透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Update 將更新套用至 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 的備妥執行個體。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update 封裝會偵測到此執行個體位於備妥狀態，並將修補程式套用到備妥的執行個體，而不會完成組態設定。  
  
 如果您要更新備妥的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 映像，您需要指定 InstanceID 參數。 如需詳細資訊和範例語法，請參閱 [從命令提示字元安裝更新](../../database-engine/install-windows/installing-updates-from-the-command-prompt.md)。  
  
## <a name="updating-a-completed-image-of-includessnoversionincludesssnoversion-mdmd"></a>更新完成的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 映像  
 更新已完成且設定好的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體會依照與任何其他已安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體相同的程序。  
  
## <a name="rebuilding-a-includesscurrentincludessscurrent-mdmd-failover-cluster-node"></a>重建 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 容錯移轉叢集節點  
 套用更新之後，如果您必須重建容錯移轉叢集中的節點，請遵循下列步驟：  
  
1.  重建容錯移轉叢集中的節點。 如需重建節點的詳細資訊，請參閱[從容錯移轉叢集執行個體失敗的狀況復原](../failover-clusters/windows/recover-from-failover-cluster-instance-failure.md)。  
  
2.  執行原始的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝程式以便將 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝到容錯移轉叢集節點。  
  
3.  在您已加入的節點上執行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新安裝程式。  
  
## <a name="restart-services-and-applications"></a>重新啟動服務及應用程式  
 當安裝程式完成時，它可能會提示您重新啟動電腦。 在系統重新啟動或在安裝程式完成 (但未要求重新啟動電腦) 之後，您可以使用 [控制台] 中的 [服務] 節點來重新啟動在套用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新之前所停止的服務。 這包括分散式交易協調器及 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search 等服務，或執行個體特定的對等服務。  
  
 重新啟動在執行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新安裝程式之前所關閉的應用程式。 您可能還想在安裝成功完成之後，立即為已升級的 `master`、`msdb` 和 `model` 資料庫進行另一次備份。  
  
## <a name="uninstalling-updates-from-includesscurrentincludessscurrent-mdmd"></a>解除安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的更新  
 您可以從 [控制台] 中的 [程式和功能] 解除安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 累計更新或 Service Pack。 若要檢視已安裝的更新清單，請依序按一下 [開始] 按鈕、[控制台]、[程式集]，然後按一下 [程式和功能] 下的 [檢視已安裝的更新]，開啟 [已安裝的更新]。 系統會個別列出每個累計更新。 然而，安裝了高於累計更新的 Service Pack 時，累計更新項目會隱藏而且在您解除安裝 Service Pack 時，才會變成可用。  
  
 若要解除安裝任何 Service Pack 及更新，您必須以套用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之執行個體最新的更新或 Service Pack 開始並回溯執行。 在下列每個範例中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在解除安裝其他的 Service Pack 或更新完成後，以累計更新 1 結束。  
  
-   如果是已安裝具有累計更新 1 及 SP1 之 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的執行個體，請移除 SP1。  
  
-   如果是已安裝具有累計更新 1、SP1 及累計更新 2 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體，請先解除安裝累計更新 2，然後再解除安裝 SP1。  
  
## <a name="see-also"></a>另請參閱  
 [從命令提示字元安裝 SQL Server 2014](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [安裝 SQL Server 2014 服務更新](../../database-engine/install-windows/install-sql-server-servicing-updates.md)   
 [驗證 SQL Server 安裝](../../database-engine/install-windows/validate-a-sql-server-installation.md)   
 [檢視與讀取 SQL Server 安裝程式記錄檔](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
