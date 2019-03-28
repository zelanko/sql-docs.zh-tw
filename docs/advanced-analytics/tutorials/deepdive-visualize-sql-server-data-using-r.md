---
title: 使用 RevoScaleR rxHistogram-SQL Server Machine Learning 的 SQL Server 資料視覺化
description: 教學課程逐步解說如何將 SQL Server 上使用 R 語言的資料視覺化。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: c39d19807cfe01ca9c96b47de020abb9227c43a0
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58513075"
---
#  <a name="visualize-sql-server-data-using-r-sql-server-and-revoscaler-tutorial"></a>使用 R （SQL Server 和 RevoScaleR 教學課程） 的 SQL Server 資料視覺化
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這一課是屬於[RevoScaleR 教學課程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

在這一課中，使用 R 函數來檢視中的值分佈*creditLine*依性別資料行。

> [!div class="checklist"]
> * 建立長條圖輸入的最小值-最大值變數
> * 在長條圖中使用的資料視覺化**rxHistogram**從**RevoScaleR**
> * 使用散佈圖使用將資料視覺化**levelplot**從**斜格紋**包含在基底 R 散發

如本課程中所示，您可以結合開放原始碼和 Microsoft 專有的函式，在相同的指令碼。

## <a name="add-maximum-and-minimum-values"></a>加入最大和最小值

根據計算摘要統計資料，在上一課，您發現您可以插入進一步計算的資料來源的資料的一些實用的資訊。 例如，最小和最大值可以用來計算長條圖。 在此練習中，新增到的最大值高和最低值**RxSqlServerData**資料來源。

1. 一開始先設定一些暫存變數。
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. 使用變數*ccColInfo*您在資料來源中定義的資料行上一課中建立。
  
   新增新的計算資料行 (*numTrans*， *Fraudrisk*，並*creditLine*) 來覆寫原始定義的資料行集合。 下列指令碼將根據最小和最大值，從取得 sumOut，這儲存於記憶體中輸出的因素**rxSummary**。 
  
    ```R 
    ccColInfo <- list(
        gender = list(type = "factor",
          levels = c("1", "2"), 
          newLevels = c("Male", "Female")),
        cardholder = list(type = "factor",
          levels = c("1", "2"), 
          newLevels = c("Principal", "Secondary")), 
        state = list(type = "factor", 
          levels = as.character(1:51), 
          newLevels = stateAbb), 
        balance  = list(type = "numeric"),
        numTrans = list(type = "factor", 
          levels = as.character(sumDF[var == "numTrans", "Min"]:sumDF[var == "numTrans", "Max"])),
        numIntlTrans = list(type = "factor",  
            levels = as.character(sumDF[var == "numIntlTrans", "Min"]:sumDF[var =="numIntlTrans", "Max"])),
        creditLine = list(type = "numeric")
            )
    ```
  
3. 已經更新的資料行集合中，套用下列陳述式，建立更新的版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您稍早定義的資料來源。
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    SqlFraudDS 資料來源現在包括使用 加入新的資料行*ccColInfo*。
  
到目前為止，所做的修改只會影響資料來源物件在 R;沒有新資料就已寫入至資料庫資料表尚未。 不過，您可以使用 sumOut 變數中擷取的資料建立視覺效果和摘要。 

> [!TIP]
> 如果您忘記您使用哪種計算內容，請執行**rxGetComputeContext()**。 傳回值的 「 RxLocalSeq 計算內容 」 表示您在本機計算內容執行。

## <a name="visualize-data-using-rxhistogram"></a>使用 rxHistogram 將資料視覺化

1. 請使用下列 R 程式碼來呼叫 [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) 函數，並傳遞公式和資料來源。 您可以先在本機執行此作業，查看預期的結果及所需時間。
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    就內部而言， **rxHistogram** 會呼叫 [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) 函數，這包含在 **RevoScaleR** 套件中。 **rxCube**輸出包含在公式中，指定每個變數的一個資料行的單一清單 （或資料框架） 再加上一個計數資料行。
    
2. 現在，設定計算內容至遠端 SQL Server 電腦，然後執行**rxHistogram**一次。
  
    ```R
    rxSetComputeContext(sqlCompute)
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
3. 結果會完全相同，因為您使用相同的資料來源，但在第二個步驟中，遠端伺服器上執行計算。 然後，系統會將結果傳回到您的本機工作站以進行繪製。
   
  ![長條圖結果](media/rsql-sue-histogramresults.jpg "長條圖結果")


## <a name="visualize-with-scatter-plots"></a>使用散佈圖將資料視覺化

散佈圖通常期間會使用資料探索來比較兩個變數之間的關聯性。 您可以基於此目的，使用內建的 R 封裝，使用所提供的輸入**RevoScaleR**函式。

1. 呼叫[rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs)函式來計算的平均值*Numtrans*每個組合*numTrans*並*numIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    若要指定用來計算群組平均值的群組，請使用 `F()` 標記法。 在此範例中，`F(numTrans):F(numIntlTrans)`表示變數中的整數`numTrans`和`numIntlTrans`應視為類別目錄的變數，且每個整數值的層級。
  
    預設的傳回值**rxCube**是*rxCube 物件*，其代表交叉資料表。 
  
2. 呼叫[rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf)函式來將結果轉換成資料框架，可輕鬆用於 R 標準繪圖函數之一。
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    **RxCube**函式包含選擇性的引數*returnDataFrame* = **TRUE**，可用來將結果直接轉換成資料框架。 例如：
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    不過的輸出**rxResultsDF**更簡潔，並保留來源資料行的名稱。 您可以執行`head(cube1)`後面接著`head(cubePlot)`輸出相比較。
  
3. 建立使用熱度對應**levelplot**函式**斜格紋**，包含所有 R 散發套件。
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **結果**
  
    ![散佈圖結果](media/rsql-sue-scatterplotresults.jpg "散佈圖結果")
  
從這個快速的分析，您可以看到詐騙的風險增加的交易數目和國際交易數目。

如需詳細資訊**rxCube**函式，並交叉資料表在一般情況下，請參閱[使用 RevoScaleR 的資料摘要](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [建立 R 模型，使用 SQL Server 資料](../../advanced-analytics/tutorials/deepdive-create-models.md)