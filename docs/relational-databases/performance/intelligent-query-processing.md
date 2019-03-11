---
title: Microsoft SQL 資料庫中的智慧查詢處理 | Microsoft Docs
description: 可改善 SQL Server 和 Azure SQL Database 查詢效能的智慧查詢處理功能。
ms.custom: ''
ms.date: 02/21/2019
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
ms.openlocfilehash: 1b92bc15079fcc85212ea3d1b51be64a3348a4b1
ms.sourcegitcommit: 2663063e29f2868ee6b6d596df4b2af2d22ade6f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/04/2019
ms.locfileid: "57305366"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>SQL 資料庫中的智慧查詢處理

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

智慧型查詢處理 (QP) 功能系列包含影響廣泛的功能。 它們會以最少的實作投入時間來改善現有工作負載效能。 移至適用的資料庫相容性層級，即可自動得益於此功能系列。

| **IQP 功能** | **Azure SQL Database 支援** | **SQL Server 支援** |
| --- | --- | --- |
| [自適性聯結 (批次模式)](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#batch-mode-adaptive-joins) | 是，屬於相容性層級 140| 是，自 SQL Server 2017 開始屬於相容性層級 140|
| [近似的相異計數](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#approximate-query-processing) | 是，公開預覽| 是，自 SQL Server 2019 CTP 2.0 開始，公開預覽|
| [資料列存放區上的批次模式](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#batch-mode-on-rowstore) | 是，屬於相容性層級 150，公開預覽| 是，自 SQL Server 2019 CTP 2.0 開始屬於相容性層級 150，公開預覽|
| [交錯執行](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#interleaved-execution-for-multi-statement-table-valued-functions) | 是，屬於相容性層級 140| 是，自 SQL Server 2017 開始屬於相容性層級 140|
| [記憶體授與意見反應 (批次模式)](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#batch-mode-memory-grant-feedback) | 是，屬於相容性層級 140| 是，自 SQL Server 2017 開始屬於相容性層級 140|
| [記憶體授與意見反應 (資料列模式)](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#row-mode-memory-grant-feedback) | 是，屬於相容性層級 150，公開預覽| 是，自 SQL Server 2019 CTP 2.0 開始屬於相容性層級 150，公開預覽|
| [純量 UDF 內嵌](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#scalar-udf-inlining) | 否，但預計在未來更新 | 是，自 SQL Server 2019 CTP 2.1 開始屬於相容性層級 150，公開預覽|
| [資料表變數延後編譯](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#table-variable-deferred-compilation) | 是，屬於相容性層級 150，公開預覽| 是，自 SQL Server 2019 CTP 2.0 開始屬於相容性層級 150，公開預覽|



## <a name="adaptive-query-processing"></a>彈性查詢處理

自適性查詢處理功能系列包括下列的查詢處理改善。 這些改善會調整最佳化策略，使其符合您應用程式工作負載的執行階段條件： 
- 批次模式自適性聯結
- 記憶體授與意見反應
- 交錯執行多重陳述式資料表值函式 (MSTVF)

### <a name="batch-mode-adaptive-joins"></a>批次模式自適性聯結

這項功能可讓您的計畫在使用單一快取計畫的執行期間，以動態方式切換到較佳的聯結策略。

如需批次模式自適性聯結的詳細資訊，請參閱 [SQL 資料庫中的彈性查詢處理](../../relational-databases/performance/adaptive-query-processing.md)。

### <a name="row-and-batch-mode-memory-grant-feedback"></a>資料列和批次模式記憶體授與意見反應

> [!NOTE]
> 資料列模式記憶體授與回應是公開預覽版功能。  

這項功能會重新計算查詢所需的實際記憶體。 然後更新快取計畫的授與值。 減少影響並行的過多記憶體授與。 這項功能也會修正導致佔用大量磁碟資源的低估記憶體授與。

如需記憶體授與意見反應的詳細資訊，請參閱 [SQL 資料庫中的彈性查詢處理](../../relational-databases/performance/adaptive-query-processing.md)。

### <a name="interleaved-execution-for-mstvfs"></a>MSTVF 交錯執行

利用交錯執行，我們可以使用函式的實際資料列計數制定更明智的下游查詢計劃決策。 如需多重陳述式資料表值函式 (MSTVF) 的詳細資訊，請參閱[資料表值函式](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)。

如需交錯執行的詳細資訊，請參閱 [SQL 資料庫中的彈性查詢處理](../../relational-databases/performance/adaptive-query-processing.md)。

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
[示範智慧型 QP](https://github.com/joesackmsft/Conferences/blob/master/IQPDemos/IQP_Demo_ReadMe.md)   
