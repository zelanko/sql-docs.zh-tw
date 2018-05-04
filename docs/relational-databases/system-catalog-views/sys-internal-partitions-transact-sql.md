---
title: sys.internal_partitions (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
dev_langs:
- TSQL
ms.assetid: 0262df2b-5ba7-4715-b17b-3d9ce470a38e
caps.latest.revision: 13
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 525e98f4fe0a5096e7a75242174d84f38084e696
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysinternalpartitions-transact-sql"></a>sys.internal_partitions (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  傳回一個資料列追蹤磁碟資料表上的資料行存放區索引的內部資料，每個資料列集。 這些資料列集是資料行存放區索引的內部和追蹤刪除資料列、 資料列群組對應和差異存放區資料列群組。 它們會針對每個資料表資料分割; 每個追蹤資料每一個資料表都至少一個資料分割。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在重建資料行存放區索引每次重新建立資料列集。   
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|這個資料分割的資料分割識別碼。 在資料庫中，這是唯一的。|  
|object_id|**int**|包含資料分割資料表的物件識別碼。|  
|index_id|**int**|在資料表上定義的資料行存放區索引的索引識別碼。<br /><br /> 1 = 叢集資料行存放區索引<br /><br /> 2 = 非叢集資料行存放區索引|  
|partition_number|**int**|資料分割編號。<br /><br /> 1 = 資料分割資料表，第一個資料分割或單一資料分割的非資料分割的資料表。<br /><br /> 2 = 第二個資料分割，等等。|  
|internal_object_type|**tinyint**|追蹤資料行存放區索引的內部資料的資料列集物件。<br /><br /> 2 = COLUMN_STORE_DELETE_BITMAP<br /><br /> 3 = COLUMN_STORE_DELTA_STORE<br /><br /> 4 = COLUMN_STORE_DELETE_BUFFER<br /><br /> 5 = COLUMN_STORE_MAPPING_INDEX|  
|internal_object_type_desc|**nvarchar(60)**|COLUMN_STORE_DELETE_BITMAP – 此點陣圖索引會追蹤會標示為從資料行存放區刪除的資料列。 點陣圖會為每個資料列群組，由於資料分割可以有多個資料列群組中的資料列。 資料列是，仍是實際出現且佔用的空間資料行存放區中。<br /><br /> COLUMN_STORE_DELTA_STORE – 存放區資料列群組稱為尚未壓縮到單欄式儲存體的資料列群組。 每個資料表資料分割可以有零個或多個差異存放區資料列群組。<br /><br /> COLUMN_STORE_DELETE_BUFFER – 維護可更新非叢集資料行存放區索引刪除動作。 當查詢從基礎資料列存放區資料表刪除資料列的刪除緩衝區會追蹤刪除從資料行存放區。 當已刪除的資料列數目超過 1048576 時，它們會合併回刪除點陣圖背景 Tuple Mover 執行緒或是明確的重新組織命令。  在任何給定的時間點，與聯集的刪除點陣圖的刪除緩衝區會代表所有已刪除資料列。<br /><br /> COLUMN_STORE_MAPPING_INDEX – 使用只有叢集資料行存放區索引具有次要的非叢集的索引時。 這會對應到正確的資料列群組和資料行存放區中的資料列識別碼的非叢集索引鍵。 它只會儲存索引鍵的資料列移至不同的資料列群組。這會在差異資料列群組壓縮成資料行存放區，以及合併作業來合併兩個不同的資料列群組中的資料列時發生。|  
|Row_group_id|**int**|差異存放區資料列群組的識別碼。 每個資料表資料分割可以有零個或多個差異存放區資料列群組。|  
|hobt_id|**bigint**|內部資料列集物件的識別碼。 這是良好的索引鍵的聯結與其他 Dmv，以取得有關內部的資料列集的實體特性的詳細資訊。|  
|rows|**bigint**|這個資料分割中的近似資料列數。|  
|data_compression|**tinyint**|壓縮的資料列集的狀態：<br /><br /> 0 = NONE<br /><br /> 1 = ROW<br /><br /> 2 = PAGE|  
|data_compression_desc|**nvarchar(60)**|每個資料分割的壓縮狀態。 資料列存放區資料表的可能值為 NONE、ROW 和 PAGE。 資料行存放區資料表的可能值為 COLUMNSTORE 和 COLUMNSTORE_ARCHIVE。|  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色中的成員資格。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="general-remarks"></a>一般備註  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 它會建立或重建資料行存放區索引每次重新建立新的資料行存放區內部索引。  
  
## <a name="examples"></a>範例  
  
### <a name="a-view-all-of-the-internal-rowsets-for-a-table"></a>A. 檢視所有資料表的內部資料列集  
 這個範例會傳回所有資料表的內部資料行存放區資料列集。 您也可以使用 hobt_id，若要尋找特定的資料列集的詳細資訊。  
  
```  
SELECT i.object_id, i.index_id, i.name, p.hobt_id, p.internal_object_type_id, p.internal_object_type_desc  
FROM sys.internal_partitions AS p  
JOIN sys.indexes AS i  
on i.object_id = p.object_id  
WHERE p.object_id = OBJECT_ID ( '<table name' ) ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢 SQL Server 系統目錄常見問題集](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
