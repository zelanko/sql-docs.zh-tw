---
title: "DBCC CHECKCONSTRAINTS (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 11/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC CHECKCONSTRAINTS
- DBCC_CHECKCONSTRAINTS_TSQL
- CHECKCONSTRAINTS
- CHECKCONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC CHECKCONSTRAINTS statement
- consistency [SQL Server], constraints
- checking constraint consistency
- constraints [SQL Server], consistency checks
- integrity [SQL Server], constraints
ms.assetid: da6c9cee-6687-46e8-b504-738551f9068b
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2ff75ba3c32d138d9124eba5cfe170cf146d5778
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-checkconstraints-transact-sql"></a>DBCC CHECKCONSTRAINTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

檢查目前資料庫中之指定資料表的指定條件約束或所有條件約束的完整性。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DBCC CHECKCONSTRAINTS  
[   
    (   
    table_name | table_id | constraint_name | constraint_id   
    )  
]  
    [ WITH   
    [ { ALL_CONSTRAINTS | ALL_ERRORMSGS } ]  
    [ , ] [ NO_INFOMSGS ]   
    ]  
```  
  
## <a name="arguments"></a>引數  
 *table_name* | *table_id* | *constraint_name* | *constraint_id*  
 這是要檢查的資料表或條件約束。 當*table_name*或*table_id*已指定，會檢查該資料表所有已啟用條件約束。 當*constraint_name*或*constraint_id*已指定，會檢查該條件約束。 如果未指定資料表識別碼，也未指定條件約束識別碼，就會檢查目前資料庫的所有資料表中所有已啟用的條件約束。  
 條件約束名稱會唯一識別它所屬的資料表。 如需詳細資訊，請參閱＜ [Database Identifiers](../../relational-databases/databases/database-identifiers.md)＞。  
  
 取代所有提及的  
 啟用要指定的選項。  
  
 ALL_CONSTRAINTS  
 如果指定了資料表名稱，或檢查了所有資料表，便檢查資料表所有已啟用和停用的條件約束。否則，只檢查已啟用的條件約束。 當指定條件約束名稱時，ALL_CONSTRAINTS 沒有作用。  
  
 ALL_ERRORMSGS  
 傳回所有違反所檢查之資料表中條件約束的資料列。 預設值是前 200 個資料列。  
  
 NO_INFOMSGS  
 隱藏所有參考訊息。  
  
## <a name="remarks"></a>備註  
DBCC CHECKCONSTRAINTS 會針對資料表的所有 FOREIGN KEY 條件約束和 CHECK 條件約束，建構和執行查詢。
  
例如，外部索引鍵查詢的格式如下：
  
```sql
SELECT <columns>  
FROM <table_being_checked> LEFT JOIN <referenced_table>  
    ON <table_being_checked.fkey1> = <referenced_table.pkey1>   
    AND <table_being_checked.fkey2> = <referenced_table.pkey2>  
WHERE <table_being_checked.fkey1> IS NOT NULL   
    AND <referenced_table.pkey1> IS NULL  
    AND <table_being_checked.fkey2> IS NOT NULL  
    AND <referenced_table.pkey2> IS NULL  
```  
  
查詢資料儲存在暫存資料表中。 在檢查了所有要求的資料表或條件約束之後，會傳回結果集。
DBCC CHECKCONSTRAINTS 會檢查 FOREIGN KEY 和 CHECK 條件約束的完整性，但不會檢查資料表磁碟內存資料結構的完整性。 可以透過執行這些資料結構檢查[DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)和[DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)。
  
**適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
如果*table_name*或*table_id*指定和啟用系統版本設定、 DBCC CHECKCONSTRAINTS 也會執行指定的資料表上的暫時資料一致性檢查。 當*NO_INFOMSGS*未指定，此命令會傳回在輸出中每個一致性違規單獨的一行。 將輸出的格式 ([pkcol1]，[pkcol2]...) = (\<pkcol1_value >， \<pkcol2_value >...)和\<時態表的記錄有什麼 >。
  
|檢查|如果檢查失敗的輸出中的其他資訊|  
|-----------|-----------------------------------------------|  
|PeriodEndColumn ≥ PeriodStartColumn （目前）|[sys_end] = '{0}' AND MAX(DATETIME2) = '9999-12-31 23:59:59.99999'|  
|PeriodEndColumn ≥ PeriodStartColumn （目前，記錄）|[sys_start] = '{0}' 及 [sys_end] = '{1}'|  
|PeriodStartColumn < current_utc_time （目前）|[sys_start] = '{0}' 和 SYSUTCTIME|  
|PeriodEndColumn < current_utc_time （記錄）|[sys_end] = '{0}' 和 SYSUTCTIME|  
|重疊|(sys_start1 sys_end1)，(sys_start2 sys_end2) 兩個重疊的記錄。<br /><br /> 如果有多個重疊的記錄的 2，輸出將會有多個資料列各顯示一組的重疊項目。|  
  
沒有任何方法來指定 constraint_name 或 constraint_id 才能執行只時態一致性檢查。
  
## <a name="result-sets"></a>結果集  
DBCC CHECKCONSTRAINTS 會傳回含有下列資料行的資料列集。
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|資料表名稱|**varchar**|資料表的名稱。|  
|Constraint Name|**varchar**|違反的條件約束名稱。|  
|位置|**varchar**|用來識別違反條件約束的一個或多個資料列的資料行值指派。<br /><br /> 在查詢違反條件約束的資料列之 SELECT 陳述式的 WHERE 子句中，可以使用這個資料行中的值。|  
  
## <a name="permissions"></a>Permissions  
需要 **系統管理員** 固定伺服器角色或 **db_owner** 固定資料庫角色中的成員資格。
  
## <a name="examples"></a>範例  
  
### <a name="a-checking-a-table"></a>A. 檢查資料表  
下列範例會檢查 `Table1` 資料庫中 `AdventureWorks` 資料表的條件約束完整性。
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE TABLE Table1 (Col1 int, Col2 char (30));  
GO  
INSERT INTO Table1 VALUES (100, 'Hello');  
GO  
ALTER TABLE Table1 WITH NOCHECK ADD CONSTRAINT chkTab1 CHECK (Col1 > 100);  
GO  
DBCC CHECKCONSTRAINTS(Table1);  
GO  
```  
  
### <a name="b-checking-a-specific-constraint"></a>B. 檢查特定條件約束  
下列範例會檢查 `CK_ProductCostHistory_EndDate` 條件約束的完整性。
  
```sql  
USE AdventureWorks2012;  
GO  
DBCC CHECKCONSTRAINTS ('Production.CK_ProductCostHistory_EndDate');  
GO  
```  
  
### <a name="c-checking-all-enabled-and-disabled-constraints-on-all-tables"></a>C. 檢查所有資料表之所有已啟用和停用的條件約束  
 下列範例會檢查目前資料庫中所有資料表之所有已啟用和停用之條件約束的完整性。  
  
```sql  
DBCC CHECKCONSTRAINTS WITH ALL_CONSTRAINTS;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
[DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[DBCC CHECKTABLE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  
