---
title: sys.dm_db_missing_index_details (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_missing_index_details
- dm_db_missing_index_details
- sys.dm_db_missing_index_details_TSQL
- dm_db_missing_index_details_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- missing indexes feature [SQL Server], sys.dm_db_missing_index_details dynamic management view
- sys.dm_db_missing_index_details dynamic management view
ms.assetid: ced484ae-7c17-4613-a3f9-6d8aba65a110
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 35058af357c7ab702a39e07baac96fa1ee9a38f8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47649006"
---
# <a name="sysdmdbmissingindexdetails-transact-sql"></a>sys.dm_db_missing_index_details (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回有關遺漏索引 (不包含空間索引) 的詳細資訊。  
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，動態管理檢視不可以公開可能會影響資料庫內含項目的資訊或公開有關使用者可存取之其他資料庫的資訊。 為了避免公開此資訊，包含不屬於連接租用戶之資料的每個資料列都會被篩選出來。  

  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**index_handle**|**int**|識別特定的遺漏索引。 此識別碼在伺服器中是唯一的。 **index_handle**是這個資料表的索引鍵。|  
|**database_id**|**smallint**|識別具有遺漏索引之資料表的資料庫。|  
|**object_id**|**int**|識別遺漏索引所在的資料表。|  
|**equality_columns**|**nvarchar(4000)**|作為相等述詞之資料行的逗號分隔清單，述詞格式如下：<br /><br /> *table.column* =*constant_value*|  
|**inequality_columns**|**nvarchar(4000)**|作為不相等述詞之資料行的逗號分隔清單，例如，格式如下的述詞：<br /><br /> *table.column* > *constant_value*<br /><br /> "=" 以外的其他任何比較運算子都可表示不相等。|  
|**included_columns**|**nvarchar(4000)**|可作為查詢所需涵蓋資料行之資料行的逗號分隔清單。 如需有關涵蓋或內含資料行，請參閱[建立內含資料行的索引](../../relational-databases/indexes/create-indexes-with-included-columns.md)。<br /><br /> 記憶體最佳化的索引 (雜湊和記憶體最佳化非叢集)，略過**included_columns**。 每個記憶體最佳化的索引都包含資料表的所有資料行。|  
|**陳述式**|**nvarchar(4000)**|遺漏索引所在之資料表的名稱。|  
  
## <a name="remarks"></a>備註  
 所傳回的資訊**sys.dm_db_missing_index_details**會更新查詢最佳化，查詢最佳化工具，而不會保存。 遺漏索引資訊只會保留到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新啟動為止。 如果資料庫管理員想要在伺服器回收之後保留遺漏索引資訊，應該定期製作該項資訊的備份副本。  
  
 若要判斷哪些遺漏索引群組特定遺漏索引的一部分，您可以查詢**sys.dm_db_missing_index_groups**動態管理檢視等聯結，以便它與**sys.dm_db_missing_index_details**根據**index_handle**資料行。  

  >[!NOTE]
  >結果集中的此 DMV 會限制為 600 的資料列。 每個資料列都包含一個遺漏的索引。 如果您有多個遺漏索引的 600 時，您應該先處理現有的遺漏索引，因此您可以檢視較新的。 
  
## <a name="using-missing-index-information-in-create-index-statements"></a>在 CREATE INDEX 陳述式中使用遺漏索引資訊  
 要轉換所傳回的資訊**sys.dm_db_missing_index_details**成記憶體最佳化和以磁碟為基礎的索引的 CREATE INDEX 陳述式，等號比較資料行都應該放前後不相等資料行一起它們應該要索引的索引鍵。 您應該使用 INCLUDE 子句，將內含資料行加入 CREATE INDEX 陳述式中。 若要決定相等資料行的有效次序，請依據其選擇性排列這些資料行：將選擇性最高的資料行列在最前面 (資料行清單的最左邊)。  
  
 如需有關記憶體最佳化索引的詳細資訊，請參閱 <<c0> [ 記憶體最佳化資料表的索引](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)。  
  
## <a name="transaction-consistency"></a>交易一致性  
 如果交易建立或卸除資料表，便會從這個動態管理物件中移除包含有關已卸除物件之遺漏索引資訊的資料列，以維持交易的一致性。  
  
## <a name="permissions"></a>Permissions

在  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在  [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   

## <a name="see-also"></a>另請參閱  
 [sys.dm_db_missing_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [sys.dm_db_missing_index_groups &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [sys.dm_db_missing_index_group_stats &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  
