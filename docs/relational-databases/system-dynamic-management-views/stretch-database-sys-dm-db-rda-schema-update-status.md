---
title: sys.dm_db_rda_schema_update_status (TRANSACT-SQL) |Microsoft Docs
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 930e717767c44f5d8151cd94c29f9b6aaa205fa4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47755796"
---
# <a name="stretch-database---sysdmdbrdaschemaupdatestatus"></a>Stretch Database-sys.dm_db_rda_schema_update_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  包含遠端資料封存每個已啟用 Stretch 之資料表目前的資料庫中每個結構描述更新工作的一個資料列。 工作是由其工作識別碼識別。  
  
 **dm_db_rda_schema_update_status**範圍為目前的資料庫內容。 請確定您是在您要查看結構描述更新狀態的已啟用 Stretch 之資料表的資料庫內容。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|正在更新遠端資料封存結構描述的本機已啟用 Stretch 之資料表的識別碼。|  
|**database_id**|**int**|包含區域的已啟用 Stretch 之資料表的資料庫識別碼。|  
|**task_id**|**bigint**|遠端資料封存結構描述更新工作的識別碼。|  
|**task_type**|**int**|遠端資料封存結構描述更新工作的類型。|  
|**task_type_desc**|**nvarchar**|遠端資料封存結構描述更新工作之型別的描述。|  
|**task_state**|**int**|遠端資料封存結構描述更新工作的狀態。|  
|**task_state_des**|**nvarchar**|遠端資料封存結構描述更新工作狀態的描述。|  
|**start_time_utc**|**datetime**|遠端資料封存已開始的結構描述更新的 UTC 時間。|  
|**end_time_utc**|**datetime**|已完成的遠端資料封存結構描述更新的 UTC 時間。|  
|**error_number**|**int**|如果遠端資料封存結構描述更新失敗，發生錯誤的錯誤號碼否則為 null。|  
|**error_severity**|**int**|如果遠端資料封存結構描述更新失敗，發生錯誤的嚴重性否則為 null。|  
|**error_state**|**int**|如果遠端資料封存結構描述更新失敗，發生錯誤的狀態否則為 null。 Error_state 指示的條件或發生錯誤的位置。|  
  
## <a name="see-also"></a>另請參閱  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
