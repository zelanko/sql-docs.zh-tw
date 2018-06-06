---
title: 建立簡單的模擬 （SQL 與 R 深入探討） |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7c93d91324233b05541c09e037f5043f2d9e376f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="create-a-simple-simulation-sql-and-r-deep-dive"></a>建立簡單的模擬 （SQL 與 R 深入探討）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是資料科學深入探討教學課程中，有關如何使用最後一個步驟[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

到目前為止您已經使用所設計的 R 函數特別針對移動之間的資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和本機計算內容。 不過，如果您要撰寫自己的自訂 R 函數，並想在伺服器內容中執行該函數時，該怎麼辦？

您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rxExec [函數，在](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) 電腦內容中呼叫任意函數。 您也可以使用**rxExec**來明確地將工作分散到一部伺服器中的核心。

在這一課，您可以使用 遠端伺服器來建立簡單的模擬。 模擬並不需要任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料；本範例僅示範如何設計自訂函數，然後使用 **rxExec** 函數加以呼叫。

如需更複雜的使用範例**rxExec**，請參閱這篇文章： [foreach 與 rxExec 粗略資料粒度平行處理原則](http://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)

## <a name="create-the-custom-function"></a>建立自訂函式

一般博奕遊戲通常會由擲兩顆骰子構成，規則如下︰

- 如果您在第一把擲出 7 或 11，您就贏了。
- 如果擲出 2、3 或 12，您就輸了。
- 如果擲出 4、5、6、8、9 或 10，該數字會變成您的決勝點，您可以繼續擲到擲出同個決勝點 (若擲出，您就算贏)；如果擲出 7，您就算輸。

使用 R 時，您可以建立自訂函數，並接連執行多次，以輕鬆模擬出這樣的遊戲。

1.  使用下列 R 程式碼，以建立自訂函數：
  
    ```R
    rollDice <- function()
    {
        result <- NULL
        point <- NULL
        count <- 1
            while (is.null(result))
            {
                roll <- sum(sample(6, 2, replace=TRUE))
  
                if (is.null(point))
                { point <- roll }
                if (count == 1 && (roll == 7 || roll == 11))
                {  result <- "Win" }
                else if (count == 1 && (roll == 2 || roll == 3 || roll == 12))
                { result \<- "Loss" }
                else if (count > 1 && roll == 7 )
                { result \<- "Loss" }
                else if (count > 1 && point == roll)
                { result <- "Win" }
                else { count <- count + 1 }
            }
            result
    }
    ```
  
2.  若要模擬擲骰單一遊戲，執行此函式。
  
    ```R
    rollDice()
    ```
  
    您贏了還是輸了？
  
現在讓我們來看看您可以使用**rxExec**多次執行函式，以建立模擬，可協助判斷一大勝利的機率。

## <a name="create-the-simulation"></a>建立模擬

若要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦內容中執行任意函數，請呼叫 **rxExec** 函數。 雖然**rxExec**也支援以平行方式的分散式的函式的執行在節點之間或核心伺服器內容，這裡中其 SQL Server 電腦上執行您的自訂函式。

1. 呼叫自訂函式的引數為**rxExec**搭配修改模擬其他參數。
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    - 使用 *timesToRun* 引數來指定函數應執行的次數。  在此案例中，您要擲骰子 20 次。
  
    - 引數 *RNGseed* 和 *RNGkind* 可以用來控制隨機數字的產生。 當 *RNGseed* 設為 [自動] 時，會在每一個背景工作上平行初始化隨機資料流。
  
2. **rxExec** 函數會建立一份清單，其中每個回合都有一個項目；不過，在清單未完成時，您都不會察覺到任何影響。 當所有反覆運算次數完成時，開頭為 `length` 的那一行會傳回值。
  
    您即可移至下一個步驟，以取得輸贏記錄的摘要。
  
3. 使用 R 的 `unlist` 函數將傳回的清單轉換為向量，再使用 `table` 電腦內容中呼叫任意函數。
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    結果應該如下所示：
  
     *遺失 Win* *12 8*

## <a name="conclusions"></a>結論

在本教學課程中，您會非常熟悉下列工作︰
  
-   取得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料以在分析中使用
  
-   使用 R 建立與刪除資料來源
  
-   在您的工作站和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 伺服器之間傳遞模型、資料和圖表
  

如果您想要試驗這些技巧，以使用較大的資料集的 10 百萬個觀察值，資料檔案可從 Revolution analytics 網站：[索引的資料集](http://packages.revolutionanalytics.com/datasets)

若要重新使用本逐步解說的較大的資料檔案，下載的資料，，然後修改每一個資料來源，如下所示：

1. 修改變數`ccFraudCsv`和`ccScoreCsv`以指向新的資料檔
2. 變更所參考的資料表名稱*sqlFraudTable*至 `ccFraud10`
3. 變更所參考的資料表名稱*sqlScoreTable*至 `ccFraudScore10`

## <a name="additional-samples"></a>其他範例

既然您已經精通使用的計算內容和 RevoScaler 函數來傳遞，並轉換資料，請參閱這些教學課程：

[機器學習服務的 R 教學課程](machine-learning-services-tutorials.md)
## <a name="previous-step"></a>上一個步驟

[在 SQL Server 與 XDF 檔案之間移動資料](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
