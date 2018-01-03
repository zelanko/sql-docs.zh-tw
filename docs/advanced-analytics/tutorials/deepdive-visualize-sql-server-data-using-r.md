---
title: " 使用 R （SQL 與 R 深入探討） 的 SQL Server 資料視覺化 |Microsoft 文件"
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: 10def0b3-9b09-4df9-b8aa-69516f7d7659
caps.latest.revision: "14"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 77321589a87230535502cc37a75bf09722abb66d
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2017
---
#  <a name="visualize-sql-server-data-using-r-sql-and-r-deep-dive"></a>使用 R （SQL 與 R 深入探討） 的 SQL Server 資料視覺化

本文是資料科學深入探討教學課程中，有關如何使用一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中的增強套件包含的多個函數，已針對延展性和平行處理功能進行最佳化。 這些函數通常都使用 **rx** 或 **Rx**做為字首。

對於此逐步解說中，您使用**rxHistogram**函式檢視中的值分佈_creditLine_依性別資料行。

## <a name="visualize-data-using-rxhistogram"></a>使用 rxHistogram 資料視覺化

1. 請使用下列 R 程式碼來呼叫 [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) 函數，並傳遞公式和資料來源。 您可以先在本機執行此作業，查看預期的結果及所需時間。
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    就內部而言， **rxHistogram** 會呼叫 [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) 函數，這包含在 **RevoScaleR** 套件中。 **rxCube**輸出包含一個資料行在公式中，指定每個變數的單一清單 （或資料框架） 再加上計算資料行。
    
2. 現在，設定計算內容至遠端 SQL Server 電腦，並執行**rxHistogram**一次。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
 
3. 結果會完全相同，因為您使用相同的資料來源；不過，計算是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦上執行。  然後，系統會將結果傳回到您的本機工作站以進行繪製。
   
![長條圖結果](media/rsql-sue-histogramresults.jpg "長條圖結果")

4. 您也可以呼叫**rxCube**函式，並將結果傳遞給 R 繪圖函式。  例如，下列範例使用 **rxCube** 來計算 *numTrans* 和 *numIntlTrans* 每個組合的 *fraudRisk*平均值：
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    若要指定用來計算群組平均值的群組，請使用 `F()` 標記法。 在此範例中，`F(numTrans):F(numIntlTrans)`表示變數中的整數`_numTrans`和`numIntlTrans`應視為類別變數，層級的每個整數值。
  
    因為資料來源已加入的低和高的層級`sqlFraudDS`(使用`colInfo`參數)，長條圖中就會自動使用層級。
  
5. 預設的傳回值**rxCube**是*rxCube 物件*，用來表示交叉資料表。 不過，您可以使用 [rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) 函數，將結果轉換成資料框架，以輕鬆用於 R 標準繪圖函數中。
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    **RxCube**函式包含選擇性引數， *returnDataFrame* = **TRUE**以外，您可以使用來將結果直接轉換至資料框架。 例如：
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    不過， **rxResultsDF** 的輸出比較簡潔，並保留來源資料行的名稱。
  
6. 最後，執行下列程式碼來建立使用熱門地圖`levelplot`函數從**斜格紋**隨附於所有的 R 散發的封裝。
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **結果**
  
    ![散佈圖結果](media/rsql-sue-scatterplotresults.jpg "散佈圖結果")
  
即使只是透過這個快速的分析，您都可以看出詐騙的風險會隨著交易數目和國際交易數目增加而提高。

如需有關**rxCube**函式和交叉資料表一般情況下，請參閱[資料摘要使用 RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)。

## <a name="next-step"></a>下一步

[建立 R 模型，使用 SQL Server 資料](../../advanced-analytics/tutorials/deepdive-create-models.md)

## <a name="previous-step"></a>上一個步驟

[建立及執行 R 指令碼](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
