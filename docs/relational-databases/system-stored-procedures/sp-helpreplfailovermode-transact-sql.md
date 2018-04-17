---
title: sp_helpreplfailovermode (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_helpreplfailovermode
- sp_helpreplfailovermode_TSQL
helpviewer_keywords:
- sp_helpreplfailovermode
ms.assetid: d1090e42-6840-4bf6-9aa9-327fd8987ec2
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dd85f6f45b7104c73b83b08d6fc434eb14e9c70b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpreplfailovermode-transact-sql"></a>sp_helpreplfailovermode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  顯示訂閱目前的容錯移轉模式。 這個預存程序執行於任何資料庫的訂閱者端。 如需有關容錯移轉模式的詳細資訊，請參閱[異動複寫的可更新訂閱](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpreplfailovermode [ @publisher= ] 'publisher'   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @publication = ] 'publication' ]   
    [ , [ @failover_mode_id= ] 'failover_mode_id'OUTPUT]   
    [ , [ @failover_mode = ] 'failover_mode'OUTPUT]   
```  
  
## <a name="arguments"></a>引數  
 [ **@publisher=**] **'***publisher***'**  
 這是參與這個訂閱者更新的發行者名稱。 *發行者*是**sysname**，沒有預設值。 必須已設定發行者的發行作業。  
  
 [  **@publisher_db =**] **'***publisher_db***'**  
 這是發行集資料庫的名稱。 *publisher_db*是**sysname**，沒有預設值。  
  
 [ **@publication=**] **'***publication***'**  
 這是參與這個訂閱者更新的發行集名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [  **@failover_mode_id=**] **'***failover_mode_id***' 輸出**  
 傳回容錯移轉模式的整數值，它是**輸出**參數。 *failover_mode_id*是**tinyint**預設值是**0**。 它會傳回**0**進行立即更新和**1**佇列更新。  
  
 [**@failover_mode=**] **'***failover_mode***' 輸出**  
 傳回在訂閱者端修改資料的模式。 *failover_mode*是**nvarchar （10)**預設值是 NULL。 是**輸出**參數。  
  
|Value|Description|  
|-----------|-----------------|  
|**即時運算**|立即更新：利用兩段式認可通訊協定 (2PC)，將訂閱者端的更新立即傳播到發行者。|  
|**排入佇列**|佇列更新：將訂閱者端的更新儲存在佇列中。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpreplfailovermode**其中訂閱啟用進行立即更新，佇列更新作為容錯移轉時，發生失敗時用快照式複寫或異動複寫中。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_helpreplfailovermode**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_setreplfailovermode &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md)  
  
  
