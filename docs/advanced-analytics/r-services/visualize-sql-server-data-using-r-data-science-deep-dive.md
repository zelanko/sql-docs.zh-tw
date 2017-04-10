---
title: "使用 R 將 SQL Server 資料視覺化 (資料科學深入探討) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 10def0b3-9b09-4df9-b8aa-69516f7d7659
caps.latest.revision: 14
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# 使用 R 將 SQL Server 資料視覺化 (資料科學深入探討)
[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中的增強套件包含的多個函數，已針對延展性和平行處理功能進行最佳化。 這些函數通常都使用 *rx* 或 *Rx* 做為字首。  
  
在此逐步解說中，您將使用 *rxHistogram* 函數，依性別檢視 _creditLine_ 資料行中的值分佈。  
  
## 使用 rxHistogram 和 rxCube 將資料視覺化  
  
1.  請使用下列 R 程式碼來呼叫 *rxHistogram* 函數，並傳遞公式和資料來源。 您可以先在本機執行此作業，查看預期的結果及所需時間。
  
    ```R  
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")   
    ```  
 
    就內部而言，*rxHistogram* 會呼叫 *rxCube* 函數，這包含在 **RevoScaleR** 套件中。 *rxCube* 函數會輸出一份清單 (或資料框架)，其中，公式所指定的每個變數具有一個資料行與一個計數資料行。
    
2. 現在，將計算內容設定為遠端 SQL Server 電腦，並重新執行 *rxHistogram*。
  
    ```R  
    rxSetComputeContext(sqlCompute)  
    ```  
 
3.    結果會完全相同，因為您使用相同的資料來源；不過，計算是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦上執行。  然後，系統會將結果傳回到您的本機工作站以進行繪製。  
   
![histogram results](../../advanced-analytics/r-services/media/rsql-sue-histogramresults.jpg "histogram results")  

  
4.  您也可以呼叫 *rxCube* 函數，並將結果傳遞至 R 繪製函數。  例如，下列範例使用 *rxCube* 來計算 *numTrans* 和 *numIntlTrans* 每個組合的 *fraudRisk* 平均值：  
  
    ```R  
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)   
    ```  
  
    若要指定用來計算群組平均值的群組，請使用 `F()` 標記法。 在此範例中，`F(numTrans):F(numIntlTrans)` 指出應將 _numTrans_ 和 _numIntlTrans_ 變數中的整數視為類別目錄變數，且每個整數值代表一個層級。  
  
    由於資料來源 *sqlFraudDS* 已經新增低層級和高層級 (使用 *colInfo* 參數)，因此長條圖中會自動使用這些層級。  
  
5.  *rxCube* 的傳回值預設為 *rxCube object* 物件，其代表交叉資料表。 不過，您可以使用 *rxResultsDF* 函數，將結果轉換成資料框架，以輕鬆用於 R 標準繪圖函數中。  
  
    ```R  
    cubePlot <- rxResultsDF(cube1)   
    ```  
  
    > [!TIP]  
    > 請注意，*rxCube* 函數包含 *returnDataFrame* = TRUE 選用引數，您可以用來將結果直接轉換成資料框架。 例如：  
    >   
    > `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`  
    >   
    > 不過，*rxResultsDF* 的輸出比較簡潔，並保留來源資料行的名稱。  
  
6.  最後，執行下列程式碼，使用 *levelplot* 函數 (來自所有 R 散發套件所包含的 **lattice** 套件) 來建立熱度圖。  
  
    ```R  
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)   
    ```  
  
    **結果**  
  
    ![scatterplot results](../../advanced-analytics/r-services/media/rsql-sue-scatterplotresults.jpg "scatterplot results")  
  
即使只是透過這個快速的分析，您都可以看出詐騙的風險會隨著交易數目和國際交易數目增加而提高。

如需 *rxCube* 函數和交叉資料表的一般詳細資訊，請參閱 [Data Summaries](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-summaries) (資料摘要)。  
  
## 下一個步驟  
[建立模型 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/create-models-data-science-deep-dive.md)  
  
## 上一個步驟  
[第 2 課︰建立及執行 R 指令碼 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/lesson-2-create-and-run-r-scripts-data-science-deep-dive.md)  
  
## 另請參閱  
[資料科學深入探討︰使用 RevoScaleR 套件](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
