---
title: sp_delete_log_shipping_alert_job (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_log_shipping_alert_job
- sp_delete_log_shipping_alert_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_log_shipping_alert_job
ms.assetid: 5d6c7f07-a163-48fa-8c1f-abc252043dde
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7b2a41f6d453fd1d029426afb5753f558a73ba08
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="spdeletelogshippingalertjob-transact-sql"></a>sp_delete_log_shipping_alert_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  如果作業存在，且沒有要監視的主要或次要資料庫，便從記錄傳送監視伺服器中移除警示作業。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_delete_log_shipping_alert_job  
  
```  
  
## <a name="arguments"></a>引數  
 無。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 無。  
  
## <a name="remarks"></a>備註  
 **sp_delete_log_shipping_alert_job**必須從執行**主要**監視伺服器上的資料庫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行此程序。  
  
## <a name="examples"></a>範例  
 此範例示範執行**sp_delete_log_shipping_alert_job**刪除警示作業。  
  
```  
USE master;  
GO  
EXEC sp_delete_log_shipping_alert_job;  
```  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 & #40;SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
