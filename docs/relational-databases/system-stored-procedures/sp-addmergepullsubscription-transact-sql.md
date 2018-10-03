---
title: sp_addmergepullsubscription (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepullsubscription_TSQL
- sp_addmergepullsubscription
helpviewer_keywords:
- sp_addmergepullsubscription
ms.assetid: d63909a0-8ea7-4734-9ce8-8204d936a3e4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4e6e3a2ddd7c046051b0d7f89097c7c0a075ca6f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47659009"
---
# <a name="spaddmergepullsubscription-transact-sql"></a>sp_addmergepullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [ **@publication=**] **'***publication***'**  
 這是發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [ **@publisher=**] **'***publisher***'**  
 這是發行者的名稱。 *發行者*已**sysname**，預設值是本機伺服器名稱。 發行者必須是有效伺服器。  
  
 [  **@publisher_db =**] **'***publisher_db***'**  
 這是發行者資料庫的名稱。 *publisher_db*已**sysname**，預設值是 NULL。  
  
 [  **@subscriber_type=**] **'***subscriber_type***'**  
 這是訂閱者的類型。 *subscriber_type*已**nvarchar(15)**，而且可以是**全域**，**本機**或是**匿名**。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本中，本機訂閱稱為客訂閱，而全域訂閱稱為主訂閱。  
  
 [  **@subscription_priority=**] *subscription_priority*  
 這是訂閱優先權。 *subscription_priority*已**實際**，預設值是 NULL。 本機和匿名訂閱，是優先權就是**0.0**。 在偵測到衝突時，預設解析程式會利用優先權挑選贏的一方。 如果是全域訂閱者，訂閱優先權必須小於 100，也就是發行者的優先權。  
  
 [  **@sync_type=**] **'***sync_type***'**  
 這是訂閱同步處理類型。 *sync_type*已**nvarchar(15)**，預設值是**自動**。 可以是**自動**或是**無**。 如果**自動**，結構描述和發行資料表的初始資料傳送給 「 訂閱者 」 第一次。 如果**無**，便假設訂閱者端已有的結構描述和初始資料已發行資料表。 一律會傳送系統資料表和資料。  
  
> [!NOTE]  
>  不建議您指定的值是**無**。  
  
 [  **@description=**] **'***描述***'**  
 這是這項提取訂閱的簡要描述。 *描述*已**nvarchar(255)**，預設值是 NULL。 這個值會顯示在複寫監視器**易記名稱**資料行，可用來排序受監視發行集的訂閱。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addmergepullsubscription**用於合併式複寫。  
  
 如果使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]同步處理訂用帳戶，代理程式[sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)預存程序必須執行 「 訂閱者 」 來建立代理程式，並以與發行集同步處理的作業。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_1.sql)]  
  
 [!code-sql[HowTo#sp_addmergepullsub_websync_anon](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_2.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addmergepullsubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription_agent &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [sp_changemergepullsubscription &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
