---
title: sp_addpullsubscription (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/15/2017
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
- sp_addpullsubscription
- sp_addpullsubscription_TSQL
helpviewer_keywords:
- sp_addpullsubscription
ms.assetid: 0f4bbedc-0c1c-414a-b82a-6fd47f0a6a7f
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ffbadd078651118e48977bbd46b45cbf96fd6cc4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32992595"
---
# <a name="spaddpullsubscription-transact-sql"></a>sp_addpullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  新增快照式或交易式發行集的提取訂閱。 這個預存程序執行於將建立提取訂閱之資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addpullsubscription [ @publisher= ] 'publisher'  
    [ , [ @publisher_db= ] 'publisher_db' ]  
        , [ @publication= ] 'publication'  
    [ , [ @independent_agent= ] 'independent_agent' ]  
    [ , [ @subscription_type= ] 'subscription_type' ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @update_mode= ] 'update_mode' ]  
    [ , [ @immediate_sync = ] immediate_sync ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@publisher=**] **'***publisher***'**  
 這是發行者的名稱。 *發行者*是**sysname**，沒有預設值。  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 這是發行者資料庫的名稱。 *publisher_db*是**sysname**，預設值是 NULL。 *publisher_db* Oracle 發行者會忽略。  
  
 [ **@publication=**] **'***publication***'**  
 這是發行集的名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [  **@independent_agent=**] **'***independent_agent***'**  
 指定這個發行集是否有獨立的散發代理程式。 *independent_agent*是**nvarchar （5)**，預設值是 TRUE。 如果**true**，沒有獨立的散發代理程式，針對這個發行集。 如果**false**，還有一個散發代理程式，每個發行者資料庫/訂閱者資料庫配對。 *independent_agent*是發行集的屬性，而且必須具有相同的值與 「 發行者 」 在這裡。  
  
 [  **@subscription_type=**] **'***subscription_type***'**  
 這是訂閱的類型。 *subscription_type*是**nvarchar(9)**，預設值是**匿名**。 您必須指定值為**提取**如*subscription_type*，除非您想要建立訂用帳戶不在發行者端註冊訂閱。 在此情況下，您必須指定值為**匿名**。 這是必要的您無法建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連接到 「 發行者 」 在訂閱組態期間。  
  
 [  **@description=**] **'***描述***'**  
 這是發行集的描述。 *描述*是**nvarchar （100)**，預設值是 NULL。  
  
 [  **@update_mode=**] **'***update_mode***'**  
 這是更新的類型。 *update_mode*是**nvarchar （30)**，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**唯讀**（預設值）|訂閱是唯讀的。 訂閱者的任何變更都不會傳回發行者。 當訂閱者不要更新時，便應該使用這個項目。|  
|**synctran**|啟用立即更新訂閱的支援。|  
|**佇列的交易**|啟用佇列更新的訂閱。 資料修改可以在訂閱者端進行、儲存在佇列中，再傳播給發行者。|  
|**容錯移轉**|啟用立即更新的訂閱，且利用佇列更新來做為容錯移轉。 資料修改可以在訂閱者端進行，再立即傳播給發行者。 如果發行者和訂閱者並未連接，在訂閱者端進行的資料修改可以儲存在佇列中，直到發行者和訂閱者重新連接為止。|  
|**佇列的容錯移轉**|將訂閱啟用成能夠改成立即更新模式的佇列更新訂閱。 資料修改可以在訂閱者端進行，儲存在佇列中，直到重建訂閱者和發行者之間的連接為止。 當建立連續連接時，更新模式可以改成立即更新。 *不支援 Oracle 發行者*。|  
  
 [  **@immediate_sync =**] *immediate_sync*  
 每次執行快照集代理程式時，是否要建立或重新建立同步處理檔案。 *immediate_sync*是**元**預設值是 1，而且必須設定為相同的值做為*immediate_sync*中**sp_addpublication**。*immediate_sync*是發行集的屬性，而且必須具有相同的值與 「 發行者 」 在這裡。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addpullsubscription**用於快照式複寫和異動複寫。  
  
> [!IMPORTANT]  
>  對於佇列更新訂閱，請利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來連接訂閱者，以及指定不同的連接帳戶給每個訂閱者。 當建立支援佇列更新的提取訂閱時，複寫一律會將連接設定成使用 Windows 驗證 (對於提取訂閱而言，複寫無法在訂閱者端存取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證所需要的中繼資料)。 在此情況下，您應該執行[sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md)變更要使用的連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證之後的訂閱設定。  
  
 如果[MSreplication_subscriptions &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) 「 訂閱者 」 端沒有資料表**sp_addpullsubscription**會加以建立。 它也會加入資料列來[MSreplication_subscriptions &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md)資料表。 對於提取訂閱， [sp_addsubscription &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)應該先呼叫在發行者端。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addpullsubscription-t_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addpullsubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [建立提取訂閱](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create an Updatable Subscription to a Transactional Publication](../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md) [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addpullsubscription_agent &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)   
 [sp_change_subscription_properties &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_droppullsubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [sp_helppullsubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
