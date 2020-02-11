---
title: sys.databases dm_db_rda_schema_update_status （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.dm_db_rda_schema_update_status
- sys.dm_db_rda_schema_update_status_TSQL
- dm_db_rda_schema_update_status
- dm_db_rda_schema_update_status_TSQL
helpviewer_keywords:
- sys.dm_db_rda_schema_update_status dynamic management view
ms.assetid: 364e3caa-a7c6-4be5-a029-0b19da34de3e
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 611fe9d5bea47204b655f2defe5072d2dd17be92
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67937011"
---
# <a name="stretch-database---sysdm_db_rda_schema_update_status"></a>Stretch Database-sys. dm_db_rda_schema_update_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  針對目前資料庫中每個已啟用 Stretch 之資料表的遠端資料封存，各包含一個資料列。 工作是由其工作識別碼所識別。  
  
 **dm_db_rda_schema_update_status**的範圍是目前的資料庫內容。 請確定您位於已啟用 Stretch 之資料表的資料庫內容中，而您想要查看其架構更新狀態。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|正在更新其遠端資料封存架構的本機已啟用 Stretch 之資料表的識別碼。|  
|**database_id**|**int**|包含本機已啟用 Stretch 之資料表的資料庫識別碼。|  
|**task_id**|**Bigint**|遠端資料封存架構更新工作的識別碼。|  
|**task_type**|**int**|遠端資料封存架構更新工作的類型。|  
|**task_type_desc**|**nvarchar**|遠端資料封存架構更新工作的類型描述。|  
|**task_state**|**int**|遠端資料封存架構更新工作的狀態。|  
|**task_state_des**|**nvarchar**|遠端資料封存架構更新工作的狀態原因。|  
|**start_time_utc**|**datetime**|遠端資料封存架構更新開始的 UTC 時間。|  
|**end_time_utc**|**datetime**|遠端資料封存架構更新完成的 UTC 時間。|  
|**error_number**|**int**|如果遠端資料封存架構更新失敗，則為發生之錯誤的錯誤號碼;否則為 null。|  
|**error_severity**|**int**|如果遠端資料封存架構更新失敗，則為發生之錯誤的嚴重性;否則為 null。|  
|**error_state**|**int**|如果遠端資料封存架構更新失敗，則為發生的錯誤狀態;否則為 null。 Error_state 指出發生錯誤的條件或位置。|  
  
## <a name="see-also"></a>另請參閱  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
