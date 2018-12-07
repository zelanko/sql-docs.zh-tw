---
title: Microsoft SQL 資料庫中的智慧查詢處理 | Microsoft Docs
description: 可改善 SQL Server 和 Azure SQL Database 查詢效能的智慧查詢處理功能。
ms.custom: ''
ms.date: 11/07/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords: ''
ms.assetid: ''
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d48f9fd87ff375a518b038d9ed4ef4a8d42675cc
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52403923"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>SQL 資料庫中的智慧查詢處理
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

**智慧查詢處理**功能系列都包含具有廣泛影響的功能，能夠以最少的實作投入量改善現有工作負載的效能。

![智慧查詢處理功能](./media/3_IQPFeatureFamily.png)

## <a name="adaptive-query-processing"></a>彈性查詢處理
彈性查詢處理功能系列包括查詢處理改良功能，可調整最佳化策略以符合您應用程式工作負載的執行階段條件。 包含下列改善： 
-  批次模式自適性聯結
-  記憶體授與意見反應
-  交錯執行多重陳述式資料表值函式 (MSTVF)

### <a name="batch-mode-adaptive-joins"></a>批次模式自適性聯結
這項功能可讓您的計劃在使用單一快取計畫的執行期間，以動態方式切換到較好的聯結策略。

如需批次模式自適性聯結的詳細資訊，請參閱 [SQL 資料庫中的彈性查詢處理](../../relational-databases/performance/adaptive-query-processing.md)。

### <a name="row-and-batch-mode-memory-grant-feedback"></a>資料列和批次模式記憶體授與意見反應
> [!NOTE]
> 資料列模式記憶體授與回應是公開預覽版功能。  

這項功能將會重新計算查詢所需的實際記憶體，然後更新快取計劃的授與值，減少影響並行存取的過多記憶體授與，並修正導致佔用大量磁碟資源的低估記憶體授與。

如需記憶體授與意見反應的詳細資訊，請參閱 [SQL 資料庫中的彈性查詢處理](../../relational-databases/performance/adaptive-query-processing.md)。

### <a name="interleaved-execution-for-multi-statement-table-valued-functions-mstvfs"></a>交錯執行多重陳述式資料表值函式 (MSTVF)
利用交錯執行，我們可以使用函式的實際資料列計數制定更明智的下游查詢計劃決策。 如需多重陳述式資料表值函式 (MSTVF) 的詳細資訊，請參閱[資料表值函式](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)。

如需交錯執行的詳細資訊，請參閱 [SQL 資料庫中的彈性查詢處理](../../relational-databases/performance/adaptive-query-processing.md)。

## <a name="table-variable-deferred-compilation"></a>資料表變數延後編譯
> [!NOTE]
> 資料表變數延後編譯是一項公開預覽功能。  

資料表變數延後編譯可針對參考資料表變數的查詢，提升計劃品質和整體效能。 在最佳化和初始編譯期間，此功能將會根據實際資料表變數的資料列計數，傳播基數估計值。  這個精確的資料列計數資訊將用於最佳化下游計劃作業。

使用資料表變數延後編譯時，會延遲編譯參考資料表變數的陳述式，直到第一次實際執行陳述式為止。 這個延後編譯行為與暫存資料表的行為完全相同，而且此變更會導致使用實際基數，而不是原始的單一資料列猜測。 若要在 Azure SQL Database 中啟用資料表變數延後編譯的公開預覽功能，請在執行查詢時，針對您所連線的資料庫，啟用資料庫相容性層級 150。

如需詳細資訊，請參閱[資料表變數延遲編譯](../../t-sql/data-types/table-transact-sql.md#table-variable-deferred-compilation ).

## <a name="scalar-udf-inlining"></a>純量 UDF 內嵌
> [!NOTE]
> 純量 UDF 內嵌為公開預覽功能。  

純量 UDF 內嵌會將[純量使用者定義函式 (UDF)](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#Scalar) 自動轉換成關聯運算式，並將它們內嵌在呼叫 SQL 查詢中，以改善運用純量 UDF 之工作負載的效能。 純量 UDF 內嵌有助於對 UDF 內的作業進行以成本為基礎的最佳化，以促成集合導向、平行且有效率的計畫，而不是無效率、反覆且連續的執行計畫。 根據預設，資料庫相容性層級 150 會啟用此功能。

如需詳細資訊，請參閱[純量 UDF 內嵌](https://docs.microsoft.com/sql/relational-databases/user-defined-functions/scalar-udf-inlining?view=sqlallproducts-allversions)。

## <a name="approximate-query-processing"></a>近似查詢處理
> [!NOTE]
> APPROX_COUNT_DISTINCT 是公開預覽功能。  

近似查詢處理是一個新的功能系列，其設計目的在於提供大型資料集之間的彙總，在此情況下回應性比絕對精確度更重要。  例如，針對 10 億個資料列計算 COUNT(DISTINCT())，以顯示在儀表板上。  在此情況下，絕對精確度並不重要，但回應性很重要。 新的 APPROX_COUNT_DISTINCT 彙總函式會傳回群組中非 Null 的唯一值的近似數目。

如需詳細資訊，請參閱 [APPROX_COUNT_DISTINCT (Transact-SQL)](../../t-sql/functions/approx-count-distinct-transact-sql.md)。

## <a name="batch-mode-on-rowstore"></a>資料列存放區上的批次模式 
> [!NOTE]
> 資料列存放區上的批次模式是一項公開預覽功能。  

### <a name="background"></a>背景
[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 引進了新功能，可加速分析工作負載：資料行存放區索引。 我們已擴展使用案例，並改善每一個後續版本中資料行存放區索引的效能。 到目前為止，我們已將所有這些功能作為單一功能呈現及記載：您在資料表上建立資料行存放區索引，您的分析工作負載即可「變得更快」。 但在表面下，實際上包含了兩組相關卻相異的技術：
- **資料行存放區**索引只會允許分析查詢存取其所需資料行中的資料。 相較於傳統「資料列存放區」索引的頁面壓縮，資料行存放區格式也允許更有效的壓縮。 
- **批次模式**處理允許查詢運算子透過一次使用一批資料列，而非一次僅使用一個資料列，以更有效率的方式處理資料。 其他數項延展性改善也與批次模式處理繫結。 如需批次模式的詳細資訊，請參閱[執行模式](../../relational-databases/query-processing-architecture-guide.md#execution-modes)。

這兩組功能一同使用，即可改善 I/O 和 CPU 使用率：
- 資料行存放區索引允許在記憶體中放入更多您的資料，藉此減少 I/O 的需求。
- 批次模式處理可更有效率的使用 CPU。

這兩項技術會盡可能地利用彼此的優勢。 例如，批次模式彙總可作為資料行存放區索引的一部分進行評估。 我們也會更有效率的搭配批次模式聯結和批次模式彙總，使用執行長度限制編碼來處理壓縮過的資料行存放區資料。 
 
這兩項功能已能各自獨立使用：您可以取得使用資料行存放區索引的資料列模式計劃，也能取得僅使用資料列存放區索引的批次模式計劃。 但因為在大多數的案例中，您都可以透過同時使用兩項功能來取得最佳結果，SQL 的查詢最佳化工具直到現在都將批次模式處理視為僅適用於涉及至少一個具有資料行存放區索引資料表的查詢。

針對一部分應用程式，資料行存放區索引並非可用選項，因為應用程式使用某些資料行存放區索引不支援的其他功能 (例如具有叢集資料行存放區索引的資料表上不支援觸發)。 更重要的是，資料行存放區索引會增加 DELETE 和 UPDATE 陳述式的額外負荷，因為就地修改與資料行存放區壓縮不相容。 針對某些混合式交易分析工作負載，資料行存放區索引可為分析查詢帶來的好處，仍不及為工作負載交易部分帶來的額外負荷。 這類情況可透過僅使用批次模式處理來改善 CPU 使用率，這也是**資料列存放區上的批次模式**功能會為所有查詢考慮批次模式，無論涉及索引為何的原因。

### <a name="what-workloads-may-benefit-from-batch-mode-on-rowstore"></a>可從資料列存放區上批次模式受益的工作負載
下列工作負載可從資料列存放區上的批次模式受益：
1.  工作負載的一項重要部分由分析查詢 (根據經驗法則，即為使用如聯結或彙總運算子處理成千上百，甚至更多資料列的查詢) 組成，**並且**
2.  工作負載與 CPU 繫結 (若瓶頸為 IO，仍建議盡可能考慮使用資料行存放區索引)，**並且**
3.  建立資料行存放區索引會為您工作負載的交易部分增加太多額外負荷，**或是**建立資料行存放區索引不可行，因為您的應用程式相依於資料行存放區索引尚未支援的功能。

> [!NOTE]
> 資料列存放區上的批次模式僅能協助減少 CPU 耗用量。 若您的瓶頸與 IO 相關，並且資料尚未快取 (「冷」快取)，則資料列存放區上的批次模式將無法改善耗用時間。 同樣的，若電腦上沒有足夠記憶體可供快取所有資料，則效能也不太可能獲得改善。

### <a name="what-changes-with-batch-mode-on-rowstore"></a>資料列存放區上的批次模式會有哪些變更
除了將相容性層級移動到 150 級之外，您無須變更任何項目，也能為候選工作負載啟用資料列存放區上的批次模式。

即使查詢並未涉及任何具有資料行存放區索引的資料表，查詢處理器現在也會使用啟發學習法來決定是否要考慮使用批次模式。 啟發學習法的組成要素：
1.  對資料表大小、使用的運算子，以及輸入查詢中估計基數的初始檢查。
2.  最佳化工具為查詢探索更便宜的新計劃時所帶來的額外檢查點。 若這些替代方案並未大量使用批次模式，則最佳化工具會停止探索批次模式的替代項目。

若使用資料列存放區上的批次模式，則在查詢執行計劃中，您會看到掃描運算子針對磁碟上堆積和 B 型樹狀結構使用的實際執行模式顯示為「批次模式」。  此批次模式掃描可評估批次模式點陣圖篩選。  您也可能會在計劃中看到其他批次模式運算子，例如雜湊聯結、雜湊式彙總、排序、Window 彙總、篩選、串連和計算純量運算子。

### <a name="remarks"></a>Remarks
1.  無法保證查詢計劃會使用批次模式。 查詢最佳化工具可能會判斷批次模式對查詢沒有幫助。 
2.  隨著查詢最佳化工具的搜尋空間變更，無法保證您在取得資料列模式計劃時，該計劃會與您在較低相容性層級時取得的計劃相同。 也無法保證當您取得批次模式計劃時，它會與您使用資料行存放區索引時所取得的計劃相同。 
3.  針對混合資料行存放區和資料列存放區索引的查詢，計劃可能也會因為新的批次模式資料列存放區掃描而發生輕微變更。
4.  目前針對資料列存放區掃描上的新批次模式限制：它無法針對記憶體內部 OLTP 資料表，或是任何磁碟上堆積或 B 型樹狀結構以外的索引生效。 它也無法在擷取或篩選 LOB 資料行時生效。 這項限制包含疏鬆資料行集和 XML 資料行。
5.  針對有些查詢，即使具有資料行存放區索引也不會使用批次模式 (例如涉及資料指標的查詢)，並且相同排除項目也會延伸至資料列存放區上的批次模式。

### <a name="configuring-batch-mode-on-rowstore"></a>設定資料列存放區上的批次模式
根據預設，會開啟 BATCH_MODE_ON_ROWSTORE 資料庫範圍設定，並且可用於停用資料列存放區上的批次模式，而無須變更資料庫相容性層級：

```sql
-- Disabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = OFF;

-- Enabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = ON;
```

您可以透過資料庫範圍設定停用資料列存放區上的批次模式，同時使用 ALLOW_BATCH_MODE 查詢提示覆寫設定。 下列範例會啟用資料列存放區上的批次模式，即使已透過資料庫範圍設定停用該項功能：

```sql
SELECT [Tax Rate], [Lineage Key], [Salesperson Key], SUM(Quantity) AS SUM_QTY, SUM([Unit Price]) AS SUM_BASE_PRICE, COUNT(*) AS COUNT_ORDER
FROM Fact.OrderHistoryExtended
WHERE [Order Date Key]<=DATEADD(dd, -73, '2015-11-13')
GROUP BY [Tax Rate], [Lineage Key], [Salesperson Key]
ORDER BY [Tax Rate], [Lineage Key], [Salesperson Key]
OPTION(RECOMPILE, USE HINT('ALLOW_BATCH_MODE'));
```

您也可以透過使用 DISALLOW_BATCH_MODE 查詢提示，來為特定查詢停用資料列存放區上的批次模式。 例如：

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
[執行程序邏輯和實體運算子參考](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[聯結](../../relational-databases/performance/joins.md)    
[示範自適性查詢處理](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)       
[示範智慧型 QP](https://github.com/joesackmsft/Conferences/blob/master/IQPDemos/IQP_Demo_ReadMe.md)   
