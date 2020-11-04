---
description: 'sys.dm_pdw_exec_requests (Transact-sql) '
title: sys.dm_pdw_exec_requests (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/05/2019
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
ms.openlocfilehash: 8816e2ca5872da55193fab016a459a461359c742
ms.sourcegitcommit: 985e2e8e494badeac6d6b652cd35765fd9c12d80
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/04/2020
ms.locfileid: "93328583"
---
# <a name="sysdm_pdw_exec_requests-transact-sql"></a>sys.dm_pdw_exec_requests (Transact-sql) 

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  保存目前或最近使用中的所有要求的相關資訊 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。 它會針對每個要求/查詢列出一個資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|此視圖的索引鍵。 與要求相關聯的唯一數值識別碼。|系統中的所有要求都是唯一的。|  
|session_id|**nvarchar(32)**|與執行此查詢的會話相關聯的唯一數值識別碼。 請參閱 [sys.dm_pdw_exec_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。||  
|status|**nvarchar(32)**|要求的目前狀態。|「執行中」、「已暫停」、「已完成」、「已取消」、「失敗」。|  
|submit_time|**datetime**|提交要求以執行的時間。|有效的 **日期時間** 小於或等於目前的時間和 start_time。|  
|start_time|**datetime**|開始執行要求的時間。|如果是佇列的要求，則為 Null;否則，有效的 **日期時間** 小於或等於目前的時間。|  
|end_compile_time|**datetime**|引擎完成要求編譯的時間。|Null 代表尚未編譯的要求;否則，有效的 **日期時間** 小於 start_time，且小於或等於目前的時間。|
|end_time|**datetime**|要求執行完成、失敗或已取消的時間。|若為已排入佇列或使用中的要求，為 Null否則，有效的 **日期時間** 會小於或等於目前的時間。|  
|total_elapsed_time|**int**|自開始要求以來經過的時間（以毫秒為單位）。|介於0和 submit_time 與 end_time 之間的差異。</br></br> 如果 total_elapsed_time 超過整數的最大值，total_elapsed_time 將會繼續成為最大值。 這種狀況會產生「已超過最大值」的警告。</br></br> 以毫秒為單位的最大值是與24.8 天相同。|  
|label|**nvarchar(255)**|與某些 SELECT 查詢語句相關聯的選用標籤字串。|任何包含 ' a-z '、' A-z '、' 0-9 '、' _ ' 的字串。|  
|error_id|**Nvarchar (36)**|與要求相關聯之錯誤的唯一識別碼（如果有的話）。|請參閱 [sys.dm_pdw_errors &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md);如果未發生任何錯誤，則設定為 Null。|  
|database_id|**int**|明確內容 (所使用的資料庫識別碼，例如，使用 DB_X) 。|請參閱 [sys. 資料庫中的識別碼 &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)。|  
|命令|**nvarchar(4000)**|保存使用者提交要求的完整文字。|任何有效的查詢或要求文字。 超過4000個位元組的查詢會被截斷。|  
|resource_class|**Nvarchar (20)**|用於此要求的工作負載群組。 |靜態資源類別</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80</br>            </br>靜態資源類別</br>SmallRC</br>MediumRC</br>LargeRC</br>XLargeRC|
|importance|**nvarchar(128)**|要求執行的重要性設定。  這是此工作負載群組中的要求以及共用資源的工作負載群組之間的相對重要性。  分類器中指定的重要性會覆寫工作負載群組的重要性設定。</br>適用於：Azure Synapse Analytics|NULL</br>low</br>below_normal</br>一般 (預設) </br>above_normal</br>high|
|group_name|**sysname** |針對利用資源的要求，group_name 是執行要求的工作負載群組的名稱。  如果要求不使用資源，group_name 為 null。</br>適用於：Azure Synapse Analytics|
|classifier_name|**sysname**|針對利用資源的要求，用於指派資源和重要性的分類器名稱。||
|resource_allocation_percentage|**decimal (5，2)**|配置給要求的資源數量百分比。</br>適用於：Azure Synapse Analytics|
|result_cache_hit|**int**|詳細說明已完成的查詢是否使用結果集快取。  </br>適用於：Azure Synapse Analytics| 1 = 結果集快取點擊 </br> 0 = 結果集快取遺漏 </br> 負整數值 = 未使用結果集快取的原因。  如需詳細資訊，請參閱備註一節。|
|client_correlation_id|**nvarchar(255)**|用戶端會話的選擇性使用者定義名稱。  若要為會話設定，請呼叫 sp_set_session_coNtext ' client_correlation_id '，' <CorrelationIDName> '。  執行 `SELECT SESSION_CONTEXT(N'client_correlation_id')` 以取得其值。|
||||

## <a name="remarks"></a>備註 
 如需此視圖所保留之最大資料列的相關資訊，請參閱「 [容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 」主題中的「中繼資料」一節。

Result_cache_hit 資料行中的負整數值是無法快取查詢結果集之所有套用原因的點陣圖值。  此資料行可以是下列一或多個值的 [| (位或) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) 產品：  
  
|值            |描述  |  
|-----------------|-----------------|  
|**1**|結果集快取點擊|  
|**0x00** ( **0** ) |結果集快取遺漏|  
|-**0x01** ( **-1** ) |資料庫上的結果集快取已停用。|  
|-**0x02** ( **-2** ) |會話上的結果集快取已停用。 | 
|-**0x04** ( **-4** ) |結果集快取已停用，因為查詢沒有任何資料來源。|  
|-**0x08** ( **-8** ) |因為資料列層級安全性述詞，所以已停用結果集快取。|  
|-**0x10** ( **-16** ) |結果集快取已停用，因為在查詢中使用系統資料表、臨時表或外部資料表。|  
|-**0x20** ( **-32** ) |結果集快取已停用，因為查詢包含執行時間常數、使用者定義函數或不具決定性的函數。|  
|-**0x40** ( **-64** ) |結果集快取已停用，因為估計的結果集大小為 >10GB。|  
|-**0x80** ( **-128** )  |結果集快取已停用，因為結果集所包含的資料列大小很大 ( # B0 64kb) 。|  
|-**0x100** ( **-256** )  |結果集快取已停用，因為使用細微的動態資料遮罩。|  

## <a name="permissions"></a>權限

 需要 VIEW SERVER STATE 權限。  
  
## <a name="security"></a>安全性

 sys.dm_pdw_exec_requests 不會根據資料庫特定的許可權來篩選查詢結果。 具有 VIEW SERVER STATE 許可權的登入可以取得所有資料庫的結果查詢結果  
  
>[!WARNING]  
>攻擊者可以使用 sys.dm_pdw_exec_requests 來取得特定資料庫物件的相關資訊，方法是直接取得 VIEW SERVER STATE 許可權，並不具有資料庫特定的許可權。  
  
## <a name="see-also"></a>另請參閱

 [Azure Synapse Analytics 和平行處理資料倉儲動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)
