---
title: 定義及修改資料行篩選 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server replication], column
- modifying filters, column
- modifying filters
- column filters [SQL Server replication]
ms.assetid: d7c3186a-9a8c-45d8-ab34-05beec4c26dd
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: e9da7e08751fc7c8bc72b85d174678e783cb79a3
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769895"
---
# <a name="define-and-modify-a-column-filter"></a>定義及修改資料行篩選
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中定義及修改資料行篩選。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
-   **若要定義及修改資料行篩選，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   某些資料行無法進行篩選；如需詳細資訊，請參閱[篩選發行的資料](../../../relational-databases/replication/publish/filter-published-data.md)。 如果您要在初始化訂閱後修改資料行篩選，則必須在進行變更後產生新的快照集並重新初始化所有訂閱。 如需屬性變更需求的詳細資訊，請參閱[變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在「新增發行集精靈」的 **[發行項]** 頁面中定義資料行篩選。 如需使用「新增發行集精靈」的詳細資訊，請參閱[建立發行集](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
 在 [發行集屬性 - \<發行集>]  對話方塊的 [發行項]  頁面上定義及修改資料行篩選。 如需發行集和發行項屬性的詳細資訊，請參閱[檢視及修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### <a name="to-define-a-column-filter"></a>若要定義資料行篩選  
  
1.  在「新增發行集精靈」的 **[發行項]** 頁面中，展開要在 **[發行的物件]** 窗格中篩選的資料表。  
  
2.  清除您要篩選之每個資料行旁邊的核取方塊。  
  
#### <a name="to-modify-column-filtering"></a>若要修改資料行篩選  
  
1.  在 [發行集屬性 - \<發行集>]  對話方塊的 [發行項]  頁面中，展開要在 [發行的物件]  窗格中篩選的資料表。  
  
2.  清除每個您要篩選之資料行旁邊的核取方塊，並確保為每個應包含在發行項中的資料行選取核取方塊。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 在建立資料表發行項時，您可以定義要將哪些資料行包含在發行項中，並在定義發行項之後變更資料行。 您可以使用複寫預存程序來以程式設計的方式建立及修改篩選的資料行。  
  
> [!NOTE]  
>  下列程序假設基礎資料表尚未變更。 如需複寫已發行之資料表的資料定義語言 (DDL) 變更的詳細資訊，請參閱[對發行集資料庫進行結構描述變更](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
#### <a name="to-define-a-column-filter-for-an-article-published-in-a-snapshot-or-transactional-publication"></a>針對快照式或交易式發行集中發行的發行項定義資料行篩選  
  
1.  定義要篩選的發行項。 如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  在發行集資料庫的發行者上，執行 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)。 這樣會定義要在發行項中包含或移除的資料行。  
  
    -   如果只要從包含許多資料行的資料表發行一些資料行，請針對加入的每一個資料行執行 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) 一次。 針對 **@column** 指定資料行名稱，並針對 **@operation** 指定 **@operation** 中定義及修改資料行篩選。  
  
    -   如果要在包含許多資料行的資料表中發行大多數的資料行，請執行 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)、針對 **@column** 指定 **@column** 指定資料行名稱，並針對 **@operation** 指定 **@operation** 的值來加入所有資料行。 然後針對每一個排除的資料行執行 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)一次，針對 **@operation** 指定 **@operation** 的值，並針對 **@column** 中定義及修改資料行篩選。  
  
3.  在發行集資料庫的發行者上，執行 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)。 針對 **@publication** 指定發行集名稱，並針對 **@article** 中定義及修改資料行篩選。 這樣會針對篩選的發行項建立同步處理物件。  
  
#### <a name="to-change-a-column-filter-to-include-additional-columns-for-an-article-published-in-a-snapshot-or-transactional-publication"></a>針對快照式或交易式發行集中發行的發行項變更要包含其他資料行的資料行篩選  
  
1.  在發行集資料庫的發行者上，針對每一個加入的資料行執行 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) 一次。 針對 **@column** 指定資料行名稱，並針對 **@operation** 指定 **@operation** 中定義及修改資料行篩選。  
  
2.  在發行集資料庫的發行者上，執行 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)。 針對 **@publication** 指定發行集名稱，並針對 **@article** 中定義及修改資料行篩選。 如果此發行集有現有的訂閱，請針對 **@change_active** 指定 **@change_active** 中定義及修改資料行篩選。 這樣會針對篩選的發行項重新建立同步處理物件。  
  
3.  針對此發行集重新執行快照集代理程式作業，以產生更新的快照集。  
  
4.  重新初始化訂閱。 如需詳細資訊，請參閱 [重新初始化訂閱](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
#### <a name="to-change-a-column-filter-to-remove-columns-for-an-article-published-in-a-snapshot-or-transactional-publication"></a>針對快照式或交易式發行集中發行的發行項變更要移除資料行的資料行篩選  
  
1.  在發行集資料庫的發行者上，針對每一個移除的資料行執行 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) 一次。 針對 **@column** 指定資料行名稱，並針對 **@operation** 指定 **@operation** 中定義及修改資料行篩選。  
  
2.  在發行集資料庫的發行者上，執行 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)。 針對 **@publication** 指定發行集名稱，並針對 **@article** 中定義及修改資料行篩選。 如果此發行集有現有的訂閱，請針對 **@change_active** 指定 **@change_active** 中定義及修改資料行篩選。 這樣會針對篩選的發行項重新建立同步處理物件。  
  
3.  針對此發行集重新執行快照集代理程式作業，以產生更新的快照集。  
  
4.  重新初始化訂閱。 如需詳細資訊，請參閱 [重新初始化訂閱](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
#### <a name="to-define-a-column-filter-for-an-article-published-in-a-merge-publication"></a>針對合併式發行集中發行的發行項定義資料行篩選  
  
1.  定義要篩選的發行項。 如需詳細資訊，請參閱 [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  在發行集資料庫的發行者上，執行 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md)。 這樣會定義要在發行項中包含或移除的資料行。  
  
    -   如果只要從包含許多資料行的資料表發行一些資料行，請針對加入的每一個資料行執行 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) 一次。 針對 **@column** 指定資料行名稱，並針對 **@operation** 指定 **@operation** 中定義及修改資料行篩選。  
  
    -   如果要在包含許多資料行的資料表中發行大多數的資料行，請執行 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md)、針對 **@column** 指定 **@column** 指定資料行名稱，並針對 **@operation** 指定 **@operation** 的值來加入所有資料行。 然後針對每一個排除的資料行執行 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md)一次，針對 **@operation** 指定 **@operation** 的值，並針對 **@column** 中定義及修改資料行篩選。  
  
#### <a name="to-change-a-column-filter-to-include-additional-columns-for-an-article-published-in-a-merge-publication"></a>針對合併式發行集中發行的發行項變更要包含其他資料行的資料行篩選  
  
1.  在發行集資料庫的發行者上，針對每一個加入的資料行執行 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) 一次。 針對 **@column** 指定資料行名稱、針對 **@operation** 指定 **@operation** 指定資料行名稱，並針對 **@change_active** 和 **@force_invalidate_snapshot** 指定 **@force_reinit_subscription** 中定義及修改資料行篩選。  
  
2.  針對此發行集重新執行快照集代理程式作業，以產生更新的快照集。  
  
3.  重新初始化訂閱。 如需詳細資訊，請參閱 [重新初始化訂閱](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
#### <a name="to-change-a-column-filter-to-remove-columns-for-an-article-published-in-a-merge-publication"></a>針對合併式發行集中發行的發行項變更要移除資料行的資料行篩選  
  
1.  在發行集資料庫的發行者上，針對每一個移除的資料行執行 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) 一次。 針對 **@column** 指定資料行名稱、針對 **@operation** 指定 **@operation** 指定資料行名稱，並針對 **@change_active** 和 **@force_invalidate_snapshot** 指定 **@force_reinit_subscription** 中定義及修改資料行篩選。  
  
2.  針對此發行集重新執行快照集代理程式作業，以產生更新的快照集。  
  
3.  重新初始化訂閱。 如需詳細資訊，請參閱 [重新初始化訂閱](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
###  <a name="TsqlExample"></a> 範例 &#40;Transact-SQL&#41;  
 此異動複寫範例會從根據 `DaysToManufacture` 資料表的發行項中移除 `Product` 資料行。  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-colu_1.sql)]  
  
 此合併式複寫範例會從根據 `CreditCardApprovalCode` 資料表的發行項中移除 `SalesOrderHeader` 資料行。  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-colu_2.sql)]  
  
## <a name="see-also"></a>另請參閱  
 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [篩選發行的資料](../../../relational-databases/replication/publish/filter-published-data.md)   
 [針對合併式複寫篩選發行的資料](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)  
  
  
