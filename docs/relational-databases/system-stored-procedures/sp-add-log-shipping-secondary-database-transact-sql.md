---
title: sp_add_log_shipping_secondary_database (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_secondary_database
- sp_add_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_secondary_database
ms.assetid: d29e1c24-3a3c-47a4-a726-4584afa6038a
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 70abdc5cb67beeb779af3722d3b5e7f91b923e21
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33239778"
---
# <a name="spaddlogshippingsecondarydatabase-transact-sql"></a>sp_add_log_shipping_secondary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  設定記錄傳送的次要資料庫。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_add_log_shipping_secondary_database  
[ @secondary_database = ] 'secondary_database',  
[ @primary_server = ] 'primary_server',   
[ @primary_database = ] 'primary_database',  
[, [ @restore_delay = ] 'restore_delay']  
[, [ @restore_all = ] 'restore_all']  
[, [ @restore_mode = ] 'restore_mode']  
[, [ @disconnect_users = ] 'disconnect_users']  
[, [ @block_size = ] 'block_size']  
[, [ @buffer_count = ] 'buffer_count']  
[, [ @max_transfer_size = ] 'max_transfer_size']  
[, [ @restore_threshold = ] 'restore_threshold']   
[, [ @threshold_alert = ] 'threshold_alert']   
[, [ @threshold_alert_enabled = ] 'threshold_alert_enabled']   
[, [ @history_retention_period = ] 'history_retention_period']  
```  
  
## <a name="arguments"></a>引數  
 [ **@secondary_database** =] '*secondary_database*'  
 這是次要資料庫的名稱。 *secondary_database*是**sysname**，沒有預設值。  
  
 [ **@primary_server** =] '*primary_server*'  
 主要執行個體的名稱[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]記錄傳送組態中。 *primary_server*是**sysname**不能是 NULL。  
  
 [ **@primary_database** =] '*primary_database*'  
 這是主要伺服器的資料庫名稱。 *primary_database*是**sysname**，沒有預設值。  
  
 [ **@restore_delay** = ] '*restore_delay*'  
 在還原給定的備份檔之前，次要伺服器等待的時間 (以分鐘為單位)。 *restore_delay*是**int**不能是 NULL。 預設值是 0。  
  
 [ **@restore_all** =] '*restore_all*'  
 如果設為 1，當執行還原作業時，次要伺服器會還原所有可用的交易記錄備份。 否則，它會在還原一個檔案之後停止。 *restore_all*是**元**不能是 NULL。  
  
 [ **@restore_mode** =] '*restore_mode*'  
 次要資料庫的還原模式。  
  
 0 = 以 NORECOVERY 來還原記錄。  
  
 1 = 以 STANDBY 來還原記錄。  
  
 *還原*是**元**不能是 NULL。  
  
 [ **@disconnect_users** =] '*disconnect_users*'  
 如果設為 1，當執行還原作業時，會從次要資料庫中斷使用者的連接。 預設值 = 0。 *中斷連線*users 是**元**不能是 NULL。  
  
 [ **@block_size** =] '*block_size*'  
 用來做為備份裝置區塊大小的大小 (以位元組為單位)。 *block_size*是**int**預設值為-1。  
  
 [ **@buffer_count** =] '*buffer_count*'  
 備份或還原作業所用的緩衝區總數。 *buffer_count*是**int**預設值為-1。  
  
 [ **@max_transfer_size** =] '*max_transfer_size*'  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 向備份裝置發出的最大輸入或輸出要求大小 (以位元組為單位)。 *max_transfersize*是**int**而且可以是 NULL。  
  
 [ **@restore_threshold** =] '*restore_threshold*'  
 在產生警示之前，還原作業之間所能經歷的時間 (以分鐘為單位)。 *restore_threshold*是**int**不能是 NULL。  
  
 [ **@threshold_alert** =] '*threshold_alert*'  
 這是在超出備份臨界值時，所產生的警示。 *threshold_alert*是**int**，預設值是 14,420。  
  
 [ **@threshold_alert_enabled** =] '*threshold_alert_enabled*'  
 指定是否產生警示時*backup_threshold*超過。 預設值 1 表示產生警示。 *threshold_alert_enabled*是**元**。  
  
 [ **@history_retention_period** =] '*history_retention_period*'  
 這是保留記錄的時間長度 (以分鐘為單位)。 *history_retention_period*是**int**，預設值是 NULL。 若未指定，則使用 14420。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 **sp_add_log_shipping_secondary_database**必須從執行**主要**次要伺服器上的資料庫。 這個預存程序會執行下列動作：  
  
1.  **sp_add_log_shipping_secondary_primary**應該在此初始化的主要記錄傳送次要伺服器上的資料庫資訊的預存程序之前呼叫。  
  
2.  將次要資料庫中的項目**log_shipping_secondary_databases**使用提供的引數。  
  
3.  加入本機監視記錄中的**log_shipping_monitor_secondary**次要伺服器上使用提供的引數。  
  
4.  如果監視伺服器不是從次要伺服器，會加入一項監視記錄中的**log_shipping_monitor_secondary**監視伺服器使用提供的引數。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行此程序。  
  
## <a name="examples"></a>範例  
 這個範例說明使用**sp_add_log_shipping_secondary_database**預存程序將資料庫加入**LogShipAdventureWorks**為記錄傳送組態的次要資料庫與主要資料庫[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]位於主要伺服器 TRIBECA。  
  
```  
EXEC master.dbo.sp_add_log_shipping_secondary_database   
@secondary_database = N'LogShipAdventureWorks'   
,@primary_server = N'TRIBECA'   
,@primary_database = N'AdventureWorks2012'   
,@restore_delay = 0   
,@restore_mode = 1   
,@disconnect_users = 0   
,@restore_threshold = 45     
,@threshold_alert_enabled = 0   
,@history_retention_period = 1440 ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 & #40;SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
