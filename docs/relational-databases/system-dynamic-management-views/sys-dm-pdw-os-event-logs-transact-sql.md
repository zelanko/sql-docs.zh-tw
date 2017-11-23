---
title: "sys.dm_pdw_os_event_logs (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.reviewer: 
ms.service: 
ms.component: dmv's
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: a0daa8cf-72e2-4349-8be1-d3cc0f9b1e02
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ffd9bad344ed79048a65de4139ec7c2fd44cd9c4
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwoseventlogs-transact-sql"></a>sys.dm_pdw_os_event_logs (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  會保存有關不同 Windows 事件記錄檔不同節點上。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|此記錄檔的來源應用裝置節點。<br /><br /> pdw_node_id 和 log_name 形成這個檢視的索引鍵。||  
|log_name|**nvarchar(255)**|Windows 事件記錄檔名稱。<br /><br /> pdw_node_id 和 log_name 形成這個檢視的索引鍵。||  
|log_source|**nvarchar(255)**|Windows 事件記錄檔來源名稱。||  
|event_id|**int**|事件的識別碼。 不是唯一的。||  
|event_type|**nvarchar(255)**|事件，並識別嚴重性類型。|「 資訊 」，'警告'、 'Error'|  
|event_message|**nvarchar(4000)**|事件的詳細資料。||  
|generate_time|**datetime**|建立事件的時間。||  
|write_time|**datetime**|實際事件記錄檔寫入的時間。||  
  
 這份檢視所保留的最大資料列的相關資訊，請參閱中的系統檢視的最大值 」 一節[最小和最大值 (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9)主題。  
  
## <a name="see-also"></a>請參閱＜  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
