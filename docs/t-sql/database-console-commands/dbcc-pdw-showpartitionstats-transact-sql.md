---
title: "DBCC PDW_SHOWPARTITIONSTATS (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/17/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|database-console-commands
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
caps.latest.revision: "10"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fb41140783d4c334e7ee701f44d523ec68e41435
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="dbcc-pdwshowpartitionstats-transact-sql"></a>DBCC PDW_SHOWPARTITIONSTATS (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

顯示大小和每個資料分割的資料表中的資料列數目[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]資料庫。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [TRANSACT-SQL 語法慣例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
Show the partition stats for a table  
DBCC PDW_SHOWPARTITIONSTATS ( " [ database_name . [ schema_name ] . ] | [ schema_name.] table_name  ")  
[;]  
```  
  
## <a name="arguments"></a>引數  
 [ *database_name* 。 [ *schema_name* ]。 | *schema_name* 。 ] *table_name*  
 一個、 兩個或三部分名稱，要顯示的資料表。  兩個或三部分資料表名稱，名稱必須括在雙引號 ("")。 使用引號括住的一段式資料表名稱是選擇性的。  
  
## <a name="permissions"></a>Permissions
需要**VIEW SERVER STATE**權限。
  
## <a name="result-sets"></a>結果集  
這是 DBCC PDW_SHOWPARTITIONSTATS 命令的結果。
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|partition_number|int|資料分割編號。|  
|used_page_count|bigint|針對資料使用的頁面數目。|  
|reserved_page_count|bigint|分割區配置的頁面數目。|  
|row_count|bigint|資料分割中的資料列數目。|  
|pdw_node_id|int|計算節點的資料。|  
|distribution_id|int|散發資料的識別碼。|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdwshowpartitionstats-basic-syntax-examples"></a>A. DBCC PDW_SHOWPARTITIONSTATS 基本語法範例  
下列範例會顯示已使用空間和資料列數目 FactInternetSales 資料表中的資料分割所[!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)]資料庫。
  
```sql
DBCC PDW_SHOWPARTITIONSTATS ("ssawPDW.dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS ("dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS (FactInternetSales);  
```  
## <a name="see-also"></a>另請參閱
[DBCC PDW_SHOWEXECUTIONPLAN &#40;TRANSACT-SQL &#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWSPACEUSED &#40;TRANSACT-SQL &#41;](dbcc-pdw-showspaceused-transact-sql.md)  
  
