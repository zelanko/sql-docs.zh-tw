---
description: MSrepl_errors (Transact-SQL)
title: MSrepl_errors (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_errors
- MSrepl_errors_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_errors system table
ms.assetid: c6e023c1-2c32-4269-8d76-e442ea309e4b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ab4195f63afdda44bb5e4abff1e27f8738903ea3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473188"
---
# <a name="msrepl_errors-transact-sql"></a>MSrepl_errors (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSrepl_errors**資料表包含具有擴充散發代理程式和合併代理程式失敗資訊的資料列。 這份資料表儲存在散發資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|錯誤的識別碼。|  
|**time**|**datetime**|發生錯誤的時間。|  
|**error_type_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**source_type_id**|**int**|錯誤來源類型識別碼。|  
|**source_name**|**Nvarchar (100) **|錯誤來源的名稱。|  
|**error_code**|**sysname**|錯誤碼。|  
|**error_text**|**ntext**|錯誤訊息。|  
|**xact_seqno**|**varbinary(16)**|執行失敗之批次的起始交易記錄序號。 只供散發代理程式使用，這是在執行失敗的批次中，第一項交易的交易記錄序號。|  
|**command_id**|**int**|執行失敗之批次的命令識別碼。 只供散發代理程式使用，這是在執行失敗的批次中，第一個命令的命令識別碼。|  
|**session_id**|**int**|發生錯誤之代理程式工作階段的識別碼。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
