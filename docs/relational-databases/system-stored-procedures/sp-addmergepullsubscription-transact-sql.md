---
description: sp_addmergepullsubscription (Transact-SQL)
title: sp_addmergepullsubscription (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepullsubscription_TSQL
- sp_addmergepullsubscription
helpviewer_keywords:
- sp_addmergepullsubscription
ms.assetid: d63909a0-8ea7-4734-9ce8-8204d936a3e4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: af86ada2400422732d910752538de54f42b01437
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489601"
---
# <a name="sp_addmergepullsubscription-transact-sql"></a>sp_addmergepullsubscription (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  將提取訂閱加入合併式發行集中。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addmergepullsubscription [ @publication= ] 'publication'   
    [ , [ @publisher= ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @subscriber_type= ] 'subscriber_type' ]   
    [ , [ @subscription_priority= ] subscription_priority ]   
    [ , [ @sync_type= ] 'sync_type' ]   
    [ , [ @description= ] 'description' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是發行集的名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @publisher = ] 'publisher'` 這是發行者的名稱。 *Publisher* 是 **sysname**，預設值是本機伺服器名稱。 發行者必須是有效伺服器。  
  
`[ @publisher_db = ] 'publisher_db'` 這是發行者資料庫的名稱。 *publisher_db* 是 **sysname**，預設值是 Null。  
  
`[ @subscriber_type = ] 'subscriber_type'` 這是訂閱者的類型。 *subscriber_type* 是 **Nvarchar (15) **，可以是 **global**、 **local** 或 **anonymous**。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本中，本機訂閱稱為客訂閱，而全域訂閱稱為主訂閱。  
  
`[ @subscription_priority = ] subscription_priority` 這是訂用帳戶優先權。 *subscription_priority*是 **real**，預設值是 Null。 針對本機和匿名訂閱，優先權為 **0.0**。 在偵測到衝突時，預設解析程式會利用優先權挑選贏的一方。 如果是全域訂閱者，訂閱優先權必須小於 100，也就是發行者的優先權。  
  
`[ @sync_type = ] 'sync_type'` 這是訂閱同步處理類型。 *sync_type*是 **Nvarchar (15) **，預設值是 **automatic**。 可以是 **自動** 或 **無**。 如果是 **自動**，則會先將已發行資料表的架構和初始資料傳送給訂閱者。 如果 **沒有**，就會假設訂閱者已有發行資料表的架構和初始資料。 一律會傳送系統資料表和資料。  
  
> [!NOTE]  
>  不建議您將值指定為 **none**。  
  
`[ @description = ] 'description'` 這是此提取訂閱的簡短描述。 *描述*是 **Nvarchar (255) **，預設值是 Null。 複寫監視器會在 [ **易記名稱** ] 資料行中顯示這個值，可用來排序受監視發行集的訂閱。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_addmergepullsubscription** 用於合併式複寫。  
  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來同步處理訂閱，則必須在訂閱者端執行 [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) 預存程式，以建立與發行集同步處理的代理程式和作業。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_1.sql)]  
  
 [!code-sql[HowTo#sp_addmergepullsub_websync_anon](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_2.sql)]  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_addmergepullsubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription_agent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [sp_changemergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
