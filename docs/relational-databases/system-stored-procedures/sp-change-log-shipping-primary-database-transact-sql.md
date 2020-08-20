---
description: sp_change_log_shipping_primary_database (Transact-SQL)
title: sp_change_log_shipping_primary_database (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_primary_database
- sp_change_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_primary_database
ms.assetid: 8c9dce6b-d2a3-4ca7-a832-8f59a5adb214
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 070065ae6e621c5ea52bf4be50ac0cc99af089f3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474488"
---
# <a name="sp_change_log_shipping_primary_database-transact-sql"></a>sp_change_log_shipping_primary_database (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  變更主要資料庫設定。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_change_log_shipping_primary_database [ @database = ] 'database'  
[, [ @backup_directory = ] 'backup_directory']   
[, [ @backup_share = ] 'backup_share']   
[, [ @backup_retention_period = ] 'backup_retention_period']  
[, [ @monitor_server_security_mode = ] 'monitor_server_security_mode']  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
[, [ @backup_threshold = ] 'backup_threshold']   
[, [ @threshold_alert = ] 'threshold_alert']   
[, [ @threshold_alert_enabled = ] 'threshold_alert_enabled']   
[, [ @history_retention_period = ] 'history_retention_period']  
[, [ @backup_compression = ] backup_compression_option ]   
```  
  
## <a name="arguments"></a>引數  
`[ @database = ] 'database'` 這是主伺服器上的資料庫名稱。 *primary_database* 是 **sysname**，沒有預設值。  
  
`[ @backup_directory = ] 'backup_directory'` 這是主伺服器上備份檔案夾的路徑。 *backup_directory* 是 **Nvarchar (500) **，沒有預設值，而且不能是 Null。  
  
`[ @backup_share = ] 'backup_share'` 這是主伺服器上備份目錄的網路路徑。 *backup_share* 是 **Nvarchar (500) **，沒有預設值，而且不能是 Null。  
  
`[ @backup_retention_period = ] 'backup_retention_period'` 這是將記錄備份檔案保留在主伺服器上備份目錄中的時間長度（以分鐘為單位）。 *backup_retention_period* 是 **int**，沒有預設值，而且不能是 Null。  
  
`[ @monitor_server_security_mode = ] 'monitor_server_security_mode'` 用來連接到監視伺服器的安全性模式。  
  
 1 = Windows 驗證。  
  
 0 = SQL Server 驗證。  
  
 *monitor_server_security_mode* 是 **bit** ，不能是 Null。  
  
`[ @monitor_server_login = ] 'monitor_server_login'` 這是用來存取監視伺服器之帳戶的使用者名稱。  
  
`[ @monitor_server_password = ] 'monitor_server_password'` 這是用來存取監視伺服器之帳戶的密碼。  
  
`[ @backup_threshold = ] 'backup_threshold'` 這是在引發 *threshold_alert* 錯誤之前最後一次備份之後的時間長度（以分鐘為單位）。 *backup_threshold* 是 **int**，預設值是60分鐘。  
  
`[ @threshold_alert = ] 'threshold_alert'` 當超出備份臨界值時要引發的警示。 *threshold_alert* 是 **int** ，不能是 Null。  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'` 指定當超出 *backup_threshold* 時是否引發警示。  
  
 1 = 已啟用。  
  
 0 = 已停用。  
  
 *threshold_alert_enabled* 是 **bit** ，不能是 Null。  
  
`[ @history_retention_period = ] 'history_retention_period'` 這是保留記錄的時間長度（以分鐘為單位）。 *history_retention_period* 為 **int**。如果未指定任何值，則會使用14420的值。  
  
`[ @backup_compression = ] backup_compression_option` 指定記錄傳送設定是否使用 [備份壓縮](../../relational-databases/backup-restore/backup-compression-sql-server.md)。 只有在 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (或更新版本) 中才支援這個參數。  
  
 0 = 已停用。 永遠不會壓縮記錄備份。  
  
 1 = 已啟用。 一定會壓縮記錄備份。  
  
 2 = 使用視圖的設定， [或設定備份壓縮預設伺服器設定選項](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)。 這是預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_change_log_shipping_primary_database** 必須從主伺服器的 **master** 資料庫中執行。 這個預存程序會執行下列動作：  
  
1.  視需要變更 **log_shipping_primary_database** 記錄中的設定。  
  
2.  必要時，使用提供的引數來變更主伺服器 **log_shipping_monitor_primary** 中的本機記錄。  
  
3.  如果監視伺服器與主伺服器不同，請視需要使用提供的引數，在監視伺服器上 **log_shipping_monitor_primary** 記錄變更。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行這個程式。  
  
## <a name="examples"></a>範例  
 此範例說明如何使用 **sp_change_log_shipping_primary_database** 來更新與主資料庫相關聯的設定 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 。  
  
```  
EXEC master.dbo.sp_change_log_shipping_primary_database   
 @database = N'AdventureWorks'   
, @backup_directory = N'c:\LogShipping'   
, @backup_share = N'\\tribeca\LogShipping'   
, @backup_retention_period = 1440   
, @backup_threshold = 60   
, @threshold_alert = 0   
, @threshold_alert_enabled = 1   
, @history_retention_period = 1440   
,@monitor_server_security_mode = 1  
,@backup_compression = 1;  
```  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [&#40;Transact-sql&#41;的系統預存程式 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [log_shipping_primary_databases &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md)  
  
  
