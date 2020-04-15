---
title: 系統dm_pdw_exec_requests(轉用-SQL) |微軟文件
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
ms.openlocfilehash: 851c138e00300a303b1618041a16e2c38516968e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301210"
---
# <a name="sysdm_pdw_exec_requests-transact-sql"></a>系統dm_pdw_exec_requests(轉算-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存有關 當前或最近處於活動[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]狀態 的所有請求的資訊。 它列出每個請求/查詢的一行。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|此視圖的鍵。 與請求關聯的唯一數位 ID。|系統中所有請求都獨一無二。|  
|session_id|**nvarchar(32)**|與運行此查詢的工作階段關聯的唯一數位 ID。 請參閱[系統dm_pdw_exec_sessions&#40;交易-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。||  
|status|**nvarchar(32)**|請求的當前狀態。|"運行"、"暫停"、"已完成"、"已取消"、"失敗"。|  
|submit_time|**datetime**|提交請求以執行的時間。|有效**日期時間**小於或等於當前時間和start_time。|  
|start_time|**datetime**|啟動請求執行的時間。|佇列請求的 NULL;否則,有效**日期時間**小於或等於當前時間。|  
|end_compile_time|**datetime**|發動機完成編譯請求的時間。|尚未編譯的請求的 NULL;否則有效**日期時間**小於start_time,小於或等於當前時間。|
|end_time|**datetime**|請求執行完成、失敗或取消的時間。|佇列或活動請求為空;否則,有效**日期時間**小於或等於當前時間。|  
|total_elapsed_time|**int**|請求啟動以來執行時經過的時間(以毫秒為單位)。|介於 0 和start_time和end_time之間的差異之間。</br></br> 如果total_elapsed_time超過整數的最大值,total_elapsed_time將繼續為最大值。 此條件將生成警告"已超出最大值」。</br></br> 最大值(以毫秒為單位)與24.8天相同。|  
|標籤|**nvarchar(255)**|與某些 SELECT 查詢敘述關聯的可選標籤字串。|任何包含"a-z","A-Z","0-9"的字串。|  
|error_id|**恩瓦爾查爾 (36)**|與請求關聯的錯誤的唯一 ID(如果有)。|請參閱[系統dm_pdw_errors&#40;Transact-SQL&#41;;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)如果未發生錯誤,則設置為 NULL。|  
|database_id|**int**|顯式上下文(例如,使用DB_X)使用的資料庫標識碼。|請參考系統資料庫中的 ID [&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)。|  
|命令|**nvarchar(4000)**|保存使用者提交的請求的全文。|任何有效的查詢或請求文本。 超過 4000 位元組的查詢將被截斷。|  
|resource_class|**恩瓦爾查爾 (20)**|用於此請求的工作負載組。 |靜態資源類別</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80</br>            </br>靜態資源類別</br>小RC</br>中RC</br>大RC</br>XLargeRC|
|importance|**恩瓦爾查爾 (128)**|在執行時設置請求的重要性。  這是此工作負荷組和跨工作負荷組中共享資源的請求的相對重要性。  分類器中指定的重要性將覆蓋工作負載組重要性設置。</br>適用對象：Azure SQL 資料倉儲|NULL</br>low</br>below_normal</br>正常(預設)</br>above_normal</br>high|
|group_name|**sysname** |對於使用資源的請求,group_name是請求運行下的工作負荷組的名稱。  如果請求不利用資源,group_name為空。</br>適用對象：Azure SQL 資料倉儲|
|classifier_name|**sysname**|對於使用資源的請求,用於分配資源和重要性的分類器的名稱。||
|resource_allocation_percentage|**小數(5,2)**|分配給請求的資源的百分比量。</br>適用對象：Azure SQL 資料倉儲|
|result_cache_hit|**十六進位**|詳細說明已完成的查詢是否使用了結果集緩存。  </br>適用對象：Azure SQL 資料倉儲| 1 = 結果集快取 </br> 0 = 結果集快取未命中 </br> 負值 = 不使用結果集緩存的原因。  有關詳細資訊,請參閱備註部分。|
||||
  
## <a name="remarks"></a>備註 
 有關此檢視保留的最大行的資訊,請參閱[「容量限制」](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)主題中的「元資料」 部分。

 result_cache_hit是查詢使用結果集緩存的位掩碼。  此列可以是[|( 從位或)](../../t-sql/language-elements/bitwise-or-transact-sql.md)一個或多個以下值的積:  
  
|值|描述|  
|-----------|-----------------|  
|**1**|結果集快取命中|  
|-**0 x 00**|結果集快取錯過|  
|-**0x01**|結果集緩存在資料庫上禁用。|  
|-**0x02**|結果集緩存在會話上禁用。 | 
|-**0x04**|由於沒有查詢的數據源,結果集緩存被禁用。|  
|-**0x08**|由於行級安全謂詞,結果集緩存被禁用。|  
|-**0 x 10**|由於在查詢中使用系統表、臨時表或外部表,結果集緩存被禁用。|  
|-**0 x 20**|結果集緩存被禁用,因為查詢包含運行時常量、使用者定義的函數或非確定性函數。|  
|-**0 x 40**|由於估計結果集大小過大(> 100 萬行),結果集緩存被禁用。|  
|-**0 x 80**|結果集緩存被禁用,因為結果集包含大尺寸(>64kb)的行。|  
  
## <a name="permissions"></a>權限

 需要 VIEW SERVER STATE 權限。  
  
## <a name="security"></a>安全性

 sys.dm_pdw_exec_requests 不會根據特定於資料庫的許可權篩選查詢結果。 具有「查看伺服器狀態」權限的登入可以取得所有資料庫的結果查詢結果  
  
>[!WARNING]  
>攻擊者可以使用 sys.dm_pdw_exec_requests 檢索有關特定資料庫物件的資訊,只需具有「查看伺服器狀態」許可權,並且沒有特定於資料庫的許可權即可檢索。  
  
## <a name="see-also"></a>另請參閱

 [SQL 資料倉儲和並行資料主目錄動態管理檢視&#40;處理-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)
