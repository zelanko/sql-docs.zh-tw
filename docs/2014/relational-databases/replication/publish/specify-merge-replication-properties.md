---
title: 指定合併式複寫屬性 |Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], about merge replication
- merge replication [SQL Server replication]
ms.assetid: ff87c368-4c00-4e48-809d-ea752839551e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 033999701141387ee63712a8a9ce055ad3f55cb1
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79289526"
---
# <a name="specify-merge-replication-properties"></a>指定合併式複寫屬性
本主題說明如何為合併式複寫指定各種屬性。 


## <a name="download-only"></a>僅限下載
  本節描述如何使用[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]或[!INCLUDE[tsql](../../../includes/tsql-md.md)]，在中指定合併資料表發行項僅限下載。 僅限下載發行項的設計是要供包含未在訂閱者上更新之資料的應用程式使用。 如需詳細資訊，請參閱[使用僅限下載的發行項最佳化合併式複寫效能](../merge/optimize-merge-replication-performance-with-download-only-articles.md)。  
 
  
###  <a name="limitations-and-restrictions"></a>限制事項  
  
-   如果您在初始化訂閱之後指定發行項僅限下載，則所有收到該發行項的客訂閱都必須重新初始化。 主訂閱則不需要重新初始化。 如需屬性變更效果的詳細資訊，請參閱[變更發行集與發行項屬性](change-publication-and-article-properties.md)。  
  
### <a name="using-sql-server-management-studio"></a>使用 SQL Server Management Studio  
 在 [新增發行集精靈] 的 [發行項]**** 頁面，或 [發行項屬性 - **發行項>]**** 對話方塊的 [屬性]\<** 索引標籤上指定發行項僅限下載。 [新增發行集精靈] 與 [發行集屬性 - **發行集>]\<** 對話方塊中都有提供此對話方塊。 如需使用精靈及存取對話方塊的詳細資訊，請參閱[建立發行集](../publish/create-a-publication.md)和[檢視及修改發行集屬性](../publish/view-and-modify-publication-properties.md)。  
  
#### <a name="to-specify-that-an-article-is-download-only-on-the-articles-page"></a>在發行項頁面上指定發行項僅限下載  
  
-   在「新增發行集精靈」的 **[發行項]** 頁面上選取資料表，然後選取 **[反白的資料表僅限下載]** 。 
  
#### <a name="to-specify-that-an-article-is-download-only-on-the-properties-tab-of-the-article-properties---article-dialog-box"></a>在發行項屬性 - \<發行項> 對話方塊的屬性索引標籤上指定發行項僅限下載  
  
1.  在 [新增發行集精靈] 的 [發行項]  頁面上，或是在 [發行集屬性 - **發行集>]\<** 對話方塊中，選取一個資料表，然後按一下 [發行項屬性]  。    
2.  按一下 **[設定反白顯示資料表發行項的屬性]** 或 **[設定所有資料表發行項的屬性]** 。    
3.  在 [發行項屬性 - **發行項>]** **對話方塊之 [屬性]** **索引標籤的 [目的地物件]\<** 區段中，指定 [同步處理方向]  的下列其中一個值：    
    -   **[下載至訂閱者，禁止訂閱者變更]**    
    -   **[下載至訂閱者，允許訂閱者變更]**  
  
4.  如果您在 [發行集屬性 - **發行集>]\<** 對話方塊中，請按一下 [確定]  以儲存並關閉對話方塊。    

###  <a name="using-transact-sql"></a>使用 TRANSACT-SQL  
  
#### <a name="to-specify-that-a-new-merge-table-article-is-download-only"></a>將新的合併資料表發行項指定為僅限下載    
1.  執行[sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)，為** \@** 參數指定**1**或**2**的值 subscriber_upload_options。 這些數字對應到下列行為：  
  
    -   **0** - 無限制 (預設值)。 在訂閱者端進行的變更會上傳到發行者    
    -   **1** - 允許在訂閱者端進行變更，但變更不會上傳到發行者。    
    -   **2** - 不允許在訂閱者端進行變更。  
  
        > [!NOTE]  
        >  如果發行項的來源資料表已經在另一個發行集中發行，則這兩篇文章的** \@subscriber_upload_options**值必須相同。  
  
#### <a name="to-modify-an-existing-merge-table-article-to-be-download-only"></a>將現有的合併資料表發行項修改為僅限下載  
  
1.  若要判斷發行項是否為僅限下載，請執行 [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql)。 請記下結果集中發行項的 **upload_options** 值。    
2.  如果步驟1中傳回的值為**0**，請[執行 sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)，為** \@屬性**指定**subscriber_upload_options**的值，針對** \@force_invalidate_snapshot**和** \@force_reinit_subscription**指定**1**的值，並針對** \@value**使用**1**或**2**的值，其對應于下列行為：  
  
    -   **1** - 允許在訂閱者端進行變更，但變更不會上傳到發行者。    
    -   **2** - 不允許在訂閱者端進行變更。  
  
        > [!NOTE]  
        >  如果發行項的來源資料表已在另一個發行集中發行，則兩個發行項的僅限下載行為必須相同。  
 
## <a name="interactive-conflict-resolution">互動式衝突解決</a>
[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]複寫提供互動式解析程式，可讓您在 Windows 同步處理管理員中[!INCLUDE[msCoName](../../../includes/msconame-md.md)]的視需要同步處理期間手動解決衝突。 在啟用互動式解決方案之後，在同步處理期間會使用「互動解決器」以互動方式解決衝突。 互動解決器可以從 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Synchronization Manager 使用。 如需詳細資訊，請參閱[使用 Windows Synchronization Manager 同步處理訂閱 &#40;Windows Synchronization Manager&#41;](../synchronize-a-subscription-using-windows-synchronization-manager.md)。  
  
    
###  <a name="Recommendations"></a> 建議  
  
-   如果是在 Windows Synchronization Manager 之外執行同步處理 (如 SQL Server Management Studio 或複寫監視器中已排程的同步處理或視需要同步處理)，則不需要使用者的介入，就會使用針對發行項指定的預設衝突解決方式來自動解決衝突。 如需詳細資訊，請參閱 [Interactive Conflict Resolution](../merge/advanced-merge-replication-conflict-interactive-resolution.md)。  
  
###  <a name="using-sql-server-management-studio"></a>使用 SQL Server Management Studio  
  
#### <a name="enable-interactive-conflict-resolution-for-an-article"></a>為發行項啟用互動式衝突解決  
  
1.  在 [新增發行集精靈] 的 [發行項]  頁面上，或是在 [發行集屬性 - **發行集>]\<** 對話方塊中，選取一個資料表。 如需使用精靈及存取對話方塊的詳細資訊，請參閱[建立發行集](create-a-publication.md)和[檢視及修改發行集屬性](view-and-modify-publication-properties.md)。    
2.  按一下 **[發行項屬性]** ，然後按一下 **[設定反白顯示資料表發行項的屬性]** 或 **[設定所有資料表發行項的屬性]** 。    
3.  在 [發行項屬性 - **發行項>]\<** 或 [發行項屬性 - **發行項類型>]\<** 頁面上，按一下 [解析程式]  索引標籤。    
4.  選取 **[允許訂閱者在依要求同步期間，以互動方式解決衝突]** 。    
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]    
6.  如果您在 [發行集屬性 - **發行集>]\<** 對話方塊中，請按一下 [確定]  以儲存並關閉對話方塊。  
  
#### <a name="to-specify-that-a-subscription-should-use-interactive-conflict-resolution"></a>若要指定訂閱應使用互動式衝突解決方案  
  
1.  在 [訂閱屬性 - **訂閱者>: \<訂閱資料庫>]\<** 對話方塊方塊中，將 [以互動方式解決衝突]  選項的值指定為 **True**。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Push Subscription Properties](../view-and-modify-push-subscription-properties.md) ＞與＜ [View and Modify Pull Subscription Properties](../view-and-modify-pull-subscription-properties.md)＞。 
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="using-transact-sql"></a>使用 TRANSACT-SQL  
 您可以透過程式設計方式指定在建立合併式發行集的提取訂閱時，訂閱者將使用此圖形化介面來解決發行項衝突。 只有支援此選項之發行項中的衝突才會顯示在互動式解決器中。  
  
#### <a name="create-a-merge-pull-subscription-that-uses-the-interactive-resolver"></a>建立使用互動解析程式的合併提取訂閱  
  
1.  在發行集資料庫的發行者上，執行[sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql)，並指定** \@發行**集。 請記下結果集中每一個發行項的 **allow_interactive_resolver** 值 (互動式解決器將針對它來使用)。    
    -   如果這個值是 **1**，將會使用互動式解決器。    
    -   如果這個值是 **0**，您必須先針對每一個發行項啟用互動式解決器。 若要執行這項操作，請執行[sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)、指定** \@發行** ** \@集、發行項、** ** \@屬性**的**allow_interactive_resolver**值，以及** \@value**的**true**值。    
2.  在訂閱資料庫的訂閱者上，執行 [sp_addmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql)。 如需詳細資訊，請參閱 [建立提取訂閱](../create-a-pull-subscription.md)。    
3.  在訂閱資料庫的訂閱者上，執行 [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)並指定下列參數：  
  
    -   發行者、 ** \@publisher_db** （發行的資料庫）和** \@發行**集。 ** \@ **    
    -   Enabled_for_syncmgr 的**true**值。 ** \@ **    
    -   Use_interactive_resolver 的**true**值。 ** \@ **    
    -   合併代理程式所需的安全性帳戶資訊。 如需詳細資訊，請參閱 [建立提取訂閱](../create-a-pull-subscription.md)。    
4.  在發行集資料庫的發行者上，執行 [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql)。  
  
#### <a name="define-an-article-that-supports-the-interactive-resolver"></a>定義支援互動解析程式的發行項  
  
在發行集資料庫的發行者上，執行 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)。 指定** \@發行項**所屬的發行集名稱、發行** \@項的名稱、用於** ** \@source_object**的資料庫物件，以及** \@allow_interactive_resolver**的**true**值。 如需詳細資訊，請參閱 [定義發行項](define-an-article.md)。  

## <a name="specify-the-conflict-tracking-and-resolution-level"></a>指定衝突追蹤和解決層級 
如果同步處理合併式發行集的訂閱，複寫會檢查在發行者和訂閱者上，是否有對相同資料所做之變更所造成的衝突。 您可以指定要在資料列層級偵測衝突 (此時會將資料列的任何變更視為衝突)，或是在資料行層級偵測衝突 (此時只會將相同資料列和資料行的任何變更視為衝突)。 發行項的衝突解決會在資料列層級執行。 如需有關使用邏輯記錄時衝突偵測及解決的詳細資訊，請參閱＜ [Detecting and Resolving Conflicts in Logical Records](../merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)＞。  
  

  
###  <a name="Restrictions"></a> 限制事項  
  
-   如果您在訂閱初始化之後要修改追蹤層級，則這些訂閱必須重新初始化。 如需屬性變更效果的詳細資訊，請參閱[變更發行集與發行項屬性](../publish/change-publication-and-article-properties.md)。    
-   若使用資料列層級追蹤和資料行層級追蹤，則衝突解決始終在資料列層級執行：優先資料列會覆寫失敗資料列。 合併式複寫還允許您指定在邏輯記錄層級追蹤並解決衝突，但是 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中並未提供這些選項。 如需這些設定複寫預存程序之選項的詳細資訊，請參閱＜ [定義合併資料表發行項之間的邏輯記錄關聯性](../publish/define-a-logical-record-relationship-between-merge-table-articles.md)＞。  
  
###  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在 [發行項屬性]  對話方塊的 [屬性]  索引標籤上，指定合併發行項的資料列層級追蹤或資料行層級追蹤，[新增發行集精靈] 和 [發行集屬性 - **發行集>]\<** 對話方塊皆提供此對話方塊。 如需使用精靈及存取對話方塊的詳細資訊，請參閱[建立發行集](create-a-publication.md)和[檢視及修改發行集屬性](../publish/view-and-modify-publication-properties.md)。  
  
#### <a name="specify-row--or-column-level-tracking"></a>指定資料列層級或資料行層級的追蹤  
  
1.  在 [新增發行集精靈] 的 [發行項]  頁面上，或是在 [發行集屬性 - **發行集>]\<** 對話方塊中，選取一個資料表。    
2.  按一下 **[發行項屬性]** ，然後按一下 **[設定反白顯示資料表發行項的屬性]** 或 **[設定所有資料表發行項的屬性]** 。   
3.  在 [發行項屬性 **發行項>]** **對話方塊的 [屬性]\<** 索引標籤上，針對 [追蹤層級]  屬性選取下列其中一個值：[資料列層級追蹤]  或 [資料行層級追蹤]  。    
4.  如果您在 [發行集屬性 - **發行集>]\<** 對話方塊中，請按一下 [確定]  以儲存並關閉對話方塊。  
  
###  <a name="using-transact-sql"></a>使用 TRANSACT-SQL  
  
#### <a name="specify-conflict-tracking-options-for-a-new-merge-article"></a>為新的合併發行項指定衝突追蹤選項  
  
1.  在發行集資料庫的發行者上，執行[sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) ，並為** \@column_tracking**指定下列其中一個值：  
  
    -   **true** - 針對發行項使用資料行層級追蹤。    
    -   **false** - 使用資料列層級追蹤，這是預設值。  
  
#### <a name="change-conflict-tracking-options-for-a-merge-article"></a>為合併發行項變更衝突追蹤選項  
  
1.  若要為合併發行項判斷衝突追蹤選項，請執行 [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql)。 請注意結果集中發行項的 **column_tracking** 選項值。 **1** 的值表示使用資料行層級追蹤， **0** 的值表示使用資料列層級追蹤。    
2.  在發行集資料庫的發行者上，執行 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)。 為 [ ** \@屬性**] 指定 [ **column_tracking** ] 的值，並為** \@[值**] 指定下列其中一個值：
    -   **true** - 針對發行項使用資料行層級追蹤。
    -   **false** - 使用資料列層級追蹤，這是預設值。  
  
     請為** \@force_invalidate_snapshot**和** \@force_reinit_subscription**指定**1**的值。  

## <a name="tracking-deletes"></a>追蹤刪除

> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 依預設，合併式複寫會同步處理發行者與散發者之間的 DELETE 命令。 合併式複寫可讓您保留訂閱資料庫中的資料列，即時已從發行集中刪除資料列 (反之亦然)。 您可透過程式設計方式指定在建立新的發行項時要忽略 DELETE 命令，或是可以在稍後使用複寫預存程序來啟用這項功能。  
  
> [!IMPORTANT]  
>  啟用這項功能將會導致非聚合的情況，這表示訂閱者上的資料將不會正確反映發行者上的資料。 您必須實作自己的機制，以手動移除刪除的資料列。  
  
### <a name="specify-that-deletes-be-ignored-for-a-new-merge-article"></a>指定針對新的合併發行項忽略刪除  
  
1.  在發行集資料庫的發行者端，執行 [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)。 針對 [delete_tracking] 指定的值。 ** \@ ** `false` 如需詳細資訊，請參閱 [定義發行項](../publish/define-an-article.md)。  
  
    > [!NOTE]  
    >  如果發行項的來源資料表已在另一個發行集中發行，則兩個發行項的 **delete_tracking** 值必須相同。  
  
### <a name="specify-that-deletes-be-ignored-for-an-existing-merge-article"></a>指定針對現有的合併發行項忽略刪除  
  
1.  若要判斷是否已針對發行項啟用錯誤補償，請執行 [sp_helpmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql)，並記下結果集中的 **delete_tracking** 值。 如果這個值是 **0**，就表示已經忽略刪除。    
2.  如果步驟 1 的值是 **1**，請在發行集資料庫的發行者端執行 [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)。 為 [ ** \@屬性**] 指定 [ **delete_tracking** ] 的值，並`false`為** \@[值**] 指定值。  
  
    > [!NOTE]  
    >  如果發行項的來源資料表已在另一個發行集中發行，則兩個發行項的 **delete_tracking** 值必須相同。  
  
## <a name="processing-order"></a>處理順序
  合併式複寫可讓您指定在同步處理期間，合併代理程式處理發行項的順序。 當您使用複寫預存程序建立發行項時，可以透過程式設計方式對每一個發行項指派順序。 發行項會依照從最低值到最高值的順序來處理。 如果兩個發行項有相同的值，就會同時處理它們。 如需詳細資訊，請參閱[指定合併式複寫屬性](../publish/specify-merge-replication-properties.md)。  

  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]從開始，可以覆寫合併式發行集之發行項處理的預設順序。 這非常有用，例如，如果您透過觸發程序定義參考完整性，並且那些觸發程序必須以特定順序引發。 

### <a name="how-processing-order-is-determined"></a>如何確定處理順序  
 在合併同步處理期間，依預設，發行項將按物件間相依性所需的順序處理，包括在基底資料表上定義的宣告式參考完整性 (DRI) 條件約束。 處理包括列舉對資料表所作的變更，然後套用這些變更。 如果沒有 DRI，但資料表發行項之間存在聯結篩選或邏輯記錄，發行項將以篩選和邏輯記錄所需的順序處理。 透過 DRI、聯結篩選、邏輯記錄或其他相依性與任何其他發行項無關的發行項，按照 [sysmergearticles &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/sysmergearticles-transact-sql) 系統資料表中的發行項暱稱處理。  
  
 假設發行集包含在 **SalesOrderHeader** 資料表中含主索引鍵資料行 **SalesOrderID** ，並且在 **SalesOrderDetail** 資料表中含相應外部索引鍵資料行 **SalesOrderID** 的資料表 **SalesOrderHeader** 與 **SalesOrderDetail** 。 在同步處理期間，合併式複寫透過在 **SalesOrderDetail** 中插入相關資料列之前於 **SalesOrderHeader**中插入任何新資料列，以防止外部索引鍵違規。 同樣地，在從 **SalesOrderHeader** 中刪除關聯資料列之前，可從 **SalesOrderDetail**決定中刪除資料列。  
  
 但是，在某些應用程式中，參照完整性透過資料庫觸發程序強化，或使用應用程式層級而不是透過 DRI 來強化。 以上所述的指定發行集 (而不是 DRI)， **SalesOrderDetail** 資料表具有插入觸發程序，可確保在允許插入前於 **SalesOrderHeader** 資料表中存在關聯資料列。 **SalesOrderHeader** 具有刪除觸發程序，可確保在允許刪除前於 **SalesOrderDetail** 中沒有關聯資料列。 合併式複寫在確定發行項處理順序時，不會考慮觸發程序，因為它無法在引發觸發程序前確定其結果。 同樣地，複寫不會考慮在應用程式層級上定義的條件約束。  
  
 當透過觸發程序或在應用程式層級上維護參考完整性時，您應該指定處理發行項的順序。 在使用觸發程序的範例中，您應該指定在處理 **SalesOrderDetail** 之前處理 **SalesOrderHeader**資料表，因為發行項排序是以插入順序為基礎的。 合併式複寫將自動反轉刪除順序。 沒有發行項排序，合併式複寫也不會失敗，因為如果條件約束出現違規，「合併代理程式」會繼續處理發行項；然後重試在處理其他發行項後失敗的任何作業。 只需指定發行項順序即可避免重試以及與其相關的其他處理。 如果您指定了錯誤順序 (例如，導致在標頭記錄前處理詳細記錄的順序)，合併式複寫將會重試處理，直到它成功。  

### <a name="new-article"></a>新文章
  
1.  在發行集資料庫的發行者端，執行 [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)。 指定一個整數值，代表** \@processing_order**發行項的處理順序。 如需詳細資訊，請參閱 [定義發行項](define-an-article.md)。  
  
    > [!NOTE]  
    >  當建立排序的發行項時，您應該在發行項順序值之間留一些間距。 這樣可讓您在將來更容易設定新的值。 例如，如果您有三個發行項需要指定固定的處理順序，請分別將** \@processing_order**的值設定為10、20和30，而不是1、2和3。  
  
### <a name="existing-article"></a>現有發行項
  
1.  若要決定發行項的處理順序，請執行 [sp_helpmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql)，並記下結果集中的 **processing_order** 值。  
  
2.  在發行集資料庫的發行者端，執行 [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)。 針對 [ ** \@屬性**] 指定 [ **processing_order** ] 的值，並針對 [ ** \@值**] 表示處理順序的整數值。  



## <a name="see-also"></a>另請參閱  
 [使用條件式刪除追蹤優化合併式複寫效能](../merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
 [偵測和解決邏輯記錄中的衝突](../merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)   
 [定義合併資料表發行項之間的邏輯記錄關聯性](define-a-logical-record-relationship-between-merge-table-articles.md)   
 [偵測及解決合併式複寫衝突](../merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [使用僅限下載的發行項最佳化合併式複寫效能](../merge/optimize-merge-replication-performance-with-download-only-articles.md)   
 [Define an Article](define-an-article.md)   
 [檢視和修改發行項屬性](view-and-modify-article-properties.md)  