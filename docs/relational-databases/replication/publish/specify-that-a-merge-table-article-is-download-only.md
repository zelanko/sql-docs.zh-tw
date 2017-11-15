---
title: "將合併資料表發行項指定為僅限下載 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication [SQL Server replication], download-only articles
- articles [SQL Server replication], download-only
- download-only articles
ms.assetid: 14839cec-6dbf-49c2-aa27-56847b09b4db
caps.latest.revision: "40"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 320951b05137a9e17fc6961504df77ff8a024913
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="specify-that-a-merge-table-article-is-download-only"></a>將合併資料表發行項指定為僅限下載
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 指定合併資料表發行項在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中僅限下載。 僅限下載發行項的設計是要供包含未在訂閱者上更新之資料的應用程式使用。 如需詳細資訊，請參閱[使用僅限下載的發行項最佳化合併式複寫效能](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
-   **若要將合併資料表發行項指定為僅限下載，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   如果您在初始化訂閱之後指定發行項僅限下載，則所有收到該發行項的客訂閱都必須重新初始化。 主訂閱則不需要重新初始化。 如需屬性變更效果的詳細資訊，請參閱[變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在 [新增發行集精靈] 的 [發行項] 頁面，或 [發行項屬性 - \<發行項>] 對話方塊的 [屬性] 索引標籤上指定發行項僅限下載。 [新增發行集精靈] 與 [發行集屬性 - \<發行集>] 對話方塊中都有提供此對話方塊。 如需使用精靈和存取對話方塊的詳細資訊，請參閱[建立發行集](../../../relational-databases/replication/publish/create-a-publication.md)和[檢視及修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### <a name="to-specify-that-an-article-is-download-only-on-the-articles-page"></a>在發行項頁面上指定發行項僅限下載  
  
-   在「新增發行集精靈」的 **[發行項]** 頁面上選取資料表，然後選取 **[反白的資料表僅限下載]**。  
  
#### <a name="to-specify-that-an-article-is-download-only-on-the-properties-tab-of-the-article-properties---article-dialog-box"></a>在發行項屬性 - \<發行項> 對話方塊的屬性索引標籤上指定發行項僅限下載  
  
1.  在 [新增發行集精靈] 的 [發行項] 頁面上，或是在 [發行集屬性 - \<發行集>] 對話方塊中，選取一個資料表，然後按一下 [發行項屬性]。  
  
2.  按一下 **[設定反白顯示資料表發行項的屬性]** 或 **[設定所有資料表發行項的屬性]**。  
  
3.  在 [發行項屬性 - \<發行項>] 對話方塊之 [屬性] 索引標籤的 [目的地物件] 區段中，指定 [同步處理方向] 的下列其中一個值：  
  
    -   **[下載至訂閱者，禁止訂閱者變更]**  
  
    -   **[下載至訂閱者，允許訂閱者變更]**  
  
4.  如果您在 [發行集屬性 - \<發行集>] 對話方塊中，請按一下 [確定] 儲存並關閉對話方塊。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-specify-that-a-new-merge-table-article-is-download-only"></a>將新的合併資料表發行項指定為僅限下載  
  
1.  執行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)，針對 **@subscriber_upload_options** 指定合併資料表發行項在 **1** 或 **@subscriber_upload_options**中僅限下載。 這些數字對應到下列行為：  
  
    -   **0** - 無限制 (預設值)。 在訂閱者端進行的變更會上傳到發行者  
  
    -   **1** - 允許在訂閱者端進行變更，但變更不會上傳到發行者。  
  
    -   **2** - 不允許在訂閱者端進行變更。  
  
        > [!NOTE]  
        >  如果發行項的來源資料表已經在另一個發行集發行，則兩個發行項的 **@subscriber_upload_options** 值必須相同。  
  
#### <a name="to-modify-an-existing-merge-table-article-to-be-download-only"></a>將現有的合併資料表發行項修改為僅限下載  
  
1.  若要判斷發行項是否為僅限下載，請執行 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)。 請記下結果集中發行項的 **upload_options** 值。  
  
2.  如果步驟 1 中傳回的值為 **0**，請執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)，針對 **@property** 指定 **@property**的值、針對 **@subscriber_upload_options** 指定 **@force_invalidate_snapshot** ＞和＜ **@force_reinit_subscription**的值，並針對 **@subscriber_upload_options** 指定合併資料表發行項在 **1** 指定 **@value**的值，該值會對應到以下行為：  
  
    -   **1** - 允許在訂閱者端進行變更，但變更不會上傳到發行者。  
  
    -   **2** - 不允許在訂閱者端進行變更。  
  
        > [!NOTE]  
        >  如果發行項的來源資料表已在另一個發行集中發行，則兩個發行項的僅限下載行為必須相同。  
  
## <a name="see-also"></a>另請參閱  
 [使用僅限下載的發行項最佳化合併式複寫效能](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)   
 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)   
 [檢視和修改發行項屬性](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
  
