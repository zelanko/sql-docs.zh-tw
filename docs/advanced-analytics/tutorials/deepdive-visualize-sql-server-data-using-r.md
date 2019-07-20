---
title: 使用 RevoScaleR rxHistogram 將 SQL Server 資料視覺化
description: 有關如何在 SQL Server 上使用 R 語言將資料視覺化的教學課程逐步解說。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 210fade2820c53ba585043827e7e3d2c36315319
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344649"
---
#  <a name="visualize-sql-server-data-using-r-sql-server-and-revoscaler-tutorial"></a>使用 R 將 SQL Server 資料視覺化 (SQL Server 和 RevoScaleR 教學課程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這一課是[RevoScaleR 教學](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)課程的一部分, 說明如何搭配 SQL Server 使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)。

在這一課, 您可以使用 R 函數來依性別來查看*creditLine*資料行中的值分佈。

> [!div class="checklist"]
> * 建立長條圖輸入的最小值變數
> * 使用**RevoScaleR**中的**rxHistogram**將長條圖中的資料視覺化
> * 使用基底 R 散發內含的**lattice**中的**levelplot**從散佈圖視覺化

如本課程所示, 您可以在相同的腳本中結合開放原始碼和 Microsoft 特有的函數。

## <a name="add-maximum-and-minimum-values"></a>新增最大和最小值

根據上一課的計算摘要統計資料, 您已探索到可插入資料來源以進行進一步計算的一些實用資訊。 例如, 您可以使用最小值和最大值來計算長條圖。 在此練習中, 將最高和最低值加入**RxSqlServerData**資料來源。

1. 一開始先設定一些暫存變數。
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. 使用您在上一課中建立的變數*ccColInfo*來定義資料來源中的資料行。
  
   將新的計算資料行 (*numTrans*、 *numIntlTrans*和*creditLine*) 加入至覆寫原始定義的資料行集合。 下列腳本會根據最小和最大值 (從 sumOut 取得, 這是從**rxSummary**儲存記憶體內部輸出) 來新增因素。 
  
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
  
3. 更新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料行集合之後, 請套用下列語句, 以建立您稍早定義的更新版本的資料來源。
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    SqlFraudDS 資料來源現在包含使用*ccColInfo*新增的新資料行。
  
此時, 修改只會影響 R 中的資料來源物件。尚未將任何新資料寫入資料庫資料表。 不過, 您可以使用 sumOut 變數中所捕獲的資料來建立視覺效果和摘要。 

> [!TIP]
> 如果您忘記您所使用的計算內容, 請執行**rxGetComputeCoNtext ()** 。 「RxLocalSeq 計算內容」的傳回值表示您正在本機計算內容中執行。

## <a name="visualize-data-using-rxhistogram"></a>使用 rxHistogram 將資料視覺化

1. 請使用下列 R 程式碼來呼叫 [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) 函數，並傳遞公式和資料來源。 您可以先在本機執行此作業，查看預期的結果及所需時間。
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    就內部而言， **rxHistogram** 會呼叫 [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) 函數，這包含在 **RevoScaleR** 套件中。 **rxCube**會輸出單一清單 (或資料框架), 其中包含公式中指定的每個變數的一個資料行, 加上 [計數] 資料行。
    
2. 現在, 將計算內容設定為遠端 SQL Server 電腦, 然後再次執行**rxHistogram** 。
  
    ```R
    rxSetComputeContext(sqlCompute)
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
3. 結果會完全相同, 因為您使用的是相同的資料來源, 但在第二個步驟中, 計算是在遠端伺服器上執行。 然後，系統會將結果傳回到您的本機工作站以進行繪製。
   
  ![長條圖結果](media/rsql-sue-histogramresults.jpg "長條圖結果")


## <a name="visualize-with-scatter-plots"></a>使用散佈圖進行視覺化

散佈圖通常會在資料流覽期間用來比較兩個變數之間的關聯性。 針對此用途, 您可以使用內建的 R 套件, 並搭配**RevoScaleR**函式所提供的輸入。

1. 呼叫[rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs)函式來計算每個*numTrans*和*numIntlTrans*組合的*fraudrisk 平均值*平均數:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    若要指定用來計算群組平均值的群組，請使用 `F()` 標記法。 在此範例中`F(numTrans):F(numIntlTrans)` , 表示變數`numTrans`和`numIntlTrans`中的整數應該視為類別變數, 每個整數值都有一個層級。
  
    **RxCube**的預設傳回值是*rxCube 物件*, 代表交叉表。 
  
2. 呼叫[rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf)函式, 將結果轉換成資料框架, 輕鬆地在其中一個 R 標準繪製函式中使用。
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    **RxCube**函式包含選擇性引數*returnDataFrame*  =  **TRUE**, 可讓您將結果直接轉換為數據框架。 例如:
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    不過, **rxResultsDF**的輸出會清除, 並保留來源資料行的名稱。 您可以執行`head(cube1)` , `head(cubePlot)`後面接著來比較輸出。
  
3. 使用**lattice**套件中的**levelplot**函式 (隨附于所有 R 發行版本) 來建立熱度圖。
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **結果**
  
    ![散佈圖結果](media/rsql-sue-scatterplotresults.jpg "散佈圖結果")
  
從這個快速分析中, 您可以看到詐騙的風險會隨著交易數目和國際交易數目而增加。

如需**rxCube**函數和交叉資料表的一般詳細資訊, 請參閱[使用 RevoScaleR 的資料摘要](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 SQL Server 資料建立 R 模型](../../advanced-analytics/tutorials/deepdive-create-models.md)