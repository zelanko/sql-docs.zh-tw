---
title: 受控執行個體詳細資料（SQL Server 公用程式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 6e51b7bb-a733-4852-8c33-7f4dbdf931c2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 89f962ead45c4c0670cd5adfb5da0be9373c4097
ms.sourcegitcommit: 18a7c77be31f9af92ad9d0d3ac5eecebe8eec959
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/26/2020
ms.locfileid: "83858933"
---
# <a name="managed-instance-details-sql-server-utility"></a>受管理的執行個體詳細資料 (SQL Server 公用程式)
  公用程式總管之 Managed 執行個體檢視中的資訊提供了個別 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體的使用量資料、CPU 使用量歷程記錄、檔案層級的儲存使用量詳細資料，以及檢視和更新原則臨界值的功能。 原則臨界值可以針對電腦及資料庫檔案和記錄檔在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體層級控制，也可以在存放磁碟區的層級控制。 您也可以針對個別的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Managed 執行個體檢視屬性詳細資料。  
  
## <a name="ui-element-list"></a>UI 元素清單  
 [清單] 檢視  
 上方窗格的清單檢視會依據 ComputerName\InstanceName 顯示列於資料列中的個別 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體。  
  
 健全狀態圖示會依據使用量類別提供每一個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的狀態摘要：  
  
-   綠色核取符號 - ![](../../2014/database-engine/media/well-utilized.gif "Well_utilized") - 不違反資源使用量原則的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Managed 執行個體數目。 資源的使用情況良好。  
  
-   綠色向下箭頭 - ![](../../2014/database-engine/media/utility-down-arrow.gif "Utility_down_arrow") - 資源使用量過低。  
  
-   紅色向上箭頭 - ![](../../2014/database-engine/media/utility-up-arrow.gif "Utility_up_arrow") - 資源使用量過高。  
  
 您可以變更清單檢視中資料行的順序，其方式是將資料行拖曳到左邊或右邊。 您可以加入或刪除清單檢視中的資料行，其方式是以滑鼠右鍵按一下資料行標題，並選取或取消選取資料行。 右鍵功能表也會提供排序選項。 您也可以按一下資料行名稱的上方來啟動排序。  
  
 若要存取公用程式清單檢視的篩選選項，請在 [公用程式總管] 瀏覽窗格中以滑鼠右鍵按一下 [Managed 執行個體]**** 節點，並選取 [篩選]****。 當已經實作篩選設定之後，公用程式總管中的 [受管理的執行個體]**** 節點將會標示 [受管理的執行個體 (已篩選)]****。 如需詳細資訊，請參閱[篩選設定 &#40;物件總管與公用程式總管&#41;](../ssms/object/filter-settings-object-explorer-and-utility-explorer.md)。  
  
 根據預設，下列資料行會顯示有關每一個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Managed 執行個體的健全狀態資訊。  
  
-   執行個體 CPU - 顯示配置給這個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體之處理器使用量的健全狀態。 這個參數的健全狀態是根據針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體設定的 CPU 使用量原則及動態資源評估原則的組態設定所決定。 如需詳細資訊，請參閱[降低 CPU 使用量原則的雜訊 &#40;SQL Server Utility&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
     若要檢視這個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的處理器使用量歷程記錄，或是檢視或變更原則限制，請按一下 [CPU 使用量]**** 索引標籤。  
  
-   電腦 CPU - 顯示電腦處理器使用量的健全狀態。 這個參數的健全狀態是根據針對電腦設定的 CPU 使用量原則及動態資源評估原則的組態設定所決定。 如需詳細資訊，請參閱[降低 CPU 使用量原則的雜訊 &#40;SQL Server Utility&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
     若要檢視這個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的處理器使用量歷程記錄，或是檢視或變更原則限制，請按一下 [CPU 使用量]**** 索引標籤。  
  
-   檔案空間 - 針對屬於選定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的所有資料庫來顯示檔案空間使用量的健全狀態摘要。 如果任何資料庫的健全狀態指出使用量過高，則檔案空間健全狀態將會在清單檢視中報告為使用量過高。 如果任何資料庫的健全狀態指出使用量過低，而且沒有任何資料庫使用量過高，則檔案空間健全狀態將會在清單檢視中報告為使用量過低。 否則，檔案空間健全狀態將會在清單檢視中報告為使用良好。 若要檢視或變更原則限制，請按一下 [儲存使用量]**** 索引標籤。  
  
-   磁碟區空間 - 針對包含了屬於選定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體之資料庫的所有磁碟區來顯示磁碟區空間使用量的健全狀態摘要。 如果任何磁碟區的健全狀態指出使用量過高，則磁碟區空間健全狀態將會在清單檢視中報告為使用量過高。 如果任何磁碟區的健全狀態指出使用量過低，而且沒有任何磁碟區使用量過高，則磁碟區空間健全狀態將會在清單檢視中報告為使用量過低。 否則，磁碟區空間健全狀態將會在清單檢視中報告為使用良好。 若要檢視或變更原則限制，請按一下 [儲存使用量]**** 索引標籤。  
  
-   原則類型 - 指出「全域」預設原則還是「覆寫」自訂原則對於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的 Managed 執行個體有效。  
  
 可以使用清單檢視中資料行標題區域內的右鍵功能表來顯示的其他資料行：  
  
-   處理器名稱：  
  
-   處理器速度 (MHz)：  
  
-   處理器計數：  
  
-   實體記憶體 (MB)：  
  
-   作業系統版本：  
  
-   SQL Server 版本：  
  
-   SQL Server 版本：  
  
-   叢集化：(True 或 False)  
  
-   備份目錄：  
  
-   定序：  
  
-   區分大小寫：(True 或 False)  
  
-   語言：  
  
-   上次報告時間：此資料行會使用 datetime 資料類型來顯示 UCP 本機日期和時間。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的 [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) 主題。 當您使用公用程式物件模型時，請注意 SSMS 會使用 datetimeoffset 資料類型。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的 [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) 主題。  
  
 CPU 使用量索引標籤  
 [CPU 使用量] 索引標籤會針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體和電腦的 CPU 使用量顯示歷程記錄資料的並排圖形。  
  
 此圖形會針對顯示區域右邊的選項按鈕中指定的間隔，顯示處理器使用量歷程記錄。 若要變更顯示間隔並重新整理資料集，請從清單中選取選項按鈕。  
  
 間隔選項如下：  
  
-   1 天，每隔 15 分鐘顯示。  
  
-   1 週，每隔 1 天顯示。  
  
-   1 個月，每隔 1 週顯示。  
  
-   1 年，每隔 1 個月顯示。  
  
 儲存使用量索引標籤  
 [儲存使用量] 索引標籤具有樹狀檢視，可顯示儲存使用量詳細資料。 請注意，時間資料會使用 datetime 資料類型來顯示 UCP 本機日期和時間。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的 [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) 主題。 當您使用公用程式物件模型時，請注意 SSMS 會使用 datetimeoffset 資料類型。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的 [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) 主題。  
  
 顯示畫面可以依資料庫或磁碟區來分組。 若要使用資料庫樹狀檢視，請選取 [檔案群組依據:]**** 選項中的 [資料庫]**** 選項按鈕。 若要檢視個別資料庫檔案的儲存使用量狀態，請按一下樹狀檢視中資料庫名稱旁邊的加號。 列出的資料庫檔案包含了所有屬於您在清單檢視中選取之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 受管理的執行個體的系統資料庫和使用者資料庫。  
  
 樹狀結構會對應到儲存階層。 樹狀檢視中的根節點為資料庫。 樹狀檢視的下一層包含屬於資料庫的檔案群組節點，或是屬於資料庫之記錄的記錄檔節點。 下一層包含屬於檔案群組的資料檔。  
  
 儲存使用量歷程記錄圖形中顯示的資料會因為樹狀檢視中選取的節點而有所不同：  
  
-   選取檔案群組節點，以顯示屬於選定檔案群組之所有資料檔案所使用的檔案空間圖形。  
  
-   選取記錄檔節點，以顯示屬於選定資料庫之所有記錄檔所使用的檔案空間圖形。  
  
-   選取資料庫節點來顯示一個圖形，此圖形會加入屬於選定資料庫之所有資料檔案和記錄檔所使用的檔案空間。  
  
 健全狀態圖示會提供資料庫檔案、檔案群組和記錄檔的大致狀態：  
  
 如果是資料庫：  
  
-   綠色核取符號 - 所有檔案群組和記錄檔的健全狀態 (既不是使用量過高，也不是使用量過低)。  
  
-   綠色向下箭頭 - 至少一個檔案群組或記錄檔的健全狀態表示使用量過低，而沒有任何健全狀態指出使用量過高。  
  
-   紅色向上箭頭 - 至少一個檔案群組或記錄檔的健全狀態指出使用量過高。  
  
 如果是檔案群組和記錄檔：  
  
-   綠色核取符號 - 檔案群組中所有檔案的檔案空間使用量既不是使用量過高，也不是使用量過低。  
  
-   綠色向下箭頭 - 檔案群組中至少一個檔案的檔案空間使用量過低，而且檔案群組中沒有任何檔案的使用量過高。  
  
-   紅色向上箭頭 - 檔案群組中所有資料檔案的檔案空間使用量過高。  
  
 若要依磁碟區檢視檔案，請選取 [檔案群組依據]**** 選項中的 [磁碟區]**** 選項按鈕。 儲存使用量歷程記錄的圖形會顯示存放磁碟區上所有資料檔案和記錄檔所使用的檔案空間。 針對個別資料庫資料檔案和記錄檔展開此樹狀目錄來檢視詳細資料。  
  
 狀態圖示用來提供每個磁碟區的狀態：  
  
-   綠色核取符號 - 資源使用情況良好。  
  
-   綠色向下箭頭 - 資源使用量過低。  
  
-   紅色向上箭頭 - 資源使用量過高。  
  
 [儲存使用量] 索引標籤上每一個檔案名稱旁邊的量測計都代表檔案所使用的空間量 (相較於檔案的有效容量)。 量測計旁邊所顯示的百分比值為檔案所使用的空間量比率 (相較於檔案的有效容量)。 工具提示所提供的資料是用來計算每一個磁碟區和每一個檔案相較於有效容量的百分比。  
  
 如果檔案未設定為自動成長，有效容量就是配置給檔案的空間數量。 如果檔案設定為自動成長，則有效容量就是目前配置給檔案之空間數量與目前磁碟區上可用空間數量的總和。  
  
 可以針對資料檔案和記錄檔設定儲存使用量原則。 若要檢視或變更檔案的儲存使用量原則臨界值，請按一下 [儲存使用量] 窗格底部的 [檔案原則]**** 連結。 若要檢視或變更存放磁碟區的儲存使用量原則臨界值，請按一下 [儲存使用量] 窗格底部的 [磁碟區原則]**** 連結。  
  
 若要覆寫預設原則閾值，請按一下 [覆寫預設原則]**** 選項按鈕，並指定上限和下限值，然後按一下 [確定]****。  
  
 如需變更原則違規容錯的詳細資訊，請參閱[降低 CPU 使用量原則的雜訊 &#40;SQL Server 公用程式&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
 屬性詳細資料索引標籤  
 針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體列出的屬性詳細資料包括以下類別：  
  
-   處理器名稱：  
  
-   處理器速度 (MHz)：  
  
-   處理器計數：  
  
-   實體記憶體 (MB)：  
  
-   作業系統版本：  
  
-   SQL Server 版本：  
  
-   SQL Server 版本：  
  
-   叢集化：(True 或 False)  
  
-   備份目錄：  
  
-   定序：  
  
-   區分大小寫：(True 或 False)  
  
-   語言：  
  
## <a name="see-also"></a>另請參閱  
 [部署的資料層應用程式詳細資料 &#40;SQL Server 公用程式&#41;](../../2014/database-engine/deployed-data-tier-application-details-sql-server-utility.md)   
 [公用程式儀表板 &#40;SQL Server 公用程式&#41;](../../2014/database-engine/utility-dashboard-sql-server-utility.md)   
 [監視 SQL Server 公用程式中 SQL Server 的實例](../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [SQL Server 公用程式的功能與工作](../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [疑難排解 SQL Server 公用程式](../../2014/database-engine/troubleshoot-the-sql-server-utility.md)  
  
  
