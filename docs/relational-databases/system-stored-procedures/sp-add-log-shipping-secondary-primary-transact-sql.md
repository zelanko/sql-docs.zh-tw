---
title: sp_add_log_shipping_secondary_primary (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: fc2bf117e78f897102f85a7cab43295b079db12b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47824736"
---
# <a name="spaddlogshippingsecondaryprimary-transact-sql"></a>sp_add_log_shipping_secondary_primary (Transact-SQL)
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
 [ **@primary_server** =] '*primary_server*'  
 主要執行個體名稱[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]記錄傳送組態中。 *primary_server*已**sysname**不能是 NULL。  
  
 [ **@primary_database** =] '*primary_database&lt*'  
 這是主要伺服器的資料庫名稱。 *primary_database&lt*已**sysname**，沒有預設值。  
  
 [ **@backup_source_directory** = ] '*backup_source_directory*'  
 用於儲存主要伺服器之交易記錄備份檔的目錄。 *backup_source_directory*已**nvarchar(500)** 不能是 NULL。  
  
 [ **@backup_destination_directory** =] '*backup_destination_directory*'  
 備份檔要複製到其中的次要伺服器目錄。 *backup_destination_directory*已**nvarchar(500)** 不能是 NULL。  
  
 [ **@copy_job_name** = ] '*copy_job_name*'  
 用於將交易記錄備份複製到次要伺服器中，所建立之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業所用的名稱。 *copy_job_name*已**sysname**不能是 NULL。  
  
 [ **@restore_job_name** = ] '*restore_job_name*'  
 名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]將備份還原到次要資料庫的次要伺服器上的代理程式作業。 *restore_job_name&lt*已**sysname**不能是 NULL。  
  
 [ **@file_retention_period** =] '*file_retention_period*'  
 時間，以分鐘為單位備份檔案會保留在次要伺服器中所指定的路徑長度@backup_destination_directory被刪除之前的參數。 *history_retention_period*已**int**，預設值是 NULL。 若未指定，則使用 14420。  
  
 [ **@monitor_server** =] '*monitor_server*'  
 這是監視伺服器的名稱。 *Monitor_server*已**sysname**，沒有預設值，不能是 NULL。  
  
 [ **@monitor_server_security_mode** =] '*monitor_server_security_mode&lt*'  
 用於連接到監視伺服器的安全性模式。  
  
 1 = Windows 驗證。  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。  
  
 *monitor_server_security_mode&lt*已**元**不能是 NULL。  
  
 [ **@monitor_server_login** =] '*monitor_server_login*'  
 這是用來存取監視伺服器之帳戶的使用者名稱。  
  
 [ **@monitor_server_password** =] '*monitor_server_password*'  
 這是用於存取監視伺服器之帳戶的密碼。  
  
 [ **@copy_job_id** =] '*copy_job_id*' 輸出  
 次要伺服器中之複製作業的相關識別碼。 *copy_job_id*已**uniqueidentifier**不能是 NULL。  
  
 [ **@restore_job_id** =] '*restore_job_id*' 輸出  
 次要伺服器中之還原作業的相關識別碼。 *restore_job_id*已**uniqueidentifier**不能是 NULL。  
  
 [ **@secondary_id** =] '*secondary_id*' 輸出  
 記錄傳送組態中之次要伺服器的識別碼。 *secondary_id*已**uniqueidentifier**不能是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_add_log_shipping_secondary_primary**必須從執行**主要**次要伺服器上的資料庫。 這個預存程序會執行下列動作：  
  
1.  產生指定的主要伺服器和主要資料庫的次要識別碼。  
  
2.  執行下列動作：  
  
    1.  加入的項目中的次要識別碼**log_shipping_secondary**使用提供的引數。  
  
    2.  建立停用的次要識別碼的複製作業。  
  
    3.  設定的複製作業識別碼**log_shipping_secondary**複製作業的作業識別碼的項目。  
  
    4.  建立停用的次要識別碼的還原作業。  
  
    5.  在中設定的還原作業識別碼**log_shipping_secondary**的還原作業的作業識別碼的項目。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行此程序。  
  
## <a name="examples"></a>範例  
 此範例說明如何利用**sp_add_log_shipping_secondary_primary**預存程序來設定主要資料庫的資訊[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]次要伺服器上。  
  
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
  
  
