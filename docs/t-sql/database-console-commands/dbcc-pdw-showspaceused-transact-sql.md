---
title: "DBCC PDW_SHOWSPACEUSED (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.service: sql-data-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
caps.latest.revision: 10
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4a16d4a7a10eb4f36d0ead2a19f8e37d251e417f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-pdwshowspaceused-transact-sql"></a>DBCC PDW_SHOWSPACEUSED (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

顯示的資料列、 保留的磁碟空間和用於特定的資料表，或所有資料表中的磁碟空間數目[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]資料庫。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [TRANSACT-SQL 語法慣例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Show the space used for all user tables and system tables in the current database  
DBCC PDW_SHOWSPACEUSED  
[;]  
  
-- Show the space used for a table  
DBCC PDW_SHOWSPACEUSED ( " [ database_name . [ schema_name ] . ] | [ schema_name .] table_name  " )  
[;]  
```  
  
## <a name="arguments"></a>引數  
 [ *database_name* 。 [ *schema_name* ]。 | *schema_name* 。 ] *table_name*  
 一個、 兩個或三部分名稱，要顯示的資料表。 兩個或三部分資料表名稱，名稱必須括在雙引號 ("")。 使用引號括住的一段式資料表名稱是選擇性的。 指定沒有資料表名稱時，會顯示目前的資料庫資訊。  
  
## <a name="permissions"></a>Permissions  
需要 VIEW SERVER STATE 權限。
  
## <a name="result-sets"></a>結果集  
這是結果集中的所有資料表。
  
|資料行|資料類型|Description|  
|------------|---------------|-----------------|  
|reserved_space|bigint|使用資料庫，以 kb 為單位的總空間。|  
|data_space|bigint|用於資料，以 kb 為單位的空間。|  
|index_space|bigint|使用索引，以 kb 為單位的空間。|  
|unused_space|bigint|是保留的空間的一部分，也未使用，以 kb 為單位的空間。|  
|pdw_node_id|int|用於資料的計算節點。|  
  
這是結果集中的一個資料表。
  
|資料行|資料類型|Description|範圍|  
|------------|---------------|-----------------|-----------|  
|rows|bigint|資料列數目。||  
|reserved_space|bigint|保留物件，以 kb 為單位的總空間。||  
|data_space|bigint|使用的資料，以 kb 為單位的空間。||  
|index_space|bigint|使用索引，以 kb 為單位的空間。||  
|unused_space|bigint|是保留的空間的一部分，也未使用，以 kb 為單位的空間。||  
|pdw_node_id|int|用於報告的空間使用量的計算節點。||  
|distribution_id|int|用於報告的空間使用量的分配。|值為-1 可進行複寫的資料表。|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdwshowspaceused-basic-syntax"></a>A. DBCC PDW_SHOWSPACEUSED 基本語法  
下列範例顯示多個方式來顯示資料列數目、 磁碟空間保留，並使用 FactInternetSales 資料表中的磁碟空間[!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)]資料庫。
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012.dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012..FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( FactInternetSales );  
```  
  
### <a name="b-show-the-disk-space-used-by-all-tables-in-the-current-database"></a>B. 顯示目前資料庫中的所有資料表所使用的磁碟空間  
 下列範例示範保留和所有使用者資料表和系統資料表中的所使用的磁碟空間[!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)]資料庫。  
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED;  
```  
 ## <a name="see-also"></a>另請參閱
[DBCC PDW_SHOWEXECUTIONPLAN &#40;TRANSACT-SQL &#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWPARTITIONSTATS &#40;TRANSACT-SQL &#41;](dbcc-pdw-showpartitionstats-transact-sql.md)

  

