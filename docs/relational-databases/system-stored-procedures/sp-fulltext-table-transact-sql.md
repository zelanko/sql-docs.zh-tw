---
description: sp_fulltext_table (Transact-SQL)
title: sp_fulltext_table (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_table_TSQL
- sp_fulltext_table
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_table
ms.assetid: a765f311-07fc-4af3-b74c-e9a027fbecce
author: CarlRabeler
ms.author: carlrab
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 283fdb387e60eeed95cc33dc89711631f2465380
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447127"
---
# <a name="sp_fulltext_table-transact-sql"></a>sp_fulltext_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  標示或取消標示全文檢索索引的資料表。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用 [CREATE 全文檢索索引](../../t-sql/statements/create-fulltext-index-transact-sql.md)、 [ALTER 全文檢索](../../t-sql/statements/alter-fulltext-index-transact-sql.md)索引和 [DROP 全文檢索索引](../../t-sql/statements/drop-fulltext-index-transact-sql.md) 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_fulltext_table   
   [ @tabname= ] 'qualified_table_name'           
   , [ @action= ] 'action'   
   [   
   , [ @ftcat= ] 'fulltext_catalog_name'           
   , [ @keyname= ] 'unique_index_name'   
   ]  
```  
  
## <a name="arguments"></a>引數  
`[ @tabname = ] 'qualified_table_name'` 這是一或兩部分的資料表名稱。 資料表必須在目前的資料庫中。 *qualified_table_name* 是 **Nvarchar (517) **，沒有預設值。  
  
`[ @action = ] 'action'` 這是要執行的動作。 *動作* 是 **Nvarchar (50) **，沒有預設值，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**建立**|針對 *qualified_table_name* 所參考的資料表建立全文檢索索引的中繼資料，並指定此資料表的全文檢索索引資料應該位於 *fulltext_catalog_name*中。 這個動作也會指定使用 *unique_index_name* 做為全文檢索索引鍵資料行。 這個唯一索引必須已經存在，且必須在資料表的某個資料行中定義。<br /><br /> 在擴展全文檢索目錄之前，您無法執行這份資料表的全文檢索搜尋。|  
|**下降**|卸載 *qualified_table_name*之全文檢索索引的中繼資料。 如果全文檢索索引在使用中，在卸除之後，也會自動停用。 在卸除全文檢索索引之前，不需要移除資料行。|  
|**啟用**|啟用在停用全文檢索索引資料的 *qualified_table_name*時，對其進行收集的能力。 至少必須有一個資料行參與全文檢索索引，您才能啟動它。<br /><br /> 只要加入了第一個索引資料行，全文檢索索引就會自動成為使用中 (以便擴展)。 如果從索引中卸除最後一個資料行，索引便會成為非使用中。 如果變更追蹤是開啟的，啟動非作用中的索引會啟動新的擴展。<br /><br /> 請注意，這並不會實際擴展全文檢索索引，只會在檔案系統的全文檢索目錄中登錄資料表，以便在下一次全文檢索索引擴展期間，可以抓取 *qualified_table_name* 的資料列。|  
|**關閉**|停用 *qualified_table_name* 的全文檢索索引，如此就不能再收集 *qualified_table_name*的全文檢索索引資料。 仍會保留全文檢索索引中繼資料，且可以重新啟動資料表。<br /><br /> 如果變更追蹤是開啟的，停用使用中的索引會凍結索引狀態：任何進行中的擴展都會停止，不會再將任何其他變更傳播給索引。|  
|**start_change_tracking**|啟動全文檢索索引的累加擴展。 如果資料表沒有時間戳記，便啟動全文檢索索引的完整擴展。 啟動資料表的變更追蹤。<br /><br /> 全文檢索變更追蹤不會追蹤任何在類型為 **image**、 **text**或 **Ntext**之全文檢索索引資料行上執行的 WRITETEXT 或 UPDATETEXT 作業。|  
|**stop_change_tracking**|停止資料表的追蹤變更。|  
|**update_index**|將目前追蹤的這組變更傳播給全文檢索索引。|  
|**Start_background_updateindex**|在發生追蹤的變更時，開始將這些變更傳播給全文檢索索引。|  
|**Stop_background_updateindex**|在發生追蹤的變更時，停止將這些變更傳播給全文檢索索引。|  
|**start_full**|啟動資料表的全文檢索索引的完整擴展。|  
|**start_incremental**|啟動資料表的全文檢索索引的累加擴展。|  
|**停止**|停止完整或累加擴展。|  
  
`[ @ftcat = ] 'fulltext_catalog_name'` 這是 **create** 動作之有效的現有全文檢索目錄名稱。 所有其他動作的這個參數都必須是 NULL。 *fulltext_catalog_name* 是 **sysname**，預設值是 Null。  
  
`[ @keyname = ] 'unique_index_name'`這是一個有效的單一索引鍵資料行、唯一的不可為 null 索引，適用于**create**動作的*qualified_table_name* 。 所有其他動作的這個參數都必須是 NULL。 *unique_index_name* 是 **sysname**，預設值是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 在停用特定資料表的全文檢索索引之後，現有全文檢索索引會維持在原處，直到下一次完整擴展為止;但是，不會使用這個索引，因為會 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 封鎖已停用之資料表的查詢。  
  
 如果重新啟動資料表，且沒有重新擴展索引，任何其餘啟用全文檢索的非新增資料行的查詢，仍可以使用舊索引。 在指定全部全文檢索資料行搜尋的查詢中，會符合已刪除的資料行之資料。  
  
 在定義全文檢索索引的資料表之後，將全文檢索唯一索引鍵資料行從某個資料類型切換到另一個資料類型（藉由將該資料行的資料類型變更為另一個資料行，或將全文*檢索*唯一索引鍵從某個資料行變更 key_value 為另一個資料行），如果沒有完整的自填滿，則可能會導致後續查詢期間發生失敗 *，* 並傳回錯誤訊息：「轉換成 data_type 若要避免這種情況，請使用**sp_fulltext_table**的**drop**動作卸載此資料表的全文檢索定義，然後使用**sp_fulltext_table**和**sp_fulltext_column**重新定義此資料表。  
  
 全文檢索索引鍵資料行必須定義成 900 位元組或以下。 基於效能的考量，建議您索引鍵資料行的大小，愈小愈好。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色、 **db_owner** 和 **db_ddladmin** 固定資料庫角色的成員，或是具有全文檢索目錄之參考許可權的使用者，才能夠執行 **sp_fulltext_table**。  
  
## <a name="examples"></a>範例  
  
### <a name="a-enabling-a-table-for-full-text-indexing"></a>A. 啟用資料表的全文檢索索引  
 下列範例會針對 `Document` 資料庫的 `AdventureWorks` 資料表建立全文檢索索引中繼資料。 `Cat_Desc` 是一個全文檢索目錄。 `PK_Document_DocumentID` 是 `Document` 的唯一單一資料行索引。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_table 'Production.Document', 'create', 'Cat_Desc', 'PK_Document_DocumentID';  
--Add some columns  
EXEC sp_fulltext_column 'Production.Document','DocumentSummary','add';  
-- Activate the full-text index  
EXEC sp_fulltext_table 'Production.Document','activate';  
GO  
```  
  
### <a name="b-activating-and-propagating-track-changes"></a>B. 啟動和傳播追蹤變更  
 下列範例會在發生追蹤的變更時，啟動傳播，開始將這些變更傳播給全文檢索索引。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_table 'Production.Document', 'Start_change_tracking';  
EXEC sp_fulltext_table 'Production.Document', 'Start_background_updateindex';  
GO  
```  
  
### <a name="c-removing-a-full-text-index"></a>C. 移除全文檢索索引  
 這個範例會移除 `Document` 資料庫 `AdventureWorks` 資料表的全文檢索索引中繼資料。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_table 'Production.Document', 'drop';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_help_fulltext_tables &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)   
 [sp_help_fulltext_tables_cursor &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [sp_helpindex &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)   
 [&#40;Transact-sql&#41;的系統預存程式 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [全文檢索搜尋和語義搜尋預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
