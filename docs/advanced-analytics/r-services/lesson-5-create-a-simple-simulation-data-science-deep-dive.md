---
title: "第 5 課︰建立簡單的模擬 (資料科學深入探討) | Microsoft Docs"
ms.custom: ""
ms.date: "10/03/2016"
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
ms.assetid: f420b816-ddab-4a1a-89b9-c8285a2d33a3
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# 第 5 課︰建立簡單的模擬 (資料科學深入探討)
到目前為止，您已使用過 SQL Server R 服務所提供的 R 函數，其是專為在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和本機計算內容之間移動資料精心設計。 不過，如果您要撰寫自己的自訂 R 函數，並想在伺服器內容中執行該函數時，該怎麼辦？  
  
您可以使用 *rxExec* 函數，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦內容中呼叫任意函數。 您也可以使用 *rxExec*，明確將工作分散於單一伺服器節點中的各個核心。  
  
在本課程中，您將會使用遠端伺服器來建立簡單的模擬。 模擬並不需要任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料；本範例僅示範如何設計自訂函數，然後使用 *rxExec* 函數加以呼叫。  
  
如需更複雜的 *rxExec* 使用範例，請參閱這篇文章︰[http://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html](http://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)。  
  
## 建立函數  
一般博奕遊戲通常會由擲兩顆骰子構成，規則如下︰  
  
-   如果您在第一把擲出 7 或 11，您就贏了。  
  
-   如果擲出 2、3 或 12，您就輸了。  
  
-   如果擲出 4、5、6、8、9 或 10，該數字會變成您的決勝點，您可以繼續擲到擲出同個決勝點 (若擲出，您就算贏)；如果擲出 7，您就算輸。  
  
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
                { result <- "Loss" }    
                else if (count > 1 && roll == 7 )   
                { result <- "Loss" }    
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
  
## 建立模擬  
若要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦內容中執行任意函數，請呼叫 *rxExec* 函數。 雖然 *rxExec* 也支援以平行、分散方式，跨節點或伺服器內容的核心來執行函數，但此處您只需用它來在伺服器上執行自訂函數。  
  
1.  呼叫自訂函數作為 *rxExec* 的引數，以及具有修改模擬的一些其他參數。  
  
    ```R  
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")   
    length(sqlServerExec)   
    ```  
  
    -   使用 *timesToRun* 引數來指定函數應執行的次數。  在此案例中，您要擲骰子 20 次。  
  
    -   引數 *RNGseed* 和 *RNGkind* 可以用來控制隨機數字的產生。 當 *RNGseed* 設為 [自動] 時，會在每一個背景工作上平行初始化隨機資料流。  
  
2.  *rxExec* 函數會建立一份清單，其中每個回合都有一個項目；不過，在清單未完成時，您都不會察覺到任何影響。 當所有反覆運算次數完成時，開頭為 `length` 的那一行會傳回值。  
  
    您即可移至下一個步驟，以取得輸贏記錄的摘要。  
  
3.  使用 R 的 *unlist* 函數將傳回的清單轉換為向量，再使用 *table* 函數彙總結果。  
  
    ```R  
    table(unlist(sqlServerExec))  
    ```  
  
    結果應該如下所示：  
  
     *輸贏*   
     *12  8*  
  
## 結論  
在本教學課程中，您會非常熟悉下列工作︰  
  
-   取得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料以在分析中使用  
  
-   使用 R 建立與刪除資料來源  
  
-   在您的工作站和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 伺服器之間傳遞模型、資料和圖表  
  
>  [!TIP]
> 
> 如果您想要使用較大的資料集 (1 千萬筆觀察) 來試驗這些技巧，可從 [http://packages.revolutionanalytics.com/datasets](http://packages.revolutionanalytics.com/datasets) 取得資料檔案。  
>   
> 若要使用較大的資料檔案來重複使用這個逐步解說，只需要直接下載資料，然後修改資料來源，如下所示︰   
>  -   設定變數 *ccFraudCsv* 和 *ccScoreCsv* 以指向新的資料檔案     
>  -   將 *sqlFraudTable* 所參考的資料表名稱變更為 *ccFraud10*    
>  -   將 *sqlScoreTable* 所參考的資料表名稱變更為 *ccFraudScore10*   
  
## 上一個步驟  
[在 SQL Server 與 XDF 檔案之間移動資料 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/move-data-between-sql-server-and-xdf-file-data-science-deep-dive.md)  
  
  
  
