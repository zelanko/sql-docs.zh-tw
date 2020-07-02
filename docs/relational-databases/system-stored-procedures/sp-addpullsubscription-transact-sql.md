---
title: sp_addpullsubscription （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/09/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpullsubscription
- sp_addpullsubscription_TSQL
helpviewer_keywords:
- sp_addpullsubscription
ms.assetid: 0f4bbedc-0c1c-414a-b82a-6fd47f0a6a7f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 98c966ecb91bebb4f11db49028ecf53a885cc888
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786207"
---
# <a name="sp_addpullsubscription-transact-sql"></a>sp_addpullsubscription (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

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
`[ @publisher = ] 'publisher'`這是發行者的名稱。 *publisher*是**sysname**，沒有預設值。  

> [!NOTE]
> 伺服器名稱可指定為 `<Hostname>,<PortNumber>` 。 當您使用自訂埠在 Linux 或 Windows 上部署 SQL Server，且已停用 browser 服務時，您可能需要指定連接的埠號碼。
  
`[ @publisher_db = ] 'publisher_db'`這是發行者資料庫的名稱。 *publisher_db*是**sysname**，預設值是 Null。 Oracle 發行者會忽略*publisher_db* 。  
  
`[ @publication = ] 'publication'`這是發行集的名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @independent_agent = ] 'independent_agent'`指定此發行集是否有獨立的散發代理程式。 *independent_agent*是**Nvarchar （5）**，預設值是 TRUE。 若為**true**，則表示此發行集有獨立的散發代理程式。 如果為**false**，則表示每個發行者資料庫/訂閱者資料庫配對都有一個散發代理程式。 *independent_agent*是發行集的屬性，而且在這裡的值必須與在發行者端的值相同。  
  
`[ @subscription_type = ] 'subscription_type'`這是訂用帳戶的類型。 *subscription_type*是**Nvarchar （9）**，預設值為**anonymous**。 除非您想要建立訂閱，而不是在發行者端註冊訂閱，否則您必須指定*subscription_type*的**pull**值。 在此情況下，您必須指定**匿名**的值。 在訂閱組態期間，無法建立與發行者的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接時，需要此訂閱。  
  
`[ @description = ] 'description'`這是發行集的描述。 *description*是**Nvarchar （100）**，預設值是 Null。  
  
`[ @update_mode = ] 'update_mode'`這是更新的類型。 *update_mode*是**Nvarchar （30）**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**唯讀**（預設值）|訂閱是唯讀的。 訂閱者的任何變更都不會傳回發行者。 當訂閱者不要更新時，便應該使用這個項目。|  
|**synctran**|啟用立即更新訂閱的支援。|  
|**queued tran**|啟用佇列更新的訂閱。 資料修改可以在訂閱者端進行、儲存在佇列中，再傳播給發行者。|  
|**修復**|啟用立即更新的訂閱，且利用佇列更新來做為容錯移轉。 資料修改可以在訂閱者端進行，再立即傳播給發行者。 如果發行者和訂閱者並未連接，在訂閱者端進行的資料修改可以儲存在佇列中，直到發行者和訂閱者重新連接為止。|  
|**queued failover**|將訂閱啟用成能夠改成立即更新模式的佇列更新訂閱。 資料修改可以在訂閱者端進行，儲存在佇列中，直到重建訂閱者和發行者之間的連接為止。 當建立連續連接時，更新模式可以改成立即更新。 *不支援 Oracle 發行者*。|  
  
`[ @immediate_sync = ] immediate_sync`這是指每次執行快照集代理程式時，是否要建立或重新建立同步處理檔案。 *immediate_sync*是**bit** ，預設值是1，而且必須設定為與**sp_addpublication**中*immediate_sync*相同的值。*immediate_sync*是發行集的屬性，而且在這裡的值必須與在發行者端的值相同。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addpullsubscription**用於快照式複寫和異動複寫中。  
  
> [!IMPORTANT]  
>  對於佇列更新訂閱，請利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來連接訂閱者，以及指定不同的連接帳戶給每個訂閱者。 當建立支援佇列更新的提取訂閱時，複寫一律會將連接設定成使用 Windows 驗證 (對於提取訂閱而言，複寫無法在訂閱者端存取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證所需要的中繼資料)。 在此情況下，您應該執行[sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md) ，以便在設定訂閱之後，將連接變更為使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。  
  
 如果[MSreplication_subscriptions &#40;transact-sql&#41;](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md)資料表不存在於訂閱者端， **sp_addpullsubscription**會加以建立。 它也會將資料列加入至[MSreplication_subscriptions &#40;transact-sql&#41;](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md)資料表。 對於提取訂閱，應該先在發行者[端呼叫 sp_addsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addpullsubscription-t_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_addpullsubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [建立交易式發行集的可更新訂閱](../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md)[訂閱發佈](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addpullsubscription_agent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)   
 [sp_change_subscription_properties &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_droppullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [sp_helppullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
