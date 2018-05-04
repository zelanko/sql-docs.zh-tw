---
title: sp_mergearticlecolumn (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_mergearticlecolumn
- sp_mergearticlecolumn_TSQL
helpviewer_keywords:
- sp_mergearticlecolumn
ms.assetid: b4f2b888-e094-4759-a472-d893638995eb
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: bf9aa73835ee0a83da99b109fe81fd99b6c03f4d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spmergearticlecolumn-transact-sql"></a>sp_mergearticlecolumn (Transact-SQL)
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
 [  **@publication =**] **'***發行集***'**  
 這是發行集的名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [  **@article =**] **'***文章***'**  
 這是發行集的發行項名稱。 *發行項*是**sysname**，沒有預設值。  
  
 [  **@column =**] **'***資料行***'**  
 識別用來建立垂直資料分割的資料行。 *資料行*是**sysname**，預設值是 NULL。 如果是 NULL 和 `@operation = N'add'`，依預設，會將來源資料表中所有的資料行加入至發行項。 *資料行*不能為 NULL 時*作業*設**卸除**。 若要從發行項排除資料行，請執行**sp_mergearticlecolumn**並指定*資料行*和`@operation = N'drop'`要移除的每一個資料行從指定*文章*.  
  
 [  **@operation =**] **'***作業***'**  
 這是訂閱狀態。 *作業*是**nvarchar （4)**，預設值是 ADD。 **新增**標示複寫的資料行。 **卸除**清除資料行。  
  
 [  **@schema_replication=**] **'***schema_replication***'**  
 指定當執行合併代理程式時，將傳播結構描述變更。 *schema_replication*是**nvarchar （5)**，預設值是 FALSE。  
  
> [!NOTE]  
>  只有**FALSE**支援*schema_replication*。  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 啟用或停用使快照集失效的能力。 *force_invalidate_snapshot*是**元**，預設值是**0**。  
  
 **0**指定合併發行項的變更不會使快照集失效。  
  
 **1**指定合併發行項的變更可能使快照集失效，如果這種情況下，值為和**1**提供將出現新的快照集的權限。  
  
 [* *@force_reinit_subscription =] * * * force_reinit_subscription*  
 啟用或停用重新初始化訂閱的能力。 *force_reinit_subscription*是 bit，預設值是**0**。  
  
 **0**指定合併發行項的變更不會使訂閱重新初始化。  
  
 **1**指定合併發行項的變更可能使訂閱重新初始化，以及如果這種情況下，值為**1**提供發生訂閱重新初始化的權限。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_mergearticlecolumn**用於合併式複寫中。  
  
 如果使用自動識別範圍管理，便無法從發行項中卸除識別欄位。 如需詳細資訊，請參閱[複寫識別資料欄](../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
 如果應用程式在建立初始快照集之後，設定新的垂直資料分割，就必須產生新的快照集，並重新套用至每項訂閱上。 當執行下一個已排程的快照集及散發或合併代理程式時，會套用快照集。  
  
 如果使用資料列追蹤執行衝突偵測 (預設值)，基底資料表最多可以包含 1,024 個資料行，但必須從發行項篩選資料行，以便發行最多 246 個資料行。 如果使用資料行追蹤，則基底資料表可包括的資料行數上限為 246。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_AddMergeArticle](../../relational-databases/replication/codesnippet/tsql/sp-mergearticlecolumn-tr_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_mergearticlecolumn**。  
  
## <a name="see-also"></a>另請參閱  
 [Define and Modify a Join Filter Between Merge Articles](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [針對合併發行項定義及修改參數化資料列篩選](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [篩選發行的資料](../../relational-databases/replication/publish/filter-published-data.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
