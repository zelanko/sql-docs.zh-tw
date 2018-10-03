---
title: sp_articlecolumn & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_articlecolumn
- sp_articlecolumn_TSQL
helpviewer_keywords:
- sp_articlecolumn
ms.assetid: 8abaa8c1-d99e-4788-970f-c4752246c577
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 72d9238e5b0f8ad5480e05ded3a0154eb5510904
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47640716"
---
# <a name="sparticlecolumn-transact-sql"></a>sp_articlecolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [ **@publication=**] **'***publication***'**  
 這是包含發行項的發行集名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [  **@article=**] **'***文章***'**  
 這是發行項的名稱。 *發行項*已**sysname**，沒有預設值。  
  
 [  **@column=**] **'***資料行***'**  
 這是要加入或卸除的資料行名稱。 *資料行*已**sysname**，預設值是 NULL。 如果是 NULL，就會發行所有資料行。  
  
 [  **@operation=**] **'***作業***'**  
 指定要加入或卸除發行項中的資料行。 *作業*已**nvarchar(5)**，預設值是 add。 **新增**標示複寫的資料行。 **卸除**會取消標示資料行。  
  
 [  **@refresh_synctran_procs=**] *refresh_synctran_procs*  
 指定是否重新產生支援立即更新訂閱的預存程序，以符合複寫的資料行數目。 *refresh_synctran_procs*已**位元**，預設值是**1**。 如果**1**，預存程序會重新產生。  
  
 [  **@ignore_distributor =**] *ignore_distributor*  
 指出是否在未連接到散發者的情況之下，執行這個預存程序。 *ignore_distributor*已**位元**，預設值是**0**。 如果**0**、 發行，必須啟用資料庫和發行項快取重新整理以反映新的資料行所複寫的發行項。 如果**1**，可讓發行項的資料行是要卸除之發行項的未發行的資料庫中，只用於修復的情況。  
  
 [  **@change_active =** ] *change_active*  
 可讓您修改已有訂閱之發行集的資料行。 *change_active*已**int**預設值是**0**。 如果**0**，不會修改資料行。 如果**1**，可以加入或從作用中有訂用帳戶的發行項中卸除資料行。  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 認可這個預存程序所採取的動作可能使現有的快照集失效。 *force_invalidate_snapshot*已**位元**，預設值是**0**。  
  
 **0**指定發行項的變更不會使快照集失效。 如果預存程序偵測到變更需要新的快照集，就會發生錯誤，且不會進行任何變更。  
  
 **1**指定發行項的變更可能使快照集失效，如果有現有的訂閱需要新的快照集，提供權限來標示為已棄用之現有快照集和產生新的快照集。  
  
 [ **@force_reinit_subscription =** ] *force_reinit_subscription*  
 認可這個預存程序所採取的動作可能需要重新初始化現有的訂閱。 *force_reinit_subscription*已**位元**，預設值是**0**。  
  
 **0**指定發行項的變更不會使訂閱重新初始化。 如果預存程序偵測到變更需要重新初始化訂閱，就會發生錯誤，且不會進行任何變更。 **1**指定發行項的變更會使現有的訂閱重新初始化，並提供發生之訂閱重新初始化的權限。  
  
 [  **@publisher=** ] **'***發行者***'**  
 指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *發行者*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*不應使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
 [  **@internal=** ] **'***內部***'**  
 僅供內部使用。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_articlecolumn**用於快照式複寫和異動複寫。  
  
 您可以使用篩選的取消訂閱發行項**sp_articlecolumn**。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlecolumn-transac_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_articlecolumn**。  
  
## <a name="see-also"></a>另請參閱  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [定義及修改資料行篩選](../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)   
 [篩選發行的資料](../../relational-databases/replication/publish/filter-published-data.md)   
 [sp_addarticle &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articleview &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
