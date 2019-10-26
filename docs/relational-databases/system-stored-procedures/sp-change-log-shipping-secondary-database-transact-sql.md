---
title: sp_change_log_shipping_secondary_database （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_secondary_database
- sp_change_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_secondary_database
ms.assetid: 3ebcf2f1-980f-4543-a84b-fbaeea54eeac
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d0bd62fe3462441d4eab9d3d89bce20cf1144131
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909560"
---
# <a name="sp_change_log_shipping_secondary_database-transact-sql"></a>sp_change_log_shipping_secondary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更次要資料庫設定。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [transact-sql 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_change_log_shipping_secondary_database  
[ @secondary_database = ] 'secondary_database',  
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
`[ @restore_delay = ] 'restore_delay'` 次要伺服器在還原指定的備份檔案之前等待的時間量（以分鐘為單位）。 *restore_delay*是**int** ，不能是 Null。 預設值是 0。  
  
`[ @restore_all = ] 'restore_all'` 如果設定為1，當執行還原作業時，次要伺服器會還原所有可用的交易記錄備份。 否則，它會在還原一個檔案之後停止。 *restore_all*是**bit** ，不能是 Null。  
  
`[ @restore_mode = ] 'restore_mode'` 次要資料庫的還原模式。  
  
 0 = 以 NORECOVERY 來還原記錄。  
  
 1 = 以 STANDBY 來還原記錄。  
  
 *restore*是**bit** ，不能是 Null。  
  
`[ @disconnect_users = ] 'disconnect_users'` 如果設定為1，當執行還原作業時，使用者就會與次要資料庫中斷連線。 預設值 = 0。 *disconnect_users*是**bit** ，不能是 Null。  
  
`[ @block_size = ] 'block_size'` 用來作為備份裝置區塊大小的大小（以位元組為單位）。 *block_size*是**int** ，預設值為-1。  
  
`[ @buffer_count = ] 'buffer_count'` 備份或還原作業所用的緩衝區總數。 *buffer_count*是**int** ，預設值為-1。  
  
`[ @max_transfer_size = ] 'max_transfer_size'` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 送至備份裝置的最大輸入或輸出要求大小（以位元組為單位）。 *max_transfersize*是**int** ，而且可以是 Null。  
  
`[ @restore_threshold = ] 'restore_threshold'` 在產生警示之前允許還原作業之間經過的分鐘數。 *restore_threshold*是**int** ，不能是 Null。  
  
`[ @threshold_alert = ] 'threshold_alert'` 是超過還原臨界值時所產生的警示。 *threshold_alert*是**int**，預設值是14420。  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'` 指定超出*restore_threshold*時是否會引發警示。 1 = 已啟用；0 = 已停用。 *threshold_alert_enabled*是**bit** ，不能是 Null。  
  
`[ @history_retention_period = ] 'history_retention_period'` 是將保留歷程記錄的時間長度（以分鐘為單位）。 *history_retention_period*是**int**。如果沒有指定，將會使用1440的值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>Remarks  
 **sp_change_log_shipping_secondary_database**必須從次要伺服器的**master**資料庫中執行。 這個預存程序會執行下列動作：  
  
1.  視需要變更**log_shipping_secondary_database**記錄中的設定。  
  
2.  必要時，使用提供的引數，變更次要伺服器上**log_shipping_monitor_secondary**中的本機監視器記錄。  

## <a name="permissions"></a>[權限]  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行此程式。  
  
## <a name="examples"></a>範例  
 這個範例說明如何使用**sp_change_log_shipping_secondary_database**來更新資料庫**LogShipAdventureWorks**的次要資料庫參數。  
  
```  
EXEC master.dbo.sp_change_log_shipping_secondary_database   
 @secondary_database =  'LogShipAdventureWorks'  
,  @restore_delay = 0  
,  @restore_all = 1  
,  @restore_mode = 0  
,  @disconnect_users = 0  
,  @threshold_alert = 14420  
,  @threshold_alert_enabled = 1  
,  @history_retention_period = 14420;  
```  
  
## <a name="see-also"></a>請參閱  
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
