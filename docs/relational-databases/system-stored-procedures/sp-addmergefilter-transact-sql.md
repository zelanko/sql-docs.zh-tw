---
description: sp_addmergefilter (Transact-SQL)
title: sp_addmergefilter (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergefilter
- sp_addmergefilter_TSQL
helpviewer_keywords:
- sp_addmergefilter
ms.assetid: 4c118cb1-2008-44e2-a797-34b7dc34d6b1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d1149db6cfbebcc1dc1ec2b62fcbb0ce02b93fad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489655"
---
# <a name="sp_addmergefilter-transact-sql"></a>sp_addmergefilter (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  加入合併篩選，依據與其他資料表的聯結，建立資料分割。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addmergefilter [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
        , [ @filtername = ] 'filtername'   
        , [ @join_articlename = ] 'join_articlename'   
        , [ @join_filterclause = ] join_filterclause  
    [ , [ @join_unique_key = ] join_unique_key ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @filter_type = ] filter_type ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是要加入合併篩選之發行集的名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @article = ] 'article'` 這是要加入合併篩選的發行項名稱。 *文章* 是 **sysname**，沒有預設值。  
  
`[ @filtername = ] 'filtername'` 這是篩選的名稱。 *filtername* 是必要參數。 *filtername*是 **sysname**，沒有預設值。  
  
`[ @join_articlename = ] 'join_articlename'`這是發行項所指定之子發行項的父發行項，必須使用*join_filterclause*所指定的聯結子句來*聯結，以*判斷子發行項中符合合併篩選之篩選準則的資料列。 *join_articlename* 是 **sysname**，沒有預設值。 發行項必須在 *發行*集所提供的發行集中。  
  
`[ @join_filterclause = ] join_filterclause`這是聯結子句，必須用來聯結*join_article*所指定之發行項*和父*發行項所指定的子發行項，以便判斷符合合併篩選準則的資料列。 *join_filterclause* 是 **Nvarchar (1000) **。  
  
`[ @join_unique_key = ] join_unique_key` 指定子發行 *項與父*發行項 *join_article*之間的聯結是一對多、一對一、多對一或多對多的聯結。 *join_unique_key* 是 **int**，預設值是0。 **0** 表示多對一或多對多聯結。 **1** 表示一對一或一對多的聯結的聯結。 當聯結的資料行形成*join_article*中的唯一索引鍵，*或在發行*項的外鍵和*join_article*中的主鍵之間*join_filterclause*時，此值為**1** 。  
  
> [!CAUTION]  
>  只有在保證唯一性的父發行項之基礎資料表中的聯結資料行上有條件約束時，才將此參數設定為 **1** 。 如果 *join_unique_key* 設定為 **1** 不正確，可能會發生資料非聚合。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` 認可這個預存程式所採取的動作可能使現有的快照集失效。 *force_invalidate_snapshot* 是 **bit**，預設值是 **0**。  
  
 **0** 指定合併發行項的變更不會使快照集失效。 如果預存程序偵測到變更需要新的快照集，就會發生錯誤，且不會進行任何變更。  
  
 **1** 指定合併發行項的變更可能使快照集失效，如果有現有的訂閱需要新的快照集，則會將現有快照集的許可權標示為已淘汰，並產生新的快照集。  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` 認可這個預存程式所採取的動作可能需要重新初始化現有的訂閱。 *force_reinit_subscription* 是 **bit**，預設值是0。  
  
 **0** 指定合併發行項的變更不會使訂閱重新初始化。 如果預存程序偵測到變更需要重新初始化訂閱，就會發生錯誤，且不會進行任何變更。  
  
 **1** 指定合併發行項的變更會使現有的訂閱重新初始化，且會提供將發生之訂閱重新初始化的許可權。  
  
`[ @filter_type = ] filter_type` 指定要加入的篩選類型。 *filter_type* 是 **Tinyint**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|僅聯結篩選。 支援 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 訂閱者需要這個值。|  
|**2**|僅邏輯記錄關聯性。|  
|**3**|聯結篩選和邏輯記錄關聯性。|  
  
 如需詳細資訊，請參閱[使用邏輯記錄分組相關資料列的變更](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_addmergefilter** 用於合併式複寫中。  
  
 **sp_addmergefilter** 只能用於資料表發行項。 不支援檢視和索引檢視發行項。  
  
 這個程序也可以在兩個發行項之間加入邏輯關聯性，不論這些發行項之間是否有聯結篩選。 *filter_type* 用來指定要加入的合併篩選是聯結篩選、邏輯關聯或兩者。  
  
 若要使用邏輯記錄，發行集和發行項必須符合許多需求。 如需詳細資訊，請參閱[使用邏輯記錄分組相關資料列的變更](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
 通常，這個選項用於一個有已發行主索引鍵資料表之外部索引鍵參考的發行項，且主索引鍵資料表在它的發行項中定義了篩選。 主索引鍵資料列的子集可用來決定抄寫至訂閱者的外部索引鍵資料列。  
  
 當兩個發行項的來源資料表共用相同的資料表物件名稱時，您無法在這兩個已發行的發行項之間加入聯結篩選。 在這種情況下，即使兩個資料表為不同結構描述所擁有，且具有唯一的發行項名稱，聯結篩選的建立作業仍會失敗。  
  
 當參數化資料列篩選器和聯結篩選都用於資料表發行項上時，複寫會判斷資料列是否屬於訂閱者的資料分割。 它會藉由使用 [or](../../t-sql/language-elements/or-transact-sql.md) 運算子) 來評估篩選函數或聯結篩選 (，而不是使用 [AND](../../t-sql/language-elements/and-transact-sql.md) 運算子) 來評估兩個條件的交集 (。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_addmergefilter](../../relational-databases/replication/codesnippet/tsql/sp-addmergefilter-transa_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_addmergefilter**。  
  
## <a name="see-also"></a>另請參閱  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [定義和修改合併發行項之間的聯結篩選](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [sp_changemergefilter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_dropmergefilter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [sp_helpmergefilter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
