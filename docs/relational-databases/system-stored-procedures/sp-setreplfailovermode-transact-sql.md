---
title: sp_setreplfailovermode （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 5b39a5fa53560abb825b303d37d111bcbd7d0886
ms.sourcegitcommit: 79e6d49ae4632f282483b0be935fdee038f69cc2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2019
ms.locfileid: "72173565"
---
# <a name="sp_setreplfailovermode-transact-sql"></a>sp_setreplfailovermode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  可讓您設定訂閱的容錯移轉作業模式，其中的訂閱啟用了以佇列更新進行容錯移轉的立即更新。 這個預存程序執行於訂閱資料庫的訂閱者端。 如需容錯移轉模式的詳細資訊，請參閱[異動複寫的可更新訂閱](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)。  
  
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
`[ @publisher = ] 'publisher'` 是發行集的名稱。 *發行*集是**sysname**，沒有預設值。 發行集必須已存在。  
  
`[ @publisher_db = ] 'publisher_db'` 是發行集資料庫的名稱。 *publisher_db*是**sysname**，沒有預設值。  
  
`[ @publication = ] 'publication'` 是發行集的名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @failover_mode = ] 'failover_mode'` 是訂用帳戶的容錯移轉模式。 *failover_mode*是**Nvarchar （10）** ，而且可以是下列其中一個值。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**立即**或**同步**|在訂閱者端進行的資料修改，在修改時會大量複製到發行者。|  
|**佇列**|資料修改會儲存在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的佇列中。|  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing 已被取代，不再受到支援。  
  
僅 `[ @override = ] override` 內部使用。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>Remarks  
 **sp_setreplfailovermode**用於已啟用訂閱的快照式複寫或異動複寫中（適用于有容錯移轉到立即更新的佇列更新），或以容錯移轉至佇列更新的立即更新。  
  
## <a name="permissions"></a>Permissions  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_setreplfailovermode**。  
  
## <a name="see-also"></a>另請參閱  
 [切換可更新之交易式訂閱的更新模式](../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
