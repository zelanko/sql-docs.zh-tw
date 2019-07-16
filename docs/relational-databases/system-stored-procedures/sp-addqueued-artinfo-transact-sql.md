---
title: sp_addqueued_artinfo (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addqueued_artinfo
- sp_addqueued_artinfo_TSQL
helpviewer_keywords:
- sp_addqueued_artinfo
ms.assetid: decdb6eb-3dcd-4053-a21d-fd367c3fbafb
author: stevestein
ms.author: sstein
ms.openlocfilehash: a0f94fbf686e9b9bd9fd1b6780b298c661ce42f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031016"
---
# <a name="spaddqueuedartinfo-transact-sql"></a>sp_addqueued_artinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  
  
> [!IMPORTANT]  
>  [Sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)應該用於程序，而不是**sp_addqueued_artinfo**。 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)產生的指令碼，其中包含**sp_addqueued_artinfo**並**sp_addsynctrigger**呼叫。  
  
 會建立[MSsubscription_articles](../../relational-databases/system-tables/mssubscription-articles-transact-sql.md)用來追蹤文章的訂用帳戶資訊 （佇列更新和以佇列更新進行容錯移轉的立即更新） 的訂閱者端的資料表。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addqueued_artinfo [ @artid= ] 'artid'  
        , [ @article= ] 'article'  
        , [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @dest_table= ] 'dest_table'  
        , [ @owner = ] 'owner'  
        , [ @cft_table= ] 'cft_table'  
```  
  
## <a name="arguments"></a>引數  
`[ @artid = ] 'artid'` 是發行項識別碼的名稱 *artid&lt*已**int**，沒有預設值  
  
`[ @article = ] 'article'` 是要編寫指令碼的發行項的名稱。 *發行項*已**sysname**，沒有預設值  
  
`[ @publisher = ] 'publisher'` 是發行者伺服器的名稱。 *發行者*已**sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'` 是發行者資料庫的名稱。 *publisher_db*已**sysname**，沒有預設值。  
  
`[ @publication = ] 'publication'` 是要編寫指令碼的發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
`[ @dest_table = ] _'dest_table'` 是目的地資料表的名稱。 *dest_table*已**sysname**，沒有預設值。  
  
 [ **@owner =** ] **'** _owner_ **'**  
 這是訂閱的擁有者。 *擁有者*已**sysname**，沒有預設值。  
  
`[ @cft_table = ] 'cft_table'` 這篇文章的佇列更新衝突資料表名稱。 *cft_table*已**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addqueued_artinfo**正由 「 散發代理程式做為訂閱初始化的一部分。 使用者通常不會執行這個預存程序，但如果使用者需要手動設定訂閱，它可能很有用。  
  
 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)而非**sp_addqueued_artinfo**。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addqueued_artinfo**。  
  
## <a name="see-also"></a>另請參閱  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sp_script_synctran_commands &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)   
 [MSsubscription_articles &#40;Transact SQL&#41;](../../relational-databases/system-tables/mssubscription-articles-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
