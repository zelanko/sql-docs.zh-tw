---
title: sp_refresh_log_shipping_monitor (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_refresh_log_shipping_monitor
- sp_refresh_log_shipping_monitor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_refresh_log_shipping_monitor
ms.assetid: edefb912-31c5-4d99-9aba-06629afd0171
author: stevestein
ms.author: sstein
ms.openlocfilehash: c19f9b99173ca04e6ce15862e22a25f8a2bf06e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002504"
---
# <a name="sprefreshlogshippingmonitor-transact-sql"></a>sp_refresh_log_shipping_monitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  這個預存程序會利用指定記錄傳送代理程式的給定主要或次要伺服器所提供的最新資訊，來重新整理遠端監視器資料表。 這個程序可於主要或次要伺服器上叫用。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_refresh_log_shipping_monitor  
[ @agent_id = ] 'agent_id',  
[ @agent_type = ] 'agent_type'  
[ @database = ] 'database'  
[ @mode ] n  
```  
  
## <a name="arguments"></a>引數  
`[ @agent_id = ] 'agent_id'` 備份的主要識別碼或來複製或還原的次要識別碼。 *agent_id*已**uniqueidentifier**不能是 NULL。  
  
`[ @agent_type = ] 'agent_type'` 記錄傳送作業的類型。  
  
 0 = 備份。  
  
 1 = 複製。  
  
 2 = 還原。  
  
 *agent_type*已**tinyint**不能是 NULL。  
  
`[ @database = ] 'database'` 記錄備份或還原代理程式所使用的主要或次要資料庫。  
  
`[ @mode ] n` 指定是否要重新整理監視資料，或加以清除。 資料類型*m*是 tinyint，和支援的值為：  
  
 1 = 重新整理 (這是預設值。)  
  
 2 = 刪除  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 無。  
  
## <a name="remarks"></a>備註  
 **sp_refresh_log_shipping_monitor**重新整理**log_shipping_monitor_primary**， **log_shipping_monitor_secondary**， **log_shipping_monitor_history_detail**，並**log_shipping_monitor_error_detail**與具有尚未傳送任何工作階段資訊的資料表。 這可讓您在監視器不同步一段時間之後，將監視伺服器和主要或次要伺服器同步化。 另外，必要的話，它也可讓您清除監視伺服器的監視資訊。  
  
 **sp_refresh_log_shipping_monitor**必須從執行**主要**主要或次要伺服器上的資料庫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行此程序。  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
