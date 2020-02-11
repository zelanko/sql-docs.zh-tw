---
title: sp_add_log_shipping_secondary_primary （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_secondary_primary_TSQL
- sp_add_log_shipping_secondary_primary
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_secondary_primary
ms.assetid: bfbbbee2-c255-4a59-a963-47d6e980a8e2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 155f59426e8167d5d888f3890089dd4b2ea3bf7c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "72909689"
---
# <a name="sp_add_log_shipping_secondary_primary-transact-sql"></a>sp_add_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  設定主要資訊、加入本機和遠端監視器連結，以及在次要伺服器上建立所指定主要資料庫的複製和還原作業。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_add_log_shipping_secondary_primary  
 [ @primary_server = ] 'primary_server',   
[ @primary_database = ] 'primary_database',  
[ @backup_source_directory = ] 'backup_source_directory' ,   
[ @backup_destination_directory = ] 'backup_destination_directory'  
[ @copy_job_name = ] 'copy_job_name'  
[ @restore_job_name = ] 'restore_job_name'  
[, [ @file_retention_period = ] 'file_retention_period']  
[, [ @monitor_server = ] 'monitor_server']  
[, [ @monitor_server_security_mode = ] 'monitor_server_security_mode']  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
[, [ @copy_job_id = ] 'copy_job_id' OUTPUT ]  
[, [ @restore_job_id = ] 'restore_job_id' OUTPUT ]  
[, [ @secondary_id = ] 'secondary_id' OUTPUT]  
```  
  
## <a name="arguments"></a>引數  
`[ @primary_server = ] 'primary_server'`記錄傳送設定[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]中之主要實例的名稱。 *primary_server*是**sysname** ，不能是 Null。  
  
`[ @primary_database = ] 'primary_database'`這是主伺服器上的資料庫名稱。 *primary_database*是**sysname**，沒有預設值。  
  
`[ @backup_source_directory = ] 'backup_source_directory'`儲存主伺服器交易記錄備份檔案的目錄。 *backup_source_directory*是**Nvarchar （500）** ，不能是 Null。  
  
`[ @backup_destination_directory = ] 'backup_destination_directory'`將備份檔案複製到其中的次要伺服器目錄。 *backup_destination_directory*是**Nvarchar （500）** ，不能是 Null。  
  
`[ @copy_job_name = ] 'copy_job_name'`要用來建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業的名稱，以便將交易記錄備份複製到次要伺服器。 *copy_job_name*是**sysname** ，不能是 Null。  
  
`[ @restore_job_name = ] 'restore_job_name'`這是次要伺服器上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的代理程式作業名稱，可將備份還原至次要資料庫。 *restore_job_name*是**sysname** ，不能是 Null。  
  
`[ @file_retention_period = ] 'file_retention_period'`在刪除之前，備份檔案在@backup_destination_directory參數所指定的路徑中保留在次要伺服器上的時間長度（以分鐘為單位）。 *history_retention_period*是**int**，預設值是 Null。 若未指定，則使用 14420。  
  
`[ @monitor_server = ] 'monitor_server'`這是監視伺服器的名稱。 *Monitor_server*是**sysname**，沒有預設值，而且不能是 Null。  
  
`[ @monitor_server_security_mode = ] 'monitor_server_security_mode'`用來連接到監視伺服器的安全性模式。  
  
 1 = Windows 驗證。  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。  
  
 *monitor_server_security_mode*是**bit** ，不能是 Null。  
  
`[ @monitor_server_login = ] 'monitor_server_login'`這是用來存取監視伺服器之帳戶的使用者名稱。  
  
`[ @monitor_server_password = ] 'monitor_server_password'`這是用來存取監視伺服器之帳戶的密碼。  
  
`[ @copy_job_id = ] 'copy_job_id' OUTPUT`與次要伺服器上的複製作業相關聯的識別碼。 *copy_job_id*是**uniqueidentifier** ，不能是 Null。  
  
`[ @restore_job_id = ] 'restore_job_id' OUTPUT`與次要伺服器上的還原作業相關聯的識別碼。 *restore_job_id*是**uniqueidentifier** ，不能是 Null。  
  
`[ @secondary_id = ] 'secondary_id' OUTPUT`記錄傳送設定中次要伺服器的識別碼。 *secondary_id*是**uniqueidentifier** ，不能是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_add_log_shipping_secondary_primary**必須從次要伺服器的**master**資料庫中執行。 這個預存程序會執行下列動作：  
  
1.  產生指定的主要伺服器和主要資料庫的次要識別碼。  
  
2.  執行下列動作：  

    1.  使用提供的引數，在**log_shipping_secondary**中新增次要識別碼的專案。  
  
    2.  建立停用的次要識別碼的複製作業。  
  
    3.  將**log_shipping_secondary**專案中的複製作業識別碼設定為複製作業的作業識別碼。  
  
    4.  建立停用的次要識別碼的還原作業。  
  
    5.  將**log_shipping_secondary**專案中的還原作業識別碼設定為還原作業的作業識別碼。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行此程式。  
  
## <a name="examples"></a>範例  
 這個範例說明如何使用**sp_add_log_shipping_secondary_primary**預存程式來設定次要伺服器上主資料庫[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]的資訊。  
  
```  
EXEC master.dbo.sp_add_log_shipping_secondary_primary   
@primary_server = N'TRIBECA'   
,@primary_database = N'AdventureWorks'   
,@backup_source_directory = N'\\tribeca\LogShipping'   
,@backup_destination_directory = N''   
,@copy_job_name = N''   
,@restore_job_name = N''   
,@file_retention_period = 1440   
,@monitor_server = N'ROCKAWAY'   
,@monitor_server_security_mode = 1   
,@copy_job_id = @LS_Secondary__CopyJobId OUTPUT   
,@restore_job_id = @LS_Secondary__RestoreJobId OUTPUT   
,@secondary_id = @LS_Secondary__SecondaryId OUTPUT ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
