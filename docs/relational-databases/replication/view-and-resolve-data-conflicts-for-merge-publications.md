---
title: 檢視並解決資料衝突 (合併式)
description: 了解如何檢視並解決 SQL Server 合併式發行集的資料衝突。
ms.custom: seo-lt-2019
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], viewing conflicts
- viewing conflict information
- conflict resolution [SQL Server replication], merge replication
ms.assetid: aeee9546-4480-49f9-8b1e-c71da1f056c7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 79dc4b26ee543aa99b9fc90e29f7bb6c7d571555
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "75321885"
---
# <a name="conflict-resolution-for-merge-replication"></a>解決合併式複寫的衝突
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  合併式複寫中的衝突根據為每個發行項指定的解決器進行解決。 依預設，衝突的解決不需要使用者的介入。 但是可以在「 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 複寫衝突檢視器」(Replication Conflict Viewer) 中檢視衝突並變更解決的結果。  
  
 複寫衝突檢視器可以在衝突保留期限指定的時間內使用衝突資料 (預設為 14 天)。 若要設定衝突保留期限，可以：  

-   針對 [**sp_addmergepublication &#40;Transact-SQL&#41;**](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 的 `@conflict_retention` 參數指定保留值。
  
- 針對 `@property` 參數指定 **conflict_retention** 值，並為 [**sp_changemergepublication &#40;Transact-SQL&#41;**](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) 的 `@value` 參數指定保留值。
  
 依預設，會儲存衝突資訊：    
-   如果發行集相容性層級為 90RTM 或更高，則是在「發行者」與「訂閱者」端。   
-   如果發行集相容性層級低於 80RTM，則是在發行者端。   
-   如果「訂閱者」執行 [!INCLUDE[ssEW](../../includes/ssew-md.md)]，則會儲存在「發行者」端。 衝突資料無法儲存在 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 訂閱者上。  
  
 衝突資訊的儲存由 **conflict_logging** 發行集屬性控制。 如需詳細資訊，請參閱 [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 和 [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)。  
  
 衝突也可以使用「 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 互動式解決器」在同步處理期間以互動的方式解決。 互動解決器可以從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Synchronization Manager 使用。 如需詳細資訊，請參閱[使用 Windows Synchronization Manager 同步處理訂閱 &#40;Windows Synchronization Manager&#41;](../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md)。  
  
## <a name="resolve-conflicts"></a>解決衝突  
  
1.  連線至 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的「發行者」(或「訂閱者」，如果適用)，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  以滑鼠右鍵按一下您要檢視衝突的發行集，然後按一下 **[檢視衝突]** 。  
  
    > [!NOTE]  
    >  如果將 **conflict_logging** 屬性的值指定為 **'subscriber'** ，就無法使用 **[檢視衝突]** 功能表選項。 若要檢視衝突，請從命令提示字元啟動 ConflictViewer.exe。 依預設，ConflictViewer.exe 位於下列目錄：Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE。 如需有效的啟動參數清單，請執行 ConflictViewer.exe -?。  
  
4.  在 **[選取衝突資料表]** 對話方塊中，選取要檢視衝突的資料庫、發行集和資料表。  
  
5.  在複寫衝突檢視器中，您可以：  
  
    -   使用上方格右側按鈕篩選資料列。  
  
    -   在上方格內選取資料列，以便於下方格的該資料列顯示資訊。  
  
    -   在上方方格中選取一個或多個資料列，然後按一下 **[移除]** ，這相當於按一下 **[提交成功者]** 按鈕 (不會對資料進行任何變更)。  
  
    -   按一下屬性按鈕 ([...]  ) 以檢視更多有關於衝突的資料行資訊。  
  
    -   在提交資料之前，編輯 **[衝突成功者]** 或 **[衝突失敗者]** 資料行中的資料 (灰色資料行表示資料為唯讀)。  
  
    -   按一下 **[提交成功者]** 以接受指定為衝突成功者的資料列。  
  
    -   按一下 **[提交失敗者]** ，以覆寫解決並將指定為衝突失敗者的值傳播到拓撲中的所有節點。  
  
    -   選取 **[記錄此衝突的詳細資料]** 即可將衝突資料記錄到檔案中。 若要指定檔案的位置，請指向 **[檢視]** 功能表，然後按一下 **[選項]** 。 輸入值，或按一下瀏覽按鈕 ( **[...]** )，然後導覽至適當的檔案。 按一下 **[確定]** 即可結束 **[選項]** 對話方塊。  
  
6.  關閉複寫衝突檢視器。  

## <a name="view-conflict-information"></a>檢視衝突資訊
在合併式複寫中解決衝突時，遺失之資料列的資料會寫入衝突資料表。 可以使用複寫預存程序來以程式設計的方式檢視此衝突資料。 如需詳細資訊，請參閱 [進階合併式複寫衝突偵測與解決](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)。  
  
1.  在發行集資料庫的發行者上，執行 [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)。 請注意結果集中下列資料行的值：  
  
    -   **centralized_conflicts** - 1 表示在發行者上儲存衝突資料列，0 則表示不會在發行者上儲存衝突資料列。  
  
    -   **decentralized_conflicts** - 1 表示在訂閱者上儲存衝突資料列，0 則表示不會在訂閱者上儲存衝突資料列。  
  
        > [!NOTE]  
        >  合併式發行集之衝突記錄行為是使用 `@conflict_logging`sp_addmergepublication[ 的 ](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 參數來設定。 已淘汰使用 `@centralized_conflicts` 參數。  
  
     下表描述這些資料行的值 (根據針對 `@conflict_logging` 所指定的值)。  
  
    |@conflict_logging 值|centralized_conflicts|decentralized_conflicts|  
    |------------------------------|----------------------------|------------------------------|  
    |**publisher**|1|0|  
    |**訂閱者**|0|1|  
    |**兩者**|1|1|  
  
2.  在發行集資料庫的發行者上或是在訂閱資料庫的訂閱者上，執行 [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md)。 針對 `@publication` 指定值，只傳回屬於特定發行集的發行項衝突資訊。 這樣會傳回有衝突之發行項的衝突資料表資訊。 請記下感興趣之任何發行項的 **conflict_table** 值。 如果發行項的 **conflict_table** 值為 NULL，只要刪除此發行項中已發生的衝突。  
  
3.  (選擇性) 檢閱感興趣之發行項的衝突資料列。 根據步驟 1 中 **centralized_conflicts** 和 **decentralized_conflicts** 的值而定，執行下列其中一項：  
  
    -   在發行集資料庫的發行者上，執行 [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md)。 針對 `@conflict_table` 指定發行項的衝突資料表 (來自步驟 1)。 (選擇性) 指定 `@publication` 的值，將傳回的衝突資訊限制為特定發行集。 這樣會傳回遺失之資料列的資料列資料和其他資訊。  
  
    -   在訂閱資料庫的訂閱者上，執行 [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md)。 針對 `@conflict_table` 指定發行項的衝突資料表 (來自步驟 1)。 這樣會傳回遺失之資料列的資料列資料和其他資訊。  
  
## <a name="conflict-where-delete-failed"></a>發生刪除失敗的衝突   
  
1.  在發行集資料庫的發行者上，執行 [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)。 請注意結果集中下列資料行的值：  
  
    -   **centralized_conflicts** - 1 表示在發行者上儲存衝突資料列，0 則表示不會在發行者上儲存衝突資料列。  
  
    -   **decentralized_conflicts** - 1 表示在訂閱者上儲存衝突資料列，0 則表示不會在訂閱者上儲存衝突資料列。  
  
        > [!NOTE]  
        >  合併式發行集之衝突記錄行為是使用 `@conflict_logging`sp_addmergepublication[ 的 ](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 參數來設定。 已淘汰使用 `@centralized_conflicts` 參數。  
  
2.  在發行集資料庫的發行者上或是在訂閱資料庫的訂閱者上，執行 [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md)。 針對 `@publication` 指定值，只傳回屬於特定發行集的發行項衝突資料表資訊。 這樣會傳回有衝突之發行項的衝突資料表資訊。 請記下感興趣之任何發行項的 **source_object** 值。 如果發行項的 **conflict_table** 值為 NULL，只要刪除此發行項中已發生的衝突。  
  
3.  (選擇性) 檢閱刪除衝突的衝突資訊。 根據步驟 1 中 **centralized_conflicts** 和 **decentralized_conflicts** 的值而定，執行下列其中一項：  
  
    -   在發行集資料庫的發行者上，執行 [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md)。 針對 `@source_object` 指定衝突發生所在的來源資料表名稱 (來自步驟 1)。 (選擇性) 指定 `@publication` 的值，將傳回的衝突資訊限制為特定發行集。 這樣會傳回儲存在發行者上的刪除衝突資訊。  
  
    -   在訂閱資料庫的訂閱者上，執行 [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md)。 針對 `@source_object` 指定衝突發生所在的來源資料表名稱 (來自步驟 1)。 (選擇性) 指定 `@publication` 的值，將傳回的衝突資訊限制為特定發行集。 這樣會傳回儲存在訂閱者上的刪除衝突資訊。  
  
## <a name="see-also"></a>另請參閱  
 [進階合併式複寫衝突偵測與解決](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [指定合併發行項解析程式](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
  
