---
title: sp_add_log_shipping_secondary_database （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_secondary_database
- sp_add_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_secondary_database
ms.assetid: d29e1c24-3a3c-47a4-a726-4584afa6038a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: de65ab447394d17c6400f77c58986e111839e9b4
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85879841"
---
# <a name="sp_add_log_shipping_secondary_database-transact-sql"></a>sp_add_log_shipping_secondary_database (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
`[ @secondary_database = ] 'secondary_database'`這是次要資料庫的名稱。 *secondary_database*是**sysname**，沒有預設值。  
  
`[ @primary_server = ] 'primary_server'`記錄傳送設定中之主要實例的名稱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 。 *primary_server*是**sysname** ，不能是 Null。  
  
`[ @primary_database = ] 'primary_database'`這是主伺服器上的資料庫名稱。 *primary_database*是**sysname**，沒有預設值。  
  
`[ @restore_delay = ] 'restore_delay'`在還原指定的備份檔案之前，次要伺服器等待的時間量（以分鐘為單位）。 *restore_delay*是**int** ，而且不能是 Null。 預設值為 0。  
  
`[ @restore_all = ] 'restore_all'`如果設定為1，當還原作業執行時，次要伺服器會還原所有可用的交易記錄備份。 否則，它會在還原一個檔案之後停止。 *restore_all*是**bit** ，不能是 Null。  
  
`[ @restore_mode = ] 'restore_mode'`次要資料庫的還原模式。  
  
 0 = 以 NORECOVERY 來還原記錄。  
  
 1 = 以 STANDBY 來還原記錄。  
  
 *restore*是**bit** ，不能是 Null。  
  
`[ @disconnect_users = ] 'disconnect_users'`如果設定為1，當執行還原作業時，使用者就會與次要資料庫中斷連線。 預設值 = 0。 *中斷*使用者的連線是**bit** ，不能是 Null。  
  
`[ @block_size = ] 'block_size'`以位元組為單位的大小，用來做為備份裝置的區塊大小。 *block_size*是**int** ，預設值為-1。  
  
`[ @buffer_count = ] 'buffer_count'`備份或還原作業所用的緩衝區總數。 *buffer_count*是**int** ，預設值為-1。  
  
`[ @max_transfer_size = ] 'max_transfer_size'`向備份裝置發出的最大輸入或輸出要求大小（以位元組為單位） [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 *max_transfersize*是**int** ，而且可以是 Null。  
  
`[ @restore_threshold = ] 'restore_threshold'`在產生警示之前，還原作業之間允許經過的分鐘數。 *restore_threshold*是**int** ，而且不能是 Null。  
  
`[ @threshold_alert = ] 'threshold_alert'`這是超過備份臨界值時所引發的警示。 *threshold_alert*是**int**，預設值是14420。  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'`指定超出*backup_threshold*時是否引發警示。 預設值 1 表示產生警示。 *threshold_alert_enabled*為**位**。  
  
`[ @history_retention_period = ] 'history_retention_period'`這是保留記錄的時間長度（以分鐘為單位）。 *history_retention_period*是**int**，預設值是 Null。 若未指定，則使用 14420。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_add_log_shipping_secondary_database**必須從次要伺服器的**master**資料庫中執行。 這個預存程序會執行下列動作：  
  
1.  在此預存程式之前，應該先呼叫**sp_add_log_shipping_secondary_primary** ，以初始化次要伺服器上的主要記錄傳送資料庫資訊。  
  
2.  使用提供的引數，在**log_shipping_secondary_databases**中加入次要資料庫的專案。  
  
3.  使用提供的引數，在次要伺服器的**log_shipping_monitor_secondary**中新增本機監視器記錄。  
  
4.  如果監視伺服器與次要伺服器不同，請使用提供的引數，在監視伺服器的**log_shipping_monitor_secondary**中新增監視器記錄。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行此程式。  
  
## <a name="examples"></a>範例  
 這個範例說明如何使用**sp_add_log_shipping_secondary_database**預存程式，在記錄傳送設定中，將資料庫**LogShipAdventureWorks**當做次要資料庫加入至 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 主伺服器 tribeca 有上的主資料庫。  
  
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
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
