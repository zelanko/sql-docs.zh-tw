---
title: "Specify the Conflict Tracking and Resolution Level for Merge Articles | Microsoft Docs"
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
  - "merge replication conflict resolution [SQL Server replication], levels"
  - "articles [SQL Server replication], conflict resolution"
  - "衝突解決 [SQL Server 複寫], 合併式複寫"
ms.assetid: 81e9ecb6-1d31-4a78-b32a-96f7f4d67077
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# Specify the Conflict Tracking and Resolution Level for Merge Articles
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中針對合併發行項指定衝突追蹤和解析層級。  
  
 如果同步處理合併式發行集的訂閱，複寫會檢查在發行者和訂閱者上，是否有對相同資料所做之變更所造成的衝突。 您可以指定要在資料列層級偵測衝突 (此時會將資料列的任何變更視為衝突)，或是在資料行層級偵測衝突 (此時只會將相同資料列和資料行的任何變更視為衝突)。 發行項的衝突解決會在資料列層級執行。 如需有關使用邏輯記錄時衝突偵測及解決的詳細資訊，請參閱＜ [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/detecting-and-resolving-conflicts-in-logical-records.md)＞。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
-   **若要指定合併發行項的衝突追蹤與解析層級，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   如果您在訂閱初始化之後要修改追蹤層級，則這些訂閱必須重新初始化。 屬性變更的效果相關資訊，請參閱 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
-   若使用資料列層級追蹤和資料行層級追蹤，則衝突解決始終在資料列層級執行：優先資料列會覆寫失敗資料列。 合併式複寫還允許您指定在邏輯記錄層級追蹤並解決衝突，但是 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中並未提供這些選項。 如需這些設定複寫預存程序之選項的詳細資訊，請參閱＜ [Define a Logical Record Relationship Between Merge Table Articles](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)＞。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 指定資料列或資料行層級追蹤針對合併發行項上 **屬性** ] 索引標籤的 **發行項屬性** 對話方塊中，也就是在新增發行集精靈和 **發行集屬性-\< 發行集>** 對話方塊。 如需使用精靈，並存取此對話方塊的詳細資訊，請參閱 [建立發行集](../../../relational-databases/replication/publish/create-a-publication.md) 和 [檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 若要指定資料列層級追蹤或資料行層級追蹤  
  
1.  在 **文章** 新的發行集精靈] 頁面或 **發行集屬性-\< 發行集>** 對話方塊中，選取的資料表。  
  
2.  按一下 **[發行項屬性]**，然後按一下 **[設定反白顯示資料表發行項的屬性]** 或 **[設定所有資料表發行項的屬性]**。  
  
3.  在 **屬性** ] 索引標籤的 **發行項屬性 \< 文章>** 對話方塊中，選取下列其中一個值 **追蹤層級** 屬性︰ **資料列層級追蹤** 或 **資料行層級追蹤**。  
  
4.  如果您是在 **發行集屬性-\< 發行集>** 對話方塊中，按一下 [ **確定** 儲存並關閉對話方塊。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 為新的合併發行項指定衝突追蹤選項  
  
1.  在發行集資料庫的發行者，執行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) ，並指定下列值的其中一個 **@column_tracking**:  
  
    -   **true** -發行項中使用資料行層級追蹤。  
  
    -   **false** -使用資料列層級追蹤，這是預設值。  
  
#### 為合併發行項變更衝突追蹤選項  
  
1.  若要判斷衝突追蹤選項為合併發行項，執行 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)。 記下的值 **column_tracking** 的結果集之發行項中的選項。 值為 **1** 方法，正在使用資料行層級追蹤，而值為 **0** 表示使用的資料列層級追蹤。  
  
2.  在發行集資料庫的發行者，執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 指定的值為 **column_tracking** 的 **@property** 和下列其中一個值 **@value**:  
  
    -   **true** -發行項中使用資料行層級追蹤。  
  
    -   **false** -使用資料列層級追蹤，這是預設值。  
  
     指定的值為 **1** 兩者 **@force_invalidate_snapshot** 和 **@force_reinit_subscription**。  
  
## 另請參閱  
 [進階合併式複寫衝突偵測與解決](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [偵測和解決邏輯記錄中的衝突](../../../relational-databases/replication/merge/detecting-and-resolving-conflicts-in-logical-records.md)   
 [定義合併資料表發行項之間的邏輯記錄關聯性](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)   
 [偵測及解決合併式複寫衝突](../../../relational-databases/replication/merge/detect-and-resolve-merge-replication-conflicts.md)  
  
  