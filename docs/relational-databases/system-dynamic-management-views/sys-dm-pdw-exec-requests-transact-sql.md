---
title: sys.databases dm_pdw_exec_requests （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 4f4ebcbf84da7d899b4d4cbd861cfb2ae3f75863
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "82087558"
---
# <a name="sysdm_pdw_exec_requests-transact-sql"></a>sys.databases dm_pdw_exec_requests （Transact-sql）

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存目前或最近在中作用中的所有[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]要求的相關資訊。 它會針對每個要求/查詢列出一個資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|此視圖的索引鍵。 與要求相關聯的唯一數值識別碼。|在系統的所有要求中都是唯一的。|  
|session_id|**nvarchar(32)**|與執行此查詢的會話相關聯的唯一數值識別碼。 請參閱[dm_pdw_exec_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。||  
|status|**nvarchar(32)**|要求的目前狀態。|「執行中」、「已暫停」、「已完成」、「已取消」、「失敗」。|  
|submit_time|**datetime**|提交要求以執行的時間。|有效的**日期時間**小於或等於目前的時間，並 start_time。|  
|start_time|**datetime**|開始執行要求的時間。|佇列要求為 Null;否則，有效的**日期時間**就會小於或等於目前的時間。|  
|end_compile_time|**datetime**|引擎完成編譯要求的時間。|Null 表示尚未編譯的要求;否則，有效的**日期時間**小於 start_time，且小於或等於目前的時間。|
|end_time|**datetime**|要求執行完成、失敗或已取消的時間。|針對已佇列或作用中的要求，則為 Null;否則，有效的**日期時間**就會小於或等於目前的時間。|  
|total_elapsed_time|**int**|自要求開始後執行所經過的時間（以毫秒為單位）。|介於0和 start_time 與 end_time 之間的差異。</br></br> 如果 total_elapsed_time 超過整數的最大值，total_elapsed_time 會繼續成為最大值。 此狀況會產生「已超過最大值」的警告。</br></br> 最大值（以毫秒為單位）與24.8 天相同。|  
|標籤|**nvarchar(255)**|與某些 SELECT 查詢語句相關聯的選擇性標籤字串。|包含 ' a-z '、' A-z '、' 0-9 '、' _ ' 的任何字串。|  
|error_id|**Nvarchar （36）**|與要求相關聯之錯誤的唯一識別碼（如果有的話）。|請參閱[dm_pdw_errors &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md);如果未發生錯誤，則設為 Null。|  
|database_id|**int**|明確內容所使用之資料庫的識別碼（例如，使用 DB_X）。|如[&#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)，請參閱 sys.databases 中的識別碼。|  
|命令|**nvarchar(4000)**|保留使用者提交之要求的完整文字。|任何有效的查詢或要求文字。 長度超過4000個位元組的查詢會被截斷。|  
|resource_class|**Nvarchar （20）**|用於此要求的工作負載群組。 |靜態資源類別</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80</br>            </br>靜態資源類別</br>SmallRC</br>MediumRC</br>LargeRC</br>XLargeRC|
|importance|**nvarchar(128)**|要求執行的重要性設定。  這是此工作負載群組中的要求與共用資源的工作負載群組之間的相對重要性。  分類器中指定的重要性會覆寫工作負載群組的重要性設定。</br>適用對象：Azure SQL 資料倉儲|NULL</br>low</br>below_normal</br>normal （預設值）</br>above_normal</br>high|
|group_name|**sysname** |對於使用資源的要求，group_name 是執行要求之工作負載群組的名稱。  如果要求未利用資源，group_name 是 null。</br>適用對象：Azure SQL 資料倉儲|
|classifier_name|**sysname**|針對使用資源的要求，用於指派資源和重要性的分類器名稱。||
|resource_allocation_percentage|**decimal （5，2）**|配置給要求的資源數量百分比。</br>適用對象：Azure SQL 資料倉儲|
|result_cache_hit|**十六進位**|詳細說明已完成的查詢是否使用結果集快取。  </br>適用對象：Azure SQL 資料倉儲| 1 = 結果集快取點擊 </br> 0 = 結果集快取遺漏 </br> 負值 = 未使用結果集快取的原因。  如需詳細資訊，請參閱備註一節。|
||||
  
## <a name="remarks"></a>備註 
 如需此視圖所保留之最大資料列的詳細資訊，請參閱[容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)主題中的 Metadata 一節。

 Result_cache_hit 是查詢使用結果集快取的位元遮罩。  此資料行可以是[|（位 OR）](../../t-sql/language-elements/bitwise-or-transact-sql.md)下列其中一個或多個值的乘積：  
  
|值|描述|  
|-----------|-----------------|  
|**1**|結果集快取點擊|  
|-**0x00**|結果集快取遺漏|  
|-**0x01**|資料庫上的結果集快取已停用。|  
|-**0x02**|會話上的結果集快取已停用。 | 
|-**0x04**|結果集快取已停用，因為沒有查詢的資料來源。|  
|-**0x08**|結果集快取已停用，因為資料列層級安全性述詞。|  
|-**0x10**|結果集快取已停用，因為在查詢中使用系統資料表、臨時表或外部資料表。|  
|-**0x20**|結果集快取已停用，因為查詢包含執行時間常數、使用者定義函數或不具決定性的函數。|  
|-**0x40**|結果集快取已停用，因為估計的結果集大小為 >10GB。|  
|-**0x80**|結果集快取已停用，因為結果集包含大小龐大（>64kb）的資料列。|  
  
## <a name="permissions"></a>權限

 需要 VIEW SERVER STATE 權限。  
  
## <a name="security"></a>安全性

 dm_pdw_exec_requests 不會根據資料庫特定的許可權來篩選查詢結果。 具有 VIEW SERVER STATE 許可權的登入可以取得所有資料庫的結果查詢結果  
  
>[!WARNING]  
>攻擊者可以使用 dm_pdw_exec_requests sys.databases 來抓取特定資料庫物件的相關資訊，方法是直接擁有 VIEW SERVER STATE 許可權，而不具有資料庫特定的許可權。  
  
## <a name="see-also"></a>另請參閱

 [SQL 資料倉儲和平行處理資料倉儲動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)
