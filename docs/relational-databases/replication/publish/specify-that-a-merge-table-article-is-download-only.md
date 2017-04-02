---
title: "將合併資料表發行項指定為僅限下載 | Microsoft Docs"
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
  - "合併式複寫 [SQL Server 複寫], 僅限下載發行項"
  - "發行項 [SQL Server 複寫], 僅限下載"
  - "僅限下載的發行項"
ms.assetid: 14839cec-6dbf-49c2-aa27-56847b09b4db
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# 將合併資料表發行項指定為僅限下載
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 指定合併資料表發行項在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中僅限下載。 僅限下載發行項的設計是要供包含未在訂閱者上更新之資料的應用程式使用。 如需詳細資訊，請參閱 [最佳化合併式複寫效能的 「 文章](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
-   **若要將合併資料表發行項指定為僅限下載，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   如果您在初始化訂閱之後指定發行項僅限下載，則所有收到該發行項的客訂閱都必須重新初始化。 主訂閱則不需要重新初始化。 多個效果屬性變更的詳細資訊，請參閱 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 指定發行項僅限下載的上 **文章** 新增發行集精靈 」 頁面或 **屬性** ] 索引標籤的 **發行項屬性-\< 發行項>** 對話方塊。 此對話方塊，請在新增發行集精靈和 **發行集屬性-\< 發行集>** 對話方塊。 如需使用精靈，並存取此對話方塊的詳細資訊，請參閱 [建立發行集](../../../relational-databases/replication/publish/create-a-publication.md) 和 [檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 在發行項頁面上指定發行項僅限下載  
  
-   在 **文章** 頁面的 [選取資料表，新的發行集精靈 」，然後選取核取方塊 **白的資料表僅限下載**。  
  
#### 若要指定發行項僅限下載的發行項屬性-[屬性] 索引標籤上 \< 文章> 對話方塊  
  
1.  在 **文章** 新增發行集精靈 」 頁面或 **發行集屬性-\< 發行集>** 對話方塊中，選取資料表，然後按一下 **發行項屬性**。  
  
2.  按一下 **[設定反白顯示資料表發行項的屬性]** 或 **[設定所有資料表發行項的屬性]**。  
  
3.  在 **目的地物件** 區段 **屬性** ] 索引標籤的 **發行項屬性-\< 發行項>** 對話方塊方塊中，指定下列值的其中一個 **同步處理方向**:  
  
    -   **[下載至訂閱者，禁止訂閱者變更]**  
  
    -   **[下載至訂閱者，允許訂閱者變更]**  
  
4.  如果您是在 **發行集屬性-\< 發行集>** 對話方塊中，按一下 [ **確定** 儲存並關閉對話方塊。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 將新的合併資料表發行項指定為僅限下載  
  
1.  執行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), ，指定的值為 **1** 或 **2** 參數 **@subscriber_upload_options**。 這些數字對應到下列行為：  
  
    -   **0** -沒有限制 （預設值）。 在訂閱者端進行的變更會上傳到發行者  
  
    -   **1** -允許在 「 訂閱者 」 進行變更，但不是會上載到 「 發行者 」。  
  
    -   **2** -不允許訂閱者端進行變更。  
  
        > [!NOTE]  
        >  如果發行項的來源資料表已在另一個發行集的值 **@subscriber_upload_options** 必須是兩個發行項相同。  
  
#### 將現有的合併資料表發行項修改為僅限下載  
  
1.  若要判斷是否僅限下載的發行項，請執行 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)。 記下的值 **upload_options** 發行項的結果集。  
  
2.  步驟 1 中傳回的值如果是 **0**, ，執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), ，指定的值為 **subscriber_upload_options** 的 **@property**, ，值為 **1** 的 **@force_invalidate_snapshot** 和 **@force_reinit_subscription**, ，且值為 **1** 或 **2** 的 **@value**, ，對應至下列行為︰  
  
    -   **1** -允許在 「 訂閱者 」 進行變更，但不是會上載到 「 發行者 」。  
  
    -   **2** -不允許訂閱者端進行變更。  
  
        > [!NOTE]  
        >  如果發行項的來源資料表已在另一個發行集中發行，則兩個發行項的僅限下載行為必須相同。  
  
## 另請參閱  
 [使用僅限下載的發行項最佳化合併式複寫效能](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)   
 [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)   
 [檢視和修改發行項屬性](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
  