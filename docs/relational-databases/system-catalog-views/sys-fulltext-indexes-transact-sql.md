---
title: sys.databases fulltext_indexes （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fulltext_indexes
- fulltext_indexes_TSQL
- sys.fulltext_indexes_TSQL
- sys.fulltext_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_indexes catalog view
- full-text indexes [SQL Server], properties
ms.assetid: 7fc10fdc-370f-4927-bba0-b76108a7508e
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b240c74abde034f5008416994ca9cb497e6e64f8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68133795"
---
# <a name="sysfulltext_indexes-transact-sql"></a>sys.fulltext_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對表格式物件的每個全文檢索索引，各包含一個資料列。  

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|這個全文檢索索引所屬的物件識別碼。|  
|**unique_index_id**|**int**|相對應的唯一、非全文檢索索引的識別碼，該索引可將全文檢索索引關聯到資料列。|  
|**fulltext_catalog_id**|**int**|全文檢索索引所在的全文檢索目錄之識別碼。|  
|**is_enabled**|**bit**|1 = 全文檢索索引目前是在啟用狀態。|  
|**change_tracking_state**|**char （1）**|變更追蹤的狀態。<br /><br /> M = 手動<br /><br /> A = 自動<br /><br /> O = 關閉|  
|**change_tracking_state_desc**|**Nvarchar （60）**|變更追蹤的狀態描述。<br /><br /> MANUAL<br /><br /> AUTO<br /><br /> OFF|  
|**has_crawl_completed**|**bit**|全文檢索索引完成的前次搜耙 (母體擴展)。|  
|**crawl_type**|**char （1）**|目前或前次搜耙的類型。<br /><br /> F = 完整搜耙<br /><br /> I = 累加、以時間戳記為基礎的搜耙<br /><br /> U = 以通知為根據的更新搜耙<br /><br /> P = 暫停完整搜耙。|  
|**crawl_type_desc**|**Nvarchar （60）**|目前或前次搜耙類型的描述。<br /><br /> FULL_CRAWL<br /><br /> INCREMENTAL_CRAWL<br /><br /> UPDATE_CRAWL<br /><br /> PAUSED_FULL_CRAWL|  
|**crawl_start_date**|**datetime**|目前或前次搜耙的開始。<br /><br /> NULL = 無。|  
|**crawl_end_date**|**datetime**|目前或前次搜耙的結束。<br /><br /> NULL = 無。|  
|**incremental_timestamp**|**binary （8）**|下一個累加搜耙所用的時間戳記值。<br /><br /> NULL = 無。|  
|**stoplist_id**|**int**|與此全文檢索索引相關聯的停用[字](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)詞表識別碼。|  
|**data_space_id**|**int**|這個全文檢索索引所在的檔案群組。|  
|**property_list_id**|**int**|與這個全文檢索索引相關聯之搜尋屬性清單的識別碼。 NULL 表示沒有搜尋屬性清單與此全文檢索索引相關聯。 若要取得有關此搜尋屬性清單的詳細資訊，請使用[registered_search_property_lists &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)目錄檢視。|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="examples"></a>範例  
 下列範例會針對 `HumanResources.JobCandidate` 範例資料庫的 `AdventureWorks2012` 資料表使用全文檢索索引。 此範例會傳回資料表的物件識別碼、搜尋屬性清單識別碼，以及全文檢索索引所使用之停用字詞表的停用字詞表識別碼。  
  
> [!NOTE]  
>  如需建立此全文檢索索引的程式碼範例，請參閱[CREATE 全文檢索索引 &#40;transact-sql&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)的「範例」一節。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT object_id, property_list_id, stoplist_id FROM sys.fulltext_indexes  
    where object_id = object_id('HumanResources.JobCandidate');   
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [fulltext_index_fragments &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)   
 [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)   
 [fulltext_index_catalog_usages &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql.md)   
 [&#40;Transact-sql&#41;的物件目錄檢視](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [建立及管理全文檢索索引](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
  
