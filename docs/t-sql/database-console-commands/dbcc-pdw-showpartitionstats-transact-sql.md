---
title: DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: pmasl
ms.author: umajay
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 4cb7824e3efd5a0d6cca969a790834a4e61968cb
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2020
ms.locfileid: "86196906"
---
# <a name="dbcc-pdw_showpartitionstats-transact-sql"></a>DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

顯示 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 或 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 資料庫的資料表中每個分割區的資料列大小和數目。
  
![文章連結圖示](../../database-engine/configure-windows/media/topic-link.gif "文章連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```syntaxsql
Show the partition stats for a table  
DBCC PDW_SHOWPARTITIONSTATS ( " [ database_name . [ schema_name ] . ] | [ schema_name.] table_name  ")  
[;]  
```  
  
## <a name="arguments"></a>引數  
 `[ database_name . [ schema_name ] . | schema_name . ] table_name`  
 要顯示的資料表的一段式、兩段式或三段式名稱。  兩段式或三段式的資料表名稱必須以雙引號 ("") 括住。 您可以選擇是否使用引號括住一段式資料表名稱。  
  
## <a name="permissions"></a>權限
需要 **VIEW SERVER STATE** 權限。
  
## <a name="result-sets"></a>結果集  
此集合為 DBCC PDW_SHOWPARTITIONSTATS 命令的結果。
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|partition_number|int|資料分割編號。|  
|used_page_count|BIGINT|資料的使用頁數。|  
|reserved_page_count|BIGINT|分割區的保留頁數。|  
|row_count|BIGINT|分割區中的資料列數。|  
|pdw_node_id|int|資料的計算節點。|  
|distribution_id|int|資料的散發識別碼。|  
  
## <a name="examples-sssdw-and-sspdw"></a>範例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdw_showpartitionstats-basic-syntax-examples"></a>A. DBCC PDW_SHOWPARTITIONSTATS 基本語法範例  
下列範例依分割區顯示 [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] 資料庫中 FactInternetSales 資料表的已使用空間和資料列數目。
  
```sql
DBCC PDW_SHOWPARTITIONSTATS ("ssawPDW.dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS ("dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS (FactInternetSales);  
```  
## <a name="see-also"></a>另請參閱
[DBCC PDW_SHOWEXECUTIONPLAN &#40;Transact-SQL&#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWSPACEUSED &#40;Transact-SQL&#41;](dbcc-pdw-showspaceused-transact-sql.md)  
 
