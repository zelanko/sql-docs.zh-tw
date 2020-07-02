---
title: sp_reinitsubscription （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_reinitsubscription
- sp_reinitsubscription_TSQL
helpviewer_keywords:
- sp_reinitsubscription
ms.assetid: d56ae218-6128-4ff9-b06c-749914505c7b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8bc377c269eeb6034ebbe0e5753f2605464ecd8a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85645782"
---
# <a name="sp_reinitsubscription-transact-sql"></a>sp_reinitsubscription (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

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
`[ @publication = ] 'publication'`這是發行集的名稱。 *發行*集是**sysname**，預設值是 all。  
  
`[ @article = ] 'article'`這是發行項的名稱。 發行*項是* **sysname**，預設值是 all。 對於立即更新發行集，*文章*必須是**all**;否則，預存程式會略過發行集並報告錯誤。  
  
`[ @subscriber = ] 'subscriber'`這是訂閱者的名稱。 *訂閱者*是**sysname**，沒有預設值。  
  
`[ @destination_db = ] 'destination_db'`這是目的地資料庫的名稱。 *destination_db*是**sysname**，預設值是 all。  
  
`[ @for_schema_change = ] 'for_schema_change'`指出是否因發行集資料庫的架構變更而發生重新初始化。 *for_schema_change*是**bit**，預設值是0。 如果是**0**，只要重新初始化整個發行集，而不只是部分發行項，就會重新開機允許立即更新之發行集的使用中訂閱。 這表示會因結構描述變更而重新初始化。 如果是**1**，則在快照集代理程式執行之前，不會重新開機使用中的訂閱。  
  
`[ @publisher = ] 'publisher'`指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *publisher*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  *發行者*不應用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。  
  
`[ @ignore_distributor_failure = ] ignore_distributor_failure`即使散發者不存在或已離線，也允許重新初始化。 *ignore_distributor_failure*是**bit**，預設值是0。 如果是**0**，當散發者不存在或離線時重新初始化就會失敗。  
  
`[ @invalidate_snapshot = ] invalidate_snapshot`使現有的發行集快照集失效。 *invalidate_snapshot*是**bit**，預設值是0。 如果是**1**，就會為發行集產生新的快照集。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_reinitsubscription**用於異動複寫中。  
  
 對等異動複寫不支援**sp_reinitsubscription** 。  
  
 如果是會自動套用初始快照集且發行集不允許可更新的訂閱之訂閱，就必須在執行這個預存程序之後執行快照集代理程式，以便準備結構描述和大量複製程式，然後散發代理程式就能夠重新同步處理訂閱。  
  
 如果是會自動套用初始快照集且發行集允許可更新的訂閱之訂閱，散發代理程式會利用快照集代理程式先前所建立的大量複製程式和最新的結構描述，來重新同步處理訂閱。 如果散發代理程式不忙碌，散發代理程式會在使用者執行**sp_reinitsubscription**之後立即重新同步訂閱;否則，同步處理可能會在訊息間隔之後執行（由散發代理程式命令提示字元參數所指定： **MessageInterval**）。  
  
 **sp_reinitsubscription**不會影響以手動方式套用初始快照集的訂閱。  
  
 若要重新同步處理發行集的匿名訂閱，請傳入**all**或 Null 當做*訂閱者*。  
  
 異動複寫支援發行項層級的訂閱重新初始化。 將發行項標示重新初始化之後，在下次同步處理期間，訂閱者端會重新套用發行項的快照集。 不過，如果相同訂閱者也訂閱了相依的發行項，除非發行集中的相依發行項也在特定情況之下自動重新初始化，否則，在發行項上重新套用快照集可能會失敗：  
  
-   如果發行項的前建立命令是 'drop'，則這個發行項的基底物件之結構描述繫結檢視和結構描述繫結預存程序的發行項，也會標示重新初始化。  
  
-   如果發行項的結構描述選項包括主索引鍵之宣告參考完整性的指令碼，則基底資料表與重新初始化的發行項之基底資料表有外部索引鍵關聯性的發行項，也會標示重新初始化。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_reinittranpushsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitsubscription-tr_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員、 **db_owner**固定資料庫角色的成員，或訂閱的建立者，才能夠執行**sp_reinitsubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [重新初始化訂閱](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [重新初始化訂閱](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
