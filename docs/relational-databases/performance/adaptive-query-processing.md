---
title: "Microsoft SQL 資料庫中的彈性查詢處理 | Microsoft Docs | Microsoft Docs"
description: "可改善 SQL Server (2017 和更新版本) 和 Azure SQL Database 查詢效能的彈性查詢處理功能。"
ms.custom: 
ms.date: 11/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: 
ms.assetid: 
author: joesackmsft
ms.author: josack;monicar
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 139d73430346cdad7baa27d90c14ad692be5bbeb
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="adaptive-query-processing-in-sql-databases"></a>SQL 資料庫中的彈性查詢處理
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

本文介紹的這些彈性查詢處理功能，可用來改善 SQL Server 和 Azure SQL Database 的查詢效能：
- 批次模式記憶體授與意見反應。
- 批次模式自適性聯結。
- 交錯執行。 

在一般的層級中，SQL Server 執行查詢如下：
1. 查詢最佳化程序會針對特定的查詢產生一組可行的執行計劃。 在此期間，會評估計劃選項的成本，並使用預估成本最低的計劃。
1. 查詢執行程序會採用查詢最佳化工具所選擇的計劃，並使用它執行作業。
    
有時候查詢最佳化工具所選擇的計劃因種種原因而不適合。 例如，預估流經查詢計劃的資料列數目可能不正確。 預估成本可協助判斷選取使用哪一個計劃執行。 如果基數估計值不正確，即使原始假設不佳，仍使用原始方案。

![彈性查詢處理功能](./media/1_AQPFeatures.png)

### <a name="how-to-enable-adaptive-query-processing"></a>如何啟用彈性查詢處理
您可以啟用資料庫的相容性層級 140，讓工作負載自動符合使用彈性查詢處理。  您可以使用 Transact-SQL 設定此項目。 例如：
```sql
ALTER DATABASE [WideWorldImportersDW] SET COMPATIBILITY_LEVEL = 140;
```
## <a name="batch-mode-memory-grant-feedback"></a>批次模式記憶體授與意見反應
SQL Server 中的查詢後續執行計劃，包含執行所需的最小記憶體，以及能將所有資料列納入記憶體的理想記憶體授權大小。 當調整的記憶體授與大小不正確時，就會降低效能。 授與過多會浪費記憶體並降低並行。 記憶體授與不足會佔用大量磁碟資源。 透過處理重複的工作負載，批次模式記憶體授與意見反應會重新計算查詢實際所需的記憶體，然後更新快取計劃的授與值。  執行相同的查詢陳述式時，此查詢會使用修訂過的記憶體授權大小，減少影響並行的過多記憶體授與，並修正導致佔用大量磁碟資源的記憶體授與低估。
下圖顯示使用批次模式調整記憶體授與意見反應的一個範例。 由於高溢出，第一次執行查詢的持續時間為「88 秒」：
```sql
DECLARE @EndTime datetime = '2016-09-22 00:00:00.000';
DECLARE @StartTime datetime = '2016-09-15 00:00:00.000';
SELECT TOP 10 hash_unique_bigint_id
FROM dbo.TelemetryDS
WHERE Timestamp BETWEEN @StartTime and @EndTime
GROUP BY hash_unique_bigint_id
ORDER BY MAX(max_elapsed_time_microsec) DESC;
```
![高溢出](./media/2_AQPGraphHighSpills.png)

啟用記憶體授與意見反應後，第二次執行的持續時間是「1 秒」 (從 88 秒降下)，溢出全部移除，且授與較高： 

![沒有溢出](./media/3_AQPGraphNoSpills.png)

### <a name="memory-grant-feedback-sizing"></a>記憶體授與意見反應調整大小
「針對授與過多」，如果授與的記憶體超過實際使用記憶體大小的兩倍，記憶體授與意見反應會重新計算記憶體授與並更新快取計劃。  記憶體授與小於 1 MB 的計劃不會重新計算處理超額問題。
「針對記憶體授與大小不足」以致批次模式運算子磁碟溢出，記憶體授與意見反應會觸發記憶體授與的重新計算。 Spill 事件會報告到記憶體授與意見反應，且可以透過 *spilling_report_to_memory_grant_feedback* XEvent 事件顯示。 此事件會傳回計劃的節點識別碼和該節點溢出的資料大小。

### <a name="memory-grant-feedback-and-parameter-sensitive-scenarios"></a>記憶體授與意見反應與參數敏感的情況
不同的參數值可能也需要不同的查詢計劃，以維持最佳狀態。 這類型的查詢即定義為「參數敏感」。 凡是參數敏感的計劃，如果記憶體授與意見反應有不穩定的記憶體需求，就會在查詢上自行停用。  計劃在查詢重複數輪後停用，透過監視 *memory_grant_feedback_loop_disabled* XEvent 可觀察到此狀況。

### <a name="memory-grant-feedback-caching"></a>記憶體授與意見反應快取
意見反應可以儲存在快取計劃中供單次執行之用。 這是該陳述式的連續執行，但得益自記憶體授與意見反應的調整。 此功能適用於重複執行的陳述式。 記憶體授與意見反應僅會變更快取的計劃。 查詢存放區目前並未擷取變更。
如已從快取收回計劃，則不保存意見反應。 如有容錯移轉，也會遺失意見反應。 使用 OPTION(RECOMPILE) 的陳述式會建立新的計劃，不是快取計劃。 因為它不是快取而來，所以不會產生記憶體授與意見反應，也不會儲存供編譯及執行。  不過，如果快取並重複執行了「不曾」使用 OPTION(RECOMPILE) 的對等陳述式 (亦即使用相同的查詢雜湊)，則連續的陳述式可得益於記憶體授與意見反應。

### <a name="tracking-memory-grant-feedback-activity"></a>追蹤記憶體授與意見反應活動
您可以使用 *memory_grant_updated_by_feedback* XEvent 事件來追蹤記憶體授與意見反應事件。  此事件會追蹤目前的執行計數記錄、記憶體授與意見反應更新計劃的次數，以及記憶體授與意見反應修改快取計劃前後的理想額外記憶體授權。

### <a name="memory-grant-feedback-resource-governor-and-query-hints"></a>記憶體授與意見反應、資源管理員和查詢提示
實際的記憶體授與會接受由資源管理員或查詢提示所決定的查詢記憶體限制。

## <a name="batch-mode-adaptive-joins"></a>批次模式自適性聯結
批次模式自適性聯結功能可讓選擇的雜湊聯結或巢狀迴圈聯結方法，延後到已掃描的第一個輸入「之後」。  自適性聯結運算子定義的閾值是用於決定何時要切換至巢狀迴圈計劃。 因此，您的計劃可在執行期間動態切換至較佳的聯結策略。
運作方式：
- 如果組建聯結輸入的資料列計數小到巢狀迴圈聯結比雜湊聯結更佳，則您的計劃就會切換成巢狀迴圈演算法。
- 如果組建聯結輸入超過特定的資料列計數閾值，就不切換，您的計劃會繼續執行雜湊聯結。

下列查詢用來說明自適性聯結範例：

```sql
SELECT  [fo].[Order Key], [si].[Lead Time Days],
[fo].[Quantity]
FROM    [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE   [fo].[Quantity] = 360;
```

此查詢會傳回 336 個資料列。  啟用我們在以下計劃中看到的即時查詢統計資料：

![查詢結果 336 個資料列](./media/4_AQPStats336Rows.png)

我們在計劃中看到：
1. 我們使用了資料行存放區索引掃描，為雜湊聯結建置階段提供資料列。
1. 我們有新的自適性聯結運算子。 此運算子定義的閾值是用於決定何時要切換至巢狀迴圈計劃。  本例中的閾值是 78 個資料列。  凡是 &gt;= 78 資料列的計劃都會使用雜湊聯結。  如果小於閾值，就會使用巢狀迴圈聯結。
1. 因為我們傳回 336 個資料列，超過閾值；所以第二個分支表示標準雜湊聯結作業的探查階段。 請注意，即時查詢統計資料會顯示流經運算子的資料列，本例中為 “672 of 672”。
1. 而最後一個分支是我們的叢集索引搜尋，供未超過閾值的巢狀迴圈聯結所使用。 請注意，我們看到的顯示是 “0 of 336” 資料列 (分支未使用)。
 現在來對比使用相同查詢的計劃，但這次的數量值在資料表中只有一個資料列：
 
```sql
SELECT  [fo].[Order Key], [si].[Lead Time Days],
[fo].[Quantity]
FROM    [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE   [fo].[Quantity] = 361;
```
查詢會傳回一個資料列。  啟用我們在以下計劃中看到的即時查詢統計資料：

![查詢結果一個資料列](./media/5_AQPStatsOneRow.png)

我們在計劃中看到：
- 因為傳回一個資料列，您會看到叢集索引搜尋中有資料列通過。
- 而且，因為我們並未繼續雜湊聯結建置階段，所以您不會看到任何資料列通過第二個分支。

### <a name="adaptive-join-benefits"></a>自適性聯結的優點
經常在小型和大型聯結輸入掃描間變動的工作負載，由此功能獲益最大。

### <a name="adaptive-join-overhead"></a>自適性聯結的負擔
自調性聯結導入的記憶體需求，比索引巢狀的迴圈聯結相等計劃更高。 巢狀迴圈像是雜湊聯結一樣，要求額外的記憶體。 在時快時慢作業的組建階段與巢狀迴圈資料流相等聯結的比較中另有額外負荷。 加上額外的成本，隨組建輸入資料列計數浮動的案例而變動。

### <a name="adaptive-join-caching-and-re-use"></a>自適性聯結快取和重複使用
批次模式自適性聯結適合初次執行的陳述式使用，而且一旦編譯，連續執行仍會根據編譯的自適性聯結閾值和流經外部輸入組建階段的執行階段資料列聯結自動調整。

### <a name="tracking-adaptive-join-activity"></a>追蹤自適性聯結活動
自適性聯結運算子有下列計劃運算子屬性：

| 計劃屬性 | 描述 |
|--- |--- |
| AdaptiveThresholdRows | 顯示從雜湊聯結切換至巢狀迴圈聯結所使用的閾值。 |
| EstimatedJoinType | 可能的聯結類型。 |
| ActualJoinType | 在實際的計劃中，顯示根據閾值最後選擇的聯結演算法。 |

評估計劃會顯示自適性聯結計劃圖形，以及定義的自適性聯結閾值和預估的聯結類型。

### <a name="adaptive-join-and-query-store-interoperability"></a>自適性整聯結和查詢存放區互通性
查詢存放區擷取並可強制執行批次模式自適性聯結計劃。

### <a name="adaptive-join-eligible-statements"></a>符合自適性聯結的陳述式
有幾個條件讓邏輯聯結符合批次模式自適性聯結：
- 資料庫相容性層級是 140
- 查詢是 SELECT 陳述式 (資料修改陳述式目前不適合)
- 聯結能夠由索引巢狀迴圈聯結或雜湊聯結實體演算法執行
- 雜湊聯結使用批次模式 – 透過顯示整體查詢中的資料行存放區索引，或顯示聯結直接參考的資料行存放區索引資料表。
- 產生的巢狀迴圈聯結和雜湊聯結替代解決方案應該有相同的第一個子系 (外部參考)

### <a name="adaptive-joins-and-nested-loop-efficiency"></a>自適性聯結與巢狀迴圈效率
如果自適性聯結切換成巢狀迴圈作業，會使用雜湊聯結組建已讀取的資料列。 運算子「不會」再次重新讀取外部參考資料列。

### <a name="adaptive-threshold-rows"></a>自適性閾值資料列
下圖顯示雜湊聯結成本與替代的巢狀迴圈聯結成本之間的交集範例。  在此交集點決定的閾值，會隨之決定用於聯結作業的實際演算法。

![聯結閾值](./media/6_AQPJoinThreshold.png)

## <a name="interleaved-execution-for-multi-statement-table-valued-functions"></a>交錯執行多重陳述式資料表值函式
交錯執行會變更單次查詢執行的最佳化和執行階段之間的單向界限，並讓計劃根據修改過的基數估計值調整。 在最佳化期間，如果我們遇到交錯執行的候選項目，目前是**多重陳述式資料表值函式 (MSTVF)**，我們會暫停最佳化、執行適用的樹狀子目錄、擷取精確的基數估計值，再繼續下游作業的最佳化。
MSTVF 在 SQL Server 2014 和 SQL Server 2016 的固定基數估計值為 "100"，舊版中是 "1"。 交錯執行有利處理因為這些與多重陳述式資料表值函式建立關聯之固定基數估計值引起的工作負載效能問題。

下圖說明即時查詢統計資料輸出，它是整體執行計劃的子集，顯示 MSTVF 固定基數估計值的影響。 您可以查看實際的資料列流程與估計的資料列。 此計劃有三個重要區域 (流向為由右至左)：
1. MSTVF 資料表掃描的固定估計值是 100 個資料列。 但此範例有 *527,597* 個資料列流經此 MSTVF 資料表掃描，如即時查詢統計資料中所見的 “527597 of 100” 估計實值，所以固定的估計值大幅扭曲。
1. 至於巢狀迴圈作業，假定外部端聯結只會傳回 100 個資料列。 如果 MSTVF 實際傳回大量的資料列，使用完全不同的聯結演算法可能會更好。
1. 至於雜湊比對作業，請注意小型警告符號，它在本例中表示溢出到磁碟。

![資料列流程與估計的資料列](./media/7_AQPFlowThreeAreas.png)

對比之前的計劃與啟用交錯執行所產生的實際計劃：

![交錯的計劃](./media/8_AQPInterleavedEnabledPlan.png)

1. 請注意，MSTVF 資料表掃描現在反映精確的基數估計值。 亦請注意此資料表掃描的重新排序和其他作業。
1. 而關於聯結演算法，我們已改從巢狀迴圈作業切換到雜湊比對作業，如果涉及大量的資料列，這樣更接近最佳狀態。
1. 亦請注意，我們不再顯示溢出警告，因為我們要根據 MSTVF 資料表掃描的實際資料列計數，授與更多記憶體。

### <a name="interleaved-execution-eligible-statements"></a>符合交錯執行的陳述式
在交錯執行中參考陳述式的 MSTVF，目前必須是唯讀的，且不為資料修改作業的一部分。 此外，如果 MSTVF 未使用執行階段常數，則不適用於交錯執行。

### <a name="interleaved-execution-benefits"></a>交錯執行的優點
一般情況下，預估和實際資料列數目間的扭曲愈高，加上下游計劃作業的數目，對效能的影響就愈大。
一般而言，交錯執行有益於下列情況的查詢：
1. 中繼結果集的預估和實際資料列數目間有很大的扭曲 (本例中為 MSTVF)，而...
1. ...整體查詢對中繼結果的大小變更十分敏感。 這通常發生在查詢計劃有樹狀子目錄的複雜樹狀結構時。
僅僅 MSTVF 的 "SELECT *" 不會得益於交錯執行。

### <a name="interleaved-execution-overhead"></a>交錯執行的負擔
負擔應該最小，甚至完全沒有。 在引入交錯執行前，MSTVF 已被具體化，不過差異在於，現在我們要允許延遲最佳化，並利用具體化資料列集的基數估計值。
就像任何會影響變更的計劃一樣，有些計劃的變更，會識我們以較佳的樹狀子目錄基數，得到整體查詢更差的計劃。 風險降低可以包括還原相容性層級，或使用查詢存放區強制執行非迴歸版的計劃。

### <a name="interleaved-execution-and-consecutive-executions"></a>交錯執行和連續執行
一旦快取交錯執行計劃，第一次執行即修改過估計值的計劃會用於連續執行，不必重新具現化交錯執行。

### <a name="tracking-interleaved-execution-activity"></a>追蹤交錯執行活動
您可以在實際的查詢執行計劃中看到使用方式屬性：

| 計劃屬性 | 描述 |
| --- | --- |
| ContainsInterleavedExecutionCandidates | 為 "true" 時，套用至 *QueryPlan* 節點，這表示此計劃包含交錯執行候選項目。 |
| IsInterleavedExecuted | 此屬性位在 TVF 節點之 RelOp 下的 RuntimeInformation 項目內。 為 "true" 時，這表示作業已具體化為交錯執行作業的一部分。 |

您也可以透過下列 XEvent 追蹤交錯執行項目：

| XEvent | 描述 |
| ---- | --- |
| interleaved_exec_status | 交錯執行進行時會引發這個事件。 |
| interleaved_exec_stats_update | 此事件會描述由交錯執行更新的基數估計值。 |
| Interleaved_exec_disabled_reason | 當具有交錯執行可能候選項目的查詢不會實際取得交錯執行時，就會引發這個事件。 |

必須執行查詢，才能讓交錯執行修改 MSTVF 基數估計值。 不過，有透過 ContainsInterleavedExecutionCandidates 屬性的交錯執行候選項目時，仍會顯示預估執行計劃。

### <a name="interleaved-execution-caching"></a>交錯執行快取
如果從快取清除或收回計劃，就會在執行查詢時重新整理使用交錯執行的編譯。
使用 OPTION(RECOMPILE) 的陳述式會建立使用交錯執行的新計劃，且不會快取它。

### <a name="interleaved-execution-and-query-store-interoperability"></a>交錯執行和查詢存放區互通性
使用交錯執行的計劃可以強制執行。 此計劃是根據初始執行更正基數估計值的版本。

## <a name="see-also"></a>另請參閱

[SQL Server Database Engine 和 Azure SQL Database 的效能中心](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)

[查詢處理架構指南](../../relational-databases/query-processing-architecture-guide.md)

[示範彈性查詢處理](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)      

