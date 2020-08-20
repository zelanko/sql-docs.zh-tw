---
description: MSlogreader_history (Transact-SQL)
title: MSlogreader_history (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSlogreader_history_TSQL
- MSlogreader_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSlogreader_history system table
ms.assetid: 2e399fa1-3591-4c1c-96b7-7964fe82c7c4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c792ab21d4fb59df13f0cc86a2d81558b2c506a7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488768"
---
# <a name="mslogreader_history-transact-sql"></a>MSlogreader_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSlogreader_history**資料表包含與本機散發者相關聯之記錄讀取器代理程式的記錄資料列。 這份資料表儲存在散發資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|記錄讀取器代理程式的識別碼。|  
|**runstatus**|**int**|執行狀態如下：<br /><br /> 1 = 啟動。<br /><br /> 2 = 成功。<br /><br /> 3 = 進行中。<br /><br /> 4 = 閒置。<br /><br /> 5 = 重試。<br /><br /> 6 = 失敗。|  
|**start_time**|**datetime**|開始執行作業的時間。|  
|**time**|**datetime**|記錄訊息的時間。|  
|**duration**|**int**|訊息工作階段的持續時間 (以秒為單位)。|  
|**評論**|**nvarchar(255)**|訊息文字。|  
|**xact_seqno**|**varbinary(16)**|前次處理的交易序號。|  
|**delivery_time**|**int**|傳遞第一項交易的時間。|  
|**delivered_transactions**|**int**|在工作階段所傳遞的交易總數。|  
|**delivered_commands**|**int**|在工作階段所傳遞的命令總數。|  
|**average_commands**|**int**|在工作階段所傳遞的命令平均數。|  
|**delivery_rate**|**float**|平均每秒傳遞的命令數。|  
|**delivery_latency**|**int**|進入發行資料庫的命令以及被進入散發資料庫的命令，兩者之間的延遲時間 (毫秒)。|  
|**error_id**|**int**|**MSrepl_error**系統資料表中錯誤的識別碼。|  
|**timestamp**|**timestamp**|這份資料表的時間戳記資料行。|  
|**updateable_row**|**bit**|如果可以覆寫歷程記錄資料列，請設定為 **1** 。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
