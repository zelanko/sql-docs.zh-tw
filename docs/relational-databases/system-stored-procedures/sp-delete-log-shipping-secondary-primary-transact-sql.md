---
description: sp_delete_log_shipping_secondary_primary (Transact-SQL)
title: sp_delete_log_shipping_secondary_primary (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_log_shipping_secondary_primary_TSQL
- sp_delete_log_shipping_secondary_primary
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_log_shipping_secondary_primary
ms.assetid: 507fc744-73d9-4cb7-8d2a-bcff88841c6a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8eee58b97415073dcc93cd689603077151f29a73
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447304"
---
# <a name="sp_delete_log_shipping_secondary_primary-transact-sql"></a>sp_delete_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  這個預存程序會從次要伺服器中移除指定主要伺服器的相關資訊，且會從次要伺服器中移除複製作業和還原作業。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_delete_log_shipping_secondary_primary  
[ @primary_server = ] 'primary_server'  
[ @primary_database = ] 'primary_database'  
```  
  
## <a name="arguments"></a>引數  
`[ @primary_server = ] 'primary_server'` 記錄傳送設定中之主要實例的名稱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 。 *primary_server* 為 **sysname** ，而且不可以是 Null。  
  
`[ @primary_database = ] 'primary_database'` 這是主伺服器上的資料庫名稱。 *primary_database* 是 **sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 無。  
  
## <a name="remarks"></a>備註  
 **sp_delete_log_shipping_secondary_primary** 必須從次要伺服器的 **master** 資料庫中執行。 這個預存程序會執行下列動作：  
  
1.  刪除次要識別碼的複製和還原作業。  
  
2.  在 **log_shipping_secondary**中刪除專案。  
  
3.  在監視伺服器上呼叫 **sp_delete_log_shipping_alert_job** 。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行這個程式。  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
