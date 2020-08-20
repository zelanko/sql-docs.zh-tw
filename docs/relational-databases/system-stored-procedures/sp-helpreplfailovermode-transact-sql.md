---
description: sp_helpreplfailovermode (Transact-SQL)
title: sp_helpreplfailovermode (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpreplfailovermode
- sp_helpreplfailovermode_TSQL
helpviewer_keywords:
- sp_helpreplfailovermode
ms.assetid: d1090e42-6840-4bf6-9aa9-327fd8987ec2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5503291dc5011366ab6fe3b4a2d60b0a1310ba79
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489278"
---
# <a name="sp_helpreplfailovermode-transact-sql"></a>sp_helpreplfailovermode (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  顯示訂閱目前的容錯移轉模式。 這個預存程序執行於任何資料庫的訂閱者端。 如需容錯移轉模式的詳細資訊，請參閱 [異動複寫的可更新訂閱](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)。  
  
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
`[ @publisher = ] 'publisher'` 這是參與這個訂閱者更新的發行者名稱。 *publisher* 是 **sysname**，沒有預設值。 必須已設定發行者的發行作業。  
  
`[ @publisher_db = ] 'publisher_db'` 這是發行集資料庫的名稱。 *publisher_db* 是 **sysname**，沒有預設值。  
  
`[ @publication = ] 'publication'` 這是參與這個訂閱者更新的發行集名稱。 *發行*集是 **sysname**，沒有預設值。  
  
`[ @failover_mode_id = ] 'failover_mode_id' OUTPUT` 傳回容錯移轉模式的整數值，而且是 **輸出** 參數。 *failover_mode_id* 是 **Tinyint** ，預設值是 **0**。 它會傳回 **0** 以進行立即更新，並傳回 **1** 以進行佇列更新。  
  
`[ @failover_mode = ] 'failover_mode' OUTPUT` 傳回在訂閱者端進行資料修改的模式。 *failover_mode* 是 **Nvarchar (10) ** ，預設值是 Null。 是 **輸出** 參數。  
  
|值|描述|  
|-----------|-----------------|  
|**立即**|立即更新：利用兩段式認可通訊協定 (2PC)，將訂閱者端的更新立即傳播到發行者。|  
|**排隊**|佇列更新：將訂閱者端的更新儲存在佇列中。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_helpreplfailovermode** 用於快照式複寫或異動複寫中，針對已啟用佇列更新的訂用帳戶已啟用，以便在發生失敗時進行立即更新。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_helpreplfailovermode**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_setreplfailovermode &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md)  
  
  
