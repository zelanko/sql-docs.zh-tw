---
title: sp_indexoption (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_indexoption
- sp_indexoption_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_indexoption
ms.assetid: 75f836be-d322-4a53-a45d-25bee6b42a52
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 6bc44ee2cbce8c96b314172a2bb856a9c3346e2a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33260724"
---
# <a name="spindexoption-transact-sql"></a>sp_indexoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對使用者自訂叢集和非叢集索引，或不含叢集索引的資料表，來設定鎖定選項值。  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會自動選擇頁面、資料列或資料表層級的鎖定。 您不需要手動設定這些選項。 **sp_indexoption**專家級使用者確實特定類型的鎖定都適用。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)] 請改用[ALTER INDEX &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_indexoption [ @IndexNamePattern = ] 'table_or_index_name'   
    , [ @OptionName = ] 'option_name'   
    , [ @OptionValue = ] 'value'  
```  
  
## <a name="arguments"></a>引數  
 [  **@IndexNamePattern=**] **'***table_or_index_name***'**  
 這是使用者定義資料表或索引的完整或非完整名稱。 *table_or_index_name*是**nvarchar(1035)**，沒有預設值。 只有在指定完整索引或資料表名稱時，才會需要引號。 如果提供其中包括資料庫名稱的完整資料表名稱，資料庫名稱就必須是目前資料庫的名稱。 如果指定資料表名稱，但不含索引，且沒有任何叢集索引存在，便會將指定的選項值設給這份資料表的所有索引以及資料表本身。  
  
 [  **@OptionName =**] **'***option_name***'**  
 這是索引選項名稱。 *option_name*是**varchar （35)**，沒有預設值。 *option_name*可以有下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**AllowRowLocks**|當設為 TRUE 時，在存取索引時，允許資料列鎖定。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會決定使用資料列鎖定的時機。 當設為 FALSE 時，不會使用資料列鎖定。 預設值是 TRUE。|  
|**AllowPageLocks**|當設為 TRUE 時，在存取索引時，允許頁面鎖定。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會決定使用頁面鎖定的時機。 當設為 FALSE 時，不會使用頁面鎖定。 預設值是 TRUE。|  
|**DisAllowRowLocks**|當設為 TRUE 時，不會使用資料列鎖定。 當設為 FALSE 時，在存取索引時，允許資料列鎖定。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會決定使用資料列鎖定的時機。|  
|**DisAllowPageLocks**|當設為 TRUE 時，不會使用頁面鎖定。 當設為 FALSE 時，在存取索引時，允許頁面鎖定。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會決定使用頁面鎖定的時機。|  
  
 [  **@OptionValue =**] **'***值***'**  
 指定是否*option_name*設定為啟用 （TRUE、 ON、 yes 或 1） 或停用 (FALSE、 OFF、 no 或 0)。 *值*是**varchar(12)**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或大於零 (失敗)  
  
## <a name="remarks"></a>備註  
 不支援 XML 索引。 如果指定了 XML 索引，或指定了資料表名稱，但不含索引名稱，且資料表包含 XML 索引，陳述式便會失敗。 若要設定這些選項，請使用[ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)改為。  
  
 若要顯示的目前資料列和頁面鎖定屬性，請使用[INDEXPROPERTY](../../t-sql/functions/indexproperty-transact-sql.md)或[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)目錄檢視。  
  
-   存取索引時允許資料列、 頁面和資料表層級鎖定時**AllowRowLocks** = TRUE 或**DisAllowRowLocks** = FALSE，和**AllowPageLocks** = TRUE 或**DisAllowPageLocks** = FALSE。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會選擇適當的鎖定，且可以將鎖定從資料列或頁面鎖定擴大到資料表鎖定。  
  
 存取索引時，允許資料表層級鎖定時**AllowRowLocks** = FALSE 或**DisAllowRowLocks** = TRUE 和**AllowPageLocks** = FALSE 或**DisAllowPageLocks** = TRUE。  
  
 如果指定資料表名稱，但不含索引，設定便適用於這份資料表的所有索引。 當基礎資料表沒有叢集索引 (也就是說，它是一個堆積) 時，就會依照下列方式來套用設定：  
  
-   當**AllowRowLocks**或**DisAllowRowLocks**會設為 TRUE 或 FALSE，此設定會套用在堆積及任何相關聯的非叢集索引。  
  
-   當**AllowPageLocks**選項設定為 TRUE 或**DisAllowPageLocks**設為 FALSE，會將設定套用在堆積及任何相關聯的非叢集索引。  
  
-   當**AllowPageLocks**選項設為 FALSE 或**DisAllowPageLocks**是設為 TRUE，設定完整套用在非叢集索引。 也就是說，在非叢集索引上，不允許使用任何頁面鎖定。 在堆積上，不允許的鎖定只有頁面的共用 (S)、更新 (U) 和獨佔 (X) 鎖定。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 仍能取得意圖頁面鎖定 (IS、IU 或 IX)，供內部使用。  
  
## <a name="permissions"></a>Permissions  
 需要資料表的 ALTER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-setting-an-option-on-a-specific-index"></a>A. 設定特定索引的選項  
 下列範例會禁止在頁面鎖定`IX_Customer_TerritoryID`上的索引`Customer`資料表。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_indexoption N'Sales.Customer.IX_Customer_TerritoryID',  
    N'disallowpagelocks', TRUE;  
```  
  
### <a name="b-setting-an-option-on-all-indexes-on-a-table"></a>B. 設定資料表所有索引的選項  
 下列範例會禁止 `Product` 資料表所有相關聯索引的資料列鎖定。 在執行 `sys.indexes` 程序來顯示陳述式結果之前和之後，都會查詢 `sp_indexoption` 目錄檢視。  
  
```sql  
USE AdventureWorks2012;  
GO  
--Display the current row and page lock options for all indexes on the table.  
SELECT name, type_desc, allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE object_id = OBJECT_ID(N'Production.Product');  
GO  
-- Set the disallowrowlocks option on the Product table.   
EXEC sp_indexoption N'Production.Product',  
    N'disallowrowlocks', TRUE;  
GO  
--Verify the row and page lock options for all indexes on the table.  
SELECT name, type_desc, allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE object_id = OBJECT_ID(N'Production.Product');  
GO  
```  
  
### <a name="c-setting-an-option-on-a-table-with-no-clustered-index"></a>C. 設定不含任何叢集索引之資料表的選項  
 下列範例會禁止不含任何叢集索引之資料表 (堆積) 的頁面鎖定。 `sys.indexes`之前和之後，會查詢目錄檢視`sp_indexoption`執行程序來顯示陳述式的結果。  
  
```sql  
USE AdventureWorks2012;  
GO  
--Display the current row and page lock options of the table.   
SELECT OBJECT_NAME (object_id) AS [Table], type_desc, allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE OBJECT_NAME (object_id) = N'DatabaseLog';  
GO  
-- Set the disallowpagelocks option on the table.   
EXEC sp_indexoption DatabaseLog,  
    N'disallowpagelocks', TRUE;  
GO  
--Verify the row and page lock settings of the table.  
SELECT OBJECT_NAME (object_id) AS [Table], allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE OBJECT_NAME (object_id) = N'DatabaseLog';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  
