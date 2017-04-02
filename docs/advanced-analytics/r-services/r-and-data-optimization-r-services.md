---
title: "R 和資料最佳化 (R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b6104878-ed19-47a7-ac37-21e4d6e2a1af
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# R 和資料最佳化 (R Services)
本主題說明更新您的 R 程式碼，以提升效能，或避免已知的問題的方法。

## 計算內容

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 可以使用 __本機__ 或 __SQL__ 執行分析時，計算內容。 當使用 __本機__ 計算內容中，分析用戶端電腦上執行，而且資料必須從提取 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 在網路上。 此網路轉移取決於傳輸的資料大小，網路連線的速度以及同時發生其他網路傳輸，並產生效能影響。

如果計算內容是 __SQL Server__, ，然後分析函式內執行 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 資料是本機 「 分析 」 工作，因此沒有網路負荷，方法導入。 

當使用大型資料集，您應該一律使用 SQL 計算內容。

## 因素

R 語言會將字串從資料表轉換成因素。 許多資料來源物件採取 `colInfo` 做為參數來控制資料行的方式。 例如， `c(“fruit” = c(type = “factor”, levels=as.character(c(1:3)), newLevels=c(“apple”, “orange”, “banana”)))` 會取用整數 1、 2 和 3，從資料表和層級的因素將它們視為 `apple`, ，`orange`, ，和 `banana`。 

資料科學家經常使用因子變數中的公式。不過，當來源資料是一個整數，請使用因素會造成對效能造成影響的整數會轉換為字串，在執行階段。 不過，如果資料行包含的字串，您可以指定時間，使用前面的層級 `colInfo`。 在此情況下，會是相同的陳述式  `c(“fruit” = c(type = “factor”, levels= c(“apple”, “orange”, “banana”)))`, ，這會將字串視為因素在讀取。 

若要避免執行的階段轉換，請考慮將層級儲存為資料表中的整數和公式的第一個範例中所述使用它。 如果沒有任何模型層代中的語意差異，這種方法可以指向更佳的效能。

## 資料轉換

資料科學家通常會使用轉換函數以 R 撰寫分析的一部分。 轉換函式必須套用至從資料表中擷取每個資料列。 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], ，這項轉換會在批次模式，而且涉及 R 解譯器和分析引擎之間的通訊。 若要執行轉換，從 SQL 分析引擎，然後與 R 解譯器處理序之間的來回移動的資料。 因此，使用轉換可以容納大幅負面影響演算法的效能，視資料量所示範。

會將所有必要的資料行的資料表或檢視，再執行分析，以避免轉換運算期間更有效率。 如果您不可以將其他資料行加入至現有的資料表，請考慮使用已轉換的資料行建立另一個資料表或檢視表，並使用適當的查詢來擷取資料。

## 批次處理

SQL 資料來源 (`RxSqlServerData`) 有一個選項來指示使用參數的批次大小 `rowsPerRead`。 這個參數會指定每次處理的資料列數目。 在執行階段，演算法會讀取指定的每個批次中的資料列編號。 根據預設，此參數的值設為 50000，以確保這些演算法可以也即使在發生記憶體不足的電腦上執行。 如果電腦有足夠的可用記憶體，增加此值 500000 或甚至百萬個可能會產生較佳的效能，尤其是對大型資料表。 

增加此值可能不一定會產生更好的結果，而且可能需要一些實驗，以決定最佳的值。 這個優點會更明顯大型資料集上使用多處理序 (`numTasks` 設的值大於 `1`)。

## 平行處理

若要改善效能的分析函式內執行 rx [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], ，[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 依賴使用上的可用核心的平行處理 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 機器。 有兩種方式可達成的平行處理 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]:

* 當使用 `sp_execute_external_script` 執行 R 指令碼的預存程序設定 `@parallel` 參數 `1`。 這是適用於不使用的 「 接收 」 開頭通常為 RevoScaleR 函式的 R 指令碼。 如果指令碼會使用 RevoScaleR 函式，會自動處理平行處理，而且您不應將 `@parallel` 到 `1`。

    如果 R 指令碼可以平行處理，而且如果 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 查詢可平行處理，然後 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 會建立多個平行的處理序 (最多 __最大程度的平行處理原則 MAXDOP__ 設定 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)],，) 和跨所有處理程序中執行相同的指令碼。 每個處理序只會收到資料的一部分，因此不適合用於指令碼，一定會看到所有的資料，例如當定型模型。 不過，最好以平行方式執行工作，例如批次預測時。 如需有關使用平行處理原則與 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), ，請參閱 __進階提示︰ 平行處理__ 區段 [TRANSACT-SQL 中使用 R 程式碼](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md)。

* 當使用 SQL Server 計算內容 rx 函式，設定 `numTasks` 到您想要建立的處理序數目。 建立處理序的實際數目由 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], ，且可能會小於您要求。 建立處理序的數目不能超過 __MAXDOP__。

    如果 R 指令碼可以平行處理，而且如果 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 查詢可平行處理，然後 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 時執行的接收函式會建立多個平行的處理序。

將建立的處理序的數目取決於許多因素，例如資源管理、 目前的資源使用量、 其他工作階段，以及使用 R 指令碼用查詢的查詢執行計畫。 

### 查詢平行處理

若要確保以平行方式，可以分析資料，用來擷取資料的查詢應該一種則可以平行執行的轉譯本身已框架處理。 

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 支援使用 SQL 資料來源使用 `RxSqlServerData` 指定的來源。 來源可以是資料表或查詢。 例如，下列程式碼同時定義 R 資料來源物件的 SQL 查詢︰
~~~~
RxSqlServerData(table=”airline”, connectionString = sqlConnString)
~~~~

~~~~
RxSqlServerData(sqlquery=”select [ArrDelay],[CRSDepTime],[DayOfWeek] from airlineWithIndex where rowNum <= 100000”, connectionString = sqlConnString)
~~~~ 

分析演算法提取較大的資料表中的資料，請務必指定給查詢 `RxSqlServerData` 最適合平行執行。 不會導致平行執行計畫的查詢會導致計算的單一處理序。

[!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 可以用來分析執行計畫，並改善查詢效能。 例如，遺漏索引的資料表上可能會影響執行查詢所花費的時間。 請參閱 [的效能監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md) 如需詳細資訊。

此查詢會擷取所需的資料行時可能會影響效能的另一個監督。 比方說，如果公式根據只有 3 個資料行，資料表有 30 個資料行，請勿使用查詢例如 `select *` 或選取多個資料行比所需的其中一個。

> [!NOTE]
> 如果資料表中資料來源，而不是查詢中，指定 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 在內部將決定必要的資料行從資料表擷取; 不過，這種方法是不太可能會導致平行執行。

## 演算法參數

許多 rx 訓練演算法都支援參數來控制如何產生定型模型。 雖然精確度和模型的正確性很重要，則可能同樣重要的是演算法的效能。 您可以修改 parametersthe 模型訓練參數，以增加速度的計算，並在許多情況下，您可能可以改善效能，而不會降低精確度或正確性。 

例如， `rxDTree` 支援 `maxDepth` 參數，控制樹狀目錄深度上限。 做為 `maxDepth` 會增加，效能可能會降低，所以一定要分析的效能影響與深度增加的優點。 

其中一個參數，可以搭配 `rxLinMod` 和 `rxLogit` 是 `cube` 引數。 時，公式的第一個相依變數是因素變數，則可以使用這個引數。 如果 `cube` 設為 `TRUE`, ，迴歸是使用資料分割的反向，它可能會比較快，並使用較少的記憶體比標準迴歸的計算。 如果公式中有大量的變數，則可能更為顯著提升效能。

 [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) 控制模型適合各種演算法使用者指南 》 有一些實用資訊。 例如，使用 `rxDTree` 您可以控制時間複雜性和預測精確度，例如調整參數之間的平衡 `maxNumBins`, ，`maxDepth`, ，`maxComplete`, ，和 `maxSurrogate`。 增加超過 10 或 15 至深度可以讓計算非常耗費資源。

如需有關微調效能 `rxDForest` 和 `rxDTree`, ，請參閱 [效能微調選項 rxDForest/rxDTree](https://support.microsoft.com/kb/3104235)。

## 模型和預測

一旦完成訓練，並選取最佳的模型，我們建議您在資料庫中儲存模型，使其容易供預測。 對於需要預測的線上交易處理，從預測資料庫載入預先計算的模型是很有效率。 範例指令碼會使用此方法來序列化和模型儲存在資料庫資料表中。 預測模型是從資料庫還原序列化。

某些演算法，例如 lm 或 glm 所產生的模型可以很大，尤其是大型資料集上使用。 有一些可以儲存在資料大小限制 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 您應該清除模型，再將其儲存至資料庫。

> [!NOTE] 如果使用預存的模型以及整合到應用程式的分析快速預測是重要的案例，我們建議您 __DeployR__。 它可用來輕鬆地將 web、 桌面、 行動及儀表板應用程式內的 R 分析的整合。 特別是，它非常適合儲存模型，然後再執行單一資料列使用儲存的模型的預測。 如需詳細資訊，請參閱 [有關 DeployR](https://msdn.microsoft.com/microsoft-r/rserver/deployr-about)。

## 另請參閱
[資源控管](../../advanced-analytics/r-services/resource-governance-for-r-services.md)
[資源管理員](../../relational-databases/resource-governor/resource-governor.md)

[建立外部的資源集區](../../t-sql/statements/create-external-resource-pool-transact-sql.md)

 [SQL Server R 服務效能微調的指南](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
 [R 服務的 SQL Server 組態](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
 
 [效能案例研究](../../advanced-analytics/r-services/performance-case-study-r-services.md)
 