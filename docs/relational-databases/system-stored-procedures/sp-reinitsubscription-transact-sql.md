---
title: sp_reinitsubscription (TRANSACT-SQL) |Microsoft 文件
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
- sp_reinitsubscription
- sp_reinitsubscription_TSQL
helpviewer_keywords:
- sp_reinitsubscription
ms.assetid: d56ae218-6128-4ff9-b06c-749914505c7b
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 233448ed17ee55bb2d2c1c2b0a906191c73d4cf6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33000685"
---
# <a name="spreinitsubscription-transact-sql"></a>sp_reinitsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  標示重新初始化訂閱。 這個預存程序執行於發送訂閱的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_reinitsubscription [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
        , [ @subscriber = ] 'subscriber'  
    [ , [ @destination_db = ] 'destination_db']  
    [ , [ @for_schema_change = ] 'for_schema_change']  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @ignore_distributor_failure = ] ignore_distributor_failure ]   
    [ , [ @invalidate_snapshot = ] invalidate_snapshot ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@publication=**] **'***publication***'**  
 這是發行集的名稱。 *發行集*是**sysname**，所有的預設值。  
  
 [  **@article=**] **'***文章***'**  
 這是發行項的名稱。 *發行項*是**sysname**，所有的預設值。 立即更新發行集*文章*必須**所有**; 否則預存程序會略過發行集，並報告錯誤。  
  
 [  **@subscriber=**] **'***訂閱者***'**  
 這是訂閱者的名稱。 *訂閱者*是**sysname**，沒有預設值。  
  
 [  **@destination_db=**] **'***destination_db***'**  
 這是目的地資料庫的名稱。 *destination_db*是**sysname**，所有的預設值。  
  
 [  **@for_schema_change=**] **'***for_schema_change***'**  
 指出是否因發行集資料庫的結構描述變更而重新初始化。 *for_schema_change*是**元**，預設值是 0。 如果**0**，只要重新初始化整個發行集，而不只是某些發行項，就會重新啟動允許立即更新的發行集的使用中訂閱。 這表示會因結構描述變更而重新初始化。 如果**1**，使用中的訂閱不會重新啟動快照集代理程式執行之前。  
  
 [  **@publisher=** ] **'***發行者***'**  
 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *發行者*是**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*不能用於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
 [  **@ignore_distributor_failure=** ] *ignore_distributor_failure*  
 即使散發者不存在或已離線，也可以進行重新初始化。 *ignore_distributor_failure*是**元**，預設值是 0。 如果**0**，如果散發者不存在或離線，重新初始化就會失敗。  
  
 [  **@invalidate_snapshot=** ] *invalidate_snapshot*  
 現有的發行集快照集失效。 *invalidate_snapshot*是**元**，預設值是 0。 如果**1**，發行集產生新的快照集。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_reinitsubscription**用於異動複寫中。  
  
 **sp_reinitsubscription**至點對點異動複寫不支援。  
  
 如果是會自動套用初始快照集且發行集不允許可更新的訂閱之訂閱，就必須在執行這個預存程序之後執行快照集代理程式，以便準備結構描述和大量複製程式，然後散發代理程式就能夠重新同步處理訂閱。  
  
 如果是會自動套用初始快照集且發行集允許可更新的訂閱之訂閱，散發代理程式會利用快照集代理程式先前所建立的大量複製程式和最新的結構描述，來重新同步處理訂閱。 散發代理程式會重新同步處理訂用帳戶的使用者執行後立即**sp_reinitsubscription**，如果 「 散發代理程式不是忙碌中; 否則同步處理可能在訊息間隔 （之後散發代理程式命令提示字元參數所指定： **MessageInterval**)。  
  
 **sp_reinitsubscription**並手動套用初始快照集是訂用帳戶沒有影響。  
  
 若要重新同步處理發行集的匿名訂閱，傳入**所有**或 NULL 做為*訂閱者*。  
  
 異動複寫支援發行項層級的訂閱重新初始化。 將發行項標示重新初始化之後，在下次同步處理期間，訂閱者端會重新套用發行項的快照集。 不過，如果相同訂閱者也訂閱了相依的發行項，除非發行集中的相依發行項也在特定情況之下自動重新初始化，否則，在發行項上重新套用快照集可能會失敗：  
  
-   如果發行項的前建立命令是 'drop'，則這個發行項的基底物件之結構描述繫結檢視和結構描述繫結預存程序的發行項，也會標示重新初始化。  
  
-   如果發行項的結構描述選項包括主索引鍵之宣告參考完整性的指令碼，則基底資料表與重新初始化的發行項之基底資料表有外部索引鍵關聯性的發行項，也會標示重新初始化。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_reinittranpushsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitsubscription-tr_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色、 成員的**db_owner**固定的資料庫角色或訂閱的建立者可以執行**sp_reinitsubscription**.  
  
## <a name="see-also"></a>另請參閱  
 [重新初始化訂閱](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [重新初始化訂閱](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
