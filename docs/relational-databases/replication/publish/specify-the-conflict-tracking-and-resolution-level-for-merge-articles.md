---
title: "指定合併發行項的衝突追蹤與解決方法層級 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], levels
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 81e9ecb6-1d31-4a78-b32a-96f7f4d67077
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 18b5650ce77b40deb101a16ebd1379600394dcbf
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="specify-the-conflict-tracking-and-resolution-level-for-merge-articles"></a>指定合併發行項的衝突追蹤與解決層級
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中針對合併發行項指定衝突追蹤和解析層級。  
  
 如果同步處理合併式發行集的訂閱，複寫會檢查在發行者和訂閱者上，是否有對相同資料所做之變更所造成的衝突。 您可以指定要在資料列層級偵測衝突 (此時會將資料列的任何變更視為衝突)，或是在資料行層級偵測衝突 (此時只會將相同資料列和資料行的任何變更視為衝突)。 發行項的衝突解決會在資料列層級執行。 如需有關使用邏輯記錄時衝突偵測及解決的詳細資訊，請參閱＜ [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)＞。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
-   **若要指定合併發行項的衝突追蹤與解析層級，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   如果您在訂閱初始化之後要修改追蹤層級，則這些訂閱必須重新初始化。 如需屬性變更效果的詳細資訊，請參閱[變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
-   若使用資料列層級追蹤和資料行層級追蹤，則衝突解決始終在資料列層級執行：優先資料列會覆寫失敗資料列。 合併式複寫還允許您指定在邏輯記錄層級追蹤並解決衝突，但是 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中並未提供這些選項。 如需這些設定複寫預存程序之選項的詳細資訊，請參閱＜ [Define a Logical Record Relationship Between Merge Table Articles](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)＞。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在 [發行項屬性] 對話方塊的 [屬性] 索引標籤上，指定合併發行項的資料列層級追蹤或資料行層級追蹤，[新增發行集精靈] 和 [發行集屬性 - \<發行集>] 對話方塊皆提供此對話方塊。 如需使用精靈和存取對話方塊的詳細資訊，請參閱[建立發行集](../../../relational-databases/replication/publish/create-a-publication.md)和[檢視及修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### <a name="to-specify-row--or-column-level-tracking"></a>若要指定資料列層級追蹤或資料行層級追蹤  
  
1.  在 [新增發行集精靈] 的 [發行項] 頁面上，或是在 [發行集屬性 - \<發行集>] 對話方塊中，選取一個資料表。  
  
2.  按一下 **[發行項屬性]**，然後按一下 **[設定反白顯示資料表發行項的屬性]** 或 **[設定所有資料表發行項的屬性]**。  
  
3.  在 [發行項屬性 \<發行項>] 對話方塊的 [屬性] 索引標籤上，針對 [追蹤層級] 屬性選取下列其中一個值：[資料列層級追蹤] 或 [資料行層級追蹤]。  
  
4.  如果您在 [發行集屬性 - \<發行集>] 對話方塊中，請按一下 [確定] 儲存並關閉對話方塊。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-specify-conflict-tracking-options-for-a-new-merge-article"></a>為新的合併發行項指定衝突追蹤選項  
  
1.  在發行集資料庫的發行者上，執行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) ，並為 **@column_tracking**指定下列其中一個值：  
  
    -   **true** - 針對發行項使用資料行層級追蹤。  
  
    -   **false** - 使用資料列層級追蹤，這是預設值。  
  
#### <a name="to-change-conflict-tracking-options-for-a-merge-article"></a>為合併發行項變更衝突追蹤選項  
  
1.  若要為合併發行項判斷衝突追蹤選項，請執行 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)。 請注意結果集中發行項的 **column_tracking** 選項值。 **1** 的值表示使用資料行層級追蹤， **0** 的值表示使用資料列層級追蹤。  
  
2.  在發行集資料庫的發行者上，執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 為 **column_tracking** 指定 **@property** 的值，並為 **@value**指定下列其中一個值：  
  
    -   **true** - 針對發行項使用資料行層級追蹤。  
  
    -   **false** - 使用資料列層級追蹤，這是預設值。  
  
     為 **1** 和 **@force_invalidate_snapshot** ＞和＜ **@force_reinit_subscription**中針對合併發行項指定衝突追蹤和解析層級。  
  
## <a name="see-also"></a>另請參閱  
 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)   
 [Define a Logical Record Relationship Between Merge Table Articles](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)   
 [偵測及解決合併式複寫衝突](../../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md)  
  
  
