---
title: DBCC UPDATEUSAGE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- UPDATEUSAGE
- UPDATEUSAGE_TSQL
- DBCC_UPDATEUSAGE_TSQL
- DBCC UPDATEUSAGE
dev_langs:
- TSQL
helpviewer_keywords:
- inaccurate page or row counts [SQL Server]
- space [SQL Server], usage reports
- updating space usage information
- updating row counts
- disk space [SQL Server], inaccurate counts
- counting pages
- reporting count inaccuracies
- updating page counts
- synchronization [SQL Server], inaccurate counts
- incorrect space usage reports [SQL Server]
- DBCC UPDATEUSAGE statement
- integrity [SQL Server], database objects
- counting rows
- row count accuracy [SQL Server]
- page count accuracy [SQL Server]
ms.assetid: b8752ecc-db45-4e23-aee7-13b8bc3cbae2
author: pmasl
ms.author: umajay
ms.openlocfilehash: fa1bd6767a81142e115e02d242a54b9715bf78f8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85643857"
---
# <a name="dbcc-updateusage-transact-sql"></a>DBCC UPDATEUSAGE (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

報告和更正目錄檢視中不準確的頁面和資料列計數。 這些不準確可能會使 sp_spaceused 系統預存程序傳回不正確的空間使用方式報表。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```syntaxsql
DBCC UPDATEUSAGE   
(   { database_name | database_id | 0 }   
    [ , { table_name | table_id | view_name | view_id }   
    [ , { index_name | index_id } ] ]   
) [ WITH [ NO_INFOMSGS ] [ , ] [ COUNT_ROWS ] ]   
```  
  
## <a name="arguments"></a>引數  
*database_name* | *database_id* | 0  
這是要報告和更正空間使用方式統計資料之資料庫的名稱或識別碼。 如果指定 0，就會使用目前的資料庫。 資料庫名稱必須符合[識別碼](../../relational-databases/databases/database-identifiers.md)的規則。  
  
*table_name* | *table_id* | *view_name* | *view_id*  
這是要報告和更正空間使用方式統計資料之資料表或索引檢視表的名稱或識別碼。 資料表和檢視表名稱必須符合識別碼的規則。  
  
*index_id* | *index_name*  
這是要使用之索引的識別碼或名稱。 若未指定，陳述式會處理指定資料表或檢視表的所有索引。  
  
WITH  
接受即將指定的選項。  
  
NO_INFOMSGS  
隱藏所有參考訊息。  
  
COUNT_ROWS  
指定利用資料表或檢視表中目前的資料列計數來更新 row count 資料行。  
  
## <a name="remarks"></a>備註  
DBCC UPDATEUSAGE 會更正資料表或索引中的每一個資料分割的資料列、使用頁面、保留頁面、分葉頁和資料頁的計數。 如果系統資料表中沒有不準確的情況，DBCC UPDATEUSAGE 不會傳回任何資料。 如果找到且更正了不準確的情況，就不會使用 WITH NO_INFOMSGS，DBCC UPDATEUSAGE 會傳回系統資料表所更新的資料列和資料行。
  
DBCC CHECKDB 已經增強，可在頁面或資料列計數變成負數時偵測出。 偵測到時，DBCC CHECKDB 輸出會包含警告及執行 DBCC UPDATEUSAGE 來處理這個問題的建議。
  
## <a name="best-practices"></a>最佳做法  
我們的建議如下：
-   請勿例行性地執行 DBCC UPDATEUSAGE。 DBCC UPDATEUSAGE 可能需要一些時間才能在大型資料表或資料庫上執行，因此，除非您懷疑 sp_spaceused 所傳回的值不正確，否則不應僅使用它。
-   只有在資料庫進行頻繁的資料定義語言 (DDL) 修改 (如 CREATE、ALTER 或 DROP 陳述式) 時，才考慮例行地執行 DBCC UPDATEUSAGE (例如，每週)。  
  
## <a name="result-sets"></a>結果集  
DBCC UPDATEUSAGE 會傳回 (值可能不同)：
  
`DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
## <a name="permissions"></a>權限  
需要 **系統管理員** 固定伺服器角色或 **db_owner** 固定資料庫角色中的成員資格。
  
## <a name="examples"></a>範例  
  
### <a name="a-updating-page-or-row-counts-or-both-for-all-objects-in-the-current-database"></a>A. 更新目前資料庫中之所有物件的頁面及 (或) 資料列計數  
下列範例會在資料庫名稱中指定 `0`，而 `DBCC UPDATEUSAGE` 會報告目前資料庫的已更新頁面或資料列計數資訊。
  
```sql
DBCC UPDATEUSAGE (0);  
GO  
```  
  
### <a name="b-updating-page-or-row-counts-or-both-for-adventureworks-and-suppressing-informational-messages"></a>B. 更新 AdventureWorks 的頁面及 (或) 資料列計數，以及抑制參考訊息  
下列範例會將資料庫名稱指定為 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]，且會抑制所有參考訊息。
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012) WITH NO_INFOMSGS;   
GO  
```  
  
### <a name="c-updating-page-or-row-counts-or-both-for-the-employee-table"></a>C. 更新 Employee 資料表的頁面及 (或) 資料列計數  
下列範例會報告 `Employee` 資料庫中 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料表的已更新頁面或資料列計數資訊。
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012,'HumanResources.Employee');  
GO  
```  
  
### <a name="d-updating-page-or-row-counts-or-both-for-a-specific-index-in-a-table"></a>D. 更新資料表中特定索引的頁面及 (或) 資料列計數  
 下列範例會指定 `IX_Employee_ManagerID` 來做為索引名稱。  
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012, 'HumanResources.Employee', IX_Employee_OrganizationLevel_OrganizationNode);  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)  
[UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)
  
  
