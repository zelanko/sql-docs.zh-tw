---
title: sp_add_log_shipping_primary_database (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_primary_database
- sp_add_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_primary_database
ms.assetid: 69531611-113f-46b5-81a6-7bf496d0353c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5af11c14c7b0bf3b8e32d503c4b77e59623ce9ff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140451"
---
# <a name="spaddlogshippingprimarydatabase-transact-sql"></a>sp_add_log_shipping_primary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  設定記錄傳送組態的主要資料庫，其中包括備份作業、本機監視記錄，以及遠端監視記錄。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_add_log_shipping_primary_database [ @database = ] 'database',   
[ @backup_directory = ] 'backup_directory',   
[ @backup_share = ] 'backup_share',   
[ @backup_job_name = ] 'backup_job_name',   
[, [ @backup_retention_period = ] backup_retention_period]  
[, [ @monitor_server = ] 'monitor_server']  
[, [ @monitor_server_security_mode = ] monitor_server_security_mode]  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
[, [ @backup_threshold = ] backup_threshold ]   
[, [ @threshold_alert = ] threshold_alert ]   
[, [ @threshold_alert_enabled = ] threshold_alert_enabled ]   
[, [ @history_retention_period = ] history_retention_period ]  
[, [ @backup_job_id = ] backup_job_id OUTPUT ]  
[, [ @primary_id = ] primary_id OUTPUT]  
[, [ @backup_compression = ] backup_compression_option ]  
  
```  
  
## <a name="arguments"></a>引數  
`[ @database = ] 'database'` 是記錄傳送主要資料庫的名稱。 *資料庫*已**sysname**，沒有預設值，不能是 NULL。  
  
`[ @backup_directory = ] 'backup_directory'` 是主要伺服器上備份資料夾的路徑。 *backup_directory*已**nvarchar(500)** ，沒有預設值，不能是 NULL。  
  
`[ @backup_share = ] 'backup_share'` 是主要伺服器上備份目錄的網路路徑。 *backup_share*已**nvarchar(500)** ，沒有預設值，不能是 NULL。  
  
`[ @backup_job_name = ] 'backup_job_name'` 是將備份複製到備份資料夾之主要伺服器上的 SQL Server Agent 作業的名稱。 *backup_job_name*已**sysname**不能是 NULL。  
  
`[ @backup_retention_period = ] backup_retention_period` 這是時間的以分鐘為單位，將記錄備份檔儲存在備份目錄中主要伺服器上長度。 *backup_retention_period*已**int**，沒有預設值，不能是 NULL。  
  
`[ @monitor_server = ] 'monitor_server'` 是監視伺服器的名稱。 *Monitor_server*已**sysname**，沒有預設值，不能是 NULL。  
  
`[ @monitor_server_security_mode = ] monitor_server_security_mode` 用來連接到監視伺服器的安全性模式。  
  
 1 = Windows 驗證。  
  
 0 =[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。 *monitor_server_security_mode&lt*已**元**不能是 NULL。  
  
`[ @monitor_server_login = ] 'monitor_server_login'` 是用來存取監視伺服器的使用者名稱。  
  
`[ @monitor_server_password = ] 'monitor_server_password'` 這是帳戶的用來存取監視伺服器密碼。  
  
`[ @backup_threshold = ] backup_threshold` 是一段時間，以分鐘為單位，在之前的最後一個備份之後*threshold_alert*就會引發錯誤。 *backup_threshold*已**int**，預設值是 60 分鐘的時間。  
  
`[ @threshold_alert = ] threshold_alert` 是，要在超出備份臨界值時產生警示。 *threshold_alert*已**int**，預設值是 14,420。  
  
`[ @threshold_alert_enabled = ] threshold_alert_enabled` 指定是否可以警示時引發*backup_threshold*超過。 預設值零 (0) 表示警示已停用，而且將不會引發。 *threshold_alert_enabled*已**元**。  
  
`[ @history_retention_period = ] history_retention_period` 這是時間的以分鐘為單位中保留記錄長度。 *history_retention_period*已**int**，預設值是 NULL。 若未指定，則使用 14420。  
  
`[ @backup_job_id = ] backup_job_id OUTPUT` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]與主要伺服器上的備份作業相關聯的代理程式作業識別碼。 *backup_job_id*已**uniqueidentifier**不能是 NULL。  
  
`[ @primary_id = ] primary_id OUTPUT` 記錄傳送組態的主要資料庫的識別碼。 *primary_id*已**uniqueidentifier**不能是 NULL。  
  
`[ @backup_compression = ] backup_compression_option` 指定是否要使用記錄傳送組態[備份壓縮](../../relational-databases/backup-restore/backup-compression-sql-server.md)。 只有在 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (或更新版本) 中才支援這個參數。  
  
 0 = 已停用。 永遠不會壓縮記錄備份。  
  
 1 = 已啟用。 一定會壓縮記錄備份。  
  
 2 = 使用的設定[檢視或設定 backup compression default 伺服器組態選項](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)。 這是預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_add_log_shipping_primary_database**必須從執行**主要**主要伺服器上的資料庫。 這個預存程序會執行下列功能：  
  
1.  會產生主要識別碼，並在資料表中加入主要資料庫的項目**log_shipping_primary_databases**使用提供的引數。  
  
2.  為停用的主要資料庫建立備份作業。  
  
3.  設定中的備份作業識別碼**log_shipping_primary_databases**備份作業的作業識別碼的項目。  
  
4.  在資料表中加入本機監視記錄**log_shipping_monitor_primary**主要伺服器上使用提供的引數。  
  
5.  如果監視伺服器不是從主要伺服器，新增一項監視記錄在**log_shipping_monitor_primary**監視伺服器使用提供的引數。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行此程序。  
  
## <a name="examples"></a>範例  
 這個範例會在記錄傳送組態中，加入 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫來做為主要資料庫。  
  
```  
DECLARE @LS_BackupJobId AS uniqueidentifier ;  
DECLARE @LS_PrimaryId AS uniqueidentifier ;  
  
EXEC master.dbo.sp_add_log_shipping_primary_database   
@database = N'AdventureWorks'   
,@backup_directory = N'c:\lsbackup'   
,@backup_share = N'\\tribeca\lsbackup'   
,@backup_job_name = N'LSBackup_AdventureWorks'   
,@backup_retention_period = 1440  
,@monitor_server = N'rockaway'   
,@monitor_server_security_mode = 1   
,@backup_threshold = 60   
,@threshold_alert = 0   
,@threshold_alert_enabled = 0   
,@history_retention_period = 1440   
,@backup_job_id = @LS_BackupJobId OUTPUT   
,@primary_id = @LS_PrimaryId OUTPUT   
,@overwrite = 1   
,@backup_compression = 0;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
