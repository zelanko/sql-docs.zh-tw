---
title: SET RESULT SET CACHING  (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/03/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords: ''
dev_langs:
- TSQL
helpviewer_keywords: ''
author: XiaoyuL-Preview
ms.author: xiaoyul
manager: craigg
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: cd0141a6fbd21c11f7401fa2c45dae0cc75b983d
ms.sourcegitcommit: ccea98fa0768d01076cb6ffef0b4bdb221b2f9d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2019
ms.locfileid: "65561491"
---
# <a name="set-result-set-caching-transact-sql"></a>SET RESULT SET CACHING (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

使 Azure SQL 資料倉儲快取查詢結果集。
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法

```
SET RESULT_SET_CACHING { ON | OFF };
```  
  
## <a name="remarks"></a>Remarks  
  
此命令必須在連線到 master 資料庫時執行。  對此資料庫設定的變更會立即生效。  儲存體費用會以快取查詢結果集的數目計算。 停用資料庫的結果快取後，會立即從 Azure SQL 資料倉儲儲存體中刪除先前保存的結果快取。 我們在 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql?view=azure-sqldw-latest
) 中引進了稱為 is_result_set_caching_on 的新資料行，用來顯示資料庫的結果快取設定。  

**ON** 指定從此資料庫傳回的查詢結果集會在 Azure SQL 資料倉儲儲存體中進行快取。

**OFF** 指定從此資料庫傳回的查詢結果集不會在 Azure SQL 資料倉儲儲存體進行快取。

使用者可以使用特定的 request_id 查詢 [sys.pdw_request_steps](/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql?view=azure-sqldw-latest)，來得知所執行查詢的結果快取為命中或是遺漏。 若有快取命中，則查詢結果會具有包含下列詳細資料的單一步驟：

|**資料行名稱**|**[運算子]**|**ReplTest1**|
|----|----|----|
|operation_type|=|ReturnOperation|
|step_index|=|0|
|location_type|=|Control|
|command|相似|%DWResultCacheDb%|
||||
  
## <a name="permissions"></a>權限

需要下列權限：

- 由佈建程序建立的伺服器層級主體登入，或
- dbmanager 資料庫角色的成員。

除非資料庫擁有者是 dbmanager 角色的成員，否則無法改變資料庫。
  
## <a name="examples"></a>範例

### <a name="enable-result-set-caching-for-a-database"></a>啟用資料庫的結果集快取

```sql
ALTER DATABASE myTestDW  
SET RESULT_SET_CACHING ON;
```

### <a name="disable-result-set-caching-for-a-database"></a>停用資料庫的結果集快取

```sql
ALTER DATABASE myTestDW  
SET RESULT_SET_CACHING OFF;
```

### <a name="check-result-set-caching-setting-for-a-database"></a>檢查資料庫的結果集快取設定

```sql
SELECT name, is_result_set_caching  
FROM sys.databases
```

### <a name="check-for-number-of-queries-with-result-set-cache-hit-and-cache-miss"></a>檢查結果集快取命中和快取遺漏的查詢數

```sql
SELECT  
Queries=CacheHits+CacheMisses,
CacheHits,
CacheMisses,
CacheHitPct=CacheHits*1.0/(CacheHits+CacheMisses)
FROM  
(SELECT  
CacheHits=count(distinct case when s.command like '%DWResultCacheDb%' and
r.resource_class IS NULL and s.operation_type = 'ReturnOperation' and  
s.step_index = 0 then s.request_id else null end) ,
CacheMisses=count(distinct case when r.resource_class IS NOT NULL then  
s.request_id else null end)
     FROM sys.dm_pdw_request_steps s  
     JOIN sys.dm_pdw_exec_requests r  
     ON s.request_id = r.request_id) A
```

### <a name="check-for-result-set-cache-hit-or-cache-miss-for-a-query"></a>檢查查詢的結果集快取命中或快取遺漏

```sql
If
(SELECT step_index  
FROM sys.dm_pdw_request_steps  
WHERE request_id = 'QID58286'
      and operation_type = 'ReturnOperation'
      and command like '%DWResultCacheDb%') = 0
SELECT 1 as is_cache_hit  
ELSE
SELECT 0 as is_cache_hit
```

### <a name="check-for-all-queries-with-result-set-cache-hits"></a>檢查結果集快取命中的所有查詢

```sql
SELECT *  
FROM sys.dm_pdw_request_steps  
WHERE command like '%DWResultCacheDb%' and step_index = 0
```

## <a name="see-also"></a>另請參閱

[SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)</br>
[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)