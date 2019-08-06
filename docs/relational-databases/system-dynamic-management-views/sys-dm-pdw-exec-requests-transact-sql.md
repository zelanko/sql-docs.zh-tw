---
title: _pdw_exec_requests (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 390225cc-23e8-4051-a5f6-221e33e4c0b4
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 72af3975378b2450e51b3880e8814705bb514c1a
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811404"
---
# <a name="sysdm_pdw_exec_requests-transact-sql"></a>sys.dm_pdw_exec_requests (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存目前或最近在中作用中的所有[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]要求的相關資訊。 它會針對每個要求/查詢列出一個資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|此視圖的索引鍵。 與要求相關聯的唯一數值識別碼。|在系統的所有要求中都是唯一的。|  
|session_id|**nvarchar(32)**|與執行此查詢的會話相關聯的唯一數值識別碼。 請參閱[sys.databases _pdw_exec_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。||  
|status|**nvarchar(32)**|要求的目前狀態。|「執行中」、「已暫停」、「已完成」、「已取消」、「失敗」。|  
|submit_time|**datetime**|提交要求以執行的時間。|有效的**日期時間**小於或等於目前的時間和 start_time。|  
|start_time|**datetime**|開始執行要求的時間。|佇列要求為 Null;否則, 有效的**日期時間**就會小於或等於目前的時間。|  
|end_compile_time|**datetime**|引擎完成編譯要求的時間。|Null 表示尚未編譯的要求;否則, 有效的**日期時間**小於 start_time, 且小於或等於目前的時間。|
|end_time|**datetime**|要求執行完成、失敗或已取消的時間。|針對已佇列或作用中的要求, 則為 Null;否則, 有效的**日期時間**就會小於或等於目前的時間。|  
|total_elapsed_time|**int**|自要求開始後執行所經過的時間 (以毫秒為單位)。|介於0和 start_time 與 end_time 之間的差異。</br></br> 如果 total_elapsed_time 超過整數的最大值, total_elapsed_time 將會繼續成為最大值。 此狀況會產生「已超過最大值」的警告。</br></br> 最大值 (以毫秒為單位) 與24.8 天相同。|  
|label|**nvarchar(255)**|與某些 SELECT 查詢語句相關聯的選擇性標籤字串。|包含 ' a-z '、' A-z '、' 0-9 '、' _ ' 的任何字串。|  
|error_id|**nvarchar(36)**|與要求相關聯之錯誤的唯一識別碼 (如果有的話)。|請參閱[sys.databases _pdw_errors &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md);如果未發生錯誤, 則設為 Null。|  
|database_id|**int**|明確內容所使用之資料庫的識別碼 (例如, 使用 DB_X)。|請參閱[Sys.databases &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)中的 ID。|  
|command|**nvarchar(4000)**|保留使用者提交之要求的完整文字。|任何有效的查詢或要求文字。 長度超過4000個位元組的查詢會被截斷。|  
|resource_class|**nvarchar(20)**|此要求的資源類別。 請參閱[sys.databases _pdw_resource_waits &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)中的相關**concurrency_slots_used** 。  如需資源類別的詳細資訊, 請參閱[資源類別 & 工作負載管理](https://docs.microsoft.com/azure/sql-data-warehouse/resource-classes-for-workload-management) |靜態資源類別</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80</br>            </br>靜態資源類別</br>SmallRC</br>MediumRC</br>LargeRC</br>XLargeRC|
|importance|**nvarchar(32)**|提交要求時所使用的重要性設定。 如果提交的重要性較高的要求, 則重要性較低的要求會持續排入已暫停狀態。  較高重要性的要求會在稍早提交的重要性要求之前執行。  如需重要性的詳細資訊, 請參閱[工作負載重要性](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-workload-importance)。  |NULL</br>low</br>below_normal</br>normal (預設值)</br>above_normal</br>high|
|group_name| |保留供內部使用。</br>適用於：Azure SQL 資料倉儲|
|resource_allocation_percentage| |保留供內部使用。</br>適用於：Azure SQL 資料倉儲|
|result_set_cache|**bit**|詳細說明完成的查詢是否為結果快取點擊 (1) 或不是 (0)。|0、1|
||||
  
 如需此視圖所保留之最大資料列的詳細資訊, 請參閱[容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)主題中的 Metadata 一節。   
  
## <a name="permissions"></a>Permissions

 需要 VIEW SERVER STATE 權限。  
  
## <a name="security"></a>安全性

 _pdw_exec_requests 不會根據資料庫特定的許可權來篩選查詢結果。 具有 VIEW SERVER STATE 許可權的登入可以取得所有資料庫的結果查詢結果  
  
>[!WARNING]  
>攻擊者可以使用 _pdw_exec_requests 來抓取特定資料庫物件的相關資訊, 方法是直接擁有 VIEW SERVER STATE 許可權, 而不具有資料庫特定的許可權。  
  
## <a name="see-also"></a>另請參閱

 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md) 
