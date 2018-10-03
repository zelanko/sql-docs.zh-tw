---
title: sp_change_log_shipping_secondary_primary (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: df800e141a922250cea37eee1aeee5af6f373f7f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47650226"
---
# <a name="spchangelogshippingsecondaryprimary-transact-sql"></a>sp_change_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [ **@primary_server** =] '*primary_server*'  
 主要執行個體名稱[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]記錄傳送組態中。 *primary_server*已**sysname**不能是 NULL。  
  
 [ **@primary_database** =] '*primary_database&lt*'  
 這是主要伺服器的資料庫名稱。 *primary_database&lt*已**sysname**，沒有預設值。  
  
 [ **@backup_source_directory** = ] '*backup_source_directory*'  
 用於儲存主要伺服器之交易記錄備份檔的目錄。 *backup_source_directory*已**nvarchar(500)** 不能是 NULL。  
  
 [ **@backup_destination_directory** =] '*backup_destination_directory*'  
 備份檔要複製到其中的次要伺服器目錄。 *backup_destination_directory*已**nvarchar(500)** 不能是 NULL。  
  
 [ **@file_retention_period** =] '*file_retention_period*'  
 這是保留記錄的時間長度 (以分鐘為單位)。 *history_retention_period*已**int**，預設值是 NULL。 若未指定，則使用 14420。  
  
 [ **@monitor_server_security_mode** =] '*monitor_server_security_mode&lt*'  
 用於連接到監視伺服器的安全性模式。  
  
 1 = Windows 驗證。  
  
 0 =[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。 *monitor_server_security_mode&lt*已**元**不能是 NULL。  
  
 [ **@monitor_server_login** =] '*monitor_server_login*'  
 這是用來存取監視伺服器之帳戶的使用者名稱。  
  
 [ **@monitor_server_password** =] '*monitor_server_password*'  
 這是用於存取監視伺服器之帳戶的密碼。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_change_log_shipping_secondary_primary**必須從執行**主要**次要伺服器上的資料庫。 這個預存程序會執行下列動作：  
  
1.  在設定的變更**log_shipping_secondary**記錄。  
  
2.  如果監視伺服器不是從次要伺服器，變更監視中的資料錄**log_shipping_monitor_secondary**監視伺服器使用提供的引數，如有必要。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行此程序。  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
