---
description: sp_articlecolumn (Transact-SQL)
title: sp_articlecolumn (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_articlecolumn
- sp_articlecolumn_TSQL
helpviewer_keywords:
- sp_articlecolumn
ms.assetid: 8abaa8c1-d99e-4788-970f-c4752246c577
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d67cb8b9d25b97756bd1e0f86c5425542a2601d2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548318"
---
# <a name="sp_articlecolumn-transact-sql"></a>sp_articlecolumn (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  用來指定發行項所包括的資料行，以垂直篩選已發行之資料表的資料。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_articlecolumn [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @column = ] 'column' ]  
    [ , [ @operation = ] 'operation' ]  
    [ , [ @refresh_synctran_procs = ] refresh_synctran_procs ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @change_active = ] change_actve ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @internal = ] 'internal' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是包含這篇文章的發行集名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @article = ] 'article'` 這是發行項的名稱。 *文章* 是 **sysname**，沒有預設值。  
  
`[ @column = ] 'column'` 這是要加入或卸載的資料行名稱。 資料*行*是**sysname**，預設值是 Null。 如果是 NULL，就會發行所有資料行。  
  
`[ @operation = ] 'operation'` 指定是否要在發行項中加入或卸載資料行。 *操作* 是 **Nvarchar (5) **，預設值是 add。 **add** 會標示覆寫的資料行。 **drop** 會取消資料行的標記。  
  
`[ @refresh_synctran_procs = ] refresh_synctran_procs` 指定是否重新產生支援立即更新訂閱的預存程式，以符合複寫的資料行數目。 *refresh_synctran_procs* 是 **bit**，預設值是 **1**。 如果是 **1**，就會重新產生預存程式。  
  
`[ @ignore_distributor = ] ignore_distributor` 指出是否在未連接到散發者的情況下執行這個預存程式。 *ignore_distributor* 是 **bit**，預設值是 **0**。 如果是 **0**，就必須啟用資料庫以供發行，而且應該重新整理髮行項快取，以反映發行項所複寫的新資料行。 如果為 **1**，則允許針對位於未發行之資料庫中的發行項卸載發行項資料行;應僅用於復原狀況。  
  
`[ @change_active = ] change_active` 允許修改具有訂閱之發行集的資料行。 *change_active* 是 **int** ，預設值是 **0**。 如果為 **0**，則不會修改資料行。 如果是 **1**，就可以從具有訂閱的使用中發行項加入或卸載資料行。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` 認可這個預存程式所採取的動作可能使現有的快照集失效。 *force_invalidate_snapshot* 是 **bit**，預設值是 **0**。  
  
 **0** 指定發行項的變更不會使快照集失效。 如果預存程序偵測到變更需要新的快照集，就會發生錯誤，且不會進行任何變更。  
  
 **1** 指定發行項的變更可能使快照集失效，如果有現有的訂閱需要新的快照集，則會將現有快照集的許可權標示為已淘汰，並產生新的快照集。  
  
 [** @force_reinit_subscription =** ] *force_reinit_subscription*  
 認可這個預存程序所採取的動作可能需要重新初始化現有的訂閱。 *force_reinit_subscription* 是 **bit**，預設值是 **0**。  
  
 **0** 指定發行項的變更不會使訂閱重新初始化。 如果預存程序偵測到變更需要重新初始化訂閱，就會發生錯誤，且不會進行任何變更。 **1** 指定發行項的變更會使現有的訂閱重新初始化，且會提供將發生之訂閱重新初始化的許可權。  
  
`[ @publisher = ] 'publisher'` 指定非 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *publisher* 是 **sysname**，預設值是 Null。  
  
> [!NOTE]  
>  *發行者* 不應與發行者一起使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
`[ @internal = ] 'internal'` 僅供內部使用。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_articlecolumn** 用於快照式複寫和異動複寫中。  
  
 您只能使用 **sp_articlecolumn**來篩選取消訂閱的文章。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlecolumn-transac_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_articlecolumn**。  
  
## <a name="see-also"></a>另請參閱  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [定義和修改資料行篩選](../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)   
 [篩選發行的資料](../../relational-databases/replication/publish/filter-published-data.md)   
 [sp_addarticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articleview &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
