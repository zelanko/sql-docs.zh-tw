---
title: 公用程式儀表板（SQL Server 公用程式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 999eb741-4a60-43f6-ab37-2df7dce845c1
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5f0eb497499eafe16756becfb9607b925add08e9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62773810"
---
# <a name="utility-dashboard-sql-server-utility"></a>公用程式儀表板 (SQL Server 公用程式)
  若要查看 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 公用程式儀表板中的資料，請在公用程式總管樹狀目錄中，選取最上方的節點，也就是標示為 "Utility<UCP_Name>\\(ComputerName\UCP)" 的節點。 此儀表板包含 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 公用程式內所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Managed 執行個體及所有資料層應用程式中的摘要和詳細資料。 若要重新整理儀表板中的資料，請以滑鼠右鍵按一下公用程式總管樹狀目錄中的最上方節點，然後選取 [重新整理]****。  
  
 如需如何建立公用程式控制點的詳細資訊，請參閱 [建立 SQL Server 公用程式控制點 &#40;SQL Server 公用程式&#41;](../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)。 如需如何將 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體加入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 公用程式的詳細資訊，請參閱 [註冊 SQL Server 的執行個體 &#40;SQL Server 公用程式&#41;](../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)。  
  
## <a name="uielement-list"></a>UIElement 清單  
 Managed 執行個體健全狀況  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Managed 執行個體的健全狀態會顯示在 [公用程式總管] 內容窗格的左邊。  
  
 Managed 執行個體健全狀況的參數如下：  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體的 CPU 使用量。  
  
-   資料庫檔案使用量。  
  
-   存放磁碟區空間使用量。  
  
-   電腦的 CPU 使用量。  
  
-   每個參數的狀態可分為三個類別：  
  
-   使用情況良好 - 不違反資源使用量原則的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Managed 執行個體數目。  
  
-   使用量過低 - 違反資源使用量過低原則的 Managed 資源數目。  
  
-   使用量過高 - 違反資源使用量過高原則的 Managed 資源數目。  
  
-   沒有可用的資料 - 沒有資料可供 SQL Server 的 Managed 執行個體使用，因為剛剛註冊 SQL Server 執行個體而且尚未完成第一次的資料收集作業，或是因為 SQL Server 的 Managed 執行個體發生問題，而無法收集資料並將資料上傳到 UCP。  
  
 每一個健全狀態參數的詳細狀態會列在滑動指標中。 滑動指標右邊的片段會顯示每一個狀態類別中的 Managed 執行個體數目。  
  
 若要建立 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Managed 執行個體或資料層應用程式的篩選檢視，請按一下 [公用程式儀表板] 中滑動指標旁的使用量類別連結。 例如，如果您按一下 **[公用程式總管內容]** 窗格中的 **[使用量過高的執行個體 CPU]** ，SSMS 便會建立 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Managed 執行個體的篩選清單檢視，其中包含根據目前原則設定之使用量過高的 CPU。  
  
 請注意，當您按一下使用量類別連結時，公用程式總管瀏覽窗格中對應的節點後面會加上 [(已篩選)]****，意即 [受管理的執行個體]**** 會標示為 [受管理的執行個體 (已篩選) ]****。 若要檢視篩選設定，請以滑鼠右鍵按一下瀏覽窗格中的節點，然後選取 [篩選]****，再按一下 [篩選設定]****。 若要清除篩選設定，請以滑鼠右鍵按一下瀏覽窗格中的節點，然後選取 [篩選]****，再按一下 [移除篩選]****。  
  
 如需檢視個別 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的健全狀態或是檢視或變更原則組態設定的詳細資訊，請參閱[受管理的執行個體詳細資料 &#40;SQL Server 公用程式&#41;](../../2014/database-engine/managed-instance-details-sql-server-utility.md)。  
  
 公用程式摘要  
 顯示 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 公用程式所管理之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Managed 執行個體及資料層應用程式的數目。  
  
 資料層應用程式健全狀況  
 資料層應用程式的健全狀態會顯示在 [公用程式總管] 內容窗格的右邊。  
  
 資料層應用程式健全狀況的參數如下：  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體的 CPU 使用量。  
  
-   資料庫檔案使用量。  
  
-   存放磁碟區空間使用量。  
  
-   電腦的 CPU 使用量。  
  
 每個參數的狀態可分為三個類別：  
  
-   使用情況良好 - 不違反資源使用量原則的資料層應用程式數目。  
  
-   使用量過高 - 違反資源使用量過高原則的資料層應用程式數目。  
  
-   使用量過低 - 違反資源使用量過低原則的資料層應用程式數目。  
  
-   沒有可用的資料 - 資料層應用程式沒有可用的資料，因為包含資料層應用程式的 SQL Server Managed 執行個體並未報告資料。  
  
 每一個健全狀態參數的詳細狀態會列在滑動指標中。 滑動指標右邊的片段會顯示每一個狀態類別中的資料層應用程式數目。 如需檢視個別資料層應用程式的健全狀態或是檢視或變更原則組態設定的詳細資訊，請參閱[部署的資料層應用程式詳細資料 &#40;SQL Server 公用程式&#41;](../../2014/database-engine/deployed-data-tier-application-details-sql-server-utility.md)。  
  
 公用程式儲存使用量歷程記錄  
 使用量歷程記錄會顯示在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 公用程式儀表板底部的時間圖中。 請注意，時間資料會使用 datetime 資料類型來顯示 UCP 本機日期和時間。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的 [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) 主題。 當您使用公用程式物件模型時，請注意 SSMS 會使用 datetimeoffset 資料類型。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的 [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) 主題。  
  
 使用顯示區域左邊的選項按鈕來變更圖形的報表期間。  
  
 報表間隔的選項如下：  
  
-   1 天，每隔 15 分鐘顯示。  
  
-   1 週，每隔 1 天顯示。  
  
-   1 個月，每隔 1 週顯示。  
  
-   1 年，每隔 1 個月顯示。  
  
 當您變更報表間隔後，資料會自動重新整理。  
  
 公用程式儲存使用量  
 在儀表板的右下方，儲存使用量圓形圖會顯示包含 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Managed 執行個體之電腦磁碟區上的使用空間與可用空間的比率。 此顯示畫面的資料每隔 15 分鐘會重新整理一次。  
  
## <a name="see-also"></a>另請參閱  
 [使用公用程式瀏覽器來管理 SQL Server 公用程式](../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md)   
 [註冊 SQL Server &#40;SQL Server 公用程式的實例&#41;](../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)   
 [修改資源健康情況原則定義 &#40;SQL Server 公用程式&#41;](../relational-databases/manage/modify-a-resource-health-policy-definition-sql-server-utility.md)  
  
  
