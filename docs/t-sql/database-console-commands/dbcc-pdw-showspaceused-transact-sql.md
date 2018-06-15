---
title: DBCC PDW_SHOWSPACEUSED (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
caps.latest.revision: 10
author: edmacauley
ms.author: umajay
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: b372a5cb516dbbeaa2732dfbfa676921d63708f3
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
ms.locfileid: "33701911"
---
# <a name="dbcc-pdwshowspaceused-transact-sql"></a>DBCC PDW_SHOWSPACEUSED (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

顯示 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 或 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 資料庫中的資料列數目、保留的磁碟空間和 特定的資料表或所有資料表使用的磁碟空間。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
-- Show the space used for all user tables and system tables in the current database  
DBCC PDW_SHOWSPACEUSED  
[;]  
  
-- Show the space used for a table  
DBCC PDW_SHOWSPACEUSED ( " [ database_name . [ schema_name ] . ] | [ schema_name .] table_name  " )  
[;]  
```  
  
## <a name="arguments"></a>引數  
 [ *database_name* . [ *schema_name* ] . | *schema_name* . ] *table_name*  
 要顯示的資料表的一段式、兩段式或三段式名稱。 兩段式或三段式的資料表名稱必須以雙引號 ("") 括住。 您可以選擇是否使用引號括住一段式資料表名稱。 未指定資料表名稱時，會顯示目前資料庫的資訊。  
  
## <a name="permissions"></a>Permissions  
需要 VIEW SERVER STATE 權限。
  
## <a name="result-sets"></a>結果集  
這是所有資料表的結果集。
  
|「資料行」|資料類型|描述|  
|------------|---------------|-----------------|  
|reserved_space|BIGINT|資料庫使用的總空間 (KB)。|  
|data_space|BIGINT|資料使用的空間 (KB)。|  
|index_space|BIGINT|索引使用的空間 (KB)。|  
|unused_space|BIGINT|保留未使用的空間 (KB)。|  
|pdw_node_id|ssNoversion|資料使用的計算節點。|  
  
這是單一資料表的結果集。
  
|「資料行」|資料類型|描述|範圍|  
|------------|---------------|-----------------|-----------|  
|rows|BIGINT|資料列數目。||  
|reserved_space|BIGINT|為物件保留的總空間 (KB)。||  
|data_space|BIGINT|資料使用的空間 (KB)。||  
|index_space|BIGINT|索引使用的空間 (KB)。||  
|unused_space|BIGINT|保留未使用的空間 (KB)。||  
|pdw_node_id|ssNoversion|用於報告空間使用量的計算節點。||  
|distribution_id|ssNoversion|用於報告空間使用量的分佈。|複寫資料表的值為 -1。|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdwshowspaceused-basic-syntax"></a>A. DBCC PDW_SHOWSPACEUSED 基本語法  
下列範例示範的多種方式可用來顯示 [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] 資料庫中的資料列數目、保留的磁碟空間和 FactInternetSales 資料表使用的磁碟空間。
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012.dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012..FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( FactInternetSales );  
```  
  
### <a name="b-show-the-disk-space-used-by-all-tables-in-the-current-database"></a>B. 顯示目前資料庫中的所有資料表使用的磁碟空間  
 下列範例示範 [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] 資料庫中的所有使用者資料表和系統資料表保留和使用的磁碟空間。  
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED;  
```  
 ## <a name="see-also"></a>另請參閱
[DBCC PDW_SHOWEXECUTIONPLAN &#40;Transact-SQL&#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWPARTITIONSTATS &#40;Transact-SQL&#41;](dbcc-pdw-showpartitionstats-transact-sql.md)

  
