---
title: 查詢提示 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/11/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
dev_langs:
- TSQL
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
caps.latest.revision: 136
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: d937872a3c00b453a58932dd127c3e3acc99c9f3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="hints-transact-sql---query"></a>提示 (Transact-SQL) - 查詢
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  查詢提示會指定所指出的提示應該用於整個查詢。 查詢提示會影響陳述式中的所有運算子。 如果主要查詢涉及 UNION，只有最後一個包含 UNION 作業的查詢可以有 OPTION 子句。 查詢提示是在 [OPTION 子句](../../t-sql/queries/option-clause-transact-sql.md)中指定。 如果一個或多個查詢提示造成查詢最佳化工具不會產生有效的計畫，就會產生 8622 錯誤。  
  
> [!CAUTION]  
> 由於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢最佳化工具通常會選取最好的查詢執行計畫，因此，我們建議資深的開發人員和資料庫管理員將它當做最後的解決辦法。  
  
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
  
 如果在相同查詢中，也在 FROM 子句中指定了一組特定資料表的聯結提示，在聯結兩份資料表時，雖然仍必須遵照查詢提示，但這個聯結提示優先。 因此，這組資料表的聯結提示可能只會限制查詢提示中允許使用之聯結方法的選取。 如需詳細資訊，請參閱[聯結提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-join.md)。  
  
 EXPAND VIEWS  
 指定展開索引檢視表，且查詢最佳化工具不會用任何索引檢視表來替代查詢的任何部分。 當檢視表名稱被查詢文字中的檢視表定義取代時，便會展開這份檢視表。  
  
 這個查詢提示會虛擬地禁止直接在查詢計畫中使用索引檢視表及其索引。  
  
 只有在查詢的 SELECT 部分直接參考索引檢視表，且已指定 WITH (NOEXPAND) 或 WITH (NOEXPAND, INDEX( *index_value* [ **,***...n* ] ) ) 時，才不展開這份索引檢視表。 如需有關查詢提示 WITH (NOEXPAND) 的詳細資訊，請參閱 [FROM](../../t-sql/queries/from-transact-sql.md)。  
  
 這個提示只會影響各陳述式 SELECT 部分中的檢視表，其中包括 INSERT、UPDATE、MERGE 和 DELETE 陳述式之 SELECT 部分中的檢視表。  
  
 FAST *number_rows*  
 指定將查詢最佳化，以快速擷取第一個 *number_rows*。 這是非負的整數。 在傳回第一個 *number_rows* 之後，查詢會繼續執行，並產生它的完整結果集。  
  
 FORCE ORDER  
 指定在查詢最佳化期間，保留查詢語法所指出的聯結順序。 使用 FORCE ORDER 不會影響查詢最佳化工具所可能有的角色反轉行為。  
  
> [!NOTE]  
> 在 MERGE 陳述式中，除非指定了 WHEN SOURCE NOT MATCHED 子句，否則就會根據聯結順序，先存取來源資料表，然後再存取目標資料表。 指定 FORCE ORDER 可以保留此預設行為。  
  
 { FORCE | DISABLE } EXTERNALPUSHDOWN  
 強制或停用在 Hadoop 中下推合格運算式的計算。 僅適用於使用 PolyBase 的查詢。 將不會下推到 Azure 儲存體。  
  
 KEEP PLAN  
 強制查詢最佳化工具放寬查詢的估計重新編譯臨界值。 預估的重新編譯臨界值是資料表因執行 UPDATE、DELETE、MERGE 或 INSERT 陳述式而變更了預估數目的索引資料行時，會自動重新編譯查詢的點。 指定 KEEP PLAN 可確保查詢不會依照資料表有多項更新的頻率來重新編譯。  
  
 KEEPFIXED PLAN  
 強制查詢最佳化工具不因統計資料中的變更而重新編譯查詢。 指定 KEEPFIXED PLAN 可確保只有在基礎資料表的結構描述有了改變，或針對這些資料表執行了 **sp_recompile** 時，才重新編譯查詢。  
  
 IGNORE_NONCLUSTERED_COLUMNSTORE_INDEX  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 防止查詢使用非叢集之記憶體最佳化的資料行存放區索引。 如果查詢同時包含禁止使用資料行存放區索引的查詢提示，以及使用資料行索引的索引提示，將會因為兩提示相互衝突而傳回錯誤。  
  
 MAX_GRANT_PERCENT = *percent*  
 最大記憶體授與大小 (百分比)。 查詢保證不會超過此限制。 如果 Resource Governor 設定低於此值，實際的限制可能更低。 有效值介於 0.0 與 100.0 之間。  
  
**適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 MIN_GRANT_PERCENT = *percent*  
 最小記憶體授與大小 (百分比) = 預設限制的 %。 查詢保證取得 MAX(所需的記憶體, 最小授與)，因為至少需有所需的記憶體，才能啟動查詢。 有效值介於 0.0 與 100.0 之間。  
  
**適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 MAXDOP *number*  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 針對指定這個選項的查詢覆寫 **sp_configure** 和 Resource Governor 的 **max degree of parallelism** 組態選項。 MAXDOP 查詢提示可能會超過使用 sp_configure 所設定的值。 如果 MAXDOP 超過使用 Resource Governor 所設定的值，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 就會使用 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md) 中所描述的 Resource Governor MAXDOP 值。 當您使用 MAXDOP 查詢提示時，適用所有搭配 **max degree of parallelism** 組態選項使用的語意規則。 如需詳細資訊，請參閱 [設定 max degree of parallelism 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。  
  
> [!WARNING]     
> 如果 MAXDOP 設為零，則伺服器會選擇平行處理原則的最大程度。  
  
 MAXRECURSION *number*     
 指定此查詢所能擁有的最大遞迴數。 *number* 是 0 與 32767 之間的非負整數。 當指定 0 時，不會套用任何限制。 如果未指定這個選項，伺服器的預設限制是 100。  
  
 在查詢執行期間，當到達 MAXRECURSION 限制的指定或預設數目時，查詢會結束，且會傳回錯誤。  
  
 陳述式的所有效果都會因這個錯誤而回復。 如果陳述式是 SELECT 陳述式，可能會傳回部分結果，或根本不傳回任何結果。 任何傳回的部分結果都不會包括超出指定的最大遞迴層級之遞迴層級的所有資料列。  
  
 如需詳細資訊，請參閱 [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)。     
  
 NO_PERFORMANCE_SPOOL    
 **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 防止多工緩衝處理運算子加入查詢計劃 (需有多工緩衝處理才能保證有效的更新語意的計劃除外)。 在某些情況下，多工緩衝處理運算子可能會降低效能。 例如，多工緩衝處理會使用 tempdb，因此如果有許多並行查詢與多工緩衝處理作業一起執行，可能會發生 tempdb 競爭。  
  
 OPTIMIZE FOR ( *@variable_name* { UNKNOWN | = *literal_constant }* [ **,** ...*n* ] )     
 指示查詢最佳化工具在查詢進行編譯和最佳化時，使用特定的本機變數值。 只有在查詢最佳化期間，才使用這個值，在查詢執行期間，不使用這個值。  
  
 *@variable_name*  
 這是查詢所用之本機變數的名稱，您可以指派這個本機變數的值來搭配使用 OPTIMIZE FOR 查詢提示。  
  
 *UNKNOWN*  
 指定查詢最佳化工具使用統計資料 (而非初始值) 來判斷查詢最佳化期間的區域變數值。  
  
 *literal_constant*  
 指派給 *@variable_name* 以與 OPTIMIZE FOR 查詢提示搭配使用的常值常數值。 只有在查詢最佳化時才會使用 *literal_constant*，此值不可用做查詢執行期間 *@variable_name* 的值。 *literal_constant* 可以是任何可以常值常數表示的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料類型。 *literal_constant* 的資料類型必須可以隱含地轉換為 *@variable_name* 在查詢中參考的資料類型。  
  
 OPTIMIZE FOR 可以抵銷最佳化工具的預設參數偵測行為，當您建立計畫指南時，也可以使用它。 如需詳細資訊，請參閱[重新編譯預存程序](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md)。  
  
 OPTIMIZE FOR UNKNOWN  
 指示查詢最佳化工具在編譯及最佳化查詢時，將統計資料 (而非初始值) 用於所有的區域變數，包括以強制參數化所建立的參數。  
  
 如果 OPTIMIZE FOR @variable_name = *literal_constant*，而且在相同的查詢提示中使用 OPTIMIZE FOR UNKNOWN，查詢最佳化工具會將指定的 *literal_constant* 用於特定值，並將 UNKNOWN 用於其餘的變數值。 只有在查詢最佳化期間才使用這些值，查詢執行期間則不使用這些值。  
  
 PARAMETERIZATION { SIMPLE | FORCED }     
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢最佳化工具在查詢完成時套用在查詢的參數化規則。  
  
> [!IMPORTANT]  
> 您只能在計劃指南內指定 PARAMETERIZATION 查詢提示，以覆寫 PARAMETERIZATION 資料庫 SET 選項目前的設定。 您不能在查詢中直接指定它。    
> 如需詳細資訊，請參閱[使用計劃指南指定查詢參數化行為](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)。
  
 SIMPLE 指示查詢最佳化工具嘗試簡單參數化。 FORCED 指示查詢最佳化工具嘗試使用強制參數化。 如需詳細資訊，請參閱[查詢處理架構指南中的強制參數化](../../relational-databases/query-processing-architecture-guide.md#ForcedParam)和[查詢處理架構指南中的簡單參數化](../../relational-databases/query-processing-architecture-guide.md#SimpleParam)。  
  
 RECOMPILE  
 指示 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 捨棄在執行查詢之後所產生的計畫，強制查詢最佳化工具在下次執行相同的查詢時，重新編譯查詢計畫。 在未指定 RECOMPILE 的情況下，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會快取查詢計劃並重複使用。 當編譯查詢計畫時，RECOMPILE 查詢提示會使用查詢中任何本機變數目前的值，如果查詢在預存程序內，就會將目前的值傳給任何參數。  
  
 當不必編譯整個預存程序，只需要重新編譯預存程序內的部分查詢時，RECOMPILE 是非常有用的替代方案，可供您建立使用 WITH RECOMPILE 子句的預存程序。 如需詳細資訊，請參閱[重新編譯預存程序](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md)。 另外，當您建立計畫指南時，RECOMPILE 也非常有用。  
  
 ROBUST PLAN  
 強制查詢最佳化工具嘗試一項適用於最大潛在資料列大小的計畫，可能會犧牲效能。 當處理查詢時，中繼資料表和運算子可能需要儲存和處理比任何輸入資料列還寬的資料列。 這些資料列的寬度，有時會使特定運算子無法處理資料列。 如果發生這個情況，在查詢執行期間，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會產生一則錯誤。 您可以利用 ROBUST PLAN 來指示查詢最佳化工具，不考慮任何可能發生這個問題的查詢計畫。  
  
 如果不可能執行這類計畫，查詢最佳化工具會傳回錯誤，而不是將錯誤偵測延遲到查詢執行時。 資料列可能包含可變長度的資料行；[!INCLUDE[ssDE](../../includes/ssde-md.md)] 允許資料列定義成超出 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 處理能力的最大潛在大小。 一般而言，雖然有最大潛在大小，但應用程式仍會儲存實際大小在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 處理能力限制之內的資料列。 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 發現太長的資料列，便會傳回執行錯誤。  
 
<a name="use_hint"></a> USE HINT ( **'***hint_name***'** )    
 **適用對象**：適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以上) 和 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。
 
 提供一或多個額外的提示給**單引號內**之提示名稱所指定的查詢處理器。   

 支援下列提示名稱：    
 
*  'DISABLE_OPTIMIZED_NESTED_LOOP'  
 指示查詢處理器在產生查詢計劃時，不使用排序作業 (批次排序) 以取得最佳化巢狀迴圈聯結。 這與[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2340 相同。
*  'FORCE_LEGACY_CARDINALITY_ESTIMATION'  
 強制查詢最佳化工具使用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及較早版本的[基數估計](../../relational-databases/performance/cardinality-estimation-sql-server.md)模型。 這與[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9481 或[資料庫範圍設定](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) LEGACY_CARDINALITY_ESTIMATION=ON 設定相同。
*  'ENABLE_QUERY_OPTIMIZER_HOTFIXES'  
 啟用查詢最佳化工具 Hotfix (在 SQL Server 累積更新和 Service Pack 中發佈的變更)。 這與[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4199 或[資料庫範圍設定](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) QUERY_OPTIMIZER_HOTFIXES=ON 設定相同。
*  'DISABLE_PARAMETER_SNIFFING'  
 指示查詢最佳化工具在編譯有一或多個參數的查詢時使用平均資料分佈，讓查詢計劃與查詢在編譯時一開始使用的參數值無關。 這與[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4136 或[資料庫範圍設定](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) PARAMETER_SNIFFING=OFF 設定相同。
*  'ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES'  
 導致 SQL Server 在評估篩選條件的 AND 述詞以計算相互關聯時，使用最小選擇性產生計劃。 這與[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4137 搭配 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和更早版本的基數估計模型使用時相同，而且當[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9471 搭配 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 或更新版本的基數估計模型使用時，有類似的效果。
*  'DISABLE_OPTIMIZER_ROWGOAL'  
 導致 SQL Server 產生的計劃不使用資料列目標調整來處理包含 TOP、OPTION (FAST N)、IN 或 EXISTS 關鍵字的查詢。 這與[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4138 相同。
*  'ENABLE_HIST_AMENDMENT_FOR_ASC_KEYS'  
 為需要基數估計的任何開頭索引資料行，啟用自動產生的快速統計資料 (長條圖修正)。 在查詢編譯時會調整用來預估基數的長條圖，以計算此資料行的實際最大值或最小值。 這與[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4139 相同。 
*  'ASSUME_JOIN_PREDICATE_DEPENDS_ON_FILTERS'  
 在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 或更新版本的查詢最佳化工具[基數估計](../../relational-databases/performance/cardinality-estimation-sql-server.md)模型下，導致 SQL Server 使用簡易內含項目假設產生計畫，而不使用預設的基底內含項目假設。 這與[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9476 相同。 
*  'FORCE_DEFAULT_CARDINALITY_ESTIMATION'  
 強制查詢最佳化工具使用對應至目前資料庫相容性層級的[基數估計](../../relational-databases/performance/cardinality-estimation-sql-server.md)模型。 使用此提示可覆寫[資料庫範圍設定](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) LEGACY_CARDINALITY_ESTIMATION=ON 設定或[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9481。
 
> [!TIP]
> 提示名稱不區分大小寫。
  
  您可以使用動態管理檢視 [sys.dm_exec_valid_use_hints](../../relational-databases/system-dynamic-management-views/sys-dm-exec-valid-use-hints-transact-sql.md)，來查詢所有支援的 USE HINT 名稱清單。    
  
> [!IMPORTANT] 
> 一些 USE HINT 提示可能會與在全域或工作階段層級啟用的追蹤旗標發生衝突，或與資料庫範圍設定的設定發生衝突。 在此情況下，查詢層級提示 (USE HINT) 一律優先。 如果 USE HINT 與其他查詢提示或在查詢層級啟用的追蹤旗標 (例如由 QUERYTRACEON 啟用) 發生衝突，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在嘗試執行查詢時會產生錯誤。 

 USE PLAN N **'***xml_plan***'**     
 強制查詢最佳化工具針對 **'***xml_plan***'** 所指定的查詢使用現有的查詢計劃。 USE PLAN 無法搭配 INSERT、UPDATE、MERGE 或 DELETE 陳述式一起使用。  
  
TABLE HINT **(***exposed_object_name* [ **,** \<table_hint> [ [**,** ]...*n* ] ] **)** 會將指定的資料表提示套用至與 *exposed_object_name* 對應的資料表或檢視。 我們建議您只在 [計劃指南](../../relational-databases/performance/plan-guides.md)的內容中，才將資料表提示當做查詢提示使用。  
  
 *exposed_object_name* 可以是下列其中一個參考：  
  
-   在查詢的 [FROM](../../t-sql/queries/from-transact-sql.md) 子句中，當為資料表或檢視使用別名時，*exposed_object_name* 就是別名。  
  
-   沒有使用別名時，*exposed_object_name* 就是 FROM 子句中所參考之資料表或檢視的完全相符項目。 例如，如果使用兩部分名稱參考資料表或檢視，*exposed_object_name* 就是相同的兩部分名稱。  
  
 當指定 *exposed_object_name* 但沒有同時指定資料表提示時，在查詢中指定成物件之資料表提示一部分的任何索引都會被忽略，而且查詢最佳化工具會決定索引使用方式。 當您無法修改原始的查詢時，就可以使用這項技巧來排除 INDEX 資料表提示的影響。 請參閱＜範例 J＞。  
  
**\<table_hint> ::=** { [ NOEXPAND ] { INDEX ( *index_value* [ ,...*n* ] ) | INDEX = ( *index_value* ) | FORCESEEK [**(***index_value***(***index_column_name* [**,**... ] **))** ]| FORCESCAN | HOLDLOCK | NOLOCK | NOWAIT | PAGLOCK | READCOMMITTED | READCOMMITTEDLOCK | READPAST | READUNCOMMITTED | REPEATABLEREAD | ROWLOCK | SERIALIZABLE | SNAPSHOT | SPATIAL_WINDOW_MAX_CELLS | TABLOCK | TABLOCKX | UPDLOCK | XLOCK } 這是要套用至以查詢提示形式與 *exposed_object_name* 對應之資料表或檢視表的資料表提示。 如需這些提示的說明，請參閱[資料表提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)。  
  
 除非查詢已有指定資料表提示的 WITH 子句，否則不可使用 INDEX、FORCESCAN 和 FORCESEEK 以外的資料表提示做為查詢提示。 如需詳細資訊，請參閱＜備註＞。  
  
> [!CAUTION] 
> 使用參數指定 FORCESEEK，會限制最佳化工具所能使用的計畫數目，其限制幅度將大於指定 FORCESEEK 而不指定參數時的限制。 這可能會導致在許多狀況下發生「無法產生計畫」錯誤。 在後續版本中，將會從內部修改最佳化工具，以擴大可使用的計畫範圍。  
  
## <a name="remarks"></a>Remarks  
 除非是在陳述式內使用 SELECT 子句，否則無法在 INSERT 陳述式中指定查詢提示。  
  
 您只能在最上層查詢中指定查詢提示，不能在子查詢中指定查詢提示。 當資料表提示指定為查詢提示時，您可以在最上層查詢或子查詢中指定此提示。不過，在 TABLE HINT 子句中針對 *exposed_object_name* 所指定的值必須與查詢或子查詢中的公開名稱完全相符。  
  
## <a name="specifying-table-hints-as-query-hints"></a>將資料表提示指定為查詢提示  
 建議您只有在[計劃指南](../../relational-databases/performance/plan-guides.md)的內容中，才將 INDEX、FORCESCAN 或 FORCESEEK 資料表提示作為查詢提示使用。 當您無法修改原始的查詢 (例如，因為它是協力廠商應用程式) 時，計畫指南就很有用。 在計畫指南中指定的查詢提示會先加入至查詢，然後再進行編譯和最佳化。 若為特定查詢，請在測試計畫指南陳述式時才使用 TABLE HINT 子句。 如果是所有其他特定的查詢，我們建議您將這些提示指定成資料表提示。  
  
 將 INDEX、FORCESCAN 和 FORCESEEK 資料表提示指定為查詢提示適用於下列物件：  
  
-   資料表  
-   檢視  
-   索引檢視  
-   通用資料表運算式 (此提示必須指定於結果集擴展此通用資料表運算式的 SELECT 陳述式內)  
-   動態管理檢視  
-   具名子查詢  
  
 對於不具任何現有資料表提示的查詢，也可將 INDEX、FORCESCAN 和 FORCESEEK 資料表提示指定為查詢提示，或以其取代查詢中現有的 INDEX、FORCESCAN 或 FORCESEEK 提示。 除非查詢已有指定資料表提示的 WITH 子句，否則不可使用 INDEX、FORCESCAN 和 FORCESEEK 以外的資料表提示做為查詢提示。 在此情況下，也必須在 OPTION 子句中使用 TABLE HINT 將相符的提示指定為查詢提示，以保留此查詢的語意。 例如，如果查詢包含資料表提示 NOLOCK，則計劃指南的 **@hints** 參數中的 OPTION 子句也必須包含 NOLOCK 提示。 請參閱範例 K。如果在 OPTION 子句中使用 TABLE HINT 指定 INDEX、FORCESCAN 或 FORCESEEK 以外的資料表提示，但是沒有相符的查詢提示 (反之亦然)，則會引發錯誤 8702 (指出 OPTION 子句可能會造成查詢語意變更) 並導致查詢失敗。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-merge-join"></a>A. 使用 MERGE JOIN  
 下列範例指定查詢中的 JOIN 作業由 MERGE JOIN 聯結執行。 此範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
```sql  
SELECT *   
FROM Sales.Customer AS c  
INNER JOIN Sales.CustomerAddress AS ca ON c.CustomerID = ca.CustomerID  
WHERE TerritoryID = 5  
OPTION (MERGE JOIN);  
GO    
```  
  
### <a name="b-using-optimize-for"></a>B. 使用 OPTIMIZE FOR  
 下列範例指示查詢最佳化工具在最佳化查詢時，將 `'Seattle'` 值用於區域變數 `@city_name` 及使用統計資料判斷區域變數 `@postal_code` 的值。 此範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
```sql  
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
 您可以利用 MAXRECURSION 來防止形式不良的遞迴通用資料表運算式進入無限迴圈。 下列範例會刻意建立無限迴圈，然後利用 MAXRECURSION 提示，將遞迴層級數目限制為 2。 此範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
```sql  
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
 下列範例使用 MERGE UNION 查詢提示。 此範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
```sql  
SELECT *  
FROM HumanResources.Employee AS e1  
UNION  
SELECT *  
FROM HumanResources.Employee AS e2  
OPTION (MERGE UNION);  
GO  
```  
  
### <a name="e-using-hash-group-and-fast"></a>E. 使用 HASH GROUP 與 FAST  
 下列範例使用 HASH GROUP 和 FAST 查詢提示。 此範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
```sql  
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total  
FROM Sales.SalesOrderDetail  
WHERE UnitPrice < $5.00  
GROUP BY ProductID, OrderQty  
ORDER BY ProductID, OrderQty  
OPTION (HASH GROUP, FAST 10);  
GO    
```  
  
### <a name="f-using-maxdop"></a>F. 使用 MAXDOP  
 下列範例使用 MAXDOP 查詢提示。 此範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```sql  
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
  
```sql  
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
  
```sql  
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
  
```sql  
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
  
```sql  
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
  
```sql  
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
  
```sql  
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
### <a name="l-using-use-hint"></a>L. 使用 USE HINT  
 下列範例使用 RECOMPILE 和 USE HINT 查詢提示。 此範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
**適用於**：[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。  
  
```sql  
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (RECOMPILE, USE HINT ('ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES', 'DISABLE_PARAMETER_SNIFFING')); 
GO  
```  
    
## <a name="see-also"></a>另請參閱  
 [提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)  
 [追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  
