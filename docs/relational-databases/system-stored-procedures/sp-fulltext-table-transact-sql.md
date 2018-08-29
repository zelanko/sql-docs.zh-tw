---
title: sp_fulltext_table (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_fulltext_table_TSQL
- sp_fulltext_table
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_table
ms.assetid: a765f311-07fc-4af3-b74c-e9a027fbecce
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cb6e9ec54cd4bbf038d0fe814a5101869a8e2871
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43061489"
---
# <a name="spfulltexttable-transact-sql"></a>sp_fulltext_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  標示或取消標示全文檢索索引的資料表。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md)， [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md)，並[DROP FULLTEXT INDEX](../../t-sql/statements/drop-fulltext-index-transact-sql.md)改。  
  
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
 [ **@tabname=**] **'***qualified_table_name***'**  
 這是一或兩部分的資料表名稱。 資料表必須在目前的資料庫中。 *qualified_table_name&lt*已**nvarchar(517)**，沒有預設值。  
  
 [  **@action=**] **'***動作***'**  
 這是要執行的動作。 *動作*已**nvarchar(50)**，沒有預設值，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**建立**|建立全文檢索索引所參考之資料表的中繼資料*qualified_table_name&lt* ，並指定這份資料表的全文檢索索引資料應該位於*fulltext_catalog_name*。 此動作也會指定使用*unique_index_name*全文檢索索引鍵資料行。 這個唯一索引必須已經存在，且必須在資料表的某個資料行中定義。<br /><br /> 在擴展全文檢索目錄之前，您無法執行這份資料表的全文檢索搜尋。|  
|**Drop**|卸除的全文檢索索引的中繼資料*qualified_table_name&lt*。 如果全文檢索索引在使用中，在卸除之後，也會自動停用。 在卸除全文檢索索引之前，不需要移除資料行。|  
|**Activate**|啟動全文檢索索引資料的蒐集的能力*qualified_table_name&lt*之後已停用。 至少必須有一個資料行參與全文檢索索引，您才能啟動它。<br /><br /> 只要加入了第一個索引資料行，全文檢索索引就會自動成為使用中 (以便擴展)。 如果從索引中卸除最後一個資料行，索引便會成為非使用中。 如果變更追蹤是開啟的，啟動非作用中的索引會啟動新的擴展。<br /><br /> 請注意，這實際上不會擴展全文檢索索引，但只會註冊資料表全文檢索目錄中檔案系統中因此，從資料列*qualified_table_name&lt*可以在下一步 的全文檢索索引期間擷取母體擴展。|  
|**停用**|停用的全文檢索索引*qualified_table_name&lt* ，讓全文檢索索引的資料可以不再收集*qualified_table_name&lt*。 仍會保留全文檢索索引中繼資料，且可以重新啟動資料表。<br /><br /> 如果變更追蹤是開啟的，停用使用中的索引會凍結索引狀態：任何進行中的擴展都會停止，不會再將任何其他變更傳播給索引。|  
|**start_change_tracking**|啟動全文檢索索引的累加擴展。 如果資料表沒有時間戳記，便啟動全文檢索索引的完整擴展。 啟動資料表的變更追蹤。<br /><br /> 全文檢索變更追蹤不會追蹤任何類型的全文檢索索引資料行上執行的 WRITETEXT 或 UPDATETEXT 作業**映像**，**文字**，或**ntext**。|  
|**stop_change_tracking**|停止資料表的追蹤變更。|  
|**update_index**|將目前追蹤的這組變更傳播給全文檢索索引。|  
|**start_background_updateindex**|在發生追蹤的變更時，開始將這些變更傳播給全文檢索索引。|  
|**stop_background_updateindex**|在發生追蹤的變更時，停止將這些變更傳播給全文檢索索引。|  
|**start_full**|啟動資料表的全文檢索索引的完整擴展。|  
|**start_incremental**|啟動資料表的全文檢索索引的累加擴展。|  
|**停止**|停止完整或累加擴展。|  
  
 [ **@ftcat=**] **'***fulltext_catalog_name***'**  
 是有效、 現有的全文檢索目錄名稱**建立**動作。 所有其他動作的這個參數都必須是 NULL。 *fulltext_catalog_name*已**sysname**，預設值是 NULL。  
  
 [ **@keyname=**] **'***unique_index_name***'**  
 有效的單一索引鍵資料行的唯一非 null 的索引*qualified_table_name&lt* for**建立**動作。 所有其他動作的這個參數都必須是 NULL。 *unique_index_name*已**sysname**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 全文檢索索引停用特定資料表之後，現有的全文檢索索引仍會保留直到下一步 的完整擴展;不過，此索引不會因為[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]封鎖已停用資料表上的查詢。  
  
 如果重新啟動資料表，且沒有重新擴展索引，任何其餘啟用全文檢索的非新增資料行的查詢，仍可以使用舊索引。 在指定全部全文檢索資料行搜尋的查詢中，會符合已刪除的資料行之資料。  
  
 資料表後已定義全文檢索索引時，切換全文檢索唯一索引鍵資料行從一個資料型別到另一個，藉由變更該資料行的資料類型，或從一個資料行的全文檢索唯一索引鍵變更到另一個，而不需要完整重新擴展可能會導致失敗發生在後續的查詢，並傳回錯誤訊息:"轉換為類型*data_type*無法用於全文檢索搜尋索引鍵值*key_value*。 」 若要避免這個問題，卸除此資料表使用全文檢索定義**卸除**動作**sp_fulltext_table**重新定義它使用**sp_fulltext_table**和**sp_fulltext_column**。  
  
 全文檢索索引鍵資料行必須定義成 900 位元組或以下。 基於效能的考量，建議您索引鍵資料行的大小，愈小愈好。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定伺服器角色**db_owner**並**db_ddladmin**固定資料庫角色或使用者具有全文檢索目錄可以參考權限執行**sp_fulltext_table**。  
  
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
 [遇到 sp_help_fulltext_tables &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)   
 [遇到 sp_help_fulltext_tables_cursor &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [sp_helpindex &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [全文檢索搜尋和語意搜尋預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
