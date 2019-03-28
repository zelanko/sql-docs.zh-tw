---
title: sp_cleanup_log_shipping_history (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cleanup_log_shipping_history_TSQL
- sp_cleanup_log_shipping_history
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cleanup_log_shipping_history
ms.assetid: 96d236a9-1d0e-4f83-a4d3-f825b7381e46
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d5247959cacb4df4fd51275c3f826280bffbb9fd
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538480"
---
# <a name="spcleanuplogshippinghistory-transact-sql"></a>sp_cleanup_log_shipping_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  這個預存程序會根據保留期限來清除本機和監視伺服器的記錄。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_cleanup_log_shipping_history  
[ @agent_id = ] 'agent_id',  
[ @agent_type = ] 'agent_type'  
```  
  
## <a name="arguments"></a>引數  
`[ @agent_id = ] 'agent_id',` 備份的主要識別碼或來複製或還原的次要識別碼。 *agent_id*已**uniqueidentifier**不能是 NULL。  
  
`[ @agent_type = ] 'agent_type'` 記錄傳送作業的類型。 0 = 備份、1 = 複製、2 = 還原。 *agent_type*已**tinyint**不能是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 無。  
  
## <a name="remarks"></a>備註  
 **sp_cleanup_log_shipping_history**必須從執行**主要**任何記錄傳送伺服器上的資料庫。 這個預存程序會清除本機和遠端副本**log_shipping_monitor_history_detail**並**log_shipping_monitor_error_detail**根據歷程記錄保留期限。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行此程序。  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
