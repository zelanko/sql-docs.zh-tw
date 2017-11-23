---
title: "卸除統計資料 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/22/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP STATISTICS
- DROP_STATISTICS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- removing statistics
- column statistics [SQL Server]
- DROP STATISTICS statement
- deleting statistics
- dropping statistics
- table statistics [SQL Server]
- statistical information [SQL Server], removing
ms.assetid: 222806b7-4e45-445b-8cd0-bd5461f3ca4a
caps.latest.revision: "41"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 34cc65eaccfdfcbffd38e93f613f2b2d34de23d0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="drop-statistics-transact-sql"></a>DROP STATISTICS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  卸除目前資料庫中指定資料表內多個集合的統計資料。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP STATISTICS table.statistics_name | view.statistics_name [ ,...n ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP STATISTICS [ schema_name . ] table_name.statistics_name   
[;]  
```  
  
## <a name="arguments"></a>引數  
 *資料表* | *檢視*  
 這是應該卸除統計資料之目標資料表或索引檢視的名稱。 資料表和檢視表名稱必須遵守的規則[資料庫識別項](../../relational-databases/databases/database-identifiers.md)。 資料表或檢視擁有者名稱的指定是選擇性的。  
  
 *statistics_name*  
 這是要卸除的統計資料群組名稱。 統計資料名稱必須符合識別碼的規則。  
  
## <a name="remarks"></a>備註  
 當您卸除統計資料時，請小心。 執行這個動作，可能會影響查詢最佳化工具所選擇的執行計畫。  
  
 索引的統計資料無法利用 DROP STATISTICS 來卸除。 只要索引存在，就會保留統計資料。  
  
 如需有關顯示統計資料的詳細資訊，請參閱[DBCC SHOW_STATISTICS &#40;TRANSACT-SQL &#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 需要資料表或檢視表的 ALTER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-dropping-statistics-from-a-table"></a>A. 從資料表卸除統計資料  
 下列範例會卸除兩份資料表的統計資料群組 (集合)。 `VendorCredit` 資料表的 `Vendor` 統計資料群組 (集合) 和 `CustomerTotal` 資料表的 `SalesOrderHeader` 統計資料 (集合) 都會卸除。  
  
```  
-- Create the statistics groups.  
USE AdventureWorks2012;  
GO  
CREATE STATISTICS VendorCredit  
    ON Purchasing.Vendor (Name, CreditRating)  
    WITH SAMPLE 50 PERCENT  
CREATE STATISTICS CustomerTotal  
    ON Sales.SalesOrderHeader (CustomerID, TotalDue)  
    WITH FULLSCAN;  
GO  
DROP STATISTICS Purchasing.Vendor.VendorCredit, Sales.SalesOrderHeader.CustomerTotal;  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-dropping-statistics-from-a-table"></a>B. 從資料表卸除統計資料  
 下列範例卸除`CustomerStats1`從資料表的統計資料`Customer`。  
  
```  
DROP STATISTICS Customer.CustomerStats1;  
DROP STATISTICS dbo.Customer.CustomerStats1;  
  
```  
  
## <a name="see-also"></a>請參閱＜  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [sys.stats_columns &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [sp_autostats &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_createstats &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  
  
  


