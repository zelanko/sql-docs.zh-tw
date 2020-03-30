---
title: 使用 RevoScaleR 將資料視覺化
description: RevoScaleR 教學課程 6：如何在 SQL Server 上使用 R 語言視覺化資料。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 887c5790a7de70cf111f004be65e3a41748b47bf
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "74947358"
---
#  <a name="visualize-sql-server-data-using-r-sql-server-and-revoscaler-tutorial"></a>使用 R 將 SQL Server 資料視覺化 (SQL Server 和 RevoScaleR 教學課程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

此教學課程是 [RevoScaleR 教學課程系列](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)的第 6 個，該系列說明如何搭配 SQL Server 使用 [RevoScaleR 函式](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) \(英文\)。

在此教學課程中，您將會使用 R 函式，依性別檢視 *creditLine* 資料行中的值分佈。

> [!div class="checklist"]
> * 為長條圖輸入建立 min-max 變數
> * 從 **RevoScaleR** 使用 **rxHistogram** 將長條圖中的資料視覺化
> * 使用基礎 R 發佈中包含之 **lattice** 的 **levelplot**，將散佈圖視覺化

如此教學課程所示範，您可以在相同的指令碼中結合開放原始碼與 Microsoft 特定的函式。

## <a name="add-maximum-and-minimum-values"></a>新增最大值和最小值

根據上一個教學課程計算的摘要統計資料，您發現與資料相關的一些實用資訊，可以將其插入資料來源，以供進一步計算使用。 例如，最小值和最大值可用於計算長條圖。 在此練習中，將最高值和最低值新增至 **RxSqlServerData** 資料來源。

1. 一開始先設定一些暫存變數。
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. 使用您在上一個教學課程中建立的變數 *ccColInfo*，定義資料來源中的資料行。
  
   將新的計算資料行 (*numTrans*、*numIntlTrans* 和 *creditLine*) 新增至置換原始定義的資料行集合。 以下指令碼根據從 sumOut (儲存 **rxSummary** 的記憶體內部輸出) 獲得的最小值和最大值，來新增係數。 
  
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
  
3. 更新資料行集合之後，套用下列陳述式，為您稍早定義的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源建立更新版本。
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    sqlFraudDS 資料來源現在包含使用 *ccColInfo* 新增的新資料行。
  
此時，這些修改只會影響 R 中的資料來源物件，尚未將任何新資料寫入資料庫資料表。 不過，您可以使用 sumOut 變數中所擷取的資料，以建立視覺效果和摘要。 

> [!TIP]
> 如果您忘了正在使用哪個計算內容，請執行 **rxGetComputeContext()** 。 「RxLocalSeq Compute Context」的傳回值表示您在正在本機計算內容中執行。

## <a name="visualize-data-using-rxhistogram"></a>使用 rxHistogram 將資料視覺化

1. 請使用下列 R 程式碼來呼叫 [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) 函數，並傳遞公式和資料來源。 您可以先在本機執行此作業，查看預期的結果及所需時間。
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    就內部而言， **rxHistogram** 會呼叫 [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) 函數，這包含在 **RevoScaleR** 套件中。 **rxCube** 會輸出一份清單 (或資料框架)，其中，公式所指定的每個變數具有一個資料行與一個計數資料行。
    
2. 現在，將計算內容設定為遠端 SQL Server 電腦，並重新執行 **rxHistogram**。
  
    ```R
    rxSetComputeContext(sqlCompute)
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
3. 結果會完全相同，因為您使用相同的資料來源，但是，在第二個步驟中，計算是在遠端伺服器上執行。 然後，系統會將結果傳回到您的本機工作站以進行繪製。
   
  ![長條圖結果](media/rsql-sue-histogramresults.jpg "長條圖結果")


## <a name="visualize-with-scatter-plots"></a>使用散佈圖進行視覺化

散佈圖通常會在資料探索期間用來比較兩個變數之間的關聯性。 您可以針對此用途使用內建的 R 套件，包含 **RevoScaleR** 函數提供的輸入。

1. 呼叫 [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) 函數來計算 *numTrans* 和 *numIntlTrans* 每個組合的 *fraudRisk* 平均值：
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    若要指定用來計算群組平均值的群組，請使用 `F()` 標記法。 在此範例中，`F(numTrans):F(numIntlTrans)` 表示應將 `numTrans` 和 `numIntlTrans` 變數中的整數視為類別目錄變數，而且每個整數值代表一個層級。
  
    **rxCube** 的預設傳回值為 *rxCube object*，其代表交叉資料表。 
  
2. 呼叫 [rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) 函數，將結果轉換成資料框架，以輕鬆用於 R 標準繪圖函數中。
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    **rxCube** 函數包含 *returnDataFrame* = **TRUE** 選用引數，您可以用來將結果直接轉換成資料框架。 例如：
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    不過，**rxResultsDF** 的輸出比較簡潔，並保留來源資料行的名稱。 您可以先執行 `head(cube1)`，然後執行 `head(cubePlot)`，以比較輸出。
  
3. 使用 **levelplot** 函數 (來自所有 R 發佈所包含的 **lattice** 套件) 來建立熱度圖。
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **結果**
  
    ![散佈圖結果](media/rsql-sue-scatterplotresults.jpg "散佈圖結果")
  
透過這個快速分析，您可以看出詐騙的風險會隨著交易數目和國際交易數目增加而提高。

如需一般 **rxCube** 函數和交叉資料表的更多詳細資訊，請參閱[使用 RevoScaleR 的資料摘要](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 SQL Server 資料建立 R 模型](../../advanced-analytics/tutorials/deepdive-create-models.md)