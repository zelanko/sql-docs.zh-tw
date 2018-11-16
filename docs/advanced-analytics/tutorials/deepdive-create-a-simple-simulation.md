---
title: 建立簡單的模擬 （SQL 和 R 深入探討） |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b0db5fdfd177f1303432659f7a96b0fbf111c000
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51698236"
---
# <a name="create-a-simple-simulation-sql-and-r-deep-dive"></a>建立簡單的模擬 （SQL 和 R 深入探討）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章是最後一個步驟中的資料科學深入探討教學課程中，有關如何使用[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

到目前為止您已使用 R 函數，設計專為之間移動資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和本機計算內容。 不過，如果您要撰寫自己的自訂 R 函數，並想在伺服器內容中執行該函數時，該怎麼辦？

您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rxExec [函數，在](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) 電腦內容中呼叫任意函數。 您也可以使用**rxExec**明確地將工作分散在單一伺服器的核心。

在這一課，您可以使用 遠端伺服器來建立簡單的模擬。 模擬並不需要任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料；本範例僅示範如何設計自訂函數，然後使用 **rxExec** 函數加以呼叫。

如需更複雜的使用範例**rxExec**，請參閱這篇文章： [foreach 與 rxExec 粗略資料粒度平行處理原則](https://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)

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
  
2.  若要模擬單一骰子遊戲，執行函式。
  
    ```R
    rollDice()
    ```
  
    您贏了還是輸了？
  
現在讓我們來看看如何使用**rxExec**多次執行此函式，以建立模擬並協助判斷獲勝的機率。

## <a name="create-the-simulation"></a>建立模擬

若要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦內容中執行任意函數，請呼叫 **rxExec** 函數。 雖然**rxExec**也支援函式的分散式的執行以平行方式，跨節點或核心伺服器內容，這裡就 SQL Server 電腦上執行您的自訂函式。

1. 呼叫自訂函數的引數作為**rxExec**，以及修改模擬其他參數。
  
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
  
     *輸贏* *12 8*

## <a name="conclusions"></a>結論

在本教學課程中，您會非常熟悉下列工作︰
  
-   取得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料以在分析中使用
  
-   使用 R 建立與刪除資料來源
  
-   在您的工作站和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 伺服器之間傳遞模型、資料和圖表
  

如果您想要試驗這些技巧，以使用較大的資料集的 10 萬筆觀察，資料檔案都是從 Revolution analytics 網站：[索引的資料集](https://packages.revolutionanalytics.com/datasets)

若要重複使用此逐步解說使用較大的資料檔案，下載資料，然後修改每一個資料來源，如下所示：

1. 修改變數`ccFraudCsv`和`ccScoreCsv`以指向新的資料檔案
2. 變更參考的資料表名稱*sqlFraudTable*至 `ccFraud10`
3. 變更參考的資料表名稱*sqlScoreTable*至 `ccFraudScore10`

## <a name="additional-samples"></a>其他範例

現在您已經熟悉如何使用計算內容和 RevoScaler 函式來傳遞和轉換資料，請繼續了解這些教學課程：

[Machine Learning 服務的 R 教學課程](machine-learning-services-tutorials.md)
## <a name="previous-step"></a>上一個步驟

[在 SQL Server 與 XDF 檔案之間移動資料](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
