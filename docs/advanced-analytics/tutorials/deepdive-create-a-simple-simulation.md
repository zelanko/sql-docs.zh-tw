---
title: "第 5 課︰建立簡單的模擬 (資料科學深入探討) | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: f420b816-ddab-4a1a-89b9-c8285a2d33a3
caps.latest.revision: 16
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e5bbd69bba01da2aacd3b8912aebac6b4e1c28a1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-simple-simulation"></a>建立簡單的模擬

到目前為止您已經使用所設計的 R 函數特別針對移動之間的資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和本機計算內容。 不過，如果您要撰寫自己的自訂 R 函數，並想在伺服器內容中執行該函數時，該怎麼辦？

您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rxExec **函數，在** 電腦內容中呼叫任意函數。 您也可以使用 rxExec 明確地將工作分散到單一伺服器節點中的核心。

在本課程中，您將會使用遠端伺服器來建立簡單的模擬。 模擬不需要任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料，此範例僅示範如何設計自訂函式，然後呼叫使用 rxExec 函式。

使用 rxExec 的更複雜的範例，請參閱這篇文章： [foreach 與 rxExec 粗略資料粒度平行處理原則](http://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)

## <a name="create-the-function"></a>建立函數

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
  
2.  若要模擬一個單一骰子遊戲，請執行此函數。
  
    ```R
    rollDice()
    ```
  
    您贏了還是輸了？
  
現在讓我們來看看如何多次執行函數，以建立模擬並協助判斷獲勝的機率。

## <a name="create-the-simulation"></a>建立模擬

若要執行的內容中的任意函式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]電腦，您呼叫 rxExec 函式。 雖然 rxExec 也會支援以平行方式分散式的函式的執行在節點或核心伺服器內容中的，在此您將使用它只是為了在伺服器上執行您的自訂函式。

1. 呼叫自訂函式當做 rxExec，以及修改模擬一些其他參數的引數。
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    - 使用 *timesToRun* 引數來指定函數應執行的次數。  在此案例中，您要擲骰子 20 次。
  
    - 引數 *RNGseed* 和 *RNGkind* 可以用來控制隨機數字的產生。 當 *RNGseed* 設為 [自動] 時，會在每一個背景工作上平行初始化隨機資料流。
  
2. RxExec 函式會建立清單含有一個項目，每次執行;不過，您將不會看到多發生，直到此清單完成時。 當所有反覆運算次數完成時，開頭為 `length` 的那一行會傳回值。
  
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
  
>  [!TIP]
> 
> 如果您想要試驗這些技巧，以使用較大的資料集的 10 百萬個觀察值，資料檔案可從 Revolution analytics 網站：[索引的資料集](http://packages.revolutionanalytics.com/datasets)
>   
> 若要重新使用本逐步解說的較大的資料檔案，下載的資料，，然後修改每一個資料來源，如下所示：
>  - 設定變數 *ccFraudCsv* 和 *ccScoreCsv* 以指向新的資料檔案
>  - 將 *sqlFraudTable* 所參考的資料表名稱變更為 *ccFraud10*
>  - 將 *sqlScoreTable* 所參考的資料表名稱變更為 *ccFraudScore10*

## <a name="previous-step"></a>上一個步驟

[SQL Server 和 XDF 檔案之間移動資料](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)



