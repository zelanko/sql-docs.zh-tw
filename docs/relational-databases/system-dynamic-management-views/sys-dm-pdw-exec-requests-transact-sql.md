---
title: sys.dm_pdw_exec_requests (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 390225cc-23e8-4051-a5f6-221e33e4c0b4
author: XiaoyuL-Preview
ms.author: xiaoyul
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: a3aa0219e1e8d0733926662b22f929fa923ae071
ms.sourcegitcommit: e4b241fd92689c2aa6e1f5e625874bd0b807dd01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/04/2019
ms.locfileid: "67564178"
---
# <a name="sysdmpdwexecrequests-transact-sql"></a>sys.dm_pdw_exec_requests (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保留目前或最近作用中的所有要求的相關資訊[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。 它會列出每個要求/查詢的一個資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|此檢視的索引鍵。 與要求相關聯的唯一數值識別碼。|在系統中的所有要求間是唯一的。|  
|session_id|**nvarchar(32)**|此查詢執行所在的工作階段相關聯的唯一數值識別碼。 請參閱[sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。||  
|status|**nvarchar(32)**|目前要求的狀態。|「 執行中 」、 「 已擱置且'、 '已完成'、 '已取消 」、 「 失敗 」。|  
|submit_time|**datetime**|已提交的要求的執行時間。|有效**datetime**小於或等於目前的時間和 start_time。|  
|start_time|**datetime**|開始要求執行時間。|已排入佇列的要求，都是 NULL否則，有效**datetime**小於或等於目前的時間。|  
|end_compile_time|**datetime**|引擎完成編譯要求的時間。|尚未; 尚未經過編譯的要求都是 NULL否則有效**datetime**小於 start_time 且小於或等於目前的時間。|
|end_time|**datetime**|時間的要求執行已完成、 失敗或已取消。|已排入佇列或作用中的要求; 是 null否則，有效**datetime**小於或等於目前的時間。|  
|total_elapsed_time|**int**|在執行中的事件，是因為啟動要求，以毫秒為單位經過的時間。|介於 0 到 start_time 和 end_time 之間的差異。</br></br> 如果 total_elapsed_time 超過整數的最大值，total_elapsed_time 仍是最大值。 這種情況會產生警告 」 的最大值已超過 」。</br></br> 以毫秒為單位的最大值等同於 24.8 天。|  
|label|**nvarchar(255)**|某些選取的查詢陳述式相關聯的選擇性標籤字串。|任何字串包含 'a-z '、' A-Z '、 ' 0-9'、 '_'。|  
|error_id|**nvarchar(36)**|如果有的話，與要求相關的錯誤的唯一識別碼。|請參閱[sys.dm_pdw_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md); 設為 NULL，如果沒有發生錯誤。|  
|database_id|**int**|明確內容 (例如，使用 DB_X) 所使用的資料庫識別碼。|請參閱中的識別碼[sys.databases &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)。|  
|command|**nvarchar(4000)**|保留由使用者提交要求的完整文字。|任何有效查詢或要求的文字。 查詢的長度超過 4000 個位元組會被截斷。|  
|resource_class|**nvarchar(20)**|此要求的資源類別。 請參閱相關**concurrency_slots_used**中[sys.dm_pdw_resource_waits &#40;-&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)。  如需有關資源類別的詳細資訊，請參閱[資源類別與工作負載管理](https://docs.microsoft.com/azure/sql-data-warehouse/resource-classes-for-workload-management) |靜態資源類別</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80</br>            </br>靜態資源類別</br>SmallRC</br>MediumRC</br>LargeRC</br>XLargeRC|
|importance|**nvarchar(32)**|已提交設定要求的重要性。 以較低重要性的要求會保留在佇列中暫止狀態，如果較高的重要性要求提交。  以高重要性的要求將會執行較早提交的較低重要性要求之前。  如需有關重要性的詳細資訊，請參閱[工作負載重要性](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-workload-importance)。  |NULL</br>低</br>below_normal</br>標準 （預設值）</br>above_normal</br>高|
|group_name| |保留供內部使用。</br>適用於：Azure SQL 資料倉儲|
|resource_allocation_percentage| |保留供內部使用。</br>適用於：Azure SQL 資料倉儲|
|result_set_cache|**bit**|詳細資料是否已完成的查詢結果快取命中 (1) 與否 (0)。|0,1|
||||
  
 這份檢視所保留的最大資料列的相關資訊，請參閱中的 [中繼資料] 區段[容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)主題。   
  
## <a name="permissions"></a>Permissions

 需要 VIEW SERVER STATE 權限。  
  
## <a name="security"></a>安全性

 sys.dm_pdw_exec_requests 不會篩選查詢結果，根據特定資料庫的權限。 具有 VIEW SERVER STATE 權限的登入可以取得結果之所有資料庫的查詢結果  
  
>[!WARNING]  
>攻擊者可用於將 sys.dm_pdw_exec_requests 擷取特定的資料庫物件的相關資訊，只要擁有 VIEW SERVER STATE 權限，以及沒有特定資料庫的權限中。  
  
## <a name="see-also"></a>另請參閱

 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md) 
