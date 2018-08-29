---
title: sp_delete_log_shipping_primary_database (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
manager: craigg
ms.openlocfilehash: 302cdeb85ad475354d26a988580283db57415a40
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43023574"
---
# <a name="spdeletelogshippingprimarydatabase-transact-sql"></a>sp_delete_log_shipping_primary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  這個預存程序會移除主要資料庫的記錄傳送，其中包括備份作業及本機和遠端記錄。 您已移除使用次要資料庫之後，才能使用此預存程序**sp_delete_log_shipping_primary_secondary**。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_delete_log_shipping_primary_database  
[ @database = ] 'database'  
```  
  
## <a name="arguments"></a>引數  
 [  **@database =** ] '*資料庫*'  
 這是記錄傳送主要資料庫的名稱。 *資料庫*已**sysname**，沒有預設值，不能是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 無。  
  
## <a name="remarks"></a>備註  
 **sp_delete_log_shipping_primary_database**必須從執行**主要**主要伺服器上的資料庫。 這個預存程序會執行下列動作：  
  
1.  刪除指定主要資料庫的備份作業。  
  
2.  移除在本機監視記錄**log_shipping_monitor_primary**主要伺服器上。  
  
3.  中的對應項目中移除**log_shipping_monitor_history_detail**並**log_shipping_monitor_error_detail**。  
  
4.  如果監視伺服器不是從主要伺服器，會移除中的監視資料錄**log_shipping_monitor_primary**監視伺服器上。  
  
5.  中的對應項目中移除**log_shipping_monitor_history_detail**並**log_shipping_monitor_error_detail**監視伺服器上。  
  
6.  中的項目中移除**log_shipping_primary_databases**此主要資料庫。  
  
7.  呼叫**sp_delete_log_shipping_alert_job**監視伺服器上。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行此程序。  
  
## <a name="examples"></a>範例  
 此範例說明如何利用**sp_delete_log_shipping_primary_database**以刪除主要資料庫**AdventureWorks2012**。  
  
```  
EXEC master.dbo.sp_delete_log_shipping_primary_database @database = N'AdventureWorks2012';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
