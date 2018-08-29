---
title: sys.dm_exec_query_optimizer_info (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_query_optimizer_info_TSQL
- dm_exec_query_optimizer_info
- sys.dm_exec_query_optimizer_info_TSQL
- sys.dm_exec_query_optimizer_info
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_optimizer_info dynamic management view
ms.assetid: 1d72cef1-22d8-4ae0-91db-6694fe918c9e
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a259a4f7a3f041810342e6dabc538854680dae98
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43060457"
---
# <a name="sysdmexecqueryoptimizerinfo-transact-sql"></a>sys.dm_exec_query_optimizer_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢最佳化工具作業的詳細統計資料。 您可以使用這個檢視來調整工作負載，找出查詢最佳化的問題或可供改善之處。 例如，您可以使用最佳化總數、經過時間值和最終成本值，比較目前工作負載的查詢最佳化以及調整過程中所觀察到的任何變化。 部分計數器只提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部診斷使用的相關資料。 這些計數器會標示「僅供內部使用」。  
  
> [!NOTE]  
>  若要呼叫這個屬性從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或是[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_exec_query_optimizer_info**。  
  
|名稱|資料類型|描述|  
|----------|---------------|-----------------|  
|**counter**|**nvarchar(4000)**|最佳化工具統計資料事件的名稱。|  
|**相符項目**|**bigint**|這個計數器最佳化事件的出現次數。|  
|**value**|**float**|每一事件發生的平均屬性值。|  
|**pdw_node_id**|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 這個分佈是在節點的識別碼。|  
  
## <a name="permissions"></a>Permissions  

在  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在  [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   
    
## <a name="remarks"></a>備註  
 **sys.dm_exec_query_optimizer_info**包含下列屬性 （計數器）。 所有發生值會累計並在系統重新啟動時設為 0。 所有值欄位的值於系統重新啟動時設為 NULL。 所有指定平均值的值資料行值會使用來自同一資料列的發生值作為平均值計算中的分母。 所有查詢最佳化時測量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]判斷變更**dm_exec_query_optimizer_info**，包括這兩個使用者和系統產生的查詢。 已快取的計劃的執行不會變更中的值**dm_exec_query_optimizer_info**，只有最佳化是顯著。  
  
|計數器|出現次數|值|  
|-------------|----------------|-----------|  
|最佳化數|最佳化的總數。|不適用|  
|經歷的時間|最佳化的總數。|個別陳述式 (查詢) 的每一最佳化平均經過的時間 (以秒為單位)。|  
|最終成本|最佳化的總數。|最佳化計畫的平均估計成本，以內部成本單位表示。|  
|一般計畫|僅供內部使用|僅供內部使用|  
|工作|僅供內部使用|僅供內部使用|  
|沒有計畫|僅供內部使用|僅供內部使用|  
|搜尋 0|僅供內部使用|僅供內部使用|  
|搜尋 0 時間|僅供內部使用|僅供內部使用|  
|搜尋 0 工作|僅供內部使用|僅供內部使用|  
|搜尋 1|僅供內部使用|僅供內部使用|  
|搜尋 1 時間|僅供內部使用|僅供內部使用|  
|搜尋 1 工作|僅供內部使用|僅供內部使用|  
|搜尋 2|僅供內部使用|僅供內部使用|  
|搜尋 2 時間|僅供內部使用|僅供內部使用|  
|搜尋 2 工作|僅供內部使用|僅供內部使用|  
|階段 0 到階段 1 增量|僅供內部使用|僅供內部使用|  
|階段 1 到階段 2 增量|僅供內部使用|僅供內部使用|  
|timeout|僅供內部使用|僅供內部使用|  
|超出記憶體限制|僅供內部使用|僅供內部使用|  
|INSERT 陳述式|INSERT 陳述式的最佳化數目。|不適用|  
|DELETE 陳述式|DELETE 陳述式的最佳化數目。|不適用|  
|UPDATE 陳述式|UPDATE 陳述式的最佳化數目。|不適用|  
|包含子查詢|包含至少一個子查詢之查詢的最佳化數目。|不適用|  
|UNNEST 失敗|僅供內部使用|僅供內部使用|  
|資料表|最佳化的總數。|每一最佳化查詢所參考資料表的平均數。|  
|提示|指定某個提示的次數。 計數的提示包括：JOIN、GROUP、UNION 和 FORCE ORDER 查詢提示、FORCE PLAN 設定選項，以及聯結提示。|不適用|  
|ORDER 提示|指定 FORCE ORDER 提示的次數。|不適用|  
|聯結提示|聯結提示強制執行聯結演算法的次數。|不適用|  
|檢視參考|檢視在查詢中被參考的次數。|不適用|  
|遠端查詢|查詢參考最少一個遠端資料來源 (如具有四部分名稱的資料表或 OPENROWSET 結果) 的最佳化數目。|不適用|  
|最大 DOP|最佳化的總數。|最佳化計畫的平均有效 MAXDOP 值。 根據預設，有效 MAXDOP 由**的最大平行處理原則程度**伺服器組態選項，並可能會覆寫特定查詢的 MAXDOP 查詢提示值。|  
|最大遞迴層級|查詢提示指定 MAXRECURSION 層級大於 0 的最佳化數目。|查詢提示指定最大遞迴層級之最佳化的平均 MAXRECURSION 層級。|  
|索引檢視已載入|僅供內部使用|僅供內部使用|  
|相符的索引檢視|與一或多份索引檢視相符的最佳化數目。|相符檢視的平均數。|  
|使用的索引檢視|在比對之後，一個或多個索引檢視在輸出計畫中使用的最佳化數目。|使用檢視的平均數。|  
|更新的索引檢視|產生維護一個或多個索引檢視之計畫的 DML 陳述式最佳化數目。|維護檢視的平均數。|  
|動態資料指標要求|指定動態資料指標要求的最佳化數目。|不適用|  
|向前快轉資料指標要求|指定向前快轉資料指標要求的最佳化數目。|不適用|  
|合併 stmt|MERGE 陳述式的最佳化數目。|不適用|  
  
## <a name="examples"></a>範例  
  
### <a name="a-viewing-statistics-on-optimizer-execution"></a>A. 檢視最佳化工具執行的統計資料  
 哪些是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之這個執行個體目前的最佳化工具執行統計資料？  
  
```  
SELECT * FROM sys.dm_exec_query_optimizer_info;  
```  
  
### <a name="b-viewing-the-total-number-of-optimizations"></a>B. 檢視最佳化總數  
 執行幾次最佳化？  
  
```  
SELECT occurrence AS Optimizations FROM sys.dm_exec_query_optimizer_info  
WHERE counter = 'optimizations';  
```  
  
### <a name="c-average-elapsed-time-per-optimization"></a>C. 每一次最佳化的平均經過時間  
 每一次最佳化平均經過多少時間？  
  
```  
SELECT ISNULL(value,0.0) AS ElapsedTimePerOptimization  
FROM sys.dm_exec_query_optimizer_info WHERE counter = 'elapsed time';  
```  
  
### <a name="d-fraction-of-optimizations-that-involve-subqueries"></a>D. 與子查詢相關的最佳化分數  
 有多少比例的最佳化查詢包含子查詢？  
  
```  
SELECT (SELECT CAST (occurrence AS float) FROM sys.dm_exec_query_optimizer_info WHERE counter = 'contains subquery') /  
       (SELECT CAST (occurrence AS float)   
        FROM sys.dm_exec_query_optimizer_info WHERE counter = 'optimizations')  
        AS ContainsSubqueryFraction;  
```  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [執行相關的動態管理檢視和函式 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


