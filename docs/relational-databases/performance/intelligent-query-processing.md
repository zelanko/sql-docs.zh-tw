---
title: Microsoft SQL 資料庫中的智慧查詢處理 | Microsoft Docs
description: 可改善 SQL Server 和 Azure SQL Database 查詢效能的智慧查詢處理功能。
ms.custom: ''
ms.date: 03/05/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords: ''
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 57d96068af7120ef4ccf4da8882093fa26908089
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493975"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>SQL 資料庫中的智慧查詢處理

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

智慧查詢處理 (QP) 功能系列包含具有廣泛影響的功能，能夠以最少的實作投入量改善現有工作負載的效能。 

![智慧查詢處理](./media/3_iqpfeaturefamily.png)

您可以為資料庫啟用適用的資料庫相容性層級，讓工作負載能自動滿足智慧查詢處理的資格。  您可以使用 Transact-SQL 設定此項目。 例如：  

```sql
ALTER DATABASE [WideWorldImportersDW] SET COMPATIBILITY_LEVEL = 150;
```

下表詳述了所有智慧查詢處理功能，以及這些功能對於資料庫相容性層級的任何要求。

| **IQP 功能** | **Azure SQL Database 支援** | **SQL Server 支援** |**說明** |
| --- | --- | --- |--- |
| [自適性聯結 (批次模式)](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#batch-mode-adaptive-joins) | 是，屬於相容性層級 140| 是，自 SQL Server 2017 開始屬於相容性層級 140|自適性聯結會在執行階段，依據實際輸入列而機動選取聯結類型。|
| [近似的相異計數](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#approximate-query-processing) | 是，公開預覽| 是，自 SQL Server 2019 CTP 2.0 開始，公開預覽|為巨量資料案例提供約略的 COUNT DISTINCT，享有高效能及低磁碟使用量的好處。 |
| [資料列存放區上的批次模式](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#batch-mode-on-rowstore) | 是，屬於相容性層級 150，公開預覽| 是，自 SQL Server 2019 CTP 2.0 開始屬於相容性層級 150，公開預覽|為耗用大量 CPU 的關聯式 DW 工作負載提供批次模式，而且不需要資料行存放區索引。  | 
| [交錯執行](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#interleaved-execution-for-mstvfs) | 是，屬於相容性層級 140| 是，自 SQL Server 2017 開始屬於相容性層級 140|使用在第一次編譯時遇到的多重陳述式資料表值函式實際基數，而不是定點猜測。|
| [記憶體授與意見反應 (批次模式)](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#batch-mode-memory-grant-feedback) | 是，屬於相容性層級 140| 是，自 SQL Server 2017 開始屬於相容性層級 140|若批次模式查詢有作業會溢出到磁碟，請新增記憶體以防執行中斷。 若查詢耗用了 > 50% 的記憶體，請縮減記憶體授與端，以防執行中斷。|
| [記憶體授與意見反應 (資料列模式)](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#row-mode-memory-grant-feedback) | 是，屬於相容性層級 150，公開預覽| 是，自 SQL Server 2019 CTP 2.0 開始屬於相容性層級 150，公開預覽|若資料列模式查詢有作業會溢出到磁碟，請新增記憶體以防執行中斷。 若查詢耗用了 > 50% 的記憶體，請縮減記憶體授與端，以防執行中斷。|
| [純量 UDF 內嵌](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#scalar-udf-inlining) | 否 | 是，自 SQL Server 2019 CTP 2.1 開始屬於相容性層級 150，公開預覽|純量 UDF 會轉換成「內嵌」在呼叫查詢中的對等關聯運算式，而這通常可讓效能大幅提升。|
| [資料表變數延後編譯](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#table-variable-deferred-compilation) | 是，屬於相容性層級 150，公開預覽| 是，自 SQL Server 2019 CTP 2.0 開始屬於相容性層級 150，公開預覽|使用在第一次編譯時遇到的資料表值函式實際基數，而不是定點猜測。|

## <a name="batch-mode-adaptive-joins"></a>批次模式自適性聯結

這項功能可讓您的計畫在使用單一快取計畫的執行期間，以動態方式切換到較佳的聯結策略。

批次模式自適性聯結功能可讓選擇的[雜湊聯結或巢狀迴圈聯結](../../relational-databases/performance/joins.md)方法，延後到已掃描的第一個輸入**之後**。 自適性聯結運算子定義的閾值是用於決定何時要切換至巢狀迴圈計劃。 因此，您的計劃可在執行期間動態切換至較佳的聯結策略。
運作方式如下：
-  如果組建聯結輸入的資料列計數小到巢狀迴圈聯結會比雜湊聯結更佳的情況，則您的計劃就會切換成巢狀迴圈演算法。
-  如果組建聯結輸入超過特定的資料列計數閾值，則不會切換，且您的計劃會繼續執行雜湊聯結。

下列查詢用來說明自適性聯結範例：

```sql
SELECT [fo].[Order Key], [si].[Lead Time Days], [fo].[Quantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE [fo].[Quantity] = 360;
```

此查詢會傳回 336 個資料列。 透過啟用[即時查詢統計資料](../../relational-databases/performance/live-query-statistics.md)，我們會看到下列計劃：

![查詢結果 336 個資料列](./media/4_AQPStats336Rows.png)

我們在計劃中看到：
1. 我們使用了資料行存放區索引掃描，為雜湊聯結建置階段提供資料列。
1. 我們有新的自適性聯結運算子。 此運算子定義的閾值是用於決定何時要切換至巢狀迴圈計劃。 本例中的閾值是 78 個資料列。 凡是 &gt;= 78 個資料列的計劃都會使用雜湊聯結。 如果小於該閾值，則會使用巢狀迴圈聯結。
1. 因為我們傳回 336 個資料列 (超過閾值)，所以第二個分支會表示標準雜湊聯結作業的探查階段。 請注意，即時查詢統計資料會顯示流經運算子的資料列，本例中為 "672 of 672"。
1. 而最後一個分支是我們的叢集索引搜尋，供未超過閾值的巢狀迴圈聯結所使用。 請注意，我們看到的顯示是"0 of 336" 資料列 (分支未使用)。
 現在對比使用相同查詢的計劃，但這次的 *Quantity* 值在資料表中只有一個資料列：
 
```sql
SELECT [fo].[Order Key], [si].[Lead Time Days], [fo].[Quantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE [fo].[Quantity] = 361;
```
查詢會傳回一個資料列。 啟用我們在以下計劃中看到的即時查詢統計資料：

![查詢結果一個資料列](./media/5_AQPStatsOneRow.png)

我們在計劃中看到：
- 因為傳回一個資料列，現在叢集索引搜尋中有資料列通過。
- 而且，因為雜湊聯結建置階段並未繼續，所以不會有任何資料列通過第二個分支。

### <a name="adaptive-join-benefits"></a>自適性聯結的優點
經常在小型和大型聯結輸入掃描間變動的工作負載，由此功能獲益最大。

### <a name="adaptive-join-overhead"></a>自適性聯結的負擔
自調性聯結導入的記憶體需求，會比索引巢狀的迴圈聯結相等計劃更高。 系統會以巢狀迴圈有如雜湊聯結一般的方式要求額外的記憶體。 在時快時慢作業的建置階段與巢狀迴圈資料流相等聯結的比較中，會另外產生額外負荷。 加上額外的成本，隨組建輸入資料列計數浮動的案例而變動。

### <a name="adaptive-join-caching-and-re-use"></a>自適性聯結快取和重複使用
批次模式自適性聯結適合初次執行的陳述式使用，而且一旦編譯，連續執行仍會根據編譯的自適性聯結閾值和流經外部輸入建置階段的執行階段資料列聯結自動調整。

### <a name="tracking-adaptive-join-activity"></a>追蹤自適性聯結活動
自適性聯結運算子有下列計劃運算子屬性：

| 計劃屬性 | Description |
|--- |--- |
| AdaptiveThresholdRows | 顯示從雜湊聯結切換至巢狀迴圈聯結所使用的閾值。 |
| EstimatedJoinType | 可能的聯結類型。 |
| ActualJoinType | 在實際的計劃中，顯示根據閾值最後選擇的聯結演算法。 |

評估計劃會顯示自適性聯結計劃圖形，以及定義的自適性聯結閾值和預估的聯結類型。

### <a name="adaptive-join-and-query-store-interoperability"></a>自適性整聯結和查詢存放區互通性
查詢存放區擷取並可強制執行批次模式自適性聯結計劃。

### <a name="adaptive-join-eligible-statements"></a>符合自適性聯結的陳述式
讓邏輯聯結符合批次模式自適性聯結有幾個條件：
- 資料庫相容性層級是 140。
- 查詢是 SELECT 陳述式 (資料修改陳述式目前不適合)。
- 聯結能夠由索引巢狀迴圈聯結或雜湊聯結實體演算法執行。
- 雜湊聯結使用批次模式，不論是透過存在於整體查詢中的資料行存放區索引，或是由聯結直接參考的資料行存放區索引資料表。
- 產生的巢狀迴圈聯結和雜湊聯結替代解決方案應該有相同的第一個子系 (外部參考)。

### <a name="adaptive-joins-and-nested-loop-efficiency"></a>自適性聯結與巢狀迴圈效率
如果自適性聯結切換成巢狀迴圈作業，便會使用已由雜湊聯結組建讀取的資料列。 運算子「不會」再次重新讀取外部參考資料列。

### <a name="adaptive-threshold-rows"></a>自適性閾值資料列
下圖顯示雜湊聯結成本與巢狀迴圈聯結替代方案成本之間的交集範例。  在此交集點決定的閾值，會隨之決定用於聯結作業的實際演算法。

![聯結閾值](./media/6_AQPJoinThreshold.png)

### <a name="disabling-adaptive-joins-without-changing-the-compatibility-level"></a>停用自適性聯結而不變更相容性層級

您可以在資料庫或陳述式的範圍停用自適性聯結，同時仍將資料庫相容性層級維持在 140 以上。  
若要針對源自資料庫的所有查詢執行停用自適性聯結，請在適用資料庫的內容中執行下列程式碼：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_ADAPTIVE_JOINS = ON;
```

啟用時，此設定在 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) 中會顯示為已啟用。
若要針對源自資料庫的所有查詢執行重新啟用自適性聯結，請在適用資料庫的內容中執行下列程式碼：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_ADAPTIVE_JOINS = OFF;
```

您也可以將 `DISABLE_BATCH_MODE_ADAPTIVE_JOINS` 指定為 [USE HINT 查詢提示](../../t-sql/queries/hints-transact-sql-query.md#use_hint)，以針對特定查詢停用自適性聯結。 例如：

```sql
SELECT s.CustomerID,
       s.CustomerName,
       sc.CustomerCategoryName
FROM Sales.Customers AS s
LEFT OUTER JOIN Sales.CustomerCategories AS sc
       ON s.CustomerCategoryID = sc.CustomerCategoryID
OPTION (USE HINT('DISABLE_BATCH_MODE_ADAPTIVE_JOINS')); 
```

USE HINT　查詢提示的優先順序高於資料庫範圍設定或追蹤旗標設定。

## <a name="batch-mode-memory-grant-feedback"></a>批次模式記憶體授與意見反應
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的查詢後續執行計劃，包含執行所需的最小記憶體，以及能將所有資料列納入記憶體的理想記憶體授與大小。 當調整的記憶體授與大小不正確時，就會降低效能。 授與過多會浪費記憶體並降低並行。 記憶體授與不足會佔用大量磁碟資源。 透過處理重複的工作負載，批次模式記憶體授與意見反應會重新計算查詢實際所需的記憶體，然後更新快取計劃的授與值。  執行相同的查詢陳述式時，此查詢會使用修訂過的記憶體授權大小，減少影響並行的過多記憶體授與，並修正導致佔用大量磁碟資源的記憶體授與低估。
下圖顯示使用批次模式調整記憶體授與意見反應的一個範例。 由於高溢出的緣故，第一次執行查詢的期間為  **88 秒** ：   

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

啟用記憶體授與回饋後，第二次執行的期間為  **1 秒**  (低於 88 秒)，溢出完全移除且授與變高： 

![沒有溢出](./media/3_AQPGraphNoSpills.png)

### <a name="memory-grant-feedback-sizing"></a>記憶體授與意見反應調整大小
針對記憶體授與過多的狀況，如果授與的記憶體超過實際使用記憶體大小的兩倍，記憶體授與回饋便會重新計算記憶體授與並更新快取計劃。 記憶體授與小於 1 MB 的計劃不會重新計算處理超額問題。
針對會導致批次模式運算子磁碟溢出的記憶體授與大小不足狀況，記憶體授與回饋會觸發記憶體授與的重新計算。 溢出事件會報告到記憶體授與回饋，且可以透過 *spilling_report_to_memory_grant_feedback* xEvent 顯示。 此事件會傳回計劃的節點識別碼和該節點溢出的資料大小。

### <a name="memory-grant-feedback-and-parameter-sensitive-scenarios"></a>記憶體授與意見反應與參數敏感的情況
不同的參數值可能也需要不同的查詢計劃，以維持最佳狀態。 這類型的查詢即定義為「參數敏感」。 凡是參數敏感的計劃，如果記憶體授與意見反應有不穩定的記憶體需求，就會在查詢上自行停用。 計劃會在查詢重複數輪後停用，透過監視 *memory_grant_feedback_loop_disabled* xEvent 可觀察到此狀況。 如需參數探查和參數敏感性的詳細資訊，請參閱[查詢處理架構指南](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)。

### <a name="memory-grant-feedback-caching"></a>記憶體授與意見反應快取
意見反應可以儲存在快取計劃中供單次執行之用。 這是該陳述式的連續執行，但得益自記憶體授與意見反應的調整。 此功能適用於重複執行的陳述式。 記憶體授與意見反應僅會變更快取的計劃。 查詢存放區目前並未擷取變更。
如已從快取收回計劃，則不保存意見反應。 如有容錯移轉，也會遺失意見反應。 使用 `OPTION (RECOMPILE)` 的陳述式會建立新的計劃，而不會對它進行快取。 因為它不是快取而來，所以不會產生記憶體授與意見反應，也不會儲存供編譯及執行。  不過，如果有快取並重複執行**沒有**使用 `OPTION (RECOMPILE)` 的對等陳述式 (亦即使用相同的查詢雜湊)，則連續的陳述式可得益於記憶體授與回饋。

### <a name="tracking-memory-grant-feedback-activity"></a>追蹤記憶體授與意見反應活動
您可以使用 *memory_grant_updated_by_feedback* xEvent 來追蹤記憶體授與回饋事件。 此事件會追蹤目前的執行計數記錄、記憶體授與意見反應更新計劃的次數，以及記憶體授與意見反應修改快取計劃前後的理想額外記憶體授權。

### <a name="memory-grant-feedback-resource-governor-and-query-hints"></a>記憶體授與意見反應、資源管理員和查詢提示
實際的記憶體授與會接受由資源管理員或查詢提示所決定的查詢記憶體限制。

### <a name="disabling-batch-mode-memory-grant-feedback-without-changing-the-compatibility-level"></a>停用批次模式記憶體授與意見反應，而不變更相容性層級
您可以在資料庫或陳述式的範圍停用記憶體授與意見反應，同時仍將資料庫相容性層級維持在 140 以上。 若要針對源自資料庫的所有查詢執行停用批次模式的記憶體授與意見反應，請在適用資料庫的內容中執行下列程式碼：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK = ON;
```

啟用時，此設定在 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) 中會顯示為已啟用。

若要針對源自資料庫的所有查詢執行重新啟用批次模式的記憶體授與意見反應，請在適用資料庫的內容中執行下列程式碼：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK = OFF;
```

您也可以將 `DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK` 指定為 [USE HINT 查詢提示](../../t-sql/queries/hints-transact-sql-query.md#use_hint)，以針對特定查詢停用批次模式的記憶體授與意見反應。 例如：

```sql
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (USE HINT ('DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK')); 
```

USE HINT　查詢提示的優先順序高於資料庫範圍設定或追蹤旗標設定。

## <a name="row-mode-memory-grant-feedback"></a>資料列模式記憶體授與意見反應
**適用對象**：[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]作為公開預覽功能

> [!NOTE]
> 資料列模式記憶體授與回應是公開預覽版功能。  

調整批次和資料列模式運算子的記憶體授與大小，藉此在批次模式記憶體授與意見反應功能上展開資料列模式記憶體授與意見反應。  

若要在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中啟用資料列模式記憶體授與意見反應的公開預覽功能，請在執行查詢時，針對您所連線的資料庫，啟用資料庫相容性層級 150。

透過 **memory_grant_updated_by_feedback** XEvent 將可以看到資料列模式記憶體授與意見反應活動。 

從資料列模式記憶體授與意見反應開始，針對實際執行後計畫將會顯示兩個新的查詢計畫屬性：***IsMemoryGrantFeedbackAdjusted*** 和 ***LastRequestedMemory***，它們會新增至 *MemoryGrantInfo* 查詢計畫 XML 元素。 

*LastRequestedMemory* 會在查詢執行之前，顯示授與的記憶體 (KB)。 *IsMemoryGrantFeedbackAdjusted* 屬性可讓您針對實際查詢執行計劃內的陳述式，檢查記憶體授與意見反應的狀態。 此屬性中顯示的值如下：

| IsMemoryGrantFeedbackAdjusted 值 | Description |
|---|---|
| 否：第一次執行 | 記憶體授與意見反應不會針對第一次編譯和相關聯的執行，調整記憶體。  |
| 否：精確授與 | 如果沒有溢出到磁碟，而且陳述式使用至少 50% 的授與的記憶體，則不會觸發記憶體授與意見反應。 |
| 否：意見反應已停用 | 如果記憶體授與意見反應持續遭到觸發，而且在記憶體增加和減少記憶體的作業之間波動，我們將會停用陳述式的記憶體授與意見反應。 |
| Yes：調整 | 已套用記憶體授與意見反應，而且可能會針對下一次執行進一步調整。 |
| Yes：Stable | 已套用記憶體授與意見反應，而且授與的記憶體現已穩定，表示針對上次執行授與的記憶體就是針對目前執行授與的記憶體。 |

> [!NOTE]
> 在 17.9 版與更新版本中，公開預覽版資料列模式記憶體授與意見反應計劃屬性在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 圖形化查詢執行計劃中是可見的。 

### <a name="disabling-row-mode-memory-grant-feedback-without-changing-the-compatibility-level"></a>停用資料列模式記憶體授與意見反應，而不變更相容性層級
您可以在資料庫或陳述式的範圍中停用資料列模式記憶體授與意見反應，同時仍將資料庫相容性層級維持在 150 以上。 若要針對源自資料庫的所有查詢執行停用資料列模式記憶體授與意見反應，請在適用資料庫的內容中執行下列程式碼：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ROW_MODE_MEMORY_GRANT_FEEDBACK = OFF;
```

若要針對源自資料庫的所有查詢執行重新啟用資料列模式記憶體授與意見反應，請在適用資料庫的內容中執行下列程式碼：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ROW_MODE_MEMORY_GRANT_FEEDBACK = ON;
```

您也可以將 `DISABLE_ROW_MODE_MEMORY_GRANT_FEEDBACK` 指定為 [USE HINT 查詢提示](../../t-sql/queries/hints-transact-sql-query.md#use_hint)，以針對特定查詢停用資料列模式記憶體授與意見反應。 例如：

```sql
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (USE HINT ('DISABLE_ROW_MODE_MEMORY_GRANT_FEEDBACK')); 
```

USE HINT　查詢提示的優先順序高於資料庫範圍設定或追蹤旗標設定。

## <a name="interleaved-execution-for-mstvfs"></a>MSTVF 交錯執行

利用交錯執行，我們可以使用函式的實際資料列計數制定更明智的下游查詢計劃決策。 如需多重陳述式資料表值函式 (MSTVF) 的詳細資訊，請參閱[資料表值函式](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)。

交錯執行會變更單次查詢執行的最佳化和執行階段之間的單向界限，並讓計劃根據修改過的基數估計值調整。 在最佳化期間，如果我們遇到交錯執行的候選項目，目前是**多重陳述式資料表值函式 (MSTVF)**，我們會暫停最佳化、執行適用的樹狀子目錄、擷取精確的基數估計值，然後繼續下游作業的最佳化。   

MSTVF 從 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 開始具有固定的基數估計值 100，在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中則為 1。 交錯執行有利於處理因為這些固定基數估計值與 MSTVF 建立關聯而引起的工作負載效能問題。 如需 MSTVF 的詳細資訊，請參閱[建立使用者定義函式 (資料庫引擎)](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)。

下圖說明[即時查詢統計資料](../../relational-databases/performance/live-query-statistics.md)輸出，它是整體執行計劃的子集，顯示 MSTVF 固定基數估計值的影響。 您可以查看實際的資料列流程與估計的資料列。 此計劃有三個重要區域 (流向為由右至左)：
1. MSTVF 資料表掃描的固定估計值是 100 個資料列。 但此範例有 527,597 個資料列流經此 MSTVF 資料表掃描 (如即時查詢統計資料中所見的 *527597 of 100* 估計實值)，所以固定的估計值將會大幅扭曲。
1. 至於巢狀迴圈作業，假定外部端聯結只會傳回 100 個資料列。 如果 MSTVF 實際傳回大量的資料列，使用完全不同的聯結演算法可能會更好。
1. 至於雜湊比對作業，請注意小型警告符號，它在本例中表示溢出到磁碟。

![資料列流程與估計的資料列](./media/7_AQPFlowThreeAreas.png)

對比之前的計劃與啟用交錯執行所產生的實際計劃：

![交錯的計劃](./media/8_AQPInterleavedEnabledPlan.png)

1. 請注意，MSTVF 資料表掃描現在反映精確的基數估計值。 亦請注意此資料表掃描的重新排序和其他作業。
1. 而關於聯結演算法，我們已改從巢狀迴圈作業切換到雜湊比對作業，如果涉及大量的資料列，這樣更接近最佳狀態。
1. 另請注意，我們不再顯示溢出警告，因為我們要根據 MSTVF 資料表掃描的實際資料列計數，授與更多記憶體。

### <a name="interleaved-execution-eligible-statements"></a>符合交錯執行的陳述式
在交錯執行中參考陳述式的 MSTVF，目前必須是唯讀的，且不為資料修改作業的一部分。 此外，如果 MSTVF 未使用執行階段常數，則不適用於交錯執行。

### <a name="interleaved-execution-benefits"></a>交錯執行的優點
一般情況下，預估和實際資料列數目間的扭曲愈高，加上下游計劃作業的數目，對效能的影響就愈大。
一般而言，交錯執行有益於下列情況的查詢：
1. 中繼結果集的預估和實際資料列數目間有很大的扭曲 (本例中為 MSTVF)。
1. 而整體查詢對中繼結果的大小變更十分敏感。 這通常發生在查詢計劃有樹狀子目錄的複雜樹狀結構時。
僅僅 MSTVF 的 `SELECT *` 不會受益於交錯執行。

### <a name="interleaved-execution-overhead"></a>交錯執行的負擔
負擔應該最小，甚至完全沒有。 在導入交錯執行前，MSTVF 已被具體化，不過差異在於，現在我們要允許延遲最佳化，並利用具體化資料列集的基數估計值。
就像任何會影響變更的計劃一樣，有些計劃的變更，會識我們以較佳的樹狀子目錄基數，得到整體查詢更差的計劃。 風險降低可以包括還原相容性層級，或使用查詢存放區強制執行非迴歸版的計劃。

### <a name="interleaved-execution-and-consecutive-executions"></a>交錯執行和連續執行
一旦快取交錯執行計劃，第一次執行即修改過估計值的計劃會用於連續執行，不必重新具現化交錯執行。

### <a name="tracking-interleaved-execution-activity"></a>追蹤交錯執行活動
您可以在實際的查詢執行計劃中看到使用方式屬性：

| 執行計劃屬性 | Description |
| --- | --- |
| ContainsInterleavedExecutionCandidates | 適用於 *QueryPlan* 節點。 為 *true* 時，表示計劃包含交錯執行候選項目。 |
| IsInterleavedExecuted | 位於 TVF 節點 RelOp 之下 *RuntimeInformation* 元素的屬性。 為 *true* 時，這表示作業已具體化為交錯執行作業的一部分。 |

您也可以透過下列 xEvent 追蹤交錯執行項目：

| xEvent | Description |
| ---- | --- |
| interleaved_exec_status | 交錯執行進行時會引發這個事件。 |
| interleaved_exec_stats_update | 此事件會描述由交錯執行更新的基數估計值。 |
| Interleaved_exec_disabled_reason | 當具有交錯執行可能候選項目的查詢不會實際取得交錯執行時，就會引發這個事件。 |

必須執行查詢，才能讓交錯執行修改 MSTVF 基數估計值。 不過，有透過 `ContainsInterleavedExecutionCandidates` 執行程序表屬性的交錯執行候選項目時，仍會顯示預估執行計劃。    

### <a name="interleaved-execution-caching"></a>交錯執行快取
如果從快取清除或收回計劃，就會在執行查詢時重新整理使用交錯執行的編譯。
使用 `OPTION (RECOMPILE)` 的陳述式會建立使用交錯執行的新計劃，且不會對它進行快取。     

### <a name="interleaved-execution-and-query-store-interoperability"></a>交錯執行和查詢存放區互通性
使用交錯執行的計劃可以強制執行。 此計劃是根據初始執行更正基數估計值的版本。    

### <a name="disabling-interleaved-execution-without-changing-the-compatibility-level"></a>停用交錯執行而不變更相容性層級

您可以在資料庫或陳述式的範圍停用交錯執行，同時仍將資料庫相容性層級維持在 140 以上。  若要針對源自資料庫的所有查詢執行停用交錯執行，請在適用資料庫的內容中執行下列程式碼：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_INTERLEAVED_EXECUTION_TVF = ON;
```

啟用時，此設定在 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) 中會顯示為已啟用。
若要針對源自資料庫的所有查詢執行重新啟用交錯執行，請在適用資料庫的內容中執行下列程式碼：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_INTERLEAVED_EXECUTION_TVF = OFF;
```

您也可以將 `DISABLE_INTERLEAVED_EXECUTION_TVF` 指定為 [USE HINT 查詢提示](../../t-sql/queries/hints-transact-sql-query.md#use_hint)，以針對特定查詢停用交錯執行。 例如：

```sql
SELECT [fo].[Order Key], [fo].[Quantity], [foo].[OutlierEventQuantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Fact].[WhatIfOutlierEventQuantity]('Mild Recession',
                            '1-01-2013',
                            '10-15-2014') AS [foo] ON [fo].[Order Key] = [foo].[Order Key]
                            AND [fo].[City Key] = [foo].[City Key]
                            AND [fo].[Customer Key] = [foo].[Customer Key]
                            AND [fo].[Stock Item Key] = [foo].[Stock Item Key]
                            AND [fo].[Order Date Key] = [foo].[Order Date Key]
                            AND [fo].[Picked Date Key] = [foo].[Picked Date Key]
                            AND [fo].[Salesperson Key] = [foo].[Salesperson Key]
                            AND [fo].[Picker Key] = [foo].[Picker Key]
OPTION (USE HINT('DISABLE_INTERLEAVED_EXECUTION_TVF'));
```

USE HINT　查詢提示的優先順序高於資料庫範圍設定或追蹤旗標設定。


## <a name="table-variable-deferred-compilation"></a>資料表變數延後編譯

> [!NOTE]
> 資料表變數延後編譯是一項公開預覽功能。  

資料表變數延後編譯可針對參考資料表變數的查詢，提升計畫品質和整體效能。 在最佳化和初始編譯期間，此功能會根據實際資料表變數的資料列計數，傳播基數估計值。 這項精確的資料列計數資訊會最佳化下游計畫作業。

資料表變數延後編譯會延後編譯參考資料表變數的陳述式，直到第一次實際執行陳述式為止。 此延後編譯行為與暫存資料表相同。 這項變更會導致使用實際基數，不使用原始的單一資料列猜測。 

您可在 Azure SQL Database 中公開預覽資料表變數延後編譯。 若要這樣做，請啟用執行查詢時所連線資料庫的相容性層級 150。

如需詳細資訊，請參閱[資料表變數延遲編譯](../../t-sql/data-types/table-transact-sql.md#table-variable-deferred-compilation).

## <a name="scalar-udf-inlining"></a>純量 UDF 內嵌

> [!NOTE]
> 純量使用者定義函式 (UDF) 內嵌為公開預覽功能。  

純量 UDF 內嵌會自動將[純量 UDF](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#Scalar) 轉換成關聯運算式。 將它們內嵌在呼叫的 SQL 查詢中。 此轉換可改善利用純量 UDF 的工作負載效能。 純量 UDF 內嵌有益於 UDF 內的成本型最佳化作業。 其結果會是有效率、集合導向的平行處理，而不是效率不彰、反覆執行的序列執行計畫。 根據預設，資料庫相容性層級 150 會啟用此功能。

如需詳細資訊，請參閱[純量 UDF 內嵌](../user-defined-functions/scalar-udf-inlining.md)。

## <a name="approximate-query-processing"></a>近似查詢處理

> [!NOTE]
> **APPROX_COUNT_DISTINCT** 是公開預覽功能。  

近似查詢處理是新的功能系列。 它會在回應性比絕對精確度更重要的大型資料集間執行彙總作業。 例如，在 10 億筆資料列中計算 **COUNT(DISTINCT())**，以顯示在儀表板上。 在此情況下，絕對精確度不重要，但回應性非常重要。 新的 **APPROX_COUNT_DISTINCT** 彙總函式會傳回群組中唯一非 Null 值的近似數目。

如需詳細資訊，請參閱 [APPROX_COUNT_DISTINCT (Transact-SQL)](../../t-sql/functions/approx-count-distinct-transact-sql.md)。

## <a name="batch-mode-on-rowstore"></a>資料列存放區上的批次模式 

> [!NOTE]
> 資料列存放區上的批次模式是一項公開預覽功能。  

資料列存放區上的批次模式可針對分析工作負載啟用批次模式執行功能，而不需要資料行存放區索引。  這項功能支援用於磁碟上堆積和 B 型樹狀結構索引的批次模式執行和點陣圖篩選。 資料列存放區上的批次模式可支援所有現有具備批次模式功能的運算子。

### <a name="background"></a>背景

[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 引進了新功能，可加速分析工作負載：資料行存放區索引。 我們已擴展使用案例，並改善每一個後續版本的資料行存放區索引效能。 到目前為止，我們已以單一功能的形式呈現及記載所有這些功能。 您在資料表上建立資料行存放區索引。 而且您的分析工作負載會更快。 但使用了兩種相關卻相異的技術：
- 使用**資料行存放區**索引，分析查詢只存取其所需資料行中的資料。 使用資料行存放區格式的頁面壓縮，比傳統的**資料列存放區**索引壓縮更有效。 
- 使用**批次模式**處理，查詢運算子處理資料更有效率。 它們會批次處理資料列，而不是一次處理一筆資料列。 其他數項延展性改善也與批次模式處理繫結。 如需批次模式的詳細資訊，請參閱[執行模式](../../relational-databases/query-processing-architecture-guide.md#execution-modes)。

這兩組功能一同使用，改善輸入/輸出 (I/O) 和 CPU 使用率：
- 使用資料行存放區索引，可在記憶體中放置更多資料。 減少 I/O 的需要。
- 批次模式處理可更有效率的使用 CPU。

這兩項技術會盡可能地利用彼此的優勢。 例如，批次模式彙總可作為資料行存放區索引的一部分進行評估。 我們也會更有效率的搭配批次模式聯結和批次模式彙總，使用執行長度限制編碼來處理壓縮過的資料行存放區資料。 
 
這兩項功能可獨立使用：
* 您取得使用資料行存放區索引的資料列模式計畫。
* 您取得只使用資料列存放區索引的批次模式計畫。 

兩種功能一起使用，通常會取得最佳結果。 因此到目前為止，SQL Server 查詢最佳化工具仍認為批次模式處理只適用於包含至少一個具有資料行存放區索引的資料表查詢。

資料行存放區索引不適合某些應用程式。 應用程式可能使用資料行存放區索引不支援的一些其他功能。 例如，就地修改與資料行存放區壓縮不相容。 因此，具有叢集資料行存放區索引的資料表不支援觸發程序。 更重要的是，資料行存放區索引會增加 **DELETE** 和 **UPDATE** 陳述式的額外負荷。 

針對某些混合式交易分析工作負載，工作負載交易部分所帶來額外負荷仍超過資料行存放區索引的好處。 這種狀況可以改善只使用批次模式處理的 CPU 使用量。 這就是為什麼資料列存放區功能的批次模式會考慮用批次模式處理所有查詢。 涉及哪些索引並不重要。

### <a name="workloads-that-might-benefit-from-batch-mode-on-rowstore"></a>可從資料列存放區批次模式受益的工作負載

下列工作負載可從資料列存放區的批次模式受益：
* 工作負載有很大部分是由分析查詢構成。 通常，這些查詢會有例如聯結或彙總的運算子，可處理數十萬筆或更多的資料列。
* CPU 繫結的工作負載。 如果瓶頸為 I/O，我們仍建議您盡可能考慮資料行存放區索引。
* 建立資料行存放區索引會將過多的額外負荷新增至您工作負載的交易式部分。 或者，建立資料行存放區索引不可行，因為您應用程式的相依功能尚不支援資料行存放區索引。

> [!NOTE]
> 資料列存放區上的批次模式僅協助減少 CPU 使用量。 瓶頸若與 IO 相關，且資料尚未快取 (「冷」快取)，則資料列存放區上的批次模式將無法改善已耗用時間。 同樣的，若電腦上沒有足夠記憶體可供快取所有資料，則效能也不太可能獲得改善。

### <a name="what-changes-with-batch-mode-on-rowstore"></a>資料列存放區上的批次模式有哪些變更？

除了將相容性層級移動到 150 級之外，您無須變更任何項目，也能為候選工作負載啟用資料列存放區上的批次模式。

即使查詢並未涉及任何具有資料行存放區索引的資料表，查詢處理器現在也會使用啟發學習法來決定是否要考慮使用批次模式。 啟發學習法包含下列檢查：
1. 對資料表大小、使用的運算子，以及輸入查詢中估計基數的初始檢查。
2. 最佳化工具為查詢探索更便宜的新計劃時所帶來的額外檢查點。 若這些替代方案並未大量使用批次模式，則最佳化工具會停止探索批次模式的替代項目。

如果使用資料列存放區上的批次模式，您在查詢計畫中看到的實際執行模式如同**批次模式**。 掃描運算子會使用批次模式處理磁碟上的堆積和 B 型樹狀結構索引。 此批次模式掃描可評估批次模式點陣圖篩選。 您也可能會在計畫中看到其他批次模式運算子。 例如雜湊聯結、雜湊式彙總、排序、Window 彙總、篩選、串連和計算純量運算子。

### <a name="remarks"></a>Remarks

* 查詢計畫並非一律使用批次模式。 查詢最佳化工具可能會判斷批次模式對查詢沒有幫助。 
* 查詢最佳化工具的搜尋空間正在變更。 因此，如果收到資料列模式計畫，它可能和您在較低相容性層級中取得的計畫不一樣。 而如果您收到批次模式計畫，它可能和您以資料行存放區索引取得的計畫不一樣。 
* 針對混合資料行存放區和資料列存放區索引的查詢，計畫可能也會因為新的批次模式資料列存放區掃描而變更。
* 資料列存放區掃描上新批次模式的目前限制： 
    * 對於記憶體內部 OLTP 資料表，或是磁碟上堆積與 B 型樹狀結構以外的任何索引，它無法生效。 
    * 它也無法在擷取或篩選大型物件 (LOB) 資料行時生效。 這項限制包含疏鬆資料行集和 XML 資料行。
* 甚至有具備資料行存放區索引但不使用批次模式的查詢。 例如包含資料指標的查詢。 這些相同排除項目也會擴及資料列存放區上的批次模式。

### <a name="configure-batch-mode-on-rowstore"></a>設定資料列存放區上的批次模式

預設開啟 **BATCH_MODE_ON_ROWSTORE** 資料庫範圍設定。 它會停用資料列存放區上的批次模式，但不要求變更資料庫相容性層級：

```sql
-- Disabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = OFF;

-- Enabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = ON;
```

您可以透過資料庫範圍設定停用資料列存放區上的批次模式。 但使用 **ALLOW_BATCH_MODE** 查詢提示仍可覆寫查詢層級的設定。 下列範例會啟用資料列存放區上的批次模式，即使已透過資料庫範圍設定停用該項功能：

```sql
SELECT [Tax Rate], [Lineage Key], [Salesperson Key], SUM(Quantity) AS SUM_QTY, SUM([Unit Price]) AS SUM_BASE_PRICE, COUNT(*) AS COUNT_ORDER
FROM Fact.OrderHistoryExtended
WHERE [Order Date Key]<=DATEADD(dd, -73, '2015-11-13')
GROUP BY [Tax Rate], [Lineage Key], [Salesperson Key]
ORDER BY [Tax Rate], [Lineage Key], [Salesperson Key]
OPTION(RECOMPILE, USE HINT('ALLOW_BATCH_MODE'));
```

您也可以使用 **DISALLOW_BATCH_MODE** 查詢提示，針對特定查詢停用資料列存放區上的批次模式。 請參閱下列範例：

```sql
SELECT [Tax Rate], [Lineage Key], [Salesperson Key], SUM(Quantity) AS SUM_QTY, SUM([Unit Price]) AS SUM_BASE_PRICE, COUNT(*) AS COUNT_ORDER
FROM Fact.OrderHistoryExtended
WHERE [Order Date Key]<=DATEADD(dd, -73, '2015-11-13')
GROUP BY [Tax Rate], [Lineage Key], [Salesperson Key]
ORDER BY [Tax Rate], [Lineage Key], [Salesperson Key]
OPTION(RECOMPILE, USE HINT('DISALLOW_BATCH_MODE'));
```

## <a name="see-also"></a>另請參閱

[SQL Server 資料庫引擎和 Azure SQL Database 的效能中心](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[查詢處理架構指南](../../relational-databases/query-processing-architecture-guide.md)    
[邏輯和實體運算子參考執行程序表](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[聯結](../../relational-databases/performance/joins.md)    
[示範自適性查詢處理](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)       
[示範智慧型 QP](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/intelligent-query-processing)   
