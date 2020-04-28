---
title: sp_addsynctriggers （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addsynctriggers_TSQL
- sp_addsynctriggers
helpviewer_keywords:
- sp_addsynctriggers
ms.assetid: e37d0c3b-19bf-4719-9535-96ba361372b3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2b9bdabcc11c900ae0a1cbe71280b64efb6ccdaf
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68096213"
---
# <a name="sp_addsynctriggers-transact-sql"></a>sp_addsynctriggers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在訂閱者端建立搭配所有可更新訂閱類型 (立即、佇列和以佇列更新進行容錯移轉的立即更新) 來使用的觸發程序。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
> [!IMPORTANT]  
>  應該使用[sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)程式，而不是**sp_addsynctrigger**。 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)會產生包含**sp_addsynctrigger**呼叫的腳本。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addsynctriggers [ @sub_table = ] 'sub_table'  
        , [ @sub_table_owner = ] 'sub_table_owner'  
        , [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @ins_proc = ] 'ins_proc'   
        , [ @upd_proc = ] 'upd_proc'   
        , [ @del_proc = ] 'del_proc'   
        , [ @cftproc = ] 'cftproc'  
        , [ @proc_owner = ] 'proc_owner'  
    [ , [ @identity_col = ] 'identity_col' ]  
    [ , [ @ts_col = ] 'timestamp_col' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]   
        , [ @primary_key_bitmap = ] 'primary_key_bitmap'  
    [ , [ @identity_support = ] identity_support ]  
    [ , [ @independent_agent = ] independent_agent ]  
        , [ @distributor = ] 'distributor'   
    [ , [ @pubversion = ] pubversion  
```  
  
## <a name="arguments"></a>引數  
`[ @sub_table = ] 'sub_table'`這是訂閱者資料表的名稱。 *sub_table*是**sysname**，沒有預設值。  
  
`[ @sub_table_owner = ] 'sub_table_owner'`這是訂閱者資料表的擁有者名稱。 *sub_table_owner*是**sysname**，沒有預設值。  
  
`[ @publisher = ] 'publisher'`這是發行者伺服器的名稱。 *publisher*是**sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'`這是發行者資料庫的名稱。 *publisher_db*是**sysname**，沒有預設值。 如果是 NULL，就會使用目前的資料庫。  
  
`[ @publication = ] 'publication'`這是發行集的名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @ins_proc = ] 'ins_proc'`這是支援在發行者端同步交易插入的預存程式名稱。 *ins_proc*是**sysname**，沒有預設值。  
  
`[ @upd_proc = ] 'upd_proc'`這是在發行者端支援同步交易更新的預存程式名稱。 *ins_proc*是**sysname**，沒有預設值。  
  
`[ @del_proc = ] 'del_proc'`這是在發行者端支援同步交易刪除的預存程式名稱。 *ins_proc*是**sysname**，沒有預設值。  
  
`[ @cftproc = ] 'cftproc'`這是允許佇列更新的發行集所使用之自動產生的程式名稱。 *cftproc*是**sysname**，沒有預設值。 如果是允許立即更新的發行集，這個值便是 NULL。 這個參數適用於允許佇列更新 (佇列更新和以佇列更新進行容錯移轉的立即更新) 的發行集。  
  
`[ @proc_owner = ] 'proc_owner'`在發行者中，指定用來建立更新發行集（佇列和/或立即）之所有自動產生預存程式的使用者帳戶。 *proc_owner*是**sysname** ，沒有預設值。  
  
`[ @identity_col = ] 'identity_col'`這是在發行者端之識別欄位的名稱。 *identity_col*是**sysname**，預設值是 Null。  
  
`[ @ts_col = ] 'timestamp_col'`這是發行者端的**時間戳記**資料行名稱。 *timestamp_col*是**sysname**，預設值是 Null。  
  
`[ @filter_clause = ] 'filter_clause'`這是定義水準篩選的限制（WHERE）子句。 當輸入限制子句時，請省略 WHERE 關鍵字。 *filter_clause*是**Nvarchar （4000）**，預設值是 Null。  
  
`[ @primary_key_bitmap = ] 'primary_key_bitmap'`這是資料表中主鍵資料行的點陣圖。 *primary_key_bitmap*是**Varbinary （4000）**，沒有預設值。  
  
`[ @identity_support = ] identity_support`當使用佇列更新時，啟用和停用自動識別範圍處理。 *identity_support*是**bit**，預設值是**0**。 **0**表示不支援識別範圍， **1**會啟用自動識別範圍處理。  
  
`[ @independent_agent = ] independent_agent`指出此發行集是否有單一散發代理程式（獨立的代理程式），或是每個發行集資料庫和訂閱資料庫配對的一個散發代理程式（共用的代理程式）。 這個值反映發行者端所定義之發行集的 independent_agent 屬性值。 *independent_agent*是位，預設值是**0**。 如果是**0**，代理程式就是共用代理程式。 如果是**1**，代理程式就是獨立的代理程式。  
  
`[ @distributor = ] 'distributor'`這是散發者的名稱。 散發*者是* **sysname**，沒有預設值。  
  
`[ @pubversion = ] pubversion`指出發行者的版本。 *pubversion*是**int**，預設值是1。 **1**表示發行者版本是[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 2 或更早版本;**2**表示發行者是[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] SERVICE Pack 3 （SP3）或更新版本。 當發行者版本是[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] SP3 或更新版本時， *pubversion*必須明確設定為**2** 。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 散發代理程式會在訂閱初始化過程中使用**sp_addsynctriggers** 。 使用者通常不會執行這個預存程序，但如果使用者需要手動設定非同步訂閱，它可能很有用。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_addsynctriggers**。  
  
## <a name="see-also"></a>另請參閱  
 [異動複寫的可更新訂閱](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sp_script_synctran_commands &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
