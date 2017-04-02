---
title: "定義及修改資料行篩選 | Microsoft Docs"
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
  - "filters [SQL Server replication], column"
  - "modifying filters, column"
  - "modifying filters"
  - "資料行篩選 [SQL Server 複寫]"
ms.assetid: d7c3186a-9a8c-45d8-ab34-05beec4c26dd
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# 定義及修改資料行篩選
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中定義及修改資料行篩選。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
-   **若要定義及修改資料行篩選，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   某些資料行無法篩選。如需詳細資訊，請參閱 [篩選已發佈資料](../../../relational-databases/replication/publish/filter-published-data.md)。 如果您要在初始化訂閱後修改資料行篩選，則必須在進行變更後產生新的快照集並重新初始化所有訂閱。 如需屬性變更需求的詳細資訊，請參閱 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在「新增發行集精靈」的 **[發行項]** 頁面中定義資料行篩選。 如需有關使用 「 新增發行集精靈 」 的詳細資訊，請參閱 [建立發行集](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
 上定義及修改資料行篩選 **文章** 頁面 **發行集屬性-\< 發行集>** 對話方塊。 如需有關發行集與發行項屬性的詳細資訊，請參閱 [檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 若要定義資料行篩選  
  
1.  在「新增發行集精靈」的 **[發行項]** 頁面中，展開要在 **[發行的物件]** 窗格中篩選的資料表。  
  
2.  清除您要篩選之每個資料行旁邊的核取方塊。  
  
#### 若要修改資料行篩選  
  
1.  在 **文章** 頁面 **發行集屬性-\< 發行集>** 對話方塊方塊中，展開資料表，以篩選 **發行的物件** 窗格。  
  
2.  清除每個您要篩選之資料行旁邊的核取方塊，並確保為每個應包含在發行項中的資料行選取核取方塊。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 在建立資料表發行項時，您可以定義要將哪些資料行包含在發行項中，並在定義發行項之後變更資料行。 您可以使用複寫預存程序來以程式設計的方式建立及修改篩選的資料行。  
  
> [!NOTE]  
>  下列程序假設基礎資料表尚未變更。 複寫已發行之資料表的資料定義語言 (DDL) 變更的資訊，請參閱 [對發行集資料庫進行結構描述變更](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
#### 針對快照式或交易式發行集中發行的發行項定義資料行篩選  
  
1.  定義要篩選的發行項。 如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  在發行集資料庫的發行者，執行 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)。 這樣會定義要在發行項中包含或移除的資料行。  
  
    -   如果發行只有幾個資料表中資料行包含許多資料行，請執行 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) 一次加入的每個資料行。 針對 **@column** 指定資料行名稱，並針對 **@operation** 指定 **add**的值。  
  
    -   如果中發行大多數的資料行包含許多資料行的資料表，執行 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md), ，指定的值 **null** 的 **@column** 且值為 **加入** 的 **@operation** 加入所有資料行。 然後執行 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md), 之後每個資料行中排除，指定的值為, **卸除** 的 **@operation** 和排除的資料行名稱 **@column**。  
  
3.  在發行集資料庫的發行者，執行 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)。 針對 **@publication** 指定發行集名稱，並針對 **@article**指定篩選的發行項名稱。 這樣會針對篩選的發行項建立同步處理物件。  
  
#### 針對快照式或交易式發行集中發行的發行項變更要包含其他資料行的資料行篩選  
  
1.  在發行集資料庫的發行者，執行 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) 一次加入的每個資料行。 針對 **@column** 指定資料行名稱，並針對 **@operation** 指定 **add**的值。  
  
2.  在發行集資料庫的發行者，執行 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)。 針對 **@publication** 指定發行集名稱，並針對 **@article**指定篩選的發行項名稱。 如果發行集有現有的訂閱，指定其值為 **1** 的 **@change_active**。 這樣會針對篩選的發行項重新建立同步處理物件。  
  
3.  針對此發行集重新執行快照集代理程式作業，以產生更新的快照集。  
  
4.  重新初始化訂閱。 如需詳細資訊，請參閱 [重新初始化訂閱](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
#### 針對快照式或交易式發行集中發行的發行項變更要移除資料行的資料行篩選  
  
1.  在發行集資料庫的發行者，執行 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) 移除的每個資料行一次。 針對 **@column** 指定資料行名稱，並針對 **@operation** 指定 **drop**的值。  
  
2.  在發行集資料庫的發行者，執行 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)。 針對 **@publication** 指定發行集名稱，並針對 **@article**指定篩選的發行項名稱。 如果發行集有現有的訂閱，指定其值為 **1** 的 **@change_active**。 這樣會針對篩選的發行項重新建立同步處理物件。  
  
3.  針對此發行集重新執行快照集代理程式作業，以產生更新的快照集。  
  
4.  重新初始化訂閱。 如需詳細資訊，請參閱 [重新初始化訂閱](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
#### 針對合併式發行集中發行的發行項定義資料行篩選  
  
1.  定義要篩選的發行項。 如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  在發行集資料庫的發行者，執行 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md)。 這樣會定義要在發行項中包含或移除的資料行。  
  
    -   如果發行只有幾個資料表中資料行包含許多資料行，請執行 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) 一次加入的每個資料行。 針對 **@column** 指定資料行名稱，並針對 **@operation** 指定 **add**的值。  
  
    -   如果中發行大多數的資料行包含許多資料行的資料表，執行 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md), ，指定的值 **null** 的 **@column** 且值為 **加入** 的 **@operation** 加入所有資料行。 然後執行 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md), 之後每個資料行中排除，指定的值為, **卸除** 的 **@operation** 和排除的資料行名稱 **@column**。  
  
#### 針對合併式發行集中發行的發行項變更要包含其他資料行的資料行篩選  
  
1.  在發行集資料庫的發行者，執行 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) 一次加入的每個資料行。 指定的資料行名稱 **@column**, ，值為 **加入** 的 **@operation** 且值為 **1** 兩者 **@force_invalidate_snapshot** 和 **@force_reinit_subscription**。  
  
2.  針對此發行集重新執行快照集代理程式作業，以產生更新的快照集。  
  
3.  重新初始化訂閱。 如需詳細資訊，請參閱 [重新初始化訂閱](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
#### 針對合併式發行集中發行的發行項變更要移除資料行的資料行篩選  
  
1.  在發行集資料庫的發行者，執行 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) 移除的每個資料行一次。 指定的資料行名稱 **@column**, ，值為 **卸除** 的 **@operation** 且值為 **1** 兩者 **@force_invalidate_snapshot** 和 **@force_reinit_subscription**。  
  
2.  針對此發行集重新執行快照集代理程式作業，以產生更新的快照集。  
  
3.  重新初始化訂閱。 如需詳細資訊，請參閱 [重新初始化訂閱](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 此異動複寫範例會從根據 `DaysToManufacture` 資料表的發行項中移除 `Product` 資料行。  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-colu_1.sql)]  
  
 此合併式複寫範例會從根據 `CreditCardApprovalCode` 資料表的發行項中移除 `SalesOrderHeader` 資料行。  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-colu_2.sql)]  
  
## 另請參閱  
 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [篩選發行的資料](../../../relational-databases/replication/publish/filter-published-data.md)   
 [篩選合併式複寫之發行的資料](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)  
  
  