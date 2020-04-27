---
title: 部署的資料層應用程式詳細資料（SQL Server 公用程式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.UE.dac.details.F1
helpviewer_keywords:
- utility, management
- Utility
- SQL Server Utility [SQL Server]
- data-tier application [SQL Server], utility details
- Multi-server management [SQL Server]
ms.assetid: 79c41dd9-abcb-434e-9326-00a341d5c867
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0ca9186b93e96c60e1c5128e385b5b77d5f2b94e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62754085"
---
# <a name="deployed-data-tier-application-details-sql-server-utility"></a>部署的資料層應用程式詳細資料 (SQL Server 公用程式)
  公用程式總管之 [部署的資料層應用程式] 檢視中的資訊提供了個別資料層應用程式的使用量資料、CPU 使用量歷程記錄、檔案層級的儲存使用量詳細資料，以及檢視和更新原則臨界值的功能。 原則臨界值可以針對 CPU 使用量及資料庫的資料檔案和記錄檔，於資料層應用程式層級進行控制。 您也可以針對個別的資料層應用程式來檢視屬性詳細資料。  
  
## <a name="uielement-list"></a>UIElement 清單  
 [清單] 檢視  
 上方窗格中的清單檢視會顯示有關個別資料層應用程式的資料。 健全狀態圖示會依據使用量類別提供每一個資料層應用程式的狀態摘要：  
  
-   綠色核取符號 - ![](../../2014/database-engine/media/well-utilized.gif "Well_utilized") - 不違反資源使用量原則的資料層應用程式數目。 資源的使用情況良好。  
  
-   綠色向下箭頭 - ![](../../2014/database-engine/media/utility-down-arrow.gif "Utility_down_arrow") - 資源使用量過低。  
  
-   紅色向上箭頭 - ![](../../2014/database-engine/media/utility-up-arrow.gif "Utility_up_arrow") - 資源使用量過高。  
  
 您可以變更清單檢視中資料行的順序，其方式是將資料行拖曳到左邊或右邊。 您可以加入或刪除清單檢視中的資料行，其方式是以滑鼠右鍵按一下資料行標題，並選取或取消選取資料行。 右鍵功能表也會提供排序選項。 您也可以按一下資料行名稱的上方來啟動排序。  
  
 若要存取 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 公用程式清單檢視的篩選選項，請在 [公用程式總管] 瀏覽窗格中以滑鼠右鍵按一下 [部署的資料層應用程式]**** 節點，並選取 [篩選]****。 當實作篩選設定之後，[公用程式總管] 中的 [部署的資料層應用程式]**** 節點會標示 [部署的資料層應用程式 (已篩選)]****。 如需詳細資訊，請參閱[篩選設定 &#40;物件總管與公用程式總管&#41;](../ssms/object/filter-settings-object-explorer-and-utility-explorer.md)。  
  
 根據預設，下列資料行會顯示有關每一個資料層應用程式的健全狀態資訊。  
  
-   名稱 - 資料層應用程式名稱。  
  
-   應用程式 CPU - 顯示此資料層應用程式之處理器使用量的健全狀態。 這個參數的健全狀態是根據針對資料層應用程式設定的 CPU 使用量原則及動態資源評估原則的組態設定所決定。 如需詳細資訊，請參閱[降低 CPU 使用量原則的雜訊 &#40;SQL Server Utility&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
     若要檢視這個資料層應用程式的處理器使用量歷程記錄，或是檢視或變更原則限制，請按一下 [CPU 使用量]**** 索引標籤。  
  
-   電腦 CPU - 顯示電腦處理器使用量的健全狀態。 這個參數的健全狀態是根據針對電腦設定的 CPU 使用量原則及動態資源評估原則的組態設定所決定。 如需詳細資訊，請參閱[降低 CPU 使用量原則的雜訊 &#40;SQL Server Utility&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
     若要檢視這個資料層應用程式的處理器使用量歷程記錄，或是檢視或變更原則限制，請按一下 [CPU 使用量]**** 索引標籤。  
  
-   檔案空間 - 針對每一個資料層應用程式顯示檔案空間使用量的健全狀態摘要。  
  
    -   綠色核取符號 - 所有檔案群組和記錄檔群組的健全狀態既不是使用量過高，也不是使用量過低。  
  
    -   綠色向下箭頭 - 至少一個檔案群組或記錄檔群組的健全狀態表示使用量過低，而沒有任何檔案群組或記錄檔群組的使用量過高。  
  
    -   紅色向上箭頭 - 至少一個檔案群組或記錄檔群組的健全狀態指出使用量過高。 請注意，如果資料庫處於「緊急」狀態，則健康狀態會顯示記錄檔空間過度使用。  
  
     若要檢視或變更檔案空間原則限制，請按一下 [儲存使用量]**** 索引標籤。  
  
-   磁碟區空間 - 針對包含了屬於選定資料層應用程式之資料庫的所有磁碟區來顯示磁碟區空間使用量的健全狀態摘要。 如果任何磁碟區的健全狀態指出使用量過高，則磁碟區空間健全狀態將會在清單檢視中報告為使用量過高。 如果任何磁碟區的健全狀態指出使用量過低，而且沒有任何磁碟區使用量過高，則磁碟區空間健全狀態將會在清單檢視中報告為使用量過低。 否則，磁碟區空間健全狀態將會在清單檢視中報告為使用良好。 若要檢視或變更原則限制，請按一下 [儲存使用量]**** 索引標籤。  
  
-   原則類型 - 指出「全域」預設原則還是「覆寫」自訂原則對於資料層應用程式有效。  
  
-   執行個體名稱 - 顯示主控資料層應用程式的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體名稱。  
  
 可以使用清單檢視中資料行標題區域內的右鍵功能表來顯示的其他資料行：  
  
-   資料庫名稱  
  
-   部署日期  
  
-   可信任：(True 或 False)  
  
-   定序  
  
-   相容性層級：(例如 Version100)  
  
-   加密已啟用：(True 或 False)  
  
-   復原模式：(簡單、完整或大量記錄)  
  
-   上次報告時間：此資料行會使用 datetime 資料類型來顯示 UCP 本機日期和時間。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的 [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) 主題。 當您使用公用程式物件模型時，請注意 SSMS 會使用 datetimeoffset 資料類型。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的 [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) 主題。  
  
 CPU 使用量索引標籤  
 [CPU 使用量] 索引標籤會針對資料層應用程式和電腦的 CPU 使用量顯示歷程記錄資料的並排圖形。  
  
 此圖形會針對顯示區域右邊的選項按鈕中指定的間隔，顯示處理器使用量歷程記錄。 若要變更顯示間隔並重新整理資料集，請從清單中選取選項按鈕。  
  
 間隔選項如下：  
  
-   1 天，每隔 15 分鐘顯示。  
  
-   1 週，每隔 1 天顯示。  
  
-   1 個月，每隔 1 週顯示。  
  
-   1 年，每隔 1 個月顯示。  
  
 儲存使用量索引標籤  
 [儲存使用量] 索引標籤的樹狀檢視會針對屬於清單檢視中選取之資料層應用程式的資料庫檔案和記錄檔來顯示儲存使用量詳細資料。 請注意，時間資料會使用 datetime 資料類型來顯示 UCP 本機日期和時間。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的 [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) 主題。 當您使用公用程式物件模型時，請注意 SSMS 會使用 datetimeoffset 資料類型。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的 [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) 主題。  
  
 顯示畫面可以依檔案群組或磁碟區來分組。 若要使用檔案群組樹狀檢視，請選取 [檔案群組依據]**** 選項中的 [檔案群組]**** 選項按鈕。  
  
 儲存使用量歷程記錄圖形中顯示的資料會因為樹狀檢視中選取的節點而有所不同：  
  
-   選取檔案群組節點，以顯示屬於選定檔案群組之所有資料檔案所使用的檔案空間圖形。  
  
-   選取記錄檔節點，以顯示屬於選定資料庫之所有記錄檔所使用的檔案空間圖形。  
  
-   選取資料庫節點來顯示一個圖形，此圖形會加入屬於選定資料庫之所有資料檔案和記錄檔所使用的檔案空間。  
  
 若要檢視個別檔案的儲存使用量狀態，請按一下樹狀檢視中檔案名稱旁邊的加號。  
  
 健全狀態圖示會提供每一個檔案群組相較於原則臨界值的大致狀態：  
  
-   綠色核取符號 - 檔案群組中至少有一個資料檔案的檔案空間使用量既不是使用量過高，也不是使用量過低。  
  
-   綠色向下箭頭 - 檔案群組中至少有一個資料檔案的檔案空間使用量過低，而且檔案群組中沒有任何檔案的使用量過高。  
  
-   紅色向上箭頭 - 檔案群組中所有資料檔案的檔案空間使用量過高。 請注意，如果資料庫處於「緊急」狀態，則健康狀態會顯示記錄檔空間過度使用。  
  
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
 針對資料層應用程式列出的屬性詳細資料包括以下類別：  
  
-   資料庫名稱  
  
-   部署日期  
  
-   可信任：(True 或 False)  
  
-   定序  
  
-   相容性層級：(例如 Version100)  
  
-   加密已啟用：(True 或 False)  
  
-   復原模式：(簡單、完整或大量記錄)  
  
-   上次報告時間：此資料行會使用 datetime 資料類型來顯示 UCP 本機日期和時間。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的 [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) 主題。 當您使用公用程式物件模型時，請注意 SSMS 會使用 datetimeoffset 資料類型。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的 [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) 主題。  
  
## <a name="see-also"></a>另請參閱  
 [受管理的執行個體詳細資料 &#40;SQL Server 公用程式&#41;](../../2014/database-engine/managed-instance-details-sql-server-utility.md)   
 [公用程式儀表板 &#40;SQL Server 公用程式&#41;](../../2014/database-engine/utility-dashboard-sql-server-utility.md)   
 [監視 SQL Server 公用程式中 SQL Server 的實例](../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [SQL Server 公用程式的功能與工作](../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
