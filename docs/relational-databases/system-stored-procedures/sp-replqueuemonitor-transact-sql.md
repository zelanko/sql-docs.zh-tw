---
description: sp_replqueuemonitor (Transact-SQL)
title: sp_replqueuemonitor (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replqueuemonitor
- sp_replqueuemonitor_TSQL
helpviewer_keywords:
- sp_replqueuemonitor
ms.assetid: 6909a3f1-43a2-4df5-a6a5-9e6f347ac841
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b8b0f11e5b0f62c1e874dbeba947ea136f7ee274
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446830"
---
# <a name="sp_replqueuemonitor-transact-sql"></a>sp_replqueuemonitor (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  列出佇列 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或訊息佇列中，佇列 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新訂閱指定之發行集的佇列訊息。 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 佇列，這個預存程序便執行於訂閱資料庫的訂閱者端。 如果使用 Message Queuing，這個預存程序便執行於散發資料庫的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_replqueuemonitor [ @publisher = ] 'publisher'  
    [ , [ @publisherdb = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @tranid = ] 'tranid' ]  
    [ , [ @queuetype = ] 'queuetype' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'` 這是發行者的名稱。 *publisher* 是 **sysname**，預設值是 Null。 必須設定伺服器的發行作業。 所有發行者都是 NULL。  
  
`[ @publisherdb = ] 'publisher_db' ]` 這是發行集資料庫的名稱。 *publisher_db* 是 **sysname**，預設值是 Null。 所有發行集資料庫都是 NULL。  
  
`[ @publication = ] 'publication' ]` 這是發行集的名稱。 *發行*集是 **sysname**，預設值是 Null。 所有發行集都是 NULL。  
  
`[ @tranid = ] 'tranid' ]` 這是交易識別碼。 *tranid*是 **sysname**，預設值是 Null。 所有交易都是 NULL。  
  
`[ @queuetype = ] 'queuetype' ]` 這是儲存交易的佇列類型。 *queuetype* 是 **Tinyint** ，預設值是 **0**，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|所有佇列類型|  
|**1**|訊息佇列|  
|**2**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 佇列|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_replqueuemonitor** 用於快照式複寫或具有佇列更新訂閱的異動複寫中。 不會顯示不包含 SQL 命令的佇列訊息，或本身是跨越 SQL 命令之一部分的佇列訊息。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_replqueuemonitor**。  
  
## <a name="see-also"></a>另請參閱  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
