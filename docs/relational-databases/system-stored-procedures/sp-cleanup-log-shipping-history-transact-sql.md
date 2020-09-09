---
description: sp_cleanup_log_shipping_history (Transact-SQL)
title: sp_cleanup_log_shipping_history (Transact-sql) |Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 987f9ff64b26bbc40ca4c93e20175014ba09e031
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543610"
---
# <a name="sp_cleanup_log_shipping_history-transact-sql"></a>sp_cleanup_log_shipping_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  這個預存程序會根據保留期限來清除本機和監視伺服器的記錄。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_cleanup_log_shipping_history  
[ @agent_id = ] 'agent_id',  
[ @agent_type = ] 'agent_type'  
```  
  
## <a name="arguments"></a>引數  
`[ @agent_id = ] 'agent_id',` 備份的主要識別碼或複製或還原的次要識別碼。 *agent_id* 是 **uniqueidentifier** ，不能是 Null。  
  
`[ @agent_type = ] 'agent_type'` 記錄傳送作業的類型。 0 = 備份、1 = 複製、2 = 還原。 *agent_type* 是 **Tinyint** ，不能是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 無。  
  
## <a name="remarks"></a>備註  
 **sp_cleanup_log_shipping_history** 必須從任何記錄傳送伺服器上的 **master** 資料庫執行。 這個預存程式會根據記錄保留期限，清除 **log_shipping_monitor_history_detail** 和 **log_shipping_monitor_error_detail** 的本機和遠端複本。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行這個程式。  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
