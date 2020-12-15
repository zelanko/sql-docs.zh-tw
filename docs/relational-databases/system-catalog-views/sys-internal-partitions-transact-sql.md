---
description: 'sys.internal_partitions (Transact-sql) '
title: sys.internal_partitions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0262df2b-5ba7-4715-b17b-3d9ce470a38e
author: ronortloff
ms.author: rortloff
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0b55887eadaf25aa254c8b693619df0f22411718
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484750"
---
# <a name="sysinternal_partitions-transact-sql"></a>sys.internal_partitions (Transact-sql) 

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  針對在磁片資料表上追蹤資料行存放區索引的內部資料的每個資料列集，各傳回一個資料列。 這些資料列集是內部資料行存放區索引，可追蹤已刪除的資料列、資料列群組對應和差異存放區資料列群組 它們會追蹤每個資料表分割的資料。每個資料表都至少有一個資料分割。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 每次重建資料行存放區索引時，重新建立資料列集。   
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|此分割區的資料分割識別碼。 在資料庫中，這是唯一的。|  
|object_id|**int**|包含分割區之資料表的物件識別碼。|  
|index_id|**int**|資料表上定義之資料行存放區索引的索引識別碼。<br /><br /> 1 = 叢集資料行存放區索引<br /><br /> 2 = 非叢集資料行存放區索引|  
|partition_number|**int**|分割區編號。<br /><br /> 1 = 資料分割資料表的第一個資料分割，或非資料分割資料表的單一資料分割。<br /><br /> 2 = 第二個數據分割，依此類推。|  
|internal_object_type|**tinyint**|追蹤資料行存放區索引內部資料的資料列集物件。<br /><br /> 2 = COLUMN_STORE_DELETE_BITMAP<br /><br /> 3 = COLUMN_STORE_DELTA_STORE<br /><br /> 4 = COLUMN_STORE_DELETE_BUFFER<br /><br /> 5 = COLUMN_STORE_MAPPING_INDEX|  
|internal_object_type_desc|**nvarchar(60)**|COLUMN_STORE_DELETE_BITMAP-此點陣圖索引會追蹤標示為已從資料行存放區刪除的資料列。 點陣圖是針對每個資料列群組，因為分割區可以有多個資料列群組中的資料列。 資料列仍然存在於資料行存放區中，並佔用空間。<br /><br /> COLUMN_STORE_DELTA_STORE-將尚未壓縮成單欄式儲存區的資料列群組（稱為資料列群組）儲存。 每個資料表資料分割可以有零或多個差異存放區資料列群組。<br /><br /> COLUMN_STORE_DELETE_BUFFER-用於維護可更新之非叢集資料行存放區索引的刪除。 當查詢從基礎 rowstore 資料表刪除資料列時，delete 緩衝區會追蹤資料行存放區的刪除。 當已刪除的資料列數目超過1048576時，會透過背景 Tuple Mover 執行緒或明確的重新組織命令，將它們合併回刪除點陣圖。  在任何給定的時間點，刪除點陣圖和刪除緩衝區的聯集都代表所有已刪除的資料列。<br /><br /> COLUMN_STORE_MAPPING_INDEX-只有在叢集資料行存放區索引具有次要非叢集索引時才會使用。 這會將非叢集索引鍵對應到資料行存放區中正確的資料列群組和資料列識別碼。 它只會儲存移至不同資料列群組的資料列索引鍵。當差異資料列群組壓縮到資料行存放區，以及合併作業合併來自兩個不同資料列群組的資料列時，就會發生這種情況。|  
|Row_group_id|**int**|差異存放區資料列群組的識別碼。 每個資料表資料分割可以有零或多個差異存放區資料列群組。|  
|hobt_id|**bigint**|內部資料列集物件的識別碼 (HoBT) 。 這是與其他 Dmv 聯結的好索引鍵，可取得內部資料列集之實體特性的詳細資訊。|  
|rows|**bigint**|這個資料分割中的近似資料列數。|  
|data_compression|**tinyint**|資料列集的壓縮狀態：<br /><br /> 0 = NONE<br /><br /> 1 = ROW<br /><br /> 2 = PAGE|  
|data_compression_desc|**nvarchar(60)**|每個資料分割的壓縮狀態。 資料列存放區資料表的可能值為 NONE、ROW 和 PAGE。 資料行存放區資料表的可能值為 COLUMNSTORE 和 COLUMNSTORE_ARCHIVE。|  
|optimize_for_sequential_key|**bit**|1 = 分割區已啟用最後頁面插入優化。<br><br>0 = 預設值。 分割區已停用最後頁面插入優化。|
  
## <a name="permissions"></a>權限  
 需要 `public` 角色中的成員資格。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="general-remarks"></a>一般備註  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 每次建立或重建資料行存放區索引時，重新建立新的資料行存放區內部索引。  
  
## <a name="examples"></a>範例  
  
### <a name="a-view-all-of-the-internal-rowsets-for-a-table"></a>A. 查看資料表的所有內部資料列集  
 此範例會傳回資料表的所有內部資料行存放區資料列集。 您也可以使用 hobt_id 來尋找有關特定資料列集的詳細資訊。  
  
```sql  
SELECT i.object_id, i.index_id, i.name, p.hobt_id, p.internal_object_type_id, p.internal_object_type_desc  
FROM sys.internal_partitions AS p  
JOIN sys.indexes AS i  
on i.object_id = p.object_id  
WHERE p.object_id = OBJECT_ID ( '<table name' ) ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢 SQL Server 系統目錄 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
