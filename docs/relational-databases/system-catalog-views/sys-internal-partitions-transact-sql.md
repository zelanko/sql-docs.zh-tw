---
title: sys.internal_partitions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 82b3e432321260a5efa1d25537202d351b89a380
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47603426"
---
# <a name="sysinternalpartitions-transact-sql"></a>sys.internal_partitions & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  傳回追蹤資料行存放區索引的內部資料，以磁碟為基礎的資料表上每個資料列集的一個資料列。 這些資料列集資料行存放區索引的內部，而追蹤刪除資料列、 資料列群組對應和差異存放區資料列群組。 它們會針對每個資料表資料分割; 每個追蹤資料每個資料表有至少一個資料分割。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新建立資料列集資料行存放區索引在重建每一次。   
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|此資料分割的資料分割識別碼。 在資料庫中，這是唯一的。|  
|object_id|**int**|包含資料分割資料表的物件識別碼。|  
|index_id|**int**|在資料表上定義的資料行存放區索引的索引識別碼。<br /><br /> 1 = 叢集資料行存放區索引<br /><br /> 2 = 非叢集資料行存放區索引|  
|partition_number|**int**|資料分割數目。<br /><br /> 1 = 資料分割資料表，第一個資料分割或非資料分割資料表的單一資料分割。<br /><br /> 2 = 第二個資料分割，等等。|  
|internal_object_type|**tinyint**|追蹤資料行存放區索引的內部資料的資料列集物件。<br /><br /> 2 = COLUMN_STORE_DELETE_BITMAP<br /><br /> 3 = COLUMN_STORE_DELTA_STORE<br /><br /> 4 = COLUMN_STORE_DELETE_BUFFER<br /><br /> 5 = COLUMN_STORE_MAPPING_INDEX|  
|internal_object_type_desc|**nvarchar(60)**|COLUMN_STORE_DELETE_BITMAP – 此點陣圖索引會追蹤已標示為已刪除的資料行存放區的資料列。 點陣圖會為每個資料列群組，因為分割區可以有多個資料列群組中的資料列。 資料列的仍是實際存在且佔用著空間中的資料行存放區。<br /><br /> COLUMN_STORE_DELTA_STORE – 存放區資料列群組稱為資料列群組，尚未壓縮成單欄式儲存體。 每個資料表資料分割可以有零個或多個差異存放區資料列群組。<br /><br /> COLUMN_STORE_DELETE_BUFFER – 維護可更新的非叢集資料行存放區索引的刪除動作。 當查詢從基礎資料列存放區資料表刪除資料列時，刪除緩衝區會追蹤刪除的資料行存放區。 當已刪除的資料列數目超過 1048576 時，它們會合併回刪除點陣圖背景 Tuple Mover 執行緒或明確的 Reorganize 命令。  在任何給定的時間點，刪除點陣圖] 和 [刪除緩衝區的聯集表示所有已刪除的資料列。<br /><br /> COLUMN_STORE_MAPPING_INDEX – 使用時的叢集資料行存放區索引只有次要非叢集的索引。 這會對應至正確的資料列群組和資料行存放區中的資料列識別碼的非叢集索引鍵。 它只會儲存索引鍵的資料列，移至不同的資料列群組;會發生這種情況是當差異資料列群組壓縮到資料行存放區，以及當合併作業會合併兩個不同的資料列群組中的資料列。|  
|Row_group_id|**int**|差異存放區 rowgroup 的識別碼。 每個資料表資料分割可以有零個或多個差異存放區資料列群組。|  
|hobt_id|**bigint**|內部資料列集物件的識別碼。 這是良好的索引鍵來聯結其他 Dmv 以取得有關內部的資料列集的實體特性的詳細資訊。|  
|rows|**bigint**|這個資料分割中的近似資料列數。|  
|data_compression|**tinyint**|壓縮的資料列集的狀態：<br /><br /> 0 = NONE<br /><br /> 1 = ROW<br /><br /> 2 = PAGE|  
|data_compression_desc|**nvarchar(60)**|每個資料分割的壓縮狀態。 資料列存放區資料表的可能值為 NONE、ROW 和 PAGE。 資料行存放區資料表的可能值為 COLUMNSTORE 和 COLUMNSTORE_ARCHIVE。|  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="general-remarks"></a>一般備註  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 它會建立或重建資料行存放區索引的每次重新建立新的資料行存放區內部的索引。  
  
## <a name="examples"></a>範例  
  
### <a name="a-view-all-of-the-internal-rowsets-for-a-table"></a>A. 檢視所有的內部資料表的資料列集  
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
  
  
