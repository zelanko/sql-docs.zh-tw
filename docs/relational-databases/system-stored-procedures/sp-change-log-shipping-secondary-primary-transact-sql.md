---
title: sp_change_log_shipping_secondary_primary （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_secondary_primary
- sp_change_log_shipping_secondary_primary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_secondary_primary
ms.assetid: 5bcb4df7-6df3-4f2b-9207-b97b5addf2a6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 94ee2f67f0f496a5dffc515c0145de127e823863
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85872660"
---
# <a name="sp_change_log_shipping_secondary_primary-transact-sql"></a>sp_change_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  變更次要資料庫設定。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_change_log_shipping_secondary_primary  
[ @primary_server = ] 'primary_server',  
[ @primary_database = ] 'primary_database',  
[, [ @backup_source_directory = ] 'backup_source_directory']  
[, [ @backup_destination_directory = ] 'backup_destination_directory']  
[, [ @file_retention_period = ] file_retention_period]  
[, [ @monitor_server_security_mode = ] monitor_server_security_mode]  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
```  
  
## <a name="arguments"></a>引數  
`[ @primary_server = ] 'primary_server'`記錄傳送設定中之主要實例的名稱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 。 *primary_server*是**sysname** ，不能是 Null。  
  
`[ @primary_database = ] 'primary_database'`這是主伺服器上的資料庫名稱。 *primary_database*是**sysname**，沒有預設值。  
  
`[ @backup_source_directory = ] 'backup_source_directory'`儲存主伺服器交易記錄備份檔案的目錄。 *backup_source_directory*是**Nvarchar （500）** ，不能是 Null。  
  
`[ @backup_destination_directory = ] 'backup_destination_directory'`將備份檔案複製到其中的次要伺服器目錄。 *backup_destination_directory*是**Nvarchar （500）** ，不能是 Null。  
  
`[ @file_retention_period = ] 'file_retention_period'`這是保留記錄的時間長度（以分鐘為單位）。 *history_retention_period*是**int**，預設值是 Null。 若未指定，則使用 14420。  
  
`[ @monitor_server_security_mode = ] 'monitor_server_security_mode'`用來連接到監視伺服器的安全性模式。  
  
 1 = Windows 驗證。  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 *monitor_server_security_mode*是**bit** ，不能是 Null。  
  
`[ @monitor_server_login = ] 'monitor_server_login'`這是用來存取監視伺服器之帳戶的使用者名稱。  
  
`[ @monitor_server_password = ] 'monitor_server_password'`這是用來存取監視伺服器之帳戶的密碼。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_change_log_shipping_secondary_primary**必須從次要伺服器的**master**資料庫中執行。 這個預存程序會執行下列動作：  
  
1.  視需要變更**log_shipping_secondary**記錄中的設定。  
  
2.  如果監視伺服器與次要伺服器不同，則會在監視伺服器上使用提供的引數來變更監視記錄**log_shipping_monitor_secondary** （如有必要）。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行此程式。  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
