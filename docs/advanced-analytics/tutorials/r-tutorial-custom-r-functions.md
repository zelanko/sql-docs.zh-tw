---
title: 使用 RevoScaleR rxExec-SQL Server Machine Learning 的 SQL Server 上執行自訂的 R 函式
description: 教學課程逐步解說如何使用 RevoScaleR 函式的 SQL Server 上執行自訂的 R 指令碼。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 5773641f442fe844657e6aabd6b9dcea24f4475b
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58509905"
---
# <a name="run-custom-r-functions-on-sql-server-using-rxexec"></a>使用 rxExec 的 SQL Server 上執行自訂的 R 函式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

您也可以傳遞您的函式，透過 SQL Server 的內容中執行自訂的 R 函數[rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec)，假設您的指令碼需要的任何程式庫也會安裝在伺服器上，而且這些程式庫相容基底R 的散發 

**RxExec**函式中**RevoScaleR**提供一個機制來執行您所需要的任何 R 指令碼。 此外， **rxExec**能夠明確地將工作分散到在單一伺服器中，加入為有限的原生的 R 引擎資源條件約束的指令碼的小數位數的多個核心。

在本教學課程中，您將使用模擬的資料來示範的遠端伺服器執行的自訂 R 函式執行。

## <a name="prerequisites"></a>先決條件

+ [（使用 R) SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)或[SQL Server 2016 R Services （資料庫）](../install/sql-r-services-windows-install.md)
  
+ [資料庫權限](../security/user-permission.md)和 SQL Server 資料庫使用者登入

+ [在開發工作站使用 RevoScaleR 程式庫](../r/set-up-a-data-science-client.md)

R 散發，用戶端工作站上的提供內建**Rgui**工具可供您在本教學課程中執行 R 指令碼。 您也可以使用 IDE，例如 RStudio 或 R Tools for Visual Studio。

## <a name="create-the-remote-compute-context"></a>建立遠端計算內容

用戶端工作站上執行下列 R 命令。 例如，您會使用**Rgui**，從這個位置啟動它：C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64\.

1. 指定執行計算的 SQL Server 執行個體的連接字串。 伺服器必須設定的 R 整合。 在此練習中，未使用的資料庫名稱，但連接字串需要其中一個。 如果您有測試或範例資料庫，您可以使用的。

    **使用 SQL 登入**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>; Database=<database-name>;Uid=<SQL-user-name>;Pwd=<password>"
    ```

    **使用 Windows 驗證**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>;Database=<database-name>;Trusted_Connection=True"
    ```

2. 建立遠端計算內容中的連接字串所參考的 SQL Server 執行個體。

    ```R
    sqlCompute <- RxInSqlServer(connectionString = sqlConnString)
    ```

3. 啟用計算內容，然後傳回 物件定義，並確認步驟。 您應該會看到計算內容物件的屬性。

    ```R
    rxSetComputeContext(sqlCompute)
    rxGetComputeContext()
    ```

## <a name="create-the-custom-function"></a>建立自訂函式

在此練習中，您將建立自訂的 R 函數，以模擬一般博奕，輪流骰子所組成。 遊戲規則會決定 win 或遺失的結果：

+ 在回復 7 或 11，您就贏了。
+ 向前復原 2、 3 或 12，您會遺失。
+ 4、 5、 6、 8、 9，或 10，則該數字會變成您的點，而且您可以繼續擲到決勝點 （在此情況下您就算贏） 或向前復原為 7，在其中情況下，您會遺失。

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
  
2.  單一骰子遊戲藉由模擬執行函式。
  
    ```R
    rollDice()
    ```
  
    您贏了還是輸了？
  
既然您已操作的指令碼，我們來看看如何使用**rxExec**執行函式多次，以便建立模擬並協助判斷獲勝的機率。

## <a name="pass-rolldice-in-rxexec"></a>RollDice() 傳入 rxExec

若要在遠端 SQL 伺服器的內容中執行任意的函式，呼叫**rxExec**函式。

1. 呼叫自訂函數的引數作為**rxExec**，以及修改模擬其他參數。
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    + 使用 *timesToRun* 引數來指定函數應執行的次數。  在此案例中，您要擲骰子 20 次。
  
    + 引數 *RNGseed* 和 *RNGkind* 可以用來控制隨機數字的產生。 當 *RNGseed* 設為 [自動] 時，會在每一個背景工作上平行初始化隨機資料流。
  
2. **rxExec** 函數會建立一份清單，其中每個回合都有一個項目；不過，在清單未完成時，您都不會察覺到任何影響。 當所有反覆項目都完成時，該行的開頭**長度**會傳回值。
  
    您即可移至下一個步驟，以取得輸贏記錄的摘要。
  
3. 使用 R 的 **unlist** 函數將傳回的清單轉換為向量，再使用 **table** 函數彙總結果。
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    結果應該如下所示：
  
     *輸贏* *12 8*

## <a name="conclusion"></a>結論

雖然此練習是簡單的它會示範適用於整合 SQL Server 上執行的 R 指令碼中的任意 R 函數的重要機制。 若要彙整重點，讓這項技術：

+ 必須設定 SQL Server machine learning 及 R 整合：[SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)與 [R] 功能中，或是[SQL Server 2016 R Services （資料庫）](../install/sql-r-services-windows-install.md)。

+ SQL Server 上必須安裝您的函式，包括任何相依性，所使用的開放原始碼或協力廠商程式庫。 如需詳細資訊，請參閱 <<c0> [ 安裝新的 R 套件](../r/install-additional-r-packages-on-sql-server.md)。

+ 將指令碼從開發環境移至強化後的生產環境，可以導入防火牆和網路限制。 請仔細測試，以確保您的指令碼可如預期般執行。

## <a name="next-steps"></a>後續步驟

如需更複雜的使用範例**rxExec**，請參閱這篇文章：[Foreach 與 rxExec 粗略資料粒度平行處理原則](https://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)
