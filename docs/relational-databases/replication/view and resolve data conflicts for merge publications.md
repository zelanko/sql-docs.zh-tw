---
title: "檢視並解決合併式發行集的資料衝突 (SQL Server Management Studio) | Microsoft Docs"
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
  - "合併式複寫衝突解決 [SQL Server 複寫], 檢視衝突"
  - "檢視衝突資訊"
  - "衝突解決 [SQL Server 複寫], 合併式複寫"
ms.assetid: aeee9546-4480-49f9-8b1e-c71da1f056c7
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 檢視並解決合併式發行集的資料衝突 (SQL Server Management Studio)
  合併式複寫中的衝突根據為每個發行項指定的解決器進行解決。 依預設，衝突的解決不需要使用者的介入。 但是可以在「[!INCLUDE[msCoName](../../includes/msconame-md.md)] 複寫衝突檢視器」(Replication Conflict Viewer) 中檢視衝突並變更解決的結果。  
  
 複寫衝突檢視器可以在衝突保留期限指定的時間內使用衝突資料 (預設為 14 天)。 若要設定衝突保留期限，可以：  
  
-   指定的保留值 **@conflict_retention** 參數 [sp_addmergepublication & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。  
  
-   指定的值為 **conflict_retention** 的 **@property** 參數和保留值 **@value** 參數 [sp_changemergepublication & #40;TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)。  
  
 依預設，會儲存衝突資訊：  
  
-   如果發行集相容性層級為 90RTM 或更高，則是在「發行者」與「訂閱者」端。  
  
-   如果發行集相容性層級低於 80RTM，則是在發行者端。  
  
-   如果「訂閱者」執行 [!INCLUDE[ssEW](../../includes/ssew-md.md)]，則會儲存在「發行者」端。 衝突資料無法儲存在 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 訂閱者上。  
  
 儲存體的衝突資訊會受到 **conflict_logging** 發行集屬性。 如需詳細資訊，請參閱 [sp_addmergepublication & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 和 [sp_changemergepublication & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)。  
  
 衝突也可以使用「[!INCLUDE[msCoName](../../includes/msconame-md.md)] 互動式解決器」在同步處理期間以互動的方式解決。 互動解決器可以從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Synchronization Manager 使用。 如需詳細資訊，請參閱 [同步處理訂用帳戶使用 Windows Synchronization Manager & #40。Windows Synchronization Manager & #41;](../../relational-databases/replication/synchronize a subscription using windows synchronization manager.md)。  
  
### 若要檢視並解決合併式發行集衝突  
  
1.  連接到 「 發行者 」 （或訂閱者，如果適用的話） 中 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  以滑鼠右鍵按一下您要檢視衝突，然後再按一下發行的集 **檢視衝突**。  
  
    > [!NOTE]  
    >  如果您指定的值 **'subscriber'** 的 **conflict_logging** 屬性， **檢視衝突** 就無法使用功能表選項。 若要檢視衝突，請從命令提示字元啟動 ConflictViewer.exe。 依預設，ConflictViewer.exe 位於下列目錄：Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE。 如需有效的啟動參數清單，請執行 ConflictViewer.exe -?。  
  
4.  在 **選取衝突資料表** 對話方塊中，選取 [發行集資料庫和資料表用來檢視衝突。  
  
5.  在複寫衝突檢視器中，您可以：  
  
    -   使用上方格右側按鈕篩選資料列。  
  
    -   在上方格內選取資料列，以便於下方格的該資料列顯示資訊。  
  
    -   在上方方格中，選取一或多個資料列，然後按一下 **移除**, ，相當於按一下 **提交成功者** 按鈕 （不會對資料進行任何變更）。  
  
    -   按一下屬性按鈕 (**...**) 的資料行上檢視詳細資訊有關於衝突。  
  
    -   編輯中的資料 **衝突成功者** 或 **衝突失敗者** 提交的資料 （資料是唯讀的資料行是灰色） 之前的資料行。  
  
    -   按一下 [ **提交成功者** 接受指定為衝突成功者的資料列。  
  
    -   按一下 [ **提交失敗者** 覆寫解決方法，並指定為的拓樸中的所有節點衝突失敗者的值傳播。  
  
    -   選取 **記錄這個衝突的詳細資料** 衝突資料記錄到檔案。 若要指定檔案的位置，請指向 **檢視** 功能表，然後再按一下 **選項**。 輸入值，或按一下 [瀏覽按鈕 (**...**)，然後瀏覽至適當的檔案。 按一下 **[確定]** 即可結束 **[選項]** 對話方塊。  
  
6.  關閉複寫衝突檢視器。  
  
## 另請參閱  
 [進階合併式複寫衝突偵測與解決](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [指定合併發行項解析程式](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
  