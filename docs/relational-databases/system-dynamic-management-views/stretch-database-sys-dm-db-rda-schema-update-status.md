---
title: sys.dm_db_rda_schema_update_status (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_rda_schema_update_status
- sys.dm_db_rda_schema_update_status_TSQL
- dm_db_rda_schema_update_status
- dm_db_rda_schema_update_status_TSQL
helpviewer_keywords:
- sys.dm_db_rda_schema_update_status dynamic management view
ms.assetid: 364e3caa-a7c6-4be5-a029-0b19da34de3e
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2bd3a2c4cf0edc6eddc4e0d1dc56f947d1e263a7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="stretch-database---sysdmdbrdaschemaupdatestatus"></a>Stretch Database-sys.dm_db_rda_schema_update_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  包含一個資料列的每個結構描述更新工作的目前資料庫中的每個已啟用 Stretch 的資料表遠端資料封存。 工作會依其工作識別碼識別。  
  
 **dm_db_rda_schema_update_status**範圍是目前資料庫內容。 請確定您已啟用 Stretch 的資料表，您想要查看結構描述更新狀態的資料庫內容中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|正在更新其遠端資料封存結構描述的本機已啟用 Stretch 的資料表識別碼。|  
|**database_id**|**int**|包含本機已啟用 Stretch 之資料表的資料庫識別碼。|  
|**task_id**|**bigint**|遠端資料封存結構描述更新工作的識別碼。|  
|**task_type**|**int**|遠端資料封存結構描述更新工作的類型。|  
|**task_type_desc**|**nvarchar**|遠端資料封存結構描述更新工作類型的描述。|  
|**task_state**|**int**|遠端資料封存結構描述更新工作的狀態。|  
|**task_state_des**|**nvarchar**|遠端資料封存結構描述更新工作狀態的描述。|  
|**start_time_utc**|**datetime**|遠端資料封存結構描述更新已開始的 UTC 時間。|  
|**end_time_utc**|**datetime**|已完成的遠端資料封存結構描述更新的 UTC 時間。|  
|**error_number**|**int**|如果遠端資料封存結構描述更新失敗，發生; 之錯誤的錯誤號碼否則為 null。|  
|**error_severity**|**int**|如果遠端資料封存結構描述更新失敗，發生; 之錯誤的嚴重性否則為 null。|  
|**error_state**|**int**|如果遠端資料封存結構描述更新失敗，發生; 之錯誤的狀態否則為 null。 Error_state 表示的條件或發生錯誤的位置。|  
  
## <a name="see-also"></a>另請參閱  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
