---
title: sys.databases dm_exec_cached_plan_dependent_objects （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_cached_plan_dependent_objects
- dm_exec_cached_plan_dependent_objects_TSQL
- sys.dm_exec_cached_plan_dependent_objects_TSQL
- dm_exec_cached_plan_dependent_objects
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_cached_plan_dependent_objects dynamic management function
ms.assetid: 9b6cf5f7-b267-44fb-aac8-f49c9aa10cc1
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0e0eb2bd0dc0c73eb2b6bc1ece0e0f29a1eb7954
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830702"
---
# <a name="sysdm_exec_cached_plan_dependent_objects-transact-sql"></a>sys.dm_exec_cached_plan_dependent_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對每個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 執行計畫、Common Language Runtime (CLR) 執行計畫以及與計畫相關聯的資料指標，傳回資料列。  
  
## <a name="syntax"></a>語法  
  
```  
sys.dm_exec_cached_plan_dependent_objects(plan_handle)  
```  
  
## <a name="arguments"></a>引數  
*plan_handle*  
這是一個標記，可唯一識別已執行之批次的查詢執行計畫，且其計畫位於計畫快取中。 *plan_handle*為**Varbinary （64）**。   

*Plan_handle*可以從下列動態管理物件取得：  
  
-   [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  

-   [dm_exec_procedure_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  

-   [dm_exec_trigger_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**usecounts**|**int**|已經使用的執行內容或資料指標的次數。<br /><br /> 資料行不可為 Null。|  
|**memory_object_address**|**varbinary(8)**|執行內容或資料指標的記憶體位址。<br /><br /> 資料行不可為 Null。|  
|**cacheobjtype**|**nvarchar(50)**|計畫快取物件類型。 資料行不可為 Null。 可能的值為<br /><br /> 可執行的計畫<br /><br /> CLR 編譯的函數<br /><br /> CLR 編譯的程序<br /><br /> 資料指標|  
  
## <a name="permissions"></a>權限  
 需要伺服器的 `VIEW SERVER STATE` 權限。  
  
## <a name="physical-joins"></a>實體聯結  
 ![關聯性圖表](../../relational-databases/system-dynamic-management-views/media/dm-dependent-objects.gif "關聯性圖表")  
  
## <a name="relationship-cardinalities"></a>關聯性基數  
  
|從|至|開啟|關聯性|  
|----------|--------|--------|------------------|  
|**dm_exec_cached_plan_dependent_objects**|**dm_os_memory_objects**|**memory_object_address**|一對一|  
  
## <a name="see-also"></a>另請參閱  
 [執行相關的動態管理檢視和函數 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [動態管理 Views 和函數 &#40;Transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [syscacheobjects &#40;Transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md)  
  
  
