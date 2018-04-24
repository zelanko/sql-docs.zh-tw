---
title: 公用程式總管 F1 說明 | Microsoft 文件
ms.custom: ''
ms.date: 08/19/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: maintenance-plans
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- sql13.swb.ue.navigation.f1
- sql13.SWB.UE.dac.details.F1
- sql13.SQB.UE.dac.details.F1
- utility details
helpviewer_keywords:
- Utility
- management
- data-tier application
ms.assetid: 8697e4a4-4f59-4cda-af71-7de86005bd4a
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 195806725d74efb689c14200529d6dafc6a17316
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="utility-explorer-f1-help"></a>公用程式總管 F1 說明
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  下列各節說明 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式的功能和關聯的作業。  
  
  ## <a name="utility-dashboard-sql-server-utility"></a>公用程式儀表板 (SQL Server 公用程式)
 若要查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式儀表板中的資料，請在公用程式總管樹狀目錄中，選取最上方的節點，也就是標示為 "Utility<UCP_Name>\\(ComputerName\UCP)" 的節點。 此儀表板包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式內所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Managed 執行個體及所有資料層應用程式中的摘要和詳細資料。 若要重新整理儀表板中的資料，請以滑鼠右鍵按一下公用程式總管樹狀目錄中的最上方節點，然後選取 [重新整理]。  
  
 如需如何建立公用程式控制點的詳細資訊，請參閱 [建立 SQL Server 公用程式控制點 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)。 如需如何將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體加入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式的詳細資訊，請參閱 [註冊 SQL Server 的執行個體 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)。  
 
  
### <a name="uielement-list"></a>UIElement 清單  
 Managed 執行個體健全狀況  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Managed 執行個體的健全狀態會顯示在 [公用程式總管] 內容窗格的左邊。  
  
 Managed 執行個體健全狀況的參數如下：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的 CPU 使用量。  
  
-   資料庫檔案使用量。  
  
-   存放磁碟區空間使用量。  
  
-   電腦的 CPU 使用量。  
  
-   每個參數的狀態可分為三個類別：  
  
-   使用情況良好 - 不違反資源使用量原則的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Managed 執行個體數目。  
  
-   使用量過低 - 違反資源使用量過低原則的 Managed 資源數目。  
  
-   使用量過高 - 違反資源使用量過高原則的 Managed 資源數目。  
  
-   沒有可用的資料 - 沒有資料可供 SQL Server 的 Managed 執行個體使用，因為剛剛註冊 SQL Server 執行個體而且尚未完成第一次的資料收集作業，或是因為 SQL Server 的 Managed 執行個體發生問題，而無法收集資料並將資料上傳到 UCP。  
  
 每一個健全狀態參數的詳細狀態會列在滑動指標中。 滑動指標右邊的片段會顯示每一個狀態類別中的 Managed 執行個體數目。  
  
 若要建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Managed 執行個體或資料層應用程式的篩選檢視，請按一下 [公用程式儀表板] 中滑動指標旁的使用量類別連結。 例如，如果您按一下 **[公用程式總管內容]** 窗格中的 **[使用量過高的執行個體 CPU]** ，SSMS 便會建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Managed 執行個體的篩選清單檢視，其中包含根據目前原則設定之使用量過高的 CPU。  
  
 請注意，當您按一下使用量類別連結時，公用程式總管瀏覽窗格中對應的節點後面會加上 [(已篩選)]，意即 [受管理的執行個體] 會標示為 [受管理的執行個體 (已篩選) ]。 若要檢視篩選設定，請以滑鼠右鍵按一下瀏覽窗格中的節點，然後選取 [篩選]，再按一下 [篩選設定]。 若要清除篩選設定，請以滑鼠右鍵按一下瀏覽窗格中的節點，然後選取 [篩選]，再按一下 [移除篩選]。  
  
 如需檢視個別 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的健全狀態或是檢視或變更原則組態設定的詳細資訊，請參閱[受管理的執行個體詳細資料 &#40;SQL Server 公用程式&#41;](http://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2)。  
  
 公用程式摘要  
 顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式所管理之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Managed 執行個體及資料層應用程式的數目。  
  
 資料層應用程式健全狀況  
 資料層應用程式的健全狀態會顯示在 [公用程式總管] 內容窗格的右邊。  
  
 資料層應用程式健全狀況的參數如下：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的 CPU 使用量。  
  
-   資料庫檔案使用量。  
  
-   存放磁碟區空間使用量。  
  
-   電腦的 CPU 使用量。  
  
 每個參數的狀態可分為三個類別：  
  
-   使用情況良好 - 不違反資源使用量原則的資料層應用程式數目。  
  
-   使用量過高 - 違反資源使用量過高原則的資料層應用程式數目。  
  
-   使用量過低 - 違反資源使用量過低原則的資料層應用程式數目。  
  
-   沒有可用的資料 - 資料層應用程式沒有可用的資料，因為包含資料層應用程式的 SQL Server Managed 執行個體並未報告資料。  
  
 每一個健全狀態參數的詳細狀態會列在滑動指標中。 滑動指標右邊的片段會顯示每一個狀態類別中的資料層應用程式數目。 如需檢視個別資料層應用程式的健全狀態或是檢視或變更原則組態設定的詳細資訊，請參閱[部署的資料層應用程式詳細資料 &#40;SQL Server 公用程式&#41;](http://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867)。  
  
 公用程式儲存使用量歷程記錄  
 使用量歷程記錄會顯示在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式儀表板底部的時間圖中。 請注意，時間資料會使用 datetime 資料類型來顯示 UCP 本機日期和時間。 如需詳細資訊，請參閱 [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) 主題。 當您使用公用程式物件模型時，請注意 SSMS 會使用 datetimeoffset 資料類型。 如需詳細資訊，請參閱 [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) 主題。  
  
 使用顯示區域左邊的選項按鈕來變更圖形的報表期間。  
  
 報表間隔的選項如下：  
  
-   1 天，每隔 15 分鐘顯示。  
  
-   1 週，每隔 1 天顯示。  
  
-   1 個月，每隔 1 週顯示。  
  
-   1 年，每隔 1 個月顯示。  
  
 當您變更報表間隔後，資料會自動重新整理。  
  
 公用程式儲存使用量  
 在儀表板的右下方，儲存使用量圓形圖會顯示包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Managed 執行個體之電腦磁碟區上的使用空間與可用空間的比率。 此顯示畫面的資料每隔 15 分鐘會重新整理一次。  
 
 ## <a name="deployed-data-tier-application-details-sql-server-utility"></a>部署的資料層應用程式詳細資料 (SQL Server 公用程式)
  公用程式總管之 [部署的資料層應用程式] 檢視中的資訊提供了個別資料層應用程式的使用量資料、CPU 使用量歷程記錄、檔案層級的儲存使用量詳細資料，以及檢視和更新原則臨界值的功能。 原則臨界值可以針對 CPU 使用量及資料庫的資料檔案和記錄檔，於資料層應用程式層級進行控制。 您也可以針對個別的資料層應用程式來檢視屬性詳細資料。  
  
### <a name="uielement-list"></a>UIElement 清單  
 清單檢視  
 上方窗格中的清單檢視會顯示有關個別資料層應用程式的資料。 健全狀態圖示會依據使用量類別提供每一個資料層應用程式的狀態摘要：  
  
-   綠色核取符號 - ![](../../relational-databases/manage/media/well-utilized.gif "Well_utilized") - 不違反資源使用量原則的資料層應用程式數目。 資源的使用情況良好。  
  
-   綠色向下箭頭 - ![](../../relational-databases/manage/media/utility-down-arrow.gif "Utility_down_arrow") - 資源使用量過低。  
  
-   紅色向上箭頭 - ![](../../relational-databases/manage/media/utility-up-arrow.gif "Utility_up_arrow") - 資源使用量過高。  
  
 您可以變更清單檢視中資料行的順序，其方式是將資料行拖曳到左邊或右邊。 您可以加入或刪除清單檢視中的資料行，其方式是以滑鼠右鍵按一下資料行標題，並選取或取消選取資料行。 右鍵功能表也會提供排序選項。 您也可以按一下資料行名稱的上方來啟動排序。  
  
 若要存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式清單檢視的篩選選項，請在 [公用程式總管] 瀏覽窗格中以滑鼠右鍵按一下 [部署的資料層應用程式] 節點，並選取 [篩選]。 當實作篩選設定之後，[公用程式總管] 中的 [部署的資料層應用程式] 節點會標示 [部署的資料層應用程式 (已篩選)]。 如需詳細資訊，請參閱[篩選設定 &#40;物件總管與公用程式總管&#41;](http://msdn.microsoft.com/library/4aab04bc-e1ab-4d4b-ab74-b287fc805bc2)。  
  
 根據預設，下列資料行會顯示有關每一個資料層應用程式的健全狀態資訊。  
  
-   名稱 - 資料層應用程式名稱。  
  
-   應用程式 CPU - 顯示此資料層應用程式之處理器使用量的健全狀態。 這個參數的健全狀態是根據針對資料層應用程式設定的 CPU 使用量原則及動態資源評估原則的組態設定所決定。 如需詳細資訊，請參閱[降低 CPU 使用量原則的雜訊 &#40;SQL Server Utility&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
     若要檢視這個資料層應用程式的處理器使用量歷程記錄，或是檢視或變更原則限制，請按一下 [CPU 使用量] 索引標籤。  
  
-   電腦 CPU - 顯示電腦處理器使用量的健全狀態。 這個參數的健全狀態是根據針對電腦設定的 CPU 使用量原則及動態資源評估原則的組態設定所決定。 如需詳細資訊，請參閱[降低 CPU 使用量原則的雜訊 &#40;SQL Server Utility&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
     若要檢視這個資料層應用程式的處理器使用量歷程記錄，或是檢視或變更原則限制，請按一下 [CPU 使用量] 索引標籤。  
  
-   檔案空間 - 針對每一個資料層應用程式顯示檔案空間使用量的健全狀態摘要。  
  
    -   綠色核取符號 - 所有檔案群組和記錄檔群組的健全狀態既不是使用量過高，也不是使用量過低。  
  
    -   綠色向下箭頭 - 至少一個檔案群組或記錄檔群組的健全狀態表示使用量過低，而沒有任何檔案群組或記錄檔群組的使用量過高。  
  
    -   紅色向上箭頭 - 至少一個檔案群組或記錄檔群組的健全狀態指出使用量過高。 請注意，如果資料庫處於「緊急」狀態，則健全狀態會顯示記錄檔空間過度使用。  
  
     若要檢視或變更檔案空間原則限制，請按一下 [儲存使用量] 索引標籤。  
  
-   磁碟區空間 - 針對包含了屬於選定資料層應用程式之資料庫的所有磁碟區來顯示磁碟區空間使用量的健全狀態摘要。 如果任何磁碟區的健全狀態指出使用量過高，則磁碟區空間健全狀態將會在清單檢視中報告為使用量過高。 如果任何磁碟區的健全狀態指出使用量過低，而且沒有任何磁碟區使用量過高，則磁碟區空間健全狀態將會在清單檢視中報告為使用量過低。 否則，磁碟區空間健全狀態將會在清單檢視中報告為使用良好。 若要檢視或變更原則限制，請按一下 [儲存使用量] 索引標籤。  
  
-   原則類型 - 指出「全域」預設原則還是「覆寫」自訂原則對於資料層應用程式有效。  
  
-   執行個體名稱 - 顯示主控資料層應用程式的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。  
  
 可以使用清單檢視中資料行標題區域內的右鍵功能表來顯示的其他資料行：  
  
-   資料庫名稱  
  
-   部署日期  
  
-   可信任：(True 或 False)  
  
-   定序  
  
-   相容性層級：(例如 Version100)  
  
-   加密已啟用：(True 或 False)  
  
-   復原模式：(簡單、完整或大量記錄)  
  
-   上次報告時間：此資料行會使用 datetime 資料類型來顯示 UCP 本機日期和時間。 如需詳細資訊，請參閱 [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) 主題。 當您使用公用程式物件模型時，請注意 SSMS 會使用 datetimeoffset 資料類型。 如需詳細資訊，請參閱 [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) 主題。  
  
 CPU 使用量索引標籤  
 [CPU 使用量] 索引標籤會針對資料層應用程式和電腦的 CPU 使用量顯示歷程記錄資料的並排圖形。  
  
 此圖形會針對顯示區域右邊的選項按鈕中指定的間隔，顯示處理器使用量歷程記錄。 若要變更顯示間隔並重新整理資料集，請從清單中選取選項按鈕。  
  
 間隔選項如下：  
  
-   1 天，每隔 15 分鐘顯示。  
  
-   1 週，每隔 1 天顯示。  
  
-   1 個月，每隔 1 週顯示。  
  
-   1 年，每隔 1 個月顯示。  
  
 儲存使用量索引標籤  
 [儲存使用量] 索引標籤的樹狀檢視會針對屬於清單檢視中選取之資料層應用程式的資料庫檔案和記錄檔來顯示儲存使用量詳細資料。 請注意，時間資料會使用 datetime 資料類型來顯示 UCP 本機日期和時間。 如需詳細資訊，請參閱 [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) 主題。 當您使用公用程式物件模型時，請注意 SSMS 會使用 datetimeoffset 資料類型。 如需詳細資訊，請參閱 [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) 主題。  
  
 顯示畫面可以依檔案群組或磁碟區來分組。 若要使用檔案群組樹狀檢視，請選取 [檔案群組依據] 選項中的 [檔案群組] 選項按鈕。  
  
 儲存使用量歷程記錄圖形中顯示的資料會因為樹狀檢視中選取的節點而有所不同：  
  
-   選取檔案群組節點，以顯示屬於選定檔案群組之所有資料檔案所使用的檔案空間圖形。  
  
-   選取記錄檔節點，以顯示屬於選定資料庫之所有記錄檔所使用的檔案空間圖形。  
  
-   選取資料庫節點來顯示一個圖形，此圖形會加入屬於選定資料庫之所有資料檔案和記錄檔所使用的檔案空間。  
  
 若要檢視個別檔案的儲存使用量狀態，請按一下樹狀檢視中檔案名稱旁邊的加號。  
  
 健全狀態圖示會提供每一個檔案群組相較於原則臨界值的大致狀態：  
  
-   綠色核取符號 - 檔案群組中至少有一個資料檔案的檔案空間使用量既不是使用量過高，也不是使用量過低。  
  
-   綠色向下箭頭 - 檔案群組中至少有一個資料檔案的檔案空間使用量過低，而且檔案群組中沒有任何檔案的使用量過高。  
  
-   紅色向上箭頭 - 檔案群組中所有資料檔案的檔案空間使用量過高。 請注意，如果資料庫處於「緊急」狀態，則健全狀態會顯示記錄檔空間過度使用。  
  
 若要依磁碟區檢視檔案，請選取 [檔案群組依據] 選項中的 [磁碟區] 選項按鈕。 儲存使用量歷程記錄的圖形會顯示存放磁碟區上所有資料檔案和記錄檔所使用的檔案空間。 針對個別資料庫資料檔案和記錄檔展開此樹狀目錄來檢視詳細資料。  
  
 狀態圖示用來提供每個磁碟區的狀態：  
  
-   綠色核取符號 - 資源使用情況良好。  
  
-   綠色向下箭頭 - 資源使用量過低。  
  
-   紅色向上箭頭 - 資源使用量過高。  
  
 [儲存使用量] 索引標籤上每一個檔案名稱旁邊的量測計都代表檔案所使用的空間量 (相較於檔案的有效容量)。 量測計旁邊所顯示的百分比值為檔案所使用的空間量比率 (相較於檔案的有效容量)。 工具提示所提供的資料是用來計算每一個磁碟區和每一個檔案相較於有效容量的百分比。  
  
 如果檔案未設定為自動成長，有效容量就是配置給檔案的空間數量。 如果檔案設定為自動成長，則有效容量就是目前配置給檔案之空間數量與目前磁碟區上可用空間數量的總和。  
  
 可以針對資料檔案和記錄檔設定儲存使用量原則。 若要檢視或變更檔案的儲存使用量原則臨界值，請按一下 [儲存使用量] 窗格底部的 [檔案原則] 連結。 若要檢視或變更存放磁碟區的儲存使用量原則臨界值，請按一下 [儲存使用量] 窗格底部的 [磁碟區原則] 連結。  
  
 若要覆寫預設原則閾值，請按一下 [覆寫預設原則] 選項按鈕，並指定上限和下限值，然後按一下 [確定]。  
  
 如需變更原則違規容錯的詳細資訊，請參閱[降低 CPU 使用量原則的雜訊 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
 屬性詳細資料索引標籤  
 針對資料層應用程式列出的屬性詳細資料包括以下類別：  
  
-   資料庫名稱  
  
-   部署日期  
  
-   可信任：(True 或 False)  
  
-   定序  
  
-   相容性層級：(例如 Version100)  
  
-   加密已啟用：(True 或 False)  
  
-   復原模式：(簡單、完整或大量記錄)  
  
-   上次報告時間：此資料行會使用 datetime 資料類型來顯示 UCP 本機日期和時間。 如需詳細資訊，請參閱 [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) 主題。 當您使用公用程式物件模型時，請注意 SSMS 會使用 datetimeoffset 資料類型。 如需詳細資訊，請參閱 [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) 主題。

## <a name="managed-instance-details-sql-server-utility"></a>受管理的執行個體詳細資料 (SQL Server 公用程式)
 公用程式總管之 Managed 執行個體檢視中的資訊提供了個別 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的使用量資料、CPU 使用量歷程記錄、檔案層級的儲存使用量詳細資料，以及檢視和更新原則臨界值的功能。 原則臨界值可以針對電腦及資料庫檔案和記錄檔在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體層級控制，也可以在存放磁碟區的層級控制。 您也可以針對個別的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Managed 執行個體檢視屬性詳細資料。  
  
### <a name="uielement-list"></a>UIElement 清單  
 清單檢視  
 上方窗格的清單檢視會依據 ComputerName\InstanceName 顯示列於資料列中的個別 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
 健全狀態圖示會依據使用量類別提供每一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的狀態摘要：  
  
-   綠色核取符號 - ![](../../relational-databases/manage/media/well-utilized.gif "Well_utilized") - 不違反資源使用量原則的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Managed 執行個體數目。 資源的使用情況良好。  
  
-   綠色向下箭頭 - ![](../../relational-databases/manage/media/utility-down-arrow.gif "Utility_down_arrow") - 資源使用量過低。  
  
-   紅色向上箭頭 - ![](../../relational-databases/manage/media/utility-up-arrow.gif "Utility_up_arrow") - 資源使用量過高。  
  
 您可以變更清單檢視中資料行的順序，其方式是將資料行拖曳到左邊或右邊。 您可以加入或刪除清單檢視中的資料行，其方式是以滑鼠右鍵按一下資料行標題，並選取或取消選取資料行。 右鍵功能表也會提供排序選項。 您也可以按一下資料行名稱的上方來啟動排序。  
  
 若要存取公用程式清單檢視的篩選選項，請在 [公用程式總管] 瀏覽窗格中以滑鼠右鍵按一下 [Managed 執行個體] 節點，並選取 [篩選]。 當已經實作篩選設定之後，公用程式總管中的 [受管理的執行個體] 節點將會標示 [受管理的執行個體 (已篩選)]。 如需詳細資訊，請參閱[篩選設定 &#40;物件總管與公用程式總管&#41;](http://msdn.microsoft.com/library/4aab04bc-e1ab-4d4b-ab74-b287fc805bc2)。  
  
 根據預設，下列資料行會顯示有關每一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Managed 執行個體的健全狀態資訊。  
  
-   執行個體 CPU - 顯示配置給這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之處理器使用量的健全狀態。 這個參數的健全狀態是根據針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體設定的 CPU 使用量原則及動態資源評估原則的組態設定所決定。 如需詳細資訊，請參閱[降低 CPU 使用量原則的雜訊 &#40;SQL Server Utility&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
     若要檢視這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的處理器使用量歷程記錄，或是檢視或變更原則限制，請按一下 [CPU 使用量] 索引標籤。  
  
-   電腦 CPU - 顯示電腦處理器使用量的健全狀態。 這個參數的健全狀態是根據針對電腦設定的 CPU 使用量原則及動態資源評估原則的組態設定所決定。 如需詳細資訊，請參閱[降低 CPU 使用量原則的雜訊 &#40;SQL Server Utility&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
     若要檢視這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的處理器使用量歷程記錄，或是檢視或變更原則限制，請按一下 [CPU 使用量] 索引標籤。  
  
-   檔案空間 - 針對屬於選定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的所有資料庫來顯示檔案空間使用量的健全狀態摘要。 如果任何資料庫的健全狀態指出使用量過高，則檔案空間健全狀態將會在清單檢視中報告為使用量過高。 如果任何資料庫的健全狀態指出使用量過低，而且沒有任何資料庫使用量過高，則檔案空間健全狀態將會在清單檢視中報告為使用量過低。 否則，檔案空間健全狀態將會在清單檢視中報告為使用良好。 若要檢視或變更原則限制，請按一下 [儲存使用量] 索引標籤。  
  
-   磁碟區空間 - 針對包含了屬於選定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之資料庫的所有磁碟區來顯示磁碟區空間使用量的健全狀態摘要。 如果任何磁碟區的健全狀態指出使用量過高，則磁碟區空間健全狀態將會在清單檢視中報告為使用量過高。 如果任何磁碟區的健全狀態指出使用量過低，而且沒有任何磁碟區使用量過高，則磁碟區空間健全狀態將會在清單檢視中報告為使用量過低。 否則，磁碟區空間健全狀態將會在清單檢視中報告為使用良好。 若要檢視或變更原則限制，請按一下 [儲存使用量] 索引標籤。  
  
-   原則類型 - 指出「全域」預設原則還是「覆寫」自訂原則對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 Managed 執行個體有效。  
  
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
  
-   上次報告時間：此資料行會使用 datetime 資料類型來顯示 UCP 本機日期和時間。 如需詳細資訊，請參閱 [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) 主題。 當您使用公用程式物件模型時，請注意 SSMS 會使用 datetimeoffset 資料類型。 如需詳細資訊，請參閱 [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) 主題。  
  
 CPU 使用量索引標籤  
 [CPU 使用量] 索引標籤會針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體和電腦的 CPU 使用量顯示歷程記錄資料的並排圖形。  
  
 此圖形會針對顯示區域右邊的選項按鈕中指定的間隔，顯示處理器使用量歷程記錄。 若要變更顯示間隔並重新整理資料集，請從清單中選取選項按鈕。  
  
 間隔選項如下：  
  
-   1 天，每隔 15 分鐘顯示。  
  
-   1 週，每隔 1 天顯示。  
  
-   1 個月，每隔 1 週顯示。  
  
-   1 年，每隔 1 個月顯示。  
  
 儲存使用量索引標籤  
 [儲存使用量] 索引標籤具有樹狀檢視，可顯示儲存使用量詳細資料。 請注意，時間資料會使用 datetime 資料類型來顯示 UCP 本機日期和時間。 如需詳細資訊，請參閱 [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) 主題。 當您使用公用程式物件模型時，請注意 SSMS 會使用 datetimeoffset 資料類型。 如需詳細資訊，請參閱 [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) 主題。  
  
 顯示畫面可以依資料庫或磁碟區來分組。 若要使用資料庫樹狀檢視，請選取 [檔案群組依據:] 選項中的 [資料庫] 選項按鈕。 若要檢視個別資料庫檔案的儲存使用量狀態，請按一下樹狀檢視中資料庫名稱旁邊的加號。 列出的資料庫檔案包含了所有屬於您在清單檢視中選取之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體的系統資料庫和使用者資料庫。  
  
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
  
 若要依磁碟區檢視檔案，請選取 [檔案群組依據] 選項中的 [磁碟區] 選項按鈕。 儲存使用量歷程記錄的圖形會顯示存放磁碟區上所有資料檔案和記錄檔所使用的檔案空間。 針對個別資料庫資料檔案和記錄檔展開此樹狀目錄來檢視詳細資料。  
  
 狀態圖示用來提供每個磁碟區的狀態：  
  
-   綠色核取符號 - 資源使用情況良好。  
  
-   綠色向下箭頭 - 資源使用量過低。  
  
-   紅色向上箭頭 - 資源使用量過高。  
  
 [儲存使用量] 索引標籤上每一個檔案名稱旁邊的量測計都代表檔案所使用的空間量 (相較於檔案的有效容量)。 量測計旁邊所顯示的百分比值為檔案所使用的空間量比率 (相較於檔案的有效容量)。 工具提示所提供的資料是用來計算每一個磁碟區和每一個檔案相較於有效容量的百分比。  
  
 如果檔案未設定為自動成長，有效容量就是配置給檔案的空間數量。 如果檔案設定為自動成長，則有效容量就是目前配置給檔案之空間數量與目前磁碟區上可用空間數量的總和。  
  
 可以針對資料檔案和記錄檔設定儲存使用量原則。 若要檢視或變更檔案的儲存使用量原則臨界值，請按一下 [儲存使用量] 窗格底部的 [檔案原則] 連結。 若要檢視或變更存放磁碟區的儲存使用量原則臨界值，請按一下 [儲存使用量] 窗格底部的 [磁碟區原則] 連結。  
  
 若要覆寫預設原則閾值，請按一下 [覆寫預設原則] 選項按鈕，並指定上限和下限值，然後按一下 [確定]。  
  
 如需變更原則違規容錯的詳細資訊，請參閱[降低 CPU 使用量原則的雜訊 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
 屬性詳細資料索引標籤  
 針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體列出的屬性詳細資料包括以下類別：  
  
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

## <a name="utility-administration-sql-server-utility"></a>公用程式管理 (SQL Server 公用程式)
您可以使用 [公用程式管理] 索引標籤來管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式的原則、安全性和資料倉儲設定。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式概念的詳細資訊，請參閱 [SQL Server 公用程式的功能與工作](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  
  
### <a name="uielement-list"></a>UIElement 清單
 **原則索引標籤** - 使用 [原則] 索引標籤來檢視或指定全域監視原則。  
  
 設定全域資料層應用程式監視原則。 若要展開這個選項的值清單，請按一下原則名稱旁的箭頭，或是按一下原則標題。  
 應用程式何時用完處理器容量？ 若要變更這個原則，請使用原則描述右邊的控制項，然後按一下 **[套用]**。 您也可以使用顯示畫面底部的按鈕來還原預設值或捨棄變更。  
  
-   處理器使用量的預設最大值為 70%。  
  
-   處理器使用量的預設最小值為 0%。  
  
 應用程式何時用完檔案空間？ 若要變更資料檔或記錄檔空間使用量的原則，請使用原則描述右邊的控制項，然後按一下 [套用] 。 您也可以使用顯示畫面底部的按鈕來還原預設值或捨棄變更。  
  
-   檔案空間使用量的預設最大值為 70%。  
  
-   檔案空間使用量的預設最小值為 0%。  
  
 設定 SQL Server Managed 執行個體的全域應用程式監視原則。 若要展開這個選項的值清單，請按一下原則名稱旁的箭頭，或是按一下原則標題。  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 Managed 執行個體何時用完處理器容量？ 若要變更這個原則，請使用原則描述右邊的控制項，然後按一下 **[套用]**。 您也可以使用顯示畫面底部的按鈕來還原預設值或捨棄變更。  
  
-   執行個體處理器使用量的預設最大值為 70%。  
  
-   執行個體處理器使用量的預設最小值為 0%。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦的 Managed 執行個體何時用完處理器容量？ 若要變更這個原則，請使用原則描述右邊的控制項，然後按一下 **[套用]**。 您也可以使用顯示畫面底部的按鈕來還原預設值或捨棄變更。  
  
-   電腦處理器使用量的預設最大值為 70%。  
  
-   電腦處理器使用量的預設最小值為 0%。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 Managed 執行個體何時用完檔案空間？ 若要變更資料檔或記錄檔空間使用量的原則，請使用原則描述右邊的控制項，然後按一下 **[套用]**。 您也可以使用顯示畫面底部的按鈕來還原預設值或捨棄變更。  
  
-   檔案空間使用量的預設最大值為 70%。  
  
-   檔案空間使用量的預設最小值為 0%。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦的 Managed 執行個體何時用完存放磁碟區空間？ 若要變更這個原則，請使用原則描述右邊的控制項，然後按一下 **[套用]**。 您也可以使用顯示畫面底部的按鈕來還原預設值或捨棄變更。  
  
-   電腦磁碟區空間使用量的預設最大值為 70%。  
  
-   電腦磁碟區空間使用量的預設最小值為 0%。  
  
 從高動態的資源中減少原則違規雜訊。 若要展開這項功能的控制項，請按一下顯示畫面右邊的向下箭頭。  
 如需詳細資訊，請參閱[降低 CPU 使用量原則的雜訊 &#40;SQL Server Utility&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
 
**安全性索引標籤** - 顯示有權從 UCP 管理或讀取的登入名稱。  
  
 從 UCP 選取將會加入至公用程式讀取者角色的登入。  
 公用程式讀取者權限可讓使用者帳戶：  
  
-   連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式。  
  
-   請參閱 SSMS 中公用程式總管內的所有視點。  
  
-   請參閱 SSMS 中公用程式總管內 [公用程式管理] 節點上的設定。  
  
 公用程式管理員可以將 SQL Server 執行個體註冊到 SQL Server 公用程式，並從 SQL Server 公用程式中移除 SQL Server 執行個體，也可以修改 Managed 執行個體的原則及修改 UCP 上的管理設定。  
  
 若要成為公用程式管理員，您必須擁有 SQL Server 執行個體的系統管理員 (sysadmin) 權限。 若要加入或變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 的使用者帳戶，請在 SSMS 中使用物件總管，將使用者加入至 SQL Server UCP 執行個體的伺服器登入。 如需詳細資訊，請參閱 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)。  
  
 
**資料倉儲索引標籤** - 顯示公用程式管理資料倉儲的組態詳細資料。  
  
 資料保留  
 指定針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Managed 執行個體所收集之使用量資訊的資料保留週期。 預設期間為 1 年。 最小值是 1 個月。 最長的支援期間為 2 年。  
  
 公用程式資料倉儲組態資訊  
 這一版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]無法設定下列組態設定：  
  
-   UMDW 名稱：Sysutility_mdw_\<GUID>_DATA。  
  
-   收集組上傳頻率：每隔 15 分鐘。  
  
 UMDW 目錄是可以設定的：\<系統磁碟機>:\Program Files\Microsoft SQL Server\MSSQL10_50.<UCP_Name>\MSSQL\Data\\，其中 \<系統磁碟機> 通常是 C:\ 磁碟機。 記錄檔 UMDW_\<GUID>_LOG 位於相同的目錄中。  
  
> **注意：** 可以使用卸離/附加或 ALTER DATABASE 來變更 UMDW (sysutility_mdw) 檔案的位置。 我們建議使用 ALTER DATABASE。 如需詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)。  
  
 回到原廠的預設值  
 若要將此索引標籤上的設定重設為預設值，請按一下 [還原預設值] 按鈕，然後按一下 [套用]。  
 
  
## <a name="reference"></a>參考  
 [建立 SQL Server 公用程式控制點 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)  
  
 [連接至 SQL Server 公用程式](../../relational-databases/manage/connect-to-a-sql-server-utility.md)  
  
 [註冊 SQL Server 的執行個體 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)  
  
 [設定健全狀況原則 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/configure-health-policies-sql-server-utility.md)  
  
 [監視 SQL Server 公用程式中的 SQL Server 執行個體](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 公用程式的功能與工作](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [疑難排解 SQL Server 公用程式](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  
