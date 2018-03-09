---
title: "sp_articlefilter (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_articlefilter_TSQL
- sp_articlefilter
helpviewer_keywords:
- sp_articlefilter
ms.assetid: 4c3fee32-a43f-4757-a029-30aef4696afb
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: de8979cdc3cb382aa290148e560d8eb72db94b1b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sparticlefilter-transact-sql"></a>sp_articlefilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  篩選基於資料表發行項而發行的資料。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_articlefilter [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @filter_name = ] 'filter_name' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@publication=**] **'***發行集***'**  
 這是發行項所在的發行集名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [  **@article=**] **'***文章***'**  
 這是發行項的名稱。 *發行項*是**sysname**，沒有預設值。  
  
 [  **@filter_name=**] **'***filter_name***'**  
 是要從建立篩選預存程序的名稱*filter_name*。 *filter_name*是**nvarchar （386)**，預設值是 NULL。 您必須指定發行項篩選的唯一名稱。  
  
 [  **@filter_clause=**] **'***filter_clause***'**  
 這是定義水平篩選的限制 (WHERE) 子句。 當輸入限制子句時，請省略 WHERE 關鍵字。 *filter_clause*是**ntext**，預設值是 NULL。  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 認可這個預存程序所採取的動作可能使現有的快照集失效。 *force_invalidate_snapshot*是**元**，預設值是**0**。  
  
 **0**指定發行項的變更不會使快照集失效。 如果預存程序偵測到變更需要新的快照集，就會發生錯誤，且不會進行任何變更。  
  
 **1**指定發行項的變更可能使快照集失效，如果有現有的訂閱需要新的快照集，提供權限將會標示為已棄用之現有快照集和產生新的快照集。  
  
 [  **@force_reinit_subscription =** ] *force_reinit_subscription*  
 認可這個預存程序所採取的動作可能需要重新初始化現有的訂閱。 *force_reinit_subscription*是**元**，預設值是**0**。  
  
 **0**指定發行項的變更不會使訂閱重新初始化需要。 如果預存程序偵測到變更需要重新初始化訂閱，就會發生錯誤，且不會進行任何變更。  
  
 **1**指定發行項的變更會使現有的訂閱重新初始化，並提供發生訂閱重新初始化的權限。  
  
 [  **@publisher=** ] **'***發行者***'**  
 指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *發行者*是**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*不應與[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_articlefilter**用於快照式複寫和異動複寫。  
  
 執行**sp_articlefilter**具有現有的訂閱的發行項需要，重新初始化這些訂閱。  
  
 **sp_articlefilter**建立篩選、 篩選預存程序中的識別碼插入**篩選**資料行[sysarticles &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/sysarticles-transact-sql.md)資料表，並將限制子句中的文字**filter_clause**資料行。  
  
 若要建立含水平篩選的發行項，執行[sp_addarticle &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)沒有*篩選*參數。 執行**sp_articlefilter**，提供所有參數，包括*filter_clause*，然後執行[sp_articleview &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)，提供包括相同的所有參數*filter_clause*。 如果已經有篩選，而且**類型**中**sysarticles**是**1** （記錄式發行項），會刪除先前的篩選，並建立新的篩選。  
  
 如果*filter_name*和*filter_clause*未提供，會刪除先前的篩選和篩選識別碼會設定為**0**。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlefilter-transac_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_articlefilter**。  
  
## <a name="see-also"></a>請參閱＜  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [定義及修改靜態資料列篩選](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articleview &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
