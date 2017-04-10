---
title: "使用 Windows Synchronization Manager 同步處理訂閱 (Windows Synchronization Manager) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "同步處理 [SQL Server 複寫], Windows Synchronization Manager"
  - "Windows Synchronization Manager"
ms.assetid: 80f15dd6-e84d-4f96-9866-5b34ea531f1e
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 使用 Windows Synchronization Manager 同步處理訂閱 (Windows Synchronization Manager)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 同步處理管理員只可以用來同步處理訂閱 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 同一部電腦做為同步處理管理員 」 （它也可用來同步處理離線檔案和網頁） 上執行。 若要使用 Synchronization Manager：  
  
1.  啟用同步處理提取訂閱使用 Windows Synchronization Manager 在 **訂閱屬性-\< 訂閱者>: \< u>** 對話方塊。 如需有關存取這個對話方塊的詳細資訊，請參閱 [檢視和修改提取訂閱屬性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)。  
  
2.  若要透過存取同步處理管理員 **啟動** Windows 中的功能表。  
  
 Synchronization Manager 允許您為合併訂閱使用「互動解決器」。 通常，同步處理期間偵測到的衝突會自動解決，但是如果啟用了互動式解決方案，衝突可由使用者在同步處理期間解決。 如果是在 Windows Synchronization Manager 之外執行同步處理 (如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或複寫監視器中已排程的同步處理或視需要同步處理)，則不需要使用者的介入，就會根據為發行項指定的解決器自動解決衝突。  
  
> [!NOTE]  
>  從 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] 和 [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] 開始，64 位元版本的 Windows Synchronization Manager 無法偵測 32 位元訂閱。  
  
### 若要使用 Windows Synchronization Manager 啟用提取訂閱同步處理  
  
1.  在 **一般** 頁面 **訂閱屬性-\< 訂閱者>: \< u>** 對話方塊中，選取值 **啟用** 的 **使用 Windows Synchronization Manager** 選項。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### 若要使用 Synchronization Manager 同步處理提取訂閱  
  
1.  請利用下列其中一種方法來啟動 Synchronization Manager：  
  
    -   在 Internet Explorer 中，按一下 [ **工具**, ，然後按一下 [ **同步**。  
  
    -   按一下 [ **啟動**, ，指向 **程式** 或 **所有程式**, ，指向 [ **附屬應用程式**, ，然後按一下 [ **同步**。  
  
    -   按一下 [ **啟動**, ，然後按一下 [ **執行。** 在 **執行** ] 對話方塊中，輸入 **mobsync.exe** 中 **開啟** 欄位，，然後按一下 **確定**。  
  
2.  在 **要同步處理的項目** 對話方塊方塊中，選取要同步處理訂閱。 訂閱會列在電腦上安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之下。  
  
3.  按一下 [ **同步處理**。  
  
### 若要使用 Synchronization Manager 重新初始化提取訂閱  
  
1.  在 **要同步處理的項目** 對話方塊中，選取訂閱，然後按一下 **屬性**。  
  
2.  在 **SQL Server 訂閱屬性** 對話方塊中，按一下 [ **重新初始化訂閱**。  
  
3.  按一下 **[是]**。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     下次同步處理訂閱時，依預設，訂閱資料庫會套用一個新的快照集。 如需詳細資訊，請參閱 [重新初始化訂閱](../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
> [!NOTE]  
>  合併式複寫允許在套用快照集前，將尚未處理完畢的變更上傳到「發行者」，但是此選項在 Synchronization Manager 中不可用。 若要上傳變更，請在重新初始化訂閱前，對其執行同步處理。  
  
### 若要在 Synchronization Manager 中設定提取訂閱的屬性  
  
1.  在 **要同步處理的項目** 對話方塊中，選取訂閱，然後按一下 **屬性**。  
  
2.  在下列索引標籤中檢視並修改屬性：  
  
    -   **識別**  
  
    -   **訂閱者登入**, ，**散發者登入**, ，和 **發行者登入** （適用於僅限合併式複寫）  
  
    -   **Web 伺服器資訊** （針對合併訂閱在訂閱者端執行 SQL Server 2005 或更新版本）  
  
    -   **其他**  
  
     建議對所有連接使用「Windows 驗證」。 散發代理程式 」 和 「 合併代理程式所需的權限的相關資訊，請參閱 [複寫代理程式安全性模型](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### 若要從 Synchronization Manager 中移除提取訂閱  
  
1.  在 **要同步處理的項目** 對話方塊中，選取訂閱，然後按一下 **屬性**。  
  
2.  在 **SQL Server 訂閱屬性** 對話方塊中，按一下 [ **移除訂閱**。  
  
3.  選取一個選項，在 **移除訂閱** 對話方塊。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### 若要使用互動解決器  
  
1.  啟用發行項和訂閱以使用互動式解決方案。 如需詳細資訊，請參閱 [合併發行項指定互動式衝突解決](../../relational-databases/replication/publish/specify-interactive-conflict-resolution-for-merge-articles.md)。  
  
2.  在 Synchronization Manager 中開始同步處理訂閱之後，如果啟用了互動式衝突解決方案，且一個或多個發行項有衝突，則「互動解決器」會自動啟動。 「互動解決器」每次顯示一個衝突，並為每個衝突提供一個建議的解決方案 (視建立發行集和訂閱時指定的解決器而定)。  
  
3.  選擇性地編輯任何在「互動解決器」中顯示的資料行，然後按下列其中一個按鈕，以解決衝突：  
  
    -   **[接受建議]**  
  
    -   **[接受發行者]**  
  
    -   **[接受訂閱者]**  
  
    -   **自動解決所有** （目前所有的衝突會解析不需要進一步的輸入）  
  
     選取的資料列然後會被套用到「發行者」和 (或)「訂閱者」；在後續同步處理期間，它會傳播到其他節點。  
  
> [!NOTE]  
>  僅當編輯為針對解決方案所選取之資料列的一部分時，才會被套用。 例如，如果您進行下的編輯 **發行者**, ，然後按一下 [ **接受訂閱者**, ，編輯會被捨棄。  
  
## 另請參閱  
 [互動式衝突解決](../../relational-databases/replication/merge/interactive-conflict-resolution.md)  
  
  