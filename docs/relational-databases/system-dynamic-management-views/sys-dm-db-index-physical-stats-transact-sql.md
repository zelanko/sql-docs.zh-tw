---
title: sys.dm_db_index_physical_stats (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_index_physical_stats
- sys.dm_db_index_physical_stats_TSQL
- sys.dm_db_index_physical_stats
- dm_db_index_physical_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_index_physical_stats dynamic management function
- fragmentation [SQL Server]
ms.assetid: d294dd8e-82d5-4628-aa2d-e57702230613
caps.latest.revision: 95
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f5e548a6ef4a01cd88a33c015ff2567639c91c62
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmdbindexphysicalstats-transact-sql"></a>sys.dm_db_index_physical_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中指定資料表或檢視之資料和索引的大小和片段資訊。 如果是索引，則針對每個分割區中每個層級的 B 型樹狀目錄，各傳回一個資料列。 如果是堆積，則針對每個分割區中的 IN_ROW_DATA 配置單位，各傳回一個資料列。 如果是大型物件 (LOB) 資料，則針對每個分割區中的 LOB_DATA 配置單位，各傳回一個資料列。 如果資料表中有資料列溢位資料，則針對每個分割區中的 ROW_OVERFLOW_DATA 配置單位，各傳回一個資料列。 不傳回 xVelocity 記憶體最佳化資料行存放區索引的相關資訊。  
  
> [!IMPORTANT]
> 如果您查詢**sys.dm_db_index_physical_stats**裝載 Alwayson 的伺服器執行個體[讀取的次要複本](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)，您可能會遇到 REDO 封鎖問題。 這是因為此動態管理檢視會取得指定使用者資料表或檢視表的 IS 鎖定，並因此而封鎖了對該使用者資料表或檢視表之 X 鎖定的 REDO 執行緒要求。  
  
 **sys.dm_db_index_physical_stats**不會傳回記憶體最佳化索引的相關資訊。 記憶體最佳化索引用法的相關資訊，請參閱[sys.dm_db_xtp_index_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md)。  
  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.dm_db_index_physical_stats (   
    { database_id | NULL | 0 | DEFAULT }  
  , { object_id | NULL | 0 | DEFAULT }  
  , { index_id | NULL | 0 | -1 | DEFAULT }  
  , { partition_number | NULL | 0 | DEFAULT }  
  , { mode | NULL | DEFAULT }  
)  
```  
  
## <a name="arguments"></a>引數  
 *database_id* |NULL |0 |預設值  
 資料庫的識別碼。 *database_id*是**smallint**。 有效的輸入為資料庫的識別碼、NULL、0 或 DEFAULT。 預設值是 0。 NULL、0 和 DEFAULT 是這個內容中的對等值。  
  
 請指定 NULL 來傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中之所有資料庫的資訊。 如果您指定 NULL *database_id*，您也必須指定為 NULL *object_id*， *index_id*，和。  
  
 內建函式[DB_ID](../../t-sql/functions/db-id-transact-sql.md)可以指定。 在不指定資料庫名稱的情況下使用 DB_ID 時，目前資料庫的相容性層級必須是 90 或 90 以上。  
  
 *object_id* |NULL |0 |預設值  
 這是索引所在之資料表或檢視表的物件識別碼。 *@object_id* 是 **int**。  
  
 有效的輸入為資料表和檢視表的識別碼、NULL、0 或 DEFAULT。 預設值是 0。 NULL、0 和 DEFAULT 是這個內容中的對等值。 從[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，有效的輸入也會包含 service broker 佇列名稱或佇列內部的資料表名稱。 預設參數會套用時 （也就是所有物件，所有的索引，依此類推），結果集中包含的所有佇列的片段資訊。  
  
 指定 NULL 來傳回指定之資料庫中的所有資料表和檢視表的資訊。 如果您指定 NULL *object_id*，您也必須指定為 NULL *index_id*和。  
  
 *index_id* | 0 |NULL |-1 |預設值  
 這是索引的識別碼。 *index_id*是**int**。有效輸入如下的索引 0 的識別碼，如果*object_id*是堆積，NULL，-1 或預設值。 預設值為-1。 NULL、-1，且預設值是在此內容中的對等值。  
  
 請指定 NULL 來傳回基底資料表或檢視表的所有索引資訊。 如果您指定 NULL *index_id*，您也必須指定為 NULL 。  
  
  |NULL |0 |預設值  
 這是物件的分割區編號。 是**int**。有效輸入如下： *partion_number*的索引或堆積，NULL、 0 或 DEFAULT。 預設值是 0。 NULL、0 和 DEFAULT 是這個內容中的對等值。  
  
 請指定 NULL 來傳回主控物件之所有分割區的相關資訊。  
  
 是以 1 為基礎。 非資料分割索引或堆積將設為 1。  
  
 *模式*|NULL |預設值  
 這是模式的名稱。 *模式*指定用來取得統計資料的掃描層級。 *模式*是**sysname**。 有效輸入為 DEFAULT、NULL、LIMITED、SAMPLED 或 DETAILED。 預設值 (NULL) 是 LIMITED。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|database_id|**smallint**|資料表或檢視表的資料庫識別碼。|  
|object_id|**int**|索引所在之資料表或檢視表的物件識別碼。|  
|index_id|**int**|索引的索引識別碼。<br /><br /> 0 = 堆積。|  
|partition_number|**int**|在主控物件內，以 1 為基底的分割區編號；資料表、檢視表或索引。<br /><br /> 1 = 非分割區的索引或堆積。|  
|index_type_desc|**nvarchar(60)**|索引類型的描述：<br /><br /> HEAP<br /><br /> CLUSTERED INDEX<br /><br /> NONCLUSTERED INDEX<br /><br /> PRIMARY XML INDEX<br /><br /> SPATIAL INDEX<br /><br /> XML INDEX<br /><br /> 資料行存放區對應的索引 （內部）<br /><br /> 資料行存放區 DELETEBUFFER 索引 （內部）<br /><br /> 資料行存放區 DELETEBITMAP 索引 （內部）|  
|hobt_id|**bigint**|堆積或 B 型樹狀目錄的索引或資料分割的識別碼。<br /><br /> 除了傳回的 hobt_id 的使用者定義的索引，這也會傳回內部的資料行存放區索引的 hobt_id。|  
|alloc_unit_type_desc|**nvarchar(60)**|配置單位類型的描述：<br /><br /> IN_ROW_DATA<br /><br /> LOB_DATA<br /><br /> ROW_OVERFLOW_DATA<br /><br /> 如果是 LOB_DATA 配置單位包含儲存在類型的資料行的資料**文字**， **ntext**，**映像**， **varchar （max)**， **nvarchar （max)**， **varbinary （max)**，和**xml**。 如需詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)。<br /><br /> ROW_OVERFLOW_DATA 配置單位包含儲存在類型的資料行的資料**varchar （n)**， **nvarchar （n)**， **varbinary**，和**sql_variant**已被發送非資料列。|  
|index_depth|**tinyint**|索引層級的數目。<br /><br /> 1 = 堆積，或 LOB_DATA 或 ROW_OVERFLOW_DATA 配置單位。|  
|index_level|**tinyint**|索引的目前層級。<br /><br /> 如果是索引分葉層級、堆積和 LOB_DATA 或 ROW_OVERFLOW_DATA 配置單位，則為 0。<br /><br /> 如果是非分葉索引層級，則大於 0。 *index_level*是最高根層級的索引。<br /><br /> 索引的非分葉層級只會處理時*模式*= DETAILED。|  
|avg_fragmentation_in_percent|**float**|IN_ROW_DATA 配置單位中，索引的邏輯片段或是堆積的範圍片段。<br /><br /> 其值以百分比表示，而且會考量多個檔案。 如需邏輯和範圍片段的定義，請參閱＜備註＞一節。<br /><br /> 如果是 LOB_DATA 和 ROW_OVERFLOW_DATA 配置單位，則為 0。<br /><br /> NULL 堆積，則*模式*= SAMPLED。|  
|fragment_count|**bigint**|IN_ROW_DATA 配置單位分葉層級中的片段數目。 如需有關片段的詳細資訊，請參閱＜備註＞一節。<br /><br /> 如果是索引的非分葉層級，以及 LOB_DATA 或 ROW_OVERFLOW_DATA 配置單位，則為 NULL。<br /><br /> NULL 堆積，則*模式*= SAMPLED。|  
|avg_fragment_size_in_pages|**float**|IN_ROW_DATA 配置單位的分葉層級中，一個片段的平均頁數。<br /><br /> 如果是索引的非分葉層級，以及 LOB_DATA 或 ROW_OVERFLOW_DATA 配置單位，則為 NULL。<br /><br /> NULL 堆積，則*模式*= SAMPLED。|  
|page_count|**bigint**|索引或資料頁總數。<br /><br /> 如果是索引，則為 IN_ROW_DATA 配置單位中，B 型樹狀目錄目前層級的總索引頁數。<br /><br /> 如果是堆積，則為 IN_ROW_DATA 配置單位中的總資料頁數。<br /><br /> 如果是 LOB_DATA 或 ROW_OVERFLOW_DATA 配置單位，則為配置單位中的總頁數。|  
|avg_page_space_used_in_percent|**float**|所有頁面所用之可用資料儲存空間的平均百分比。<br /><br /> 如果是索引，則為 IN_ROW_DATA 配置單位中 B 型樹狀目錄目前層級的平均數。<br /><br /> 如果是堆積，則為 IN_ROW_DATA 配置單位中所有資料頁的平均數。<br /><br /> 如果是 LOB_DATA 或 ROW_OVERFLOW DATA 配置單位，則為配置單位中所有頁面的平均數。<br /><br /> NULL*模式*= LIMITED。|  
|record_count|**bigint**|總記錄數。<br /><br /> 如果是索引，則為 IN_ROW_DATA 配置單位中，B 型樹狀目錄目前層級的總記錄數。<br /><br /> 如果是堆積，則為 IN_ROW_DATA 配置單位中的總記錄數。<br /><br /> **注意：**是堆積，從此函數傳回的記錄數目可能不符合執行選取的計數所傳回的資料列數目 (\*) 針對該堆積。 這是因為一個資料列可能包含數筆記錄。 例如，在某些更新情況下，單一的堆積資料列可能有一筆轉送記錄以及一筆當做更新作業結果的轉送記錄。 同時，在 LOB_DATA 儲存體中，會將多數大型的 LOB 資料列分割為多筆記錄。<br /><br /> 如果是 LOB_DATA 或 ROW_OVERFLOW_DATA 配置單位，則為完整配置單位中的總記錄數。<br /><br /> NULL*模式*= LIMITED。|  
|ghost_record_count|**bigint**|配置單位中，準刪除清除工作準備要移除的準刪除記錄數。<br /><br /> 如果是 IN_ROW_DATA 配置單位中索引的非分葉層級，則為 0。<br /><br /> NULL*模式*= LIMITED。|  
|version_ghost_record_count|**bigint**|配置單位中未完成之快照集隔離交易所保留的準刪除記錄數。<br /><br /> 如果是 IN_ROW_DATA 配置單位中索引的非分葉層級，則為 0。<br /><br /> NULL*模式*= LIMITED。|  
|min_record_size_in_bytes|**int**|記錄大小下限 (以位元組為單位)。<br /><br /> 如果是索引，則為 IN_ROW_DATA 配置單位中 B 型樹狀目錄目前層級的記錄大小下限。<br /><br /> 如果是堆積，則為 IN_ROW_DATA 配置單位中的記錄大小下限。<br /><br /> 如果是 LOB_DATA 或 ROW_OVERFLOW_DATA 配置單位，則為完整配置單位中的記錄大小下限。<br /><br /> NULL*模式*= LIMITED。|  
|max_record_size_in_bytes|**int**|記錄大小上限 (以位元組為單位)。<br /><br /> 如果是索引，則為 IN_ROW_DATA 配置單位中 B 型樹狀目錄目前層級的記錄大小上限。<br /><br /> 如果是堆積，則為 IN_ROW_DATA 配置單位中的記錄大小上限。<br /><br /> 如果是 LOB_DATA 或 ROW_OVERFLOW_DATA 配置單位，則為完整配置單位中的記錄大小上限。<br /><br /> NULL*模式*= LIMITED。|  
|avg_record_size_in_bytes|**float**|記錄大小平均值 (以位元組為單位)。<br /><br /> 如果是索引，則為 IN_ROW_DATA 配置單位中 B 型樹狀目錄目前層級的平均記錄大小。<br /><br /> 如果是堆積，則為 IN_ROW_DATA 配置單位中的平均記錄大小。<br /><br /> 如果是 LOB_DATA 或 ROW_OVERFLOW_DATA 配置單位，則為完整配置單位中的平均記錄大小。<br /><br /> NULL*模式*= LIMITED。|  
|forwarded_record_count|**bigint**|在堆積中，有指向另一個資料位置之轉送指標的記錄數目 (此狀態發生於更新期間，原始位置的空間不足以儲存新資料列時)。<br /><br /> 如果是 IN_ROW_DATA 配置單位以外的任何堆積配置單位，則為 NULL。<br /><br /> NULL 堆積，則*模式*= LIMITED。|  
|compressed_page_count|**bigint**|壓縮的頁面數。<br /><br /> 如果是堆積，新配置的頁面不會使用 PAGE 壓縮方式。 堆積會在兩個特殊情況下使用 PAGE 壓縮方式：大量匯入資料或是重建堆積時。 造成頁面配置的一般 DML 作業將不會使用 PAGE 壓縮方式。 當 compressed_page_count 值成長到大於您要的臨界值時，重建堆積。<br /><br /> 如果是具有叢集索引的資料表，compressed_page_count 值會指示 PAGE 壓縮的效能。|  
|hobt_id|bigint|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 透過 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /><br /> 只有資料行存放區索引，這是內部的資料行存放區資料分割的資料會追蹤的資料列集的識別碼。 資料列集是儲存為堆積，則資料或二進位樹狀目錄。 它們有相同的索引識別碼，做為父資料行存放區索引。 如需詳細資訊，請參閱[sys.internal_partitions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md)。<br /><br /> 如果為 NULL|  
|column_store_delete_buffer_state|tinyint|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 透過 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /><br /> 0 = NOT_APPLICABLE<br /><br /> 1 = OPEN<br /><br /> 2 = 清空<br /><br /> 3 = 排清<br /><br /> 4 = 淘汰<br /><br /> 5 = 已備妥|  
|column_store_delete_buff_state_desc||**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 透過 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /><br /> NOT_APPLICABLE – 父索引不是資料行存放區索引。<br /><br /> OPEN – deleters 並用掃描器。<br /><br /> 水管 – 清空 deleters 但掃描器仍然使用它。<br /><br /> 排清 – 緩衝區已關閉，並刪除點陣圖正在寫入緩衝區中的資料列。<br /><br /> 淘汰 – 已關閉的刪除緩衝區中的資料列寫入為刪除的點陣圖，但因為掃描器仍在使用它緩衝區沒有被截斷。 新的掃描程式不需要使用淘汰的緩衝區，因為開啟的緩衝區已足夠。<br /><br /> 已準備好 – 此刪除緩衝區可供使用。|  
  
## <a name="remarks"></a>備註  
 sys.dm_db_index_physical_stats 動態管理函數會取代 DBCC SHOWCONTIG 陳述式。  
  
## <a name="scanning-modes"></a>掃描模式  
 執行該函數的模式決定了取得該函數所用之統計資料所執行的掃描層級。 *模式*指定為 LIMITED、 SAMPLED 或 DETAILED。 此函數會周遊構成資料表或索引之指定分割區的配置單位頁面鏈結。 sys.dm_db_index_physical_stats 只需要一個意圖共用 (IS) 資料表鎖定，不論它執行的模式。  
  
 LIMITED 模式是最快的模式，而且可以掃描最少的頁數。 若是索引，僅會掃描 B 型樹狀目錄的父層級頁 (亦即分葉層級上面的頁面)。 若是堆積，則會檢查相關聯的 PFS 和 IAM 頁面，並以 LIMITED 模式掃描堆積的資料頁面。  
  
 在 LIMITED 模式下，compressed_page_count 是 NULL，因為 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 只會掃描 B 型樹狀目錄的非分葉頁面以及堆積的 IAM 和 PFS 頁面。 使用 SAMPLED 模式可取得 compressed_page_count 的預估的值，並使用 DETAILED 的模式可取得 compressed_page_count 的實際值。 SAMPLED 模式會傳回統計資料，該統計資料是根據索引或堆積中所有頁面之百分之 1 的取樣。 SAMPLED 模式的結果應該被視為近似。 如果索引或堆積的頁面少於 10,000 頁，則改以 DETAILED 模式取代 SAMPLED。  
  
 DETAILED 模式會掃描所有的頁面，並且傳回所有的統計資料。  
  
 從 LIMITED 到 DETAILED 的模式會愈來愈慢，因為每個模式執行的工作愈來愈多。 若要快速測量資料表或索引的大小或片段層級，請使用 LIMITED 模式。 它是最快速的模式，而且不會針對索引的 IN_ROW_DATA 配置單位中每個非分葉層級，各傳回一個資料列。  
  
## <a name="using-system-functions-to-specify-parameter-values"></a>使用系統函數指定參數值  
 您可以使用[!INCLUDE[tsql](../../includes/tsql-md.md)]函式[DB_ID](../../t-sql/functions/db-id-transact-sql.md)和[OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md)至指定的值*database_id*和*object_id*參數。 不過，傳遞對這些函數無效的值可能會造成意料之外的結果。 例如，如果找不到資料庫或物件名稱 (因為不存在或是拼法不正確)，這兩個函數都會傳回 NULL。 sys.dm_db_index_physical_stats 函數會將 NULL 解譯為萬用字元值，指定所有的資料庫或物件。  
  
 此外，OBJECT_ID 函數會處理之前在呼叫 sys.dm_db_index_physical_stats 函數，而且因此目前資料庫的內容中評估，不是資料庫中指定*database_id*。 這個行為可能會讓 OBJECT_ID 函數傳回 NULL 值；如果物件名稱同時存在於目前的資料庫內容和指定的資料庫中，則可能會傳回錯誤訊息。 下列範例示範這些意料之外的結果。  
  
```  
USE master;  
GO  
-- In this example, OBJECT_ID is evaluated in the context of the master database.   
-- Because Person.Address does not exist in master, the function returns NULL.  
-- When NULL is specified as an object_id, all objects in the database are returned.  
-- The same results are returned when an object that is not valid is specified.  
SELECT * FROM sys.dm_db_index_physical_stats  
    (DB_ID(N'AdventureWorks'), OBJECT_ID(N'Person.Address'), NULL, NULL , 'DETAILED');  
GO  
-- This example demonstrates the results of specifying a valid object name  
-- that exists in both the current database context and  
-- in the database specified in the database_id parameter of the   
-- sys.dm_db_index_physical_stats function.  
-- An error is returned because the ID value returned by OBJECT_ID does not  
-- match the ID value of the object in the specified database.  
CREATE DATABASE Test;  
GO  
USE Test;  
GO  
CREATE SCHEMA Person;  
GO  
CREATE Table Person.Address(c1 int);  
GO  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_db_index_physical_stats  
    (DB_ID(N'Test'), OBJECT_ID(N'Person.Address'), NULL, NULL , 'DETAILED');  
GO  
-- Clean up temporary database.  
DROP DATABASE Test;  
GO  
```  
  
### <a name="best-practice"></a>最佳作法  
 使用 DB_ID 或 OBJECT_ID 時，請務必確定傳回的是有效的識別碼。 例如，當您使用 OBJECT_ID 時，例如指定三部分名稱`OBJECT_ID(N'AdventureWorks2012.Person.Address')`，或測試您用於 sys.dm_db_index_physical_stats 函數之前，函式所傳回的值。 下面的範例 A 和 B 示範指定資料庫和物件識別碼的安全方法。  
  
## <a name="detecting-fragmentation"></a>偵測片段  
 片段是經由針對資料表建立的資料修改程序 (INSERT、UPDATE 和 DELETE 陳述式) 而產生，因此會產生到資料表上定義的索引。 由於這些修改通常不會平均散發在資料表和索引的各個資料列上，因此，各頁面的飽和度可能會隨著時間而不同。 如果查詢要掃描部分或全部的資料表索引，這類資料表片段可能會造成額外的頁面讀取。 這會防礙資料的平行掃描。  
  
 索引或堆積的片段層級會顯示在 avg_fragmentation_in_percent 資料行中。 如果是堆積，這個值代表該堆積的範圍片段。 如果是索引，則這個值代表該索引的邏輯片段。 與 DBCC SHOWCONTIG 不同的是，這兩種情況的片段計算演算法，都採用跨越多個檔案的儲存體，因此也較精確。  
  
 **邏輯片段**  
  
 這是索引分葉頁中，失序頁面的百分比。 失序頁面是指配置給索引之下一個實體頁面的頁面，而不是目前分葉頁中下一頁指標所指向的頁面。  
  
 **範圍片段**  
  
 這是堆積分葉頁中，失序範圍的百分比。 失序範圍是指某個包含目前堆積頁面的範圍，實際上不是包含上一頁之範圍後面的下一個範圍。  
  
 avg_fragmentation_in_percent 的值愈接近零，其效能愈好。 不過，百分之 0 到 10 之間的值都在接受範圍內。 所有縮減片段的方法 (例如，重建、重新組織或重新建立) 都可以用來縮減這些值。 如需如何分析索引片段的程度的詳細資訊，請參閱[Reorganize and Rebuild Indexes](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)。  
  
## <a name="reducing-fragmentation-in-an-index"></a>縮減索引中的片段  
 如果對索引進行片段作業之後，片段會影響到查詢效能，有三個選擇可減少片段：  
  
-   卸除和重新建立叢集索引。  
  
     重新建立叢集索引會轉散發資料，造成飽和的資料頁面。 您可以在 CREATE INDEX 中使用 FILLFACTOR 選項來設定飽和度的層級。 這個方法的缺點是在卸除和重建周期內索引是離線的，而且作業不可部分完成。 如果中斷了索引建立，就不會重建索引。 如需詳細資訊，請參閱 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)。  
  
-   以 ALTER INDEX REORGANIZE 代替 DBCC INDEXDEFRAG，依照邏輯順序來重新排列索引的分葉層級頁面。 由於這是一項線上作業，因此當執行陳述式時，可以使用索引。 這項作業即使被中斷，也不會遺失已經完成的工作。 這個方法的缺點是，其資料重新組織作業不如索引重建作業來得好，而且也不能更新統計資料。  
  
-   以 ALTER INDEX REBUILD 代替 DBCC DBREINDEX，以線上或離線方式重建索引。 如需詳細資訊，請參閱 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)。  
  
 單獨片段的這個理由，不足以重新組織或重建索引。 片段的主要影響是降低掃描索引時的頁面預先讀取的輸送量。 這樣會使得回應時間更慢。 如果片段化的資料表或索引上的查詢工作負載不含掃描在內 (因為工作負載主要是單一查閱)，移除片段不會有任何影響。 如需詳細資訊，請參閱此[Microsoft 寍鯚](http://go.microsoft.com/fwlink/?linkid=31012)。  
  
> [!NOTE]  
>  如果在壓縮作業時，部分或完全移動索引，則執行 DBCC SHRINKFILE 或 DBCC SHRINKDATABASE 可能會導入片段。 因此，即使一定要執行壓縮作業，應該在移除片段之前執行。  
  
## <a name="reducing-fragmentation-in-a-heap"></a>縮減堆積中的片段  
 若要縮減堆積的範圍片段，請在資料表上建立叢集索引，然後再卸除該索引。 此舉會在建立叢集索引的同時轉散發資料。 在散發資料庫中的可用空間時，也可以達到最佳效果。 當您卸除叢集索引來重新建立堆積時，這些資料仍然以最理想的方式留在原地，不會移走。 如需如何執行這些作業的資訊，請參閱[CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)和[DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md)。  
  
> [!CAUTION]  
>  在資料表上建立和卸除叢集索引時，會重建該資料表上的所有非叢集索引兩次。  
  
## <a name="compacting-large-object-data"></a>壓縮大型物件資料  
 根據預設，ALTER INDEX REORGANIZE 陳述式會壓縮含有大型物件 (LOB) 資料的頁面。 由於 LOB 頁在空白時不會被取消配置，因此如果已經刪除許多 LOB 資料，或是已經卸除一個 LOB 資料行，可以壓縮這些資料來改善磁碟空間的使用。  
  
 重新組織指定的叢集索引會壓縮叢集索引所包含的所有 LOB 資料行。 重新組織非叢集索引會壓縮索引中本身是非索引鍵資料行 (內含資料行) 的所有 LOB 資料行。 當陳述式內指定 ALL 時，所有與指定之資料表或檢視表相關的索引都會重新組織。 此外，所有與叢集索引、基礎資料表或附有內含資料行之非叢集索引相關聯的 LOB 資料行都會壓縮。  
  
## <a name="evaluating-disk-space-use"></a>評估磁碟空間的使用情形  
 avg_page_space_used_in_percent 資料行會指出頁面是否已經飽和。 若要妥善利用磁碟空間，對於沒有太多隨機插入的索引來說，這個值愈接近 100% 愈好。 不過，如果索引有許多隨機插入和非常飽和的頁面，頁面分割數會增加。 這會造成更多的片段。 因此，為了減少頁面分割，這個值最好能夠少於 100%。 指定 FILLFACTOR 選項來重建索引可以改變頁面飽和，讓它配合索引的查詢模式。 如需有關填滿因數的詳細資訊，請參閱[指定索引的填滿因數](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)。 同時，ALTER INDEX REORGANIZE 會盡量配合上次指定的 FILLFACTOR 來填滿頁面，以壓縮索引。 此舉會將 avg_space_used_in_percent 中的值提高。 請注意，ALTER INDEX REORGANIZE 無法縮減頁面飽和。 您必須重建索引才行。  
  
## <a name="evaluating-index-fragments"></a>評估索引片段  
 片段是由配置單位之同一檔案中，實際連續的分葉頁所組成。 一個索引至少有一個片段。 一個索引最多能擁有的片段數相當於該索引之分葉層級中的頁數。 片段較大表示若要讀取同樣數量的頁數，所需的磁碟 I/O 更少。 因此，avg_fragment_size_in_pages 值愈大，範圍掃描效能愈佳。 avg_fragment_size_in_pages 和 avg_fragmentation_in_percent 值彼此成反比。 因此，重建或重新組織索引都會減少片段的數量，以及加大片段。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 不會傳回叢集資料行存放區索引的資料。  
  
## <a name="permissions"></a>Permissions  
 需要下列權限：  
  
-   對資料庫中的指定物件具備 CONTROL 權限。  
  
-   VIEW DATABASE STATE 權限，以傳回指定的資料庫中的所有物件的相關資訊，利用物件萬用字元 @*object_id*= NULL。  
  
-   VIEW SERVER STATE 權限，以傳回所有的資料庫的相關資訊，利用資料庫萬用字元 @*database_id* = NULL。  
  
 授與 VIEW DATABASE STATE 可以傳回資料庫中的所有物件，不論特定物件是否拒絕任何 CONTROL 權限。  
  
 拒絕 VIEW DATABASE STATE 會造成不允許傳回資料庫中的所有物件 (不論是否授與特定物件任何 CONTROL 權限)。 也，當資料庫萬用字元 @*database_id*= 指定 NULL，則會省略資料庫。  
  
 如需詳細資訊，請參閱[動態管理檢視和函數&#40;TRANSACT-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-information-about-a-specified-table"></a>A. 傳回指定之資料表的相關資訊  
 下列範例會傳回 `Person.Address` 資料表之所有索引和分割區的大小和片段統計資料。 掃描模式設為 `'LIMITED'`，以達到最佳效能，並且限制傳回的統計資料。 若要執行這項查詢，至少必須有 `Person.Address` 資料表的 CONTROL 權限。  
  
```  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.Person.Address');  
  
IF @db_id IS NULL  
BEGIN;  
    PRINT N'Invalid database';  
END;  
ELSE IF @object_id IS NULL  
BEGIN;  
    PRINT N'Invalid object';  
END;  
ELSE  
BEGIN;  
    SELECT * FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'LIMITED');  
END;  
GO  
  
```  
  
### <a name="b-returning-information-about-a-heap"></a>B. 傳回堆積的相關資訊  
 下列範例會傳回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中 `dbo.DatabaseLog` 堆積的所有統計資料。 由於資料表包含 LOB 資料，因此除了針對儲存堆積資料頁的 `LOB_DATA` 傳回資料列外，`IN_ROW_ALLOCATION_UNIT` 配置單位也會傳回資料列。 若要執行這項查詢，至少必須有 `dbo.DatabaseLog` 資料表的 CONTROL 權限。  
  
```  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.DatabaseLog');  
IF @object_id IS NULL   
BEGIN;  
    PRINT N'Invalid object';  
END;  
ELSE  
BEGIN;  
    SELECT * FROM sys.dm_db_index_physical_stats(@db_id, @object_id, 0, NULL , 'DETAILED');  
END;  
GO  
  
```  
  
### <a name="c-returning-information-for-all-databases"></a>C. 傳回所有資料庫的相關資訊  
 下列範例會對所有參數指定萬用字元 `NULL`，以傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中，所有資料表和索引的所有統計資料。 執行這項查詢需要 VIEW SERVER STATE 權限。  
  
```  
SELECT * FROM sys.dm_db_index_physical_stats (NULL, NULL, NULL, NULL, NULL);  
GO  
  
```  
  
### <a name="d-using-sysdmdbindexphysicalstats-in-a-script-to-rebuild-or-reorganize-indexes"></a>D. 在指令碼中使用 sys.dm_db_index_physical_stats 來重建或重新組織索引  
 下列範例會自動重新組織或重建資料庫中所有具備 10% 以上平均片段的分割區。 執行這項查詢需要 VIEW DATABASE STATE 權限。 這個範例會指定第一個參數為 `DB_ID`，而不指定資料庫名稱。 如果目前資料庫的相容性層級是 80 或更低，將會產生錯誤。 若要解決此錯誤，請使用有效的資料庫名稱來取代 `DB_ID()`。 如需有關資料庫相容性層級的詳細資訊，請參閱[ALTER DATABASE 相容性層級&#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  
  
```  
-- Ensure a USE <databasename> statement has been executed first.  
SET NOCOUNT ON;  
DECLARE @objectid int;  
DECLARE @indexid int;  
DECLARE @partitioncount bigint;  
DECLARE @schemaname nvarchar(130);   
DECLARE @objectname nvarchar(130);   
DECLARE @indexname nvarchar(130);   
DECLARE @partitionnum bigint;  
DECLARE @partitions bigint;  
DECLARE @frag float;  
DECLARE @command nvarchar(4000);   
-- Conditionally select tables and indexes from the sys.dm_db_index_physical_stats function   
-- and convert object and index IDs to names.  
SELECT  
    object_id AS objectid,  
    index_id AS indexid,  
    partition_number AS partitionnum,  
    avg_fragmentation_in_percent AS frag  
INTO #work_to_do  
FROM sys.dm_db_index_physical_stats (DB_ID(), NULL, NULL , NULL, 'LIMITED')  
WHERE avg_fragmentation_in_percent > 10.0 AND index_id > 0;  
  
-- Declare the cursor for the list of partitions to be processed.  
DECLARE partitions CURSOR FOR SELECT * FROM #work_to_do;  
  
-- Open the cursor.  
OPEN partitions;  
  
-- Loop through the partitions.  
WHILE (1=1)  
    BEGIN;  
        FETCH NEXT  
           FROM partitions  
           INTO @objectid, @indexid, @partitionnum, @frag;  
        IF @@FETCH_STATUS < 0 BREAK;  
        SELECT @objectname = QUOTENAME(o.name), @schemaname = QUOTENAME(s.name)  
        FROM sys.objects AS o  
        JOIN sys.schemas as s ON s.schema_id = o.schema_id  
        WHERE o.object_id = @objectid;  
        SELECT @indexname = QUOTENAME(name)  
        FROM sys.indexes  
        WHERE  object_id = @objectid AND index_id = @indexid;  
        SELECT @partitioncount = count (*)  
        FROM sys.partitions  
        WHERE object_id = @objectid AND index_id = @indexid;  
  
-- 30 is an arbitrary decision point at which to switch between reorganizing and rebuilding.  
        IF @frag < 30.0  
            SET @command = N'ALTER INDEX ' + @indexname + N' ON ' + @schemaname + N'.' + @objectname + N' REORGANIZE';  
        IF @frag >= 30.0  
            SET @command = N'ALTER INDEX ' + @indexname + N' ON ' + @schemaname + N'.' + @objectname + N' REBUILD';  
        IF @partitioncount > 1  
            SET @command = @command + N' PARTITION=' + CAST(@partitionnum AS nvarchar(10));  
        EXEC (@command);  
        PRINT N'Executed: ' + @command;  
    END;  
  
-- Close and deallocate the cursor.  
CLOSE partitions;  
DEALLOCATE partitions;  
  
-- Drop the temporary table.  
DROP TABLE #work_to_do;  
GO  
  
```  
  
### <a name="e-using-sysdmdbindexphysicalstats-to-show-the-number-of-page-compressed-pages"></a>E. 使用 sys.dm_db_index_physical_stats 來顯示頁面壓縮的頁面數目  
 下列範例將示範如何針對資料列與頁面壓縮的頁面顯示和比較總頁面數目。 這項資訊可用來判斷針對索引或資料表提供壓縮的優勢。  
  
```  
SELECT o.name,  
    ips.partition_number,  
    ips.index_type_desc,  
    ips.record_count, ips.avg_record_size_in_bytes,  
    ips.min_record_size_in_bytes,  
    ips.max_record_size_in_bytes,  
    ips.page_count, ips.compressed_page_count  
FROM sys.dm_db_index_physical_stats ( DB_ID(), NULL, NULL, NULL, 'DETAILED') ips  
JOIN sys.objects o on o.object_id = ips.object_id  
ORDER BY record_count DESC;  
```  
  
### <a name="f-using-sysdmdbindexphysicalstats-in-sampled-mode"></a>F. 在 SAMPLED 模式下使用 sys.dm_db_index_physical_stats  
 下列範例示範 SAMPLED 模式如何傳回不同於 DETAILED 模式結果的近似結果。  
  
```  
CREATE TABLE t3 (col1 int PRIMARY KEY, col2 varchar(500)) WITH(DATA_COMPRESSION = PAGE);  
GO  
BEGIN TRAN  
DECLARE @idx int = 0;  
WHILE @idx < 1000000  
BEGIN  
    INSERT INTO t3 (col1, col2)   
    VALUES (@idx,   
    REPLICATE ('a', 100) + CAST (@idx as varchar(10)) + REPLICATE ('a', 380))  
    SET @idx = @idx + 1  
END  
COMMIT;  
GO  
SELECT page_count, compressed_page_count, forwarded_record_count, *   
FROM sys.dm_db_index_physical_stats (db_id(),   
    object_id ('t3'), null, null, 'SAMPLED');  
SELECT page_count, compressed_page_count, forwarded_record_count, *   
FROM sys.dm_db_index_physical_stats (db_id(),   
    object_id ('t3'), null, null, 'DETAILED');  
```  
  
### <a name="g-querying-service-broker-queues-for-index-fragmentation"></a>G. 查詢索引片段的 service broker 佇列  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
  
 下列範例將示範如何查詢 server broker 佇列的分散程度。  
  
```  
--Using queue internal table name   
select * from sys.dm_db_index_physical_stats (db_id(), object_id ('sys.queue_messages_549576996'), default, default, default)   
  
--Using queue name directly  
select * from sys.dm_db_index_physical_stats (db_id(), object_id ('ExpenseQueue'), default, default, default)  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [索引相關的動態管理檢視和函式 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.dm_db_index_usage_stats &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)   
 [sys.dm_db_partition_stats &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)   
 [sys.allocation_units &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [系統檢視表&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  

