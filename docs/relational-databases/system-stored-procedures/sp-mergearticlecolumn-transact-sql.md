---
title: sp_mergearticlecolumn （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergearticlecolumn
- sp_mergearticlecolumn_TSQL
helpviewer_keywords:
- sp_mergearticlecolumn
ms.assetid: b4f2b888-e094-4759-a472-d893638995eb
author: stevestein
ms.author: sstein
ms.openlocfilehash: ff669af64b6aed312481264127d69eee1ad674e5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68078164"
---
# <a name="sp_mergearticlecolumn-transact-sql"></a>sp_mergearticlecolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  進行合併式發行集的垂直資料分割。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_mergearticlecolumn [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @column = ] 'column'  
    [ , [ @operation = ] 'operation'   
    [ , [ @schema_replication = ] 'schema_replication' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]   
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]   
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'`這是發行集的名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @article = ] 'article'`這是發行集中的發行項名稱。 *文章*是**sysname**，沒有預設值。  
  
`[ @column = ] 'column'`識別要在其上建立垂直資料分割的資料行。 資料*行*是**sysname**，預設值是 Null。 如果是 NULL 和 `@operation = N'add'`，依預設，會將來源資料表中所有的資料行加入至發行項。 當*operation*設定為**drop**時，資料*行*不可以是 Null。 若要從發行項中排除資料**sp_mergearticlecolumn**行，請執行 sp_mergearticlecolumn `@operation = N'drop'`並指定資料*行*，並將每個資料行從指定的發行*項中移除。*  
  
`[ @operation = ] 'operation'`這是複寫狀態。 *operation*是**Nvarchar （4）**，預設值是 ADD。 [**加入**] 會標示要複寫的資料行。 **drop**會清除資料行。  
  
`[ @schema_replication = ] 'schema_replication'`指定當合併代理程式執行時，將傳播架構變更。 *schema_replication*是**Nvarchar （5）**，預設值是 FALSE。  
  
> [!NOTE]  
>  *Schema_replication*只支援**FALSE** 。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`啟用或停用使快照集失效的能力。 *force_invalidate_snapshot*是**bit**，預設值是**0**。  
  
 **0**指定合併發行項的變更不會使快照集無效。  
  
 **1**指定合併發行項的變更可能會導致快照集無效，如果是這種情況， **1**的值會提供新快照集的許可權。  
  
`[ @force_reinit_subscription = ]force_reinit_subscription_`啟用或停用訂用帳戶重新初始化能力的功能。 *force_reinit_subscription*是位，預設值是**0**。  
  
 **0**指定合併發行項的變更不會使訂閱重新初始化。  
  
 **1**指定合併發行項的變更可能會使訂閱重新初始化，如果是這種情況， **1**值會提供將進行訂閱重新初始化的許可權。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_mergearticlecolumn**用於合併式複寫中。  
  
 如果使用自動識別範圍管理，便無法從發行項中卸除識別欄位。 如需詳細資訊，請參閱[複寫識別資料欄](../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
 如果應用程式在建立初始快照集之後，設定新的垂直資料分割，就必須產生新的快照集，並重新套用至每項訂閱上。 當執行下一個已排程的快照集及散發或合併代理程式時，會套用快照集。  
  
 如果使用資料列追蹤執行衝突偵測 (預設值)，基底資料表最多可以包含 1,024 個資料行，但必須從發行項篩選資料行，以便發行最多 246 個資料行。 如果使用資料行追蹤，則基底資料表可包括的資料行數上限為 246。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_AddMergeArticle](../../relational-databases/replication/codesnippet/tsql/sp-mergearticlecolumn-tr_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_mergearticlecolumn**。  
  
## <a name="see-also"></a>另請參閱  
 [定義和修改合併發行項之間的聯結篩選](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [針對合併發行項定義及修改參數化資料列篩選](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [篩選發行的資料](../../relational-databases/replication/publish/filter-published-data.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
