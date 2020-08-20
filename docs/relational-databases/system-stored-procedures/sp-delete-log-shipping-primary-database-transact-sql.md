---
description: sp_delete_log_shipping_primary_database (Transact-SQL)
title: sp_delete_log_shipping_primary_database (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_log_shipping_primary_database
- sp_delete_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_log_shipping_primary_database
ms.assetid: cb1d5d00-2805-4d47-bd04-545232067345
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2b7a1e58188a9b9f3a845e465139e5a24d3fad88
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474373"
---
# <a name="sp_delete_log_shipping_primary_database-transact-sql"></a>sp_delete_log_shipping_primary_database (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  這個預存程序會移除主要資料庫的記錄傳送，其中包括備份作業及本機和遠端記錄。 當您使用 **sp_delete_log_shipping_primary_secondary**移除次要資料庫之後，才使用這個預存程式。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_delete_log_shipping_primary_database  
[ @database = ] 'database'  
```  
  
## <a name="arguments"></a>引數  
`[ @database = ] 'database'` 這是記錄傳送主資料庫的名稱。 *資料庫* 是 **sysname**，沒有預設值，而且不能是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 無。  
  
## <a name="remarks"></a>備註  
 **sp_delete_log_shipping_primary_database** 必須從主伺服器的 **master** 資料庫中執行。 這個預存程序會執行下列動作：  
  
1.  刪除指定主要資料庫的備份作業。  
  
2.  移除主伺服器 **log_shipping_monitor_primary** 中的本機監視記錄。  
  
3.  移除 **log_shipping_monitor_history_detail** 和 **log_shipping_monitor_error_detail**中的對應專案。  
  
4.  如果監視伺服器與主伺服器不同，則會移除監視伺服器上 **log_shipping_monitor_primary** 中的監視記錄。  
  
5.  移除監視伺服器上 **log_shipping_monitor_history_detail** 和 **log_shipping_monitor_error_detail** 中的對應專案。  
  
6.  移除這個主資料庫 **log_shipping_primary_databases** 中的專案。  
  
7.  在監視伺服器上呼叫 **sp_delete_log_shipping_alert_job** 。  

## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行這個程式。  
  
## <a name="examples"></a>範例  
 此範例說明如何使用 **sp_delete_log_shipping_primary_database** 刪除主資料庫 **AdventureWorks2012**。  
  
```  
EXEC master.dbo.sp_delete_log_shipping_primary_database @database = N'AdventureWorks2012';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
