---
title: "查詢提示 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Query_Hint_TSQL
- Query_TSQL
- Query
- Query Hint
- MAX_GRANT_PERCENT
- MAX_GRANT_PERCENT_TSQL
- MIN_GRANT_PERCENT
- MIN_GRANT_PERCENT_TSQL
- EXTERNALPUSHDOWN
- EXTERNALPUSHDOWN_TSQL
- NOLOCK_TSQL
- MAXDOP_TSQL
- USE_HINT_TSQL
dev_langs: TSQL
helpviewer_keywords:
- REPORT PLAN query hint
- FORCE ORDER query hint
- HASH JOIN query hint
- query hints [SQL Server]
- OPTIMIZE FOR query hint
- FORCESCAN query hint
- RECOMPILE query hint
- MAXRECURSION query hint
- MERGE JOIN query hint
- HASH GROUP query hint
- KEEP PLAN query hint
- UNION query hint
- FORCESEEK query hint
- ORDER GROUP query hint
- LOOP JOIN query hint
- KEEPFIXED PLAN query hint
- FAST query hint
- MAXDOP query hint
- PARAMETERIZATION query hint
- hints [SQL Server], query
- JOIN query hint
- USE PLAN query hint
- EXPAND VIEWS query hint
- MAX_GRANT_PERCENT query hint
- MIN_GRANT_PERCENT query hint
- EXTERNALPUSHDOWN query hint
- USE HINT query hint
ms.assetid: 66fb1520-dcdf-4aab-9ff1-7de8f79e5b2d
caps.latest.revision: "136"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 88d4de294e7fa31b7334b9b03cc127d479d6628a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="hints-transact-sql---query"></a>提示 (TRANSACT-SQL)-查詢
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  查詢提示會指定所指出的提示應該用於整個查詢。 查詢提示會影響陳述式中的所有運算子。 如果主要查詢涉及 UNION，只有最後一個包含 UNION 作業的查詢可以有 OPTION 子句。 指定查詢提示的一部分[OPTION 子句](../../t-sql/queries/option-clause-transact-sql.md)。 如果一個或多個查詢提示造成查詢最佳化工具不會產生有效的計畫，就會產生 8622 錯誤。  
  
> [!CAUTION]  
>  由於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢最佳化工具通常會選取最好的查詢執行計畫，因此，我們建議資深的開發人員和資料庫管理員將它當做最後的解決辦法。  
  
 **適用於：**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [INSERT](../../t-sql/statements/insert-transact-sql.md)  
  
 [SELECT](../../t-sql/queries/select-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 [MERGE](../../t-sql/statements/merge-transact-sql.md)  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
<query_hint > ::=   
{ { HASH | ORDER } GROUP   
  | { CONCAT | HASH | MERGE } UNION   
  | { LOOP | MERGE | HASH } JOIN   
  | EXPAND VIEWS   
  | FAST number_rows   
  | FORCE ORDER   
  | { FORCE | DISABLE } EXTERNALPUSHDOWN  
  | IGNORE_NONCLUSTERED_COLUMNSTORE_INDEX  
  | KEEP PLAN   
  | KEEPFIXED PLAN  
  | MAX_GRANT_PERCENT = percent  
  | MIN_GRANT_PERCENT = percent  
  | MAXDOP number_of_processors   
  | MAXRECURSION number   
  | NO_PERFORMANCE_SPOOL   
  | OPTIMIZE FOR ( @variable_name { UNKNOWN | = literal_constant } [ , ...n ] )  
  | OPTIMIZE FOR UNKNOWN  
  | PARAMETERIZATION { SIMPLE | FORCED }  
  | RECOMPILE  
  | ROBUST PLAN   
  | USE HINT ( '<hint_name>' [ , ...n ] )
  | USE PLAN N'xml_plan'  | TABLE HINT ( exposed_object_name [ , <table_hint> [ [, ]...n ] ] )  
}  
  
<table_hint> ::=  
[ NOEXPAND ] {   
    INDEX ( index_value [ ,...n ] ) | INDEX = ( index_value )  
  | FORCESEEK [( index_value ( index_column_name [,... ] ) ) ]  
  | FORCESCAN  
  | HOLDLOCK   
  | NOLOCK   
  | NOWAIT  
  | PAGLOCK   
  | READCOMMITTED   
  | READCOMMITTEDLOCK   
  | READPAST   
  | READUNCOMMITTED   
  | REPEATABLEREAD   
  | ROWLOCK   
  | SERIALIZABLE   
  | SNAPSHOT  
  | SPATIAL_WINDOW_MAX_CELLS = integer  
  | TABLOCK   
  | TABLOCKX   
  | UPDLOCK   
  | XLOCK  
}  
```  
  
## <a name="arguments"></a>引數  
 { HASH | ORDER } GROUP  
 指定查詢之 GROUP BY 或 DISTINCT 子句所描述的彙總使用雜湊或排序。  
  
 { MERGE | HASH | CONCAT } UNION  
 指定所有 UNION 作業都是藉由合併、雜湊或串連各個 UNION 集來執行的。 如果指定了多個 UNION 提示，查詢最佳化工具會從指定的提示中選取成本最低的策略。  
  
 { LOOP | MERGE | HASH } JOIN  
 指定所有聯結作業都是由整個查詢中的 LOOP JOIN、MERGE JOIN 或 HASH JOIN 來執行的。 如果指定了多個聯結提示，最佳化工具會從允許使用的聯結提示中，選取成本最低的聯結策略。  
  
 如果在相同查詢中，也在 FROM 子句中指定了一組特定資料表的聯結提示，在聯結兩份資料表時，雖然仍必須遵照查詢提示，但這個聯結提示優先。 因此，這組資料表的聯結提示可能只會限制查詢提示中允許使用之聯結方法的選取。 如需詳細資訊，請參閱[聯結提示 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/hints-transact-sql-join.md).  
  
 EXPAND VIEWS  
 指定展開索引檢視表，且查詢最佳化工具不會用任何索引檢視表來替代查詢的任何部分。 當檢視表名稱被查詢文字中的檢視表定義取代時，便會展開這份檢視表。  
  
 這個查詢提示會虛擬地禁止直接在查詢計畫中使用索引檢視表及其索引。  
  
 查詢和 WITH (NOEXPAND) 或 WITH 的 SELECT 部分直接參考檢視時，才不會展開索引檢視表 (NOEXPAND，INDEX ( *index_value* [ **，***...n*])) 指定。 如需有關查詢提示 WITH (NOEXPAND) 的詳細資訊，請參閱[FROM](../../t-sql/queries/from-transact-sql.md)。  
  
 這個提示只會影響各陳述式 SELECT 部分中的檢視表，其中包括 INSERT、UPDATE、MERGE 和 DELETE 陳述式之 SELECT 部分中的檢視表。  
  
 快速*number_rows*  
 指定查詢的最佳化，以快速擷取集合的第一個*number_rows。* 這是非負整數。 第一個之後*number_rows*傳回時，查詢會繼續執行，並產生其完整的結果集。  
  
 FORCE ORDER  
 指定在查詢最佳化期間，保留查詢語法所指出的聯結順序。 使用 FORCE ORDER 不會影響查詢最佳化工具所可能有的角色反轉行為。  
  
> [!NOTE]  
>  在 MERGE 陳述式中，除非指定了 WHEN SOURCE NOT MATCHED 子句，否則就會根據聯結順序，先存取來源資料表，然後再存取目標資料表。 指定 FORCE ORDER 可以保留此預設行為。  
  
 {FORCE |停用} EXTERNALPUSHDOWN  
 強制執行，或停用的合格 Hadoop 中的運算式的計算下推。 僅適用於使用 PolyBase 查詢。 將不下推到 Azure 儲存體。  
  
 KEEP PLAN  
 強制查詢最佳化工具放寬查詢的估計重新編譯臨界值。 預估的重新編譯臨界值是資料表因執行 UPDATE、DELETE、MERGE 或 INSERT 陳述式而變更了預估數目的索引資料行時，會自動重新編譯查詢的點。 指定 KEEP PLAN 可確保查詢不會依照資料表有多項更新的頻率來重新編譯。  
  
 KEEPFIXED PLAN  
 強制查詢最佳化工具不因統計資料中的變更而重新編譯查詢。 指定 KEEPFIXED PLAN 可確保或基礎資料表的結構描述變更時，才會重新編譯查詢**sp_recompile**針對這些資料表執行。  
  
 IGNORE_NONCLUSTERED_COLUMNSTORE_INDEX  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 防止查詢使用非叢集記憶體最佳化的資料行存放區索引。 如果查詢同時包含禁止使用資料行存放區索引的查詢提示，以及使用資料行索引的索引提示，將會因為兩提示相互衝突而傳回錯誤。  
  
 MAX_GRANT_PERCENT =*百分比*  
 最大記憶體授與大小百分比。 查詢保證不會超過此限制。 實際的限制可能低如果低於這個資源管理員設定。 有效值介於 0.0 到 100.0 之間。  
  
**適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 MIN_GRANT_PERCENT =*百分比*  
 最小記憶體授與百分比大小 = %的預設限制。 若要取得最大值 （所需的記憶體，最小 grant），因為至少需要啟動查詢需要記憶體時，就可以保證查詢。 有效值介於 0.0 到 100.0 之間。  
  
**適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 MAXDOP*數目*  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 覆寫**的最大平行處理原則程度**組態選項的**sp_configure**和資源管理員，指定這個選項的查詢。 MAXDOP 查詢提示可能會超過使用 sp_configure 所設定的值。 如果 MAXDOP 超過使用資源管理員所設定的值[!INCLUDE[ssDE](../../includes/ssde-md.md)]使用資源管理員 MAXDOP 值中所述[ALTER WORKLOAD GROUP &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-workload-group-transact-sql.md). 搭配使用所有的語意規則**的最大平行處理原則程度**使用 MAXDOP 查詢提示時，才適用於組態選項。 如需詳細資訊，請參閱 [設定 max degree of parallelism 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。  
  
> [!WARNING]  
>  如果 MAXDOP 設定為零，則伺服器會選擇平行處理原則的最大程度。  
  
 MAXRECURSION*數目*  
 指定此查詢所能擁有的最大遞迴數。 *數字*是非負整數，介於 0 到 32767 之間。 當指定 0 時，不會套用任何限制。 如果未指定這個選項，伺服器的預設限制是 100。  
  
 在查詢執行期間，當到達 MAXRECURSION 限制的指定或預設數目時，查詢會結束，且會傳回錯誤。  
  
 陳述式的所有效果都會因這個錯誤而回復。 如果陳述式是 SELECT 陳述式，可能會傳回部分結果，或根本不傳回任何結果。 任何傳回的部分結果都不會包括超出指定的最大遞迴層級之遞迴層級的所有資料列。  
  
 如需詳細資訊，請參閱[common_table_expression &#40; 與TRANSACT-SQL &#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 NO_PERFORMANCE_SPOOL  
 **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 防止多工緩衝處理運算子加入查詢計劃 （除了計劃時，才能保證有效的更新語意多工緩衝處理）。 在某些情況下，多工緩衝處理運算子可能會降低效能。 比方說，多工緩衝處理使用 tempdb，如果有許多並行查詢，利用多工緩衝處理作業執行，可能會發生競爭 tempdb。  
  
 OPTIMIZE FOR (  *@variable_name*  {未知 | = *literal_constant}* [ **，** ...*n* ] )  
 指示查詢最佳化工具在查詢進行編譯和最佳化時，使用特定的本機變數值。 只有在查詢最佳化期間，才使用這個值，在查詢執行期間，不使用這個值。  
  
 *@variable_name*  
 這是查詢所用之本機變數的名稱，您可以指派這個本機變數的值來搭配使用 OPTIMIZE FOR 查詢提示。  
  
 *未知*  
 指定查詢最佳化工具使用統計資料 (而非初始值) 來判斷查詢最佳化期間的區域變數值。  
  
 *literal_constant*  
 是要指派的常值常數值 *@variable_name*  OPTIMIZE FOR 查詢提示搭配使用。 *literal_constant*用只在查詢最佳化期間，而不是值 *@variable_name* 查詢執行期間。 *literal_constant*可以是任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以表示為常值常數的系統資料類型。 資料型別*literal_constant*必須是隱含地轉換成資料類型，  *@variable_name* 查詢中的參考。  
  
 OPTIMIZE FOR 可以抵銷最佳化工具的預設參數偵測行為，當您建立計畫指南時，也可以使用它。 如需詳細資訊，請參閱[重新編譯預存程序](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md)。  
  
 OPTIMIZE FOR UNKNOWN  
 指示查詢最佳化工具在編譯及最佳化查詢時，將統計資料 (而非初始值) 用於所有的區域變數，包括以強制參數化所建立的參數。  
  
 如果 OPTIMIZE FOR @variable_name = *literal_constant*和 OPTIMIZE FOR UNKNOWN 用於相同的查詢提示，查詢最佳化工具將使用*literal_constant*指定特定的值和其餘的變數值的未知。 只有在查詢最佳化期間才使用這些值，查詢執行期間則不使用這些值。  
  
 PARAMETERIZATION { SIMPLE | FORCED }  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢最佳化工具在查詢完成時套用在查詢的參數化規則。  
  
> [!IMPORTANT]  
>  PARAMETERIZATION 查詢提示只能指定在計畫指南內。 您不能在查詢中直接指定它。  
  
 SIMPLE 指示查詢最佳化工具嘗試簡單參數化。 FORCED 指示最佳化工具嘗試強制參數化。 PARAMETERIZATION 查詢提示用來覆寫計畫指南內 PARAMETERIZATION 資料庫 SET 選項目前的設定。 如需詳細資訊，請參閱[所使用的計畫指南指定查詢參數化行為](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)。  
  
 RECOMPILE  
 指示 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 捨棄在執行查詢之後所產生的計畫，強制查詢最佳化工具在下次執行相同的查詢時，重新編譯查詢計畫。 未指定重新編譯，[!INCLUDE[ssDE](../../includes/ssde-md.md)]快取查詢計畫和重複使用它們。 當編譯查詢計畫時，RECOMPILE 查詢提示會使用查詢中任何本機變數目前的值，如果查詢在預存程序內，就會將目前的值傳給任何參數。  
  
 當不必編譯整個預存程序，只需要重新編譯預存程序內的部分查詢時，RECOMPILE 是非常有用的替代方案，可供您建立使用 WITH RECOMPILE 子句的預存程序。 如需詳細資訊，請參閱[重新編譯預存程序](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md)。 另外，當您建立計畫指南時，RECOMPILE 也非常有用。  
  
 ROBUST PLAN  
 強制查詢最佳化工具嘗試一項適用於最大潛在資料列大小的計畫，可能會犧牲效能。 當處理查詢時，中繼資料表和運算子可能需要儲存和處理比任何輸入資料列還寬的資料列。 這些資料列的寬度，有時會使特定運算子無法處理資料列。 如果發生這個情況，在查詢執行期間，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會產生一則錯誤。 您可以利用 ROBUST PLAN 來指示查詢最佳化工具，不考慮任何可能發生這個問題的查詢計畫。  
  
 如果不可能執行這類計畫，查詢最佳化工具會傳回錯誤，而不是將錯誤偵測延遲到查詢執行時。 資料列可能包含可變長度的資料行；[!INCLUDE[ssDE](../../includes/ssde-md.md)] 允許資料列定義成超出 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 處理能力的最大潛在大小。 一般而言，雖然有最大潛在大小，但應用程式仍會儲存實際大小在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 處理能力限制之內的資料列。 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 發現太長的資料列，便會傳回執行錯誤。  
 
 使用提示 ( **'***hint_name***'** )  
 **適用於**： 適用於 SQL Server （從 2016 SP1 開始） 和 Azure SQL Database。
 
 提供一個或多個額外的提示，提示名稱所指定的查詢處理器**在單引號中**。 
  **適用於**： 開頭為[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1。

 支援下列提示名稱：
 
*  ' DISABLE_OPTIMIZED_NESTED_LOOP'  
 指示查詢處理器無法產生查詢計劃時，使用最佳化的巢狀的迴圈聯結的排序作業 （批次排序）。 這相當於[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)2340年。
*  ' FORCE_LEGACY_CARDINALITY_ESTIMATION'  
 會強制查詢最佳化工具使用[基數估計](../../relational-databases/performance/cardinality-estimation-sql-server.md)模型[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]及較早版本。 這相當於[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)9481 或[Database Scoped Configuration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)設定 LEGACY_CARDINALITY_ESTIMATION = ON。
*  ' ENABLE_QUERY_OPTIMIZER_HOTFIXES'  
 可讓查詢最佳化工具 hotfix （於 SQL Server 累計更新和 Service Pack 發行的變更）。 這相當於[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)4199 或[Database Scoped Configuration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)設定 QUERY_OPTIMIZER_HOTFIXES = ON。
*  ' DISABLE_PARAMETER_SNIFFING'  
 指示查詢最佳化工具使用編譯具有一或多個參數，對已編譯查詢時，第一次使用的參數值中獨立的查詢計劃的查詢時的平均資料散發。 這相當於[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)4136 或[Database Scoped Configuration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)設定 PARAMETER_SNIFFING = OFF。
*  ' ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES'  
 會導致 SQL Server 產生相互關聯的最小的選擇性評估 AND 篩選條件的述詞時使用的計劃。 這相當於[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)4137 的基數估計模型搭配使用時[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和舊版中，不會有類似的影響時[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)9471 搭配基數估計模型的[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]或更高版本。
*  ' DISABLE_OPTIMIZER_ROWGOAL'  
 導致產生不會使用資料列的目標調整包含 TOP，OPTION (FAST N) 的查詢計劃的 SQL Server，或已存在的關鍵字。 這相當於[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)4138。
*  ' ENABLE_HIST_AMENDMENT_FOR_ASC_KEYS'  
 啟用自動產生快速的統計資料 （長條圖修正） 開頭的基數估計需要的索引資料行。 在查詢編譯時期針對此資料行的實際大或最小值，將會調整用來預估基數的長條圖。 這相當於[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)4139。 
*  ' ASSUME_JOIN_PREDICATE_DEPENDS_ON_FILTERS'  
 使得 SQL Server 產生查詢計畫，而不基底內含項目假設使用簡單的內含項目假設，為聯結，查詢最佳化工具在[基數估計](../../relational-databases/performance/cardinality-estimation-sql-server.md)模型[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]或更新版本。 這相當於[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)9476。 
*  ' FORCE_DEFAULT_CARDINALITY_ESTIMATION'  
 會強制查詢最佳化工具使用[基數估計](../../relational-databases/performance/cardinality-estimation-sql-server.md)模型對應至目前的資料庫相容性層級。 使用這個提示來覆寫[Database Scoped Configuration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)設定 LEGACY_CARDINALITY_ESTIMATION = ON 或[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)9481。
 
> [!TIP]
> 提示名稱不區分大小寫。
  
  可以使用動態管理檢視來查詢所有支援的 USE 提示名稱的清單[sys.dm_exec_valid_use_hints ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-valid-use-hints-transact-sql.md)。
> [!IMPORTANT] 
> 一些使用提示提示可能與在全域啟用追蹤旗標發生衝突，或工作階段層級或資料庫範圍組態設定。 在此情況下，查詢層級提示 （使用提示） 一律會優先使用。 如果與另一個查詢提示或查詢層級啟用追蹤旗標是使用提示衝突 (例如由 QUERYTRACEON)，SQL Server 在嘗試執行查詢時，會產生錯誤。 

 USE PLAN N**'***xml_plan***'**  
 強制查詢最佳化工具針對所指定的查詢使用現有的查詢計劃**'***xml_plan***'**。 USE PLAN 無法搭配 INSERT、UPDATE、MERGE 或 DELETE 陳述式一起使用。  
  
資料表提示**(***exposed_object_name* [ **，** \<table_hint > [[**，** ]... *n*  ]] **)**適用於資料表或檢視對應至指定的資料表提示*exposed_object_name*。 我們建議使用資料表提示當做查詢提示的內容中僅[計劃指南](../../relational-databases/performance/plan-guides.md)。  
  
 *exposed_object_name*可以是下列參考：  
  
-   當使用中針對資料表或檢視的別名[FROM](../../t-sql/queries/from-transact-sql.md)查詢子句*exposed_object_name*別名。  
  
-   當未使用別名時， *exposed_object_name*就完全相符的資料表或檢視參考 FROM 子句中。 例如，如果資料表或檢視表使用兩部分名稱參考*exposed_object_name*是相同的兩部分名稱。  
  
 當*exposed_object_name*指定未同時指定資料表提示，因為物件的資料表提示的一部分則會略過，而且索引使用方式會決定查詢最佳化工具在查詢中指定任何索引。 當您無法修改原始的查詢時，就可以使用這項技巧來排除 INDEX 資料表提示的影響。 請參閱＜範例 J＞。  
  
**\<table_hint >:: =** {[NOEXPAND] {索引 ( *index_value* [，...*n* ] ) |索引 = ( *index_value* ) |FORCESEEK [**(***index_value***(***index_column_name* [**，**...]**))** ]|FORCESCAN |HOLDLOCK |NOLOCK |NOWAIT |PAGLOCK |READCOMMITTED |READCOMMITTEDLOCK |READPAST |READUNCOMMITTED |REPEATABLEREAD |ROWLOCK |可序列化 |快照集 |SPATIAL_WINDOW_MAX_CELLS |TABLOCK |TABLOCKX |UPDLOCK |XLOCK} 是要套用至資料表或檢視對應至資料表提示*exposed_object_name*當做查詢提示。 如需這些提示的說明，請參閱[資料表提示 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 除非查詢已有指定資料表提示的 WITH 子句，否則不可使用 INDEX、FORCESCAN 和 FORCESEEK 以外的資料表提示做為查詢提示。 如需詳細資訊，請參閱＜備註＞。  
  
> [!CAUTION] 
> 使用參數指定 FORCESEEK，會限制最佳化工具所能使用的計畫數目，其限制幅度將大於指定 FORCESEEK 而不指定參數時的限制。 這可能會導致在許多狀況下發生「無法產生計畫」錯誤。 在後續版本中，將會從內部修改最佳化工具，以擴大可使用的計畫範圍。  
  
## <a name="remarks"></a>備註  
 除非是在陳述式內使用 SELECT 子句，否則無法在 INSERT 陳述式中指定查詢提示。  
  
 您只能在最上層查詢中指定查詢提示，不能在子查詢中指定查詢提示。 在最上層查詢或子查詢; 資料表提示當做查詢提示指定時，可以指定提示不過，為指定的值*exposed_object_name*在 TABLE HINT 子句必須符合的公開的名稱完全查詢或子查詢中。  
  
## <a name="specifying-table-hints-as-query-hints"></a>將資料表提示指定為查詢提示  
 我們建議使用 INDEX、 FORCESCAN 或 FORCESEEK 資料表提示當做查詢提示的內容中僅[計劃指南](../../relational-databases/performance/plan-guides.md)。 當您無法修改原始的查詢 (例如，因為它是協力廠商應用程式) 時，計畫指南就很有用。 在計畫指南中指定的查詢提示會先加入至查詢，然後再進行編譯和最佳化。 若為特定查詢，請在測試計畫指南陳述式時才使用 TABLE HINT 子句。 如果是所有其他特定的查詢，我們建議您將這些提示指定成資料表提示。  
  
 將 INDEX、FORCESCAN 和 FORCESEEK 資料表提示指定為查詢提示適用於下列物件：  
  
-   資料表  
  
-   檢視  
  
-   索引檢視  
  
-   通用資料表運算式 (此提示必須指定於結果集擴展此通用資料表運算式的 SELECT 陳述式內)  
  
-   動態管理檢視  
  
-   具名子查詢  
  
 對於不具任何現有資料表提示的查詢，也可將 INDEX、FORCESCAN 和 FORCESEEK 資料表提示指定為查詢提示，或以其取代查詢中現有的 INDEX、FORCESCAN 或 FORCESEEK 提示。 除非查詢已有指定資料表提示的 WITH 子句，否則不可使用 INDEX、FORCESCAN 和 FORCESEEK 以外的資料表提示做為查詢提示。 在此情況下，也必須在 OPTION 子句中使用 TABLE HINT 將相符的提示指定為查詢提示，以保留此查詢的語意。 例如，如果查詢包含資料表提示 NOLOCK 中的 OPTION 子句 **@hints** 計畫指南的參數也必須包含 NOLOCK 提示。 請參閱 < 範例 k >。當沒有相符的查詢提示的 OPTION 子句中使用 TABLE HINT 指定 INDEX、 FORCESCAN 或 FORCESEEK 以外的資料表提示時，反之亦然。會引發錯誤 8702 （指出 OPTION 子句可能會造成查詢來變更語意），而且查詢會失敗。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-merge-join"></a>A. 使用 MERGE JOIN  
 下列範例會指定查詢中的聯結作業由 「 合併聯結。 此範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
```  
SELECT *   
FROM Sales.Customer AS c  
INNER JOIN Sales.CustomerAddress AS ca ON c.CustomerID = ca.CustomerID  
WHERE TerritoryID = 5  
OPTION (MERGE JOIN);  
GO    
```  
  
### <a name="b-using-optimize-for"></a>B. 使用 OPTIMIZE FOR  
 下列範例會指示查詢最佳化工具使用的值`'Seattle'`本機變數`@city_name`以及用來判斷本機變數的值的統計資料`@postal_code`最佳化查詢時。 此範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
```  
DECLARE @city_name nvarchar(30);  
DECLARE @postal_code nvarchar(15);  
SET @city_name = 'Ascheim';  
SET @postal_code = 86171;  
SELECT * FROM Person.Address  
WHERE City = @city_name AND PostalCode = @postal_code  
OPTION ( OPTIMIZE FOR (@city_name = 'Seattle', @postal_code UNKNOWN) );  
GO  
```  
  
### <a name="c-using-maxrecursion"></a>C. 使用 MAXRECURSION  
 您可以利用 MAXRECURSION 來防止形式不良的遞迴通用資料表運算式進入無限迴圈。 下列範例刻意建立無限迴圈，並使用 MAXRECURSION 提示限制為兩個的遞迴層級數目。 此範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
```tsql  
--Creates an infinite loop  
WITH cte (CustomerID, PersonID, StoreID) AS  
(  
    SELECT CustomerID, PersonID, StoreID  
    FROM Sales.Customer  
    WHERE PersonID IS NOT NULL  
  UNION ALL  
    SELECT cte.CustomerID, cte.PersonID, cte.StoreID  
    FROM cte   
    JOIN  Sales.Customer AS e   
        ON cte.PersonID = e.CustomerID  
)  
--Uses MAXRECURSION to limit the recursive levels to 2  
SELECT CustomerID, PersonID, StoreID  
FROM cte  
OPTION (MAXRECURSION 2);  
GO  
```  
  
 更正編碼錯誤之後，就不再需要 MAXRECURSION。  
  
### <a name="d-using-merge-union"></a>D. 使用 MERGE UNION  
 下列範例會使用 MERGE UNION 查詢提示。 此範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
```  
SELECT *  
FROM HumanResources.Employee AS e1  
UNION  
SELECT *  
FROM HumanResources.Employee AS e2  
OPTION (MERGE UNION);  
GO  
```  
  
### <a name="e-using-hash-group-and-fast"></a>E. 使用 HASH GROUP 與 FAST  
 下列範例會使用 HASH GROUP 與 FAST 查詢提示。 此範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
```  
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total  
FROM Sales.SalesOrderDetail  
WHERE UnitPrice < $5.00  
GROUP BY ProductID, OrderQty  
ORDER BY ProductID, OrderQty  
OPTION (HASH GROUP, FAST 10);  
GO    
```  
  
### <a name="f-using-maxdop"></a>F. 使用 MAXDOP  
 下列範例會使用 MAXDOP 查詢提示。 此範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total  
FROM Sales.SalesOrderDetail  
WHERE UnitPrice < $5.00  
GROUP BY ProductID, OrderQty  
ORDER BY ProductID, OrderQty  
OPTION (MAXDOP 2);    
GO
```  
  
### <a name="g-using-index"></a>G. 使用 INDEX  
 下列範例使用 INDEX 提示。 第一個範例會指定單一索引。 第二個範例會針對單一資料表參考指定多個索引。 在這兩個範例中，由於 INDEX 提示會套用在使用別名的資料表上，因此 TABLE HINT 子句也必須與公開物件名稱指定相同的別名。 此範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
```  
EXEC sp_create_plan_guide   
    @name = N'Guide1',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 2;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT(e, INDEX (IX_Employee_ManagerID)))';  
GO  
EXEC sp_create_plan_guide   
    @name = N'Guide2',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 2;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT(e, INDEX(PK_Employee_EmployeeID, IX_Employee_ManagerID)))';  
GO    
```  
  
### <a name="h-using-forceseek"></a>H. 使用 FORCESEEK  
 下列範例使用 FORCESEEK 資料表提示。 由於 INDEX 提示會套用在使用兩部分名稱的資料表上，因此 TABLE HINT 子句也必須與公開物件名稱指定相同的兩部分名稱。 此範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
```  
EXEC sp_create_plan_guide   
    @name = N'Guide3',   
    @stmt = N'SELECT c.LastName, c.FirstName, HumanResources.Employee.Title  
              FROM HumanResources.Employee  
              JOIN Person.Contact AS c ON HumanResources.Employee.ContactID = c.ContactID  
              WHERE HumanResources.Employee.ManagerID = 3  
              ORDER BY c.LastName, c.FirstName;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT( HumanResources.Employee, FORCESEEK))';  
GO    
```  
  
### <a name="i-using-multiple-table-hints"></a>I. 使用多個資料表提示  
 下列範例會將 INDEX 提示套用到某個資料表，並將 FORCESEEK 提示套用到另一個資料表。 此範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
```  
EXEC sp_create_plan_guide   
    @name = N'Guide4',   
    @stmt = N'SELECT e.ManagerID, c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 3;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT (e, INDEX( IX_Employee_ManagerID))   
                       , TABLE HINT (c, FORCESEEK))';  
GO  
```  
  
### <a name="j-using-table-hint-to-override-an-existing-table-hint"></a>J. 使用 TABLE HINT 覆寫現有的資料表提示  
 下列範例會示範如何使用 TABLE HINT 提示，而不指定提示來覆寫查詢之 FROM 子句中所指定的 INDEX 資料表提示行為。 此範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
```  
EXEC sp_create_plan_guide   
    @name = N'Guide5',   
    @stmt = N'SELECT e.ManagerID, c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e WITH (INDEX (IX_Employee_ManagerID))  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 3;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT(e))';  
GO    
```  
  
### <a name="k-specifying-semantics-affecting-table-hints"></a>K. 指定影響語意的資料表提示  
 下列範例在查詢中包含兩個資料表提示：影響語意的 NOLOCK 以及不會影響語意的 INDEX。 為了保留查詢的語意，會在計畫指南的 OPTIONS 子句中指定 NOLOCK 提示。 除了 NOLOCK 提示以外，當編譯及最佳化陳述式時，也會指定 INDEX 和 FORCESEEK 提示，並用它們來取代查詢中不會影響語意的 INDEX 提示。 此範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
```  
EXEC sp_create_plan_guide   
    @name = N'Guide6',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
                   WITH (NOLOCK, INDEX (PK_Employee_EmployeeID))  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 3;',  
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT (e, INDEX(IX_Employee_ManagerID), NOLOCK, FORCESEEK))';  
GO    
```  
  
 下列範例示範另一個方法來保留查詢的語意，並讓最佳化工具選擇使用不是資料表提示中所指定的索引。 其作法是在 OPTIONS 子句中指定 NOLOCK 提示 (因為它會影響語意)，並在指定 TABLE HINT 關鍵字時，只包含資料表參考而沒有 INDEX 提示。 此範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
```  
EXEC sp_create_plan_guide   
    @name = N'Guide7',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
                   WITH (NOLOCK, INDEX (PK_Employee_EmployeeID))  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 2;',  
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT (e, NOLOCK))';  
GO  
```  
### <a name="l-using-use-hint"></a>L. 使用使用提示  
 下列範例會使用重新編譯和使用提示的查詢提示。 此範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
**適用於**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]， [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。  
  
```  
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (RECOMPILE, USE HINT ('ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES', 'DISABLE_PARAMETER_SNIFFING')); 
GO  
```  
    
## <a name="see-also"></a>請參閱＜  
 [提示 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/hints-transact-sql.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_control_plan_guide &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)  
 [追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  
