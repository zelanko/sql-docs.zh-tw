---
title: sp_articlefilter (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_articlefilter_TSQL
- sp_articlefilter
helpviewer_keywords:
- sp_articlefilter
ms.assetid: 4c3fee32-a43f-4757-a029-30aef4696afb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 698a5941bc8e9920942e7ec7c962144b4ab24b62
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62998287"
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
`[ @publication = ] 'publication'` 是包含發行項的發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
`[ @article = ] 'article'` 是發行項的名稱。 *發行項*已**sysname**，沒有預設值。  
  
`[ @filter_name = ] 'filter_name'` 要從建立的篩選預存程序的名稱*filter_name*。 *filter_name*已**nvarchar(386)** ，預設值是 NULL。 您必須指定發行項篩選的唯一名稱。  
  
`[ @filter_clause = ] 'filter_clause'` 是一項限制會定義水平篩選 (WHERE) 子句。 當輸入限制子句時，請省略 WHERE 關鍵字。 *filter_clause*已**ntext**，預設值是 NULL。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` 認可這個預存程序所採取的動作可能會使現有的快照集。 *force_invalidate_snapshot*已**位元**，預設值是**0**。  
  
 **0**指定發行項的變更不會使快照集失效。 如果預存程序偵測到變更需要新的快照集，就會發生錯誤，且不會進行任何變更。  
  
 **1**指定發行項的變更可能使快照集失效，如果有現有的訂閱需要新的快照集，提供權限來標示為已棄用之現有快照集和產生新的快照集。  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` 認可這個預存程序所採取的動作可能需要重新初始化現有的訂用帳戶。 *force_reinit_subscription*已**位元**，預設值是**0**。  
  
 **0**指定發行項的變更不會使訂閱重新初始化的需求。 如果預存程序偵測到變更需要重新初始化訂閱，就會發生錯誤，且不會進行任何變更。  
  
 **1**指定發行項的變更會使現有的訂閱重新初始化，並提供發生之訂閱重新初始化的權限。  
  
`[ @publisher = ] 'publisher'` 指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *發行者*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*不應使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_articlefilter**用於快照式複寫和異動複寫。  
  
 執行**sp_articlefilter**針對具有現有的訂用帳戶的發行項需要重新初始化這些訂用帳戶。  
  
 **sp_articlefilter**建立篩選條件，將插入篩選預存程序中的識別碼**篩選**資料行[sysarticles &#40;-&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md)資料表，然後限制子句中的文字插入**filter_clause**資料行。  
  
 若要建立含水平篩選的發行項，執行[sp_addarticle &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)含*篩選*參數。 執行**sp_articlefilter**，並提供所有的參數包括*filter_clause*，然後執行[sp_articleview &#40;-&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)，提供包括相同的所有參數*filter_clause*。 如果篩選已經存在，而且如果**型別**中**sysarticles**會**1** （記錄式發行項），在刪除先前的篩選和建立新的篩選。  
  
 如果*filter_name*並*filter_clause*未提供，在刪除先前的篩選而篩選識別碼會設定為**0**。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlefilter-transac_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_articlefilter**。  
  
## <a name="see-also"></a>另請參閱  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [定義及修改靜態資料列篩選](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articleview &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
