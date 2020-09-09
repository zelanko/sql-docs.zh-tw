---
description: sp_addqueued_artinfo (Transact-SQL)
title: sp_addqueued_artinfo (Transact-sql) |Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 16709ac2b02acf8641661831c4aee831ef95bc19
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548316"
---
# <a name="sp_addqueued_artinfo-transact-sql"></a>sp_addqueued_artinfo (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  
  
> [!IMPORTANT]  
>  應該使用 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) 程式，而不是 **sp_addqueued_artinfo**。 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) 會產生包含 **sp_addqueued_artinfo** 和 **sp_addsynctrigger** 呼叫的腳本。  
  
 在「訂閱者」端建立 [MSsubscription_articles](../../relational-databases/system-tables/mssubscription-articles-transact-sql.md) 資料表，用來追蹤發行項訂閱資訊 (佇列更新，以及將佇列更新當做容錯移轉) 進行立即更新。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
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
`[ @artid = ] 'artid'` 這是發行項識別碼的名稱。 *>artid* 是 **int**，沒有預設值  
  
`[ @article = ] 'article'` 這是要編寫腳本的發行項名稱。 *文章* 是 **sysname**，沒有預設值  
  
`[ @publisher = ] 'publisher'` 這是發行者伺服器的名稱。 *publisher* 是 **sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'` 這是發行者資料庫的名稱。 *publisher_db* 是 **sysname**，沒有預設值。  
  
`[ @publication = ] 'publication'` 這是要編寫腳本的發行集名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @dest_table = ] _'dest_table'` 這是目的地資料表的名稱。 *dest_table* 是 **sysname**，沒有預設值。  
  
 [** @owner =** ] **'**_owner_**'**  
 這是訂閱的擁有者。 *owner* 是 **sysname**，沒有預設值。  
  
`[ @cft_table = ] 'cft_table'` 本文的佇列更新衝突資料表名稱。 *cft_table*是 **sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 散發代理程式會使用**sp_addqueued_artinfo**作為訂閱初始化的一部分。 使用者通常不會執行這個預存程序，但如果使用者需要手動設定訂閱，它可能很有用。  
  
 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) ，而不是 **sp_addqueued_artinfo**。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_addqueued_artinfo**。  
  
## <a name="see-also"></a>另請參閱  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sp_script_synctran_commands &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)   
 [MSsubscription_articles &#40;Transact-sql&#41;](../../relational-databases/system-tables/mssubscription-articles-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
