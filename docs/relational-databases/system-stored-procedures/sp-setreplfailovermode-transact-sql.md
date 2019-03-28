---
title: sp_setreplfailovermode & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_setreplfailovermode
- sp_setreplfailovermode_TSQL
helpviewer_keywords:
- sp_setreplfailovermode
ms.assetid: ca98a4c3-bea4-4130-88d7-79e0fd1e85f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ae89e606633fc3555745dd56fc7703ef50685468
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535220"
---
# <a name="spsetreplfailovermode-transact-sql"></a>sp_setreplfailovermode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  可讓您設定訂閱的容錯移轉作業模式，其中的訂閱啟用了以佇列更新進行容錯移轉的立即更新。 這個預存程序執行於訂閱資料庫的訂閱者端。 如需有關容錯移轉模式的詳細資訊，請參閱 <<c0> [ 異動複寫的可更新訂閱](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_setreplfailovermode [ @publisher= ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication= ] 'publication' ]  
    [ , [ @failover_mode= ] 'failover_mode' ]  
    [ , [ @override = ] override ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'` 是發行集名稱。 *發行集*已**sysname**，沒有預設值。 發行集必須已存在。  
  
`[ @publisher_db = ] 'publisher_db'` 是發行集資料庫的名稱。 *publisher_db*已**sysname**，沒有預設值。  
  
`[ @publication = ] 'publication'` 是發行集名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [**@failover_mode=**] **'***failover_mode***'**  
 這是訂閱的容錯移轉模式。 *failover_mode*已**nvarchar(10**而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**即時運算**或**同步處理**|在訂閱者端進行的資料修改，在修改時會大量複製到發行者。|  
|**queued**|資料修改會儲存在[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]佇列。|  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing 已被取代，不再受到支援。  
  
`[ @override = ] override` 僅供內部使用。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_setreplfailovermode**用於快照式複寫或異動複寫中的訂用帳戶已啟用，可能是佇列更新進行容錯移轉到立即更新，或是具有容錯移轉的立即更新排入佇列正在更新。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_setreplfailovermode**。  
  
## <a name="see-also"></a>另請參閱  
 [Switch Between Update Modes for an Updatable Transactional Subscription](../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
