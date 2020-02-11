---
title: sp_articlefilter （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: d90cd0ba957da820ce5a937ae687e39ca0302025
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68769062"
---
# <a name="sp_articlefilter-transact-sql"></a>sp_articlefilter (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

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
`[ @publication = ] 'publication'`這是包含發行項的發行集名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @article = ] 'article'`這是發行項的名稱。 *文章*是**sysname**，沒有預設值。  
  
`[ @filter_name = ] 'filter_name'`這是要從*filter_name*建立之篩選預存程式的名稱。 *filter_name*是**Nvarchar （386）**，預設值是 Null。 您必須指定發行項篩選的唯一名稱。  
  
`[ @filter_clause = ] 'filter_clause'`這是定義水準篩選的限制（WHERE）子句。 當輸入限制子句時，請省略 WHERE 關鍵字。 *filter_clause*是**Ntext**，預設值是 Null。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`認可這個預存程式所採取的動作可能會使現有的快照集失效。 *force_invalidate_snapshot*是**bit**，預設值是**0**。  
  
 **0**指定發行項的變更不會使快照集失效。 如果預存程序偵測到變更需要新的快照集，就會發生錯誤，且不會進行任何變更。  
  
 **1**指定發行項的變更可能會導致快照集無效，如果有現有的訂閱需要新的快照集，則會提供要標示為已淘汰之現有快照集的許可權，並產生新的快照集。  
  
`[ @force_reinit_subscription = ] force_reinit_subscription`認可這個預存程式所採取的動作可能需要重新初始化現有的訂閱。 *force_reinit_subscription*是**bit**，預設值是**0**。  
  
 **0**指定發行項的變更不會造成重新初始化訂閱的需求。 如果預存程序偵測到變更需要重新初始化訂閱，就會發生錯誤，且不會進行任何變更。  
  
 **1**指定發行項的變更會使現有的訂閱重新初始化，並提供要進行訂閱重新初始化的許可權。  
  
`[ @publisher = ] 'publisher'`指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *publisher*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  *發行者*不應用於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_articlefilter**用於快照式複寫和異動複寫中。  
  
 針對具有現有訂閱的發行項執行**sp_articlefilter** ，需要重新初始化這些訂閱。  
  
 **sp_articlefilter**建立篩選器，會將篩選預存程式的識別碼插入[sysarticles &#40;transact-sql&#41;](../../relational-databases/system-tables/sysarticles-transact-sql.md)資料表的**篩選**條件資料行中，然後在**filter_clause**資料行中插入限制子句的文字。  
  
 若要建立具有水準篩選的發行項，請執行不含*篩選*參數的[sp_addarticle &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 。 執行**sp_articlefilter**，提供包括*filter_clause*在內的所有參數，然後執行[sp_articleview &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)，提供所有參數，包括相同的*filter_clause*。 如果篩選已存在，而且**sysarticles**中的**類型**為**1** （記錄式發行項），則會刪除先前的篩選，並建立新的篩選。  
  
 如果未提供*filter_name*和*filter_clause* ，則會刪除先前的篩選準則，並將篩選識別碼設定為**0**。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlefilter-transac_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_articlefilter**。  
  
## <a name="see-also"></a>另請參閱  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [定義及修改靜態資料列篩選](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articleview &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
