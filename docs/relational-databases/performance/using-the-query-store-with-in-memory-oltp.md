---
title: 使用含有記憶體內部 OLTP 的查詢存放區 | Microsoft 文件
ms.custom: ''
ms.date: 03/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store, in-memory
ms.assetid: aae5ae6d-7c90-4661-a1c5-df704319888a
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: db274ccde27abf92617e0eadf95b1971e740705a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "72251291"
---
# <a name="using-the-query-store-with-in-memory-oltp"></a>使用含有記憶體內部 OLTP 的查詢存放區
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢存放區可讓您針對執行記憶體內部 OLTP 的工作負載，監視原生編譯程式碼的效能。  
編譯和執行階段統計資料是使用與以磁碟為基礎的工作負載相同的方式來收集與公開。   
當您移轉至記憶體內部 OLTP 時，可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中繼續使用查詢存放區檢視，以及您在移轉之前針對以磁碟為基礎的工作負載開發的自訂指令碼。 這可節省您在學習查詢存放區技術方面的投資，而且通常可使用它來移難排解所有類型的工作負載。  
如需使用查詢存放區的一般資訊，請參閱 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)。  
  
 使用含有記憶體內部 OLTP 的查詢存放區不需要任何額外的功能組態。 當您在資料庫上啟用此功能時，它就能用於所有類型的工作負載。   
不過，有一些特定層面是使用者在使用含有記憶體內部 OLTP 的查詢存放區時應該了解的︰  
  
-   啟用查詢存放區時，預設會收集查詢、計劃和編譯時間統計資料。 不過，除非您明確使用 [sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md) 明確啟用執行階段統計資料收集，則不會啟用此功能。  
  
-   當您將 *\@new_collection_value* 設定為 0 時，查詢存放區將針對受影響的程序或整個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，停止收集執行階段統計資料。  
  
-   使用 [sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md) 設定的值不會保留。 請務必在重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之後，再次檢查並設定統計資料收集。  
  
-   如同一般查詢統計資料收集的情況，當您使用查詢存放區來追蹤工作負載執行時，可能會降低效能。 您可能想要考慮只針對原生編譯預存程序的重要子集啟用統計資料收集。  
  
-   查詢與計劃是在第一次原生編譯時擷取並儲存，並在每次重新編譯時更新。  
  
-   如果您已啟用查詢存放區，或已在編譯所有原生預存程序之後清除其內容，則必須手動重新編譯它們，查詢存放區才能擷取它們。 如果您使用 [sp_query_store_remove_query &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md) 或 [sp_query_store_remove_plan &#40;Transct-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md) 手動移除查詢，這同樣適用。 使用 [sp_recompile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md) 強制程序重新編譯。  
  
-   查詢存放區會在編譯期間，利用來自記憶體內部 OLTP 的計劃產生機制，來擷取查詢執行計劃。 預存的計劃在語意上相當於使用 `SET SHOWPLAN_XML ON` 取得的計劃，但有一點不同︰查詢存放區中的計劃會依據個別的陳述式進行分割和儲存。  
    
-   當您在含有混合工作負載的資料庫中執行查詢存放區時，則可從 **sys.query_store_plan &#40;Transact-SQL&#41;** 使用 [is_natively_compiled](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) 欄位，快速找到原生程式碼編譯所產生的查詢計劃。  
  
-   查詢存放區擷取模式 (*ALTER TABLE* 陳述式中的 **QUERY_CAPTURE_MODE** 參數) 不會影響來自原生編譯模組的查詢，因為不論組態值為何，一律會擷取它們。 這包括 `QUERY_CAPTURE_MODE = NONE`設定。  
  
-   查詢存放區所擷取的查詢編譯期間只會包含在產生原生程式碼之前，進行查詢最佳化所花費的時間。 更精確地說，它不包含編譯 C 程式碼的時間，以及產生 C 程式碼所需之內部結構的產生時間。  
  
-   不會針對原生編譯的查詢填入 [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md) 中的記憶體授與計量；其值永遠為 0。 記憶體授與資料行為：avg_query_max_used_memory、last_query_max_used_memory、min_query_max_used_memory、max_query_max_used_memory 和 stdev_query_max_used_memory。  
  
## <a name="enabling-and-using-query-store-with-in-memory-oltp"></a>啟用和使用含有記憶體內部 OLTP 的查詢存放區  
 下列簡單的範例示範如何在端對端使用者案例中，使用含有記憶體內部 OLTP 的查詢存放區。 在此範例中，我們假設資料庫 (`MemoryOLTP`) 已針對記憶體內部 OLTP 啟用。  
    如需記憶體最佳化資料表之必要條件的詳細資訊，請參閱 [建立記憶體最佳化資料表和原生編譯的預存程序](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)。  
  
```  
USE MemoryOLTP;  
GO  
  
-- Create a simple memory-optimized table   
CREATE TABLE dbo.Ord  
   (OrdNo INTEGER not null PRIMARY KEY NONCLUSTERED,   
    OrdDate DATETIME not null,   
    CustCode NVARCHAR(5) not null)   
WITH (MEMORY_OPTIMIZED=ON);  
GO  
  
-- Enable Query Store before native module compilation  
ALTER DATABASE MemoryOLTP SET QUERY_STORE = ON;  
GO  
  
-- Create natively compiled stored procedure  
CREATE PROCEDURE dbo.OrderInsert(@OrdNo integer, @CustCode nvarchar(5))  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS   
    BEGIN ATOMIC WITH  
    (TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
    LANGUAGE = N'English')  
  
    DECLARE @OrdDate DATETIME = GETDATE();  
    INSERT INTO dbo.Ord (OrdNo, CustCode, OrdDate)   
        VALUES (@OrdNo, @CustCode, @OrdDate);  
END;  
GO  
  
-- Enable runtime stats collection for queries from dbo.OrderInsert stored procedure  
DECLARE @db_id INT = DB_ID()  
DECLARE @proc_id INT = OBJECT_ID('dbo.OrderInsert');  
DECLARE @collection_enabled BIT;  
  
EXEC [sys].[sp_xtp_control_query_exec_stats] @new_collection_value = 1,   
    @database_id = @db_id, @xtp_object_id = @proc_id;  
  
-- Check the state of the collection flag  
EXEC sp_xtp_control_query_exec_stats @database_id = @db_id,   
    @xtp_object_id = @proc_id,   
    @old_collection_value= @collection_enabled output;  
SELECT @collection_enabled AS 'collection status';  
  
-- Execute natively compiled workload  
EXEC dbo.OrderInsert 1, 'A';  
EXEC dbo.OrderInsert 2, 'B';  
EXEC dbo.OrderInsert 3, 'C';  
EXEC dbo.OrderInsert 4, 'D';  
EXEC dbo.OrderInsert 5, 'E';  
  
-- Check Query Store Data  
-- Compile time data  
SELECT q.query_id, plan_id, object_id, query_hash, p.query_plan,  
    p.initial_compile_start_time, p.last_compile_start_time,   
    p.last_execution_time, p.avg_compile_duration,  
    p.last_force_failure_reason, p.force_failure_count  
FROM sys.query_store_query AS q  
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.plan_id  
WHERE q.object_id = OBJECT_ID('dbo.OrderInsert');  
  
-- Get runtime stats  
-- Check count_executions field to verify that runtime statistics   
-- have been collected by the Query Store  
SELECT q.query_id, p.plan_id, object_id, rsi.start_time, rsi.end_time,    
    p.last_force_failure_reason, p.force_failure_count, rs.*  
FROM sys.query_store_query AS q  
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.plan_id  
JOIN sys.query_store_runtime_stats AS rs   
    ON rs.plan_id = p.plan_id  
JOIN sys.query_store_runtime_stats_interval AS rsi   
    ON rs.runtime_stats_interval_id = rsi.runtime_stats_interval_id  
WHERE q.object_id = OBJECT_ID('dbo.OrderInsert');  
```  
  
## <a name="see-also"></a>另請參閱  
 [相關檢視、函數與程序](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [建立記憶體最佳化資料表和原生編譯的預存程序](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)   
 [查詢存放區的最佳作法](../../relational-databases/performance/best-practice-with-the-query-store.md)   
 [查詢存放區預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [查詢存放區目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)  
  
  
