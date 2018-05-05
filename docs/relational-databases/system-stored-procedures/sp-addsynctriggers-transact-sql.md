---
title: sp_addsynctriggers (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_addsynctriggers_TSQL
- sp_addsynctriggers
helpviewer_keywords:
- sp_addsynctriggers
ms.assetid: e37d0c3b-19bf-4719-9535-96ba361372b3
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 711126c199480bd1d8ef836b9b587f51db8e4552
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spaddsynctriggers-transact-sql"></a>sp_addsynctriggers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在訂閱者端建立搭配所有可更新訂閱類型 (立即、佇列和以佇列更新進行容錯移轉的立即更新) 來使用的觸發程序。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
> [!IMPORTANT]  
>  [Sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)應該用於程序，而不是**sp_addsynctrigger**。 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)包含的指令碼會產生**sp_addsynctrigger**呼叫。  
  
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
 [  **@sub_table=**] **'***sub_table***'**  
 這是訂閱者資料表的名稱。 *sub_table*是**sysname**，沒有預設值。  
  
 [  **@sub_table_owner=**] **'***sub_table_owner***'**  
 這是訂閱者資料表的擁有者名稱。 *sub_table_owner*是**sysname**，沒有預設值。  
  
 [ **@publisher=**] **'***publisher***'**  
 這是發行者伺服器的名稱。 *發行者*是**sysname**，沒有預設值。  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 這是發行者資料庫的名稱。 *publisher_db*是**sysname**，沒有預設值。 如果是 NULL，就會使用目前的資料庫。  
  
 [ **@publication=**] **'***publication***'**  
 這是發行集的名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [  **@ins_proc=**] **'***ins_proc***'**  
 這是支援在發行者端之同步交易插入的預存程序名稱。 *ins_proc*是**sysname**，沒有預設值。  
  
 [  **@upd_proc=**] **'***upd_proc***'**  
 這是支援在發行者端之同步交易更新的預存程序名稱。 *ins_proc*是**sysname**，沒有預設值。  
  
 [  **@del_proc=**] **'***del_proc***'**  
 這是支援在發行者端之同步交易刪除的預存程序名稱。 *ins_proc*是**sysname**，沒有預設值。  
  
 [  **@cftproc =** ] **'***cftproc***'**  
 這是允許佇列更新的發行集所用的自動產生程序名稱。 *cftproc*是**sysname**，沒有預設值。 如果是允許立即更新的發行集，這個值便是 NULL。 這個參數適用於允許佇列更新 (佇列更新和以佇列更新進行容錯移轉的立即更新) 的發行集。  
  
 [  **@proc_owner =** ] **'***proc_owner***'**  
 在發行者中，指定用來建立更新發行集 (佇列和/或立即) 所有自動產生的預存程序之使用者帳戶。 *proc_owner*是**sysname**沒有預設值。  
  
 [  **@identity_col=**] **'***identity_col***'**  
 這是在發行者端之識別欄位的名稱。 *identity_col*是**sysname**，預設值是 NULL。  
  
 [  **@ts_col=**] **'***timestamp_col***'**  
 名稱**時間戳記**在發行者端的資料行。 *timestamp_col*是**sysname**，預設值是 NULL。  
  
 [  **@filter_clause=**] **'***filter_clause***'**  
 這是定義水平篩選的限制 (WHERE) 子句。 當輸入限制子句時，請省略 WHERE 關鍵字。 *filter_clause*是**nvarchar （4000)**，預設值是 NULL。  
  
 [  **@primary_key_bitmap =**] **'***primary_key_bitmap***'**  
 這是資料表中之主索引鍵資料行的點陣圖。 *primary_key_bitmap*是**varbinary （4000)**，沒有預設值。  
  
 [  **@identity_support =** ] *identity_support*  
 在使用佇列更新時，啟用和停用自動識別範圍處理。 *identity_support*是**元**，預設值是**0**。 **0**表示沒有識別範圍的支援， **1**啟用自動識別範圍處理。  
  
 [  **@independent_agent =** ] *independent_agent*  
 指出這個發行集有單一散發代理程式 (獨立代理程式)，或每一組發行集資料庫和訂閱資料庫有一個散發代理程式 (共用代理程式)。 這個值反映發行者端所定義之發行集的 independent_agent 屬性值。 *independent_agent*是 bit，預設值是**0**。 如果**0**，代理程式會共用代理程式。 如果**1**，代理程式是獨立的代理程式。  
  
 [  **@distributor =** ] **'***散發者***'**  
 這是散發者的名稱。 *散發者*是**sysname**，沒有預設值。  
  
 [ **@pubversion**=] *pubversion*  
 指出發行者的版本。 *pubversion*是**int**，預設值是 1。 **1**表示發行者版本是[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 2 或更早版本。**2**表示發行者是[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]Service Pack 3 (SP3) 或更新版本。 *pubversion*必須明確設定為**2**當發行者版本是[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]SP3 或更新版本。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addsynctriggers**由散發代理程式做為訂閱初始化的一部分。 使用者通常不會執行這個預存程序，但如果使用者需要手動設定非同步訂閱，它可能很有用。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addsynctriggers**。  
  
## <a name="see-also"></a>另請參閱  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sp_script_synctran_commands &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
