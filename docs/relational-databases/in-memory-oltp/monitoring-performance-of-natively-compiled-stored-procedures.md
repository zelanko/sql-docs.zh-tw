---
title: 監視原生編譯預存程序的效能 | Microsoft Docs
ms.custom: ''
ms.date: 04/03/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 55548cb2-77a8-4953-8b5a-f2778a4f13cf
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f3b341f6e40fdc5acf618d3f81c5932b9be50149
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65106225"
---
# <a name="monitoring-performance-of-natively-compiled-stored-procedures"></a>監視原生編譯預存程序的效能

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  本文討論如何監視原生編譯預存程序和其他原生編譯 T-SQL 模組的效能。  
  
## <a name="using-extended-events"></a>使用擴充的事件  
 使用 **sp_statement_completed** 擴充事件來追蹤查詢的執行。 以此事件建立擴充事件工作階段，選擇性地針對特定原生編譯預存程序篩選 object_id。 執行每項查詢之後都將引發此擴充事件。 擴充事件所報告的 CPU 時間和持續時間代表了查詢的 CPU 使用率和執行時間。 原生編譯預存程序若佔用大量的 CPU 時間，可能就會導致效能問題。  
  
 **line_number**連同擴充事件中的 **object_id** 皆可用來調查查詢。 使用下列查詢即可擷取程序定義。 行號可用來識別定義內的查詢：  
  
```sql  
SELECT [definition]
    from sys.sql_modules
    where object_id=object_id;
```  
  
  
## <a name="using-data-management-views-and-query-store"></a>使用資料管理檢視和查詢存放區
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 支援收集原生編譯預存程序在程序層級和查詢層級的執行統計資料。 收集執行統計資料會影響效能，所以預設並未啟用。  

執行統計資料會反映在系統檢視表 [sys.dm_exec_procedure_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md) 和 [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)，也會反映在[查詢存放區](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)。

## <a name="procedure-level-execution-statistics"></a>程序層級執行統計資料

**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**：使用 [sys.sp_xtp_control_proc_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md) 在程序層級啟用或停用原生編譯預存程序的統計資料收集。  下列陳述式可以在目前的執行個體上啟用所有原生編譯 T-SQL 模組的程序層級執行統計資料收集：
```sql
EXEC sys.sp_xtp_control_proc_exec_stats 1
```

**[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]**：使用 [database-scoped configuration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 選項 `XTP_PROCEDURE_EXECUTION_STATISTICS` 來在程序層級啟用或停用原生編譯預存程序的統計資料收集。 下列陳述式可以在目前的資料庫上啟用所有原生編譯 T-SQL 模組的程序層級執行統計資料收集：
```sql
ALTER DATABASE
    SCOPED CONFIGURATION
    SET XTP_PROCEDURE_EXECUTION_STATISTICS = ON;
```

## <a name="query-level-execution-statistics"></a>查詢層級執行統計資料

**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**：使用 [sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md) 在查詢層級啟用和停用原生編譯預存程序的統計資料收集。  下列陳述式可以在目前的執行個體上啟用所有原生編譯 T-SQL 模組的查詢層級執行統計資料收集：
```sql
EXEC sys.sp_xtp_control_query_exec_stats 1
```

**[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]**：使用 [database-scoped configuration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 選項 `XTP_QUERY_EXECUTION_STATISTICS` 在陳述式層級啟用或停用原生編譯預存程序的統計資料收集。 下列陳述式可以在目前的資料庫上啟用所有原生編譯 T-SQL 模組的陳述式層級執行統計資料收集：
```sql
ALTER DATABASE
    SCOPED CONFIGURATION
    SET XTP_QUERY_EXECUTION_STATISTICS = ON;
```

## <a name="sample-queries"></a>範例查詢

 收集統計資料之後，使用 [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md) 和 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) 分別可查詢原生編譯預存程序的程序層級和查詢層級執行統計資料。  
 
  
 下列查詢會在收集統計資料之後傳回目前資料庫中原生編譯預存程序的程序名稱和執行統計資料：  

```sql
SELECT
        object_id,
        object_name(object_id) as 'object name',
        cached_time,
        last_execution_time,  execution_count,
        total_worker_time,    last_worker_time,
        min_worker_time,      max_worker_time,
        total_elapsed_time,   last_elapsed_time,
        min_elapsed_time,     max_elapsed_time
    from
        sys.dm_exec_procedure_stats
    where
        database_id = db_id()
        and
        object_id in
            (
            SELECT object_id
                from sys.sql_modules
                where uses_native_compilation=1
            )
    order by
        total_worker_time desc;
```

下列查詢會傳回目前資料庫中已收集統計資料的原生編譯預存程序內，所有查詢的查詢文字和執行統計資料，依工作者時間總計以遞減順序排序：  

```sql
SELECT
        st.objectid,
        object_name(st.objectid) as 'object name',
        SUBSTRING()
            st.text,
            (qs.statement_start_offset/2) + 1,
            ((qs.statement_end_offset-qs.statement_start_offset)/2) + 1
            ) as 'query text',
        qs.creation_time,
        qs.last_execution_time,   qs.execution_count,
        qs.total_worker_time,     qs.last_worker_time,
        qs.min_worker_time,       qs.max_worker_time,
        qs.total_elapsed_time,    qs.last_elapsed_time,
        qs.min_elapsed_time,      qs.max_elapsed_time
    FROM
                    sys.dm_exec_query_stats qs
        cross apply sys.dm_exec_sql_text(sql_handle) st
    WHERE
        st.dbid = db_id()
        and
        st.objectid in
            (SELECT object_id
                from sys.sql_modules
                where uses_native_compilation=1
            )
    ORDER BY
        qs.total_worker_time desc;
```

## <a name="query-execution-plans"></a>查詢執行計畫

 原生編譯預存程序支援 SHOWPLAN_XML (估計執行計畫)。 估計執行計畫可用來檢查查詢計劃，以找出任何的計劃錯誤問題。 計劃錯誤的常見原因包括：  
  
-   在建立程序之前未先更新統計資料。  
  
-   遺漏索引。  
  
 執行程序表 XML 可透過執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)]取得：  
  
```sql  
SET SHOWPLAN_XML ON  
GO  
EXEC my_proc   
GO  
SET SHOWPLAN_XML OFF  
GO  
```  
  
 或者，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中選取程序名稱，然後按一下 **[顯示估計執行計畫]**。  
  
 原生編譯預存程序的估計執行計畫會顯示程序內各查詢的查詢運算子和運算式。 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 並未支援原生編譯預存程序的所有 SHOWPLAN_XML 屬性。 例如，與查詢最佳化工具成本相關的屬性並未納入程序的 SHOWPLAN_XML。  
  
## <a name="see-also"></a>另請參閱  
 [原生編譯的預存程序](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
