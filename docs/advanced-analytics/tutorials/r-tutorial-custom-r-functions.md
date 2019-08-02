---
title: 使用 RevoScaleR rxExec 在 SQL Server 上執行自訂 R 函數
description: 有關如何使用 RevoScaleR 函數在 SQL Server 上執行自訂 R 腳本的教學課程逐步解說。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 439b21bce4e081025db1db53ab44498415ca44af
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715409"
---
# <a name="run-custom-r-functions-on-sql-server-using-rxexec"></a>使用 rxExec 在 SQL Server 上執行自訂 R 函數
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

您可以透過[rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec)傳遞函式, 在 SQL Server 的內容中執行自訂 R 函式, 假設您的腳本所需的任何程式庫也安裝在伺服器上, 而且這些程式庫與 R 的基底散發相容。 

**RevoScaleR**中的**rxExec**函式提供了一種機制, 可讓您執行任何所需的 R 腳本。 此外, **rxExec**可以在單一伺服器中明確地將工作分散到多個核心, 並將擴充功能新增至僅限於原生 R 引擎的資源限制式的腳本。

在本教學課程中, 您將使用模擬資料來示範如何執行在遠端伺服器上執行的自訂 R 函數。

## <a name="prerequisites"></a>先決條件

+ [SQL Server Machine Learning 服務 (使用 R)](../install/sql-machine-learning-services-windows-install.md)或[SQL Server 2016 R Services (資料庫內)](../install/sql-r-services-windows-install.md)
  
+ [資料庫許可權](../security/user-permission.md)和 SQL Server 資料庫使用者登入

+ [具有 RevoScaleR 程式庫的開發工作站](../r/set-up-a-data-science-client.md)

用戶端工作站上的 R 散發會提供內建的**rgui.exe**工具, 可讓您在本教學課程中用來執行 R 腳本。 您也可以使用 IDE, 例如 RStudio 或 Visual Studio R 工具。

## <a name="create-the-remote-compute-context"></a>建立遠端計算內容

在用戶端工作站上執行下列 R 命令。 例如, 您使用的是**rgui.exe**, 請從這個位置啟動它:C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64\.

1. 針對執行計算的 SQL Server 實例指定連接字串。 伺服器必須針對 R 整合進行設定。 此練習中不會使用資料庫名稱, 但是連接字串需要一個。 如果您有測試或範例資料庫, 您可以使用它。

    **使用 SQL 登入**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>; Database=<database-name>;Uid=<SQL-user-name>;Pwd=<password>"
    ```

    **使用 Windows 驗證**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>;Database=<database-name>;Trusted_Connection=True"
    ```

2. 建立遠端計算內容至連接字串中所參考的 SQL Server 實例。

    ```R
    sqlCompute <- RxInSqlServer(connectionString = sqlConnString)
    ```

3. 啟動計算內容, 然後傳回物件定義做為確認步驟。 您應該會看到 compute 內容物件的屬性。

    ```R
    rxSetComputeContext(sqlCompute)
    rxGetComputeContext()
    ```

## <a name="create-the-custom-function"></a>建立自訂函數

在此練習中, 您將建立自訂的 R 函式, 以模擬由輪流一對骰子組成的一般賭場。 遊戲的規則決定了勝利或遺失的結果:

+ 在最初的變換中, 將7或11變換為獲勝。
+ 第2、3或12卷會遺失。
+ 變換4、5、6、8、9或 10, 該數位就會變成您的點數, 而您會繼續進行迴圈, 直到您再次變換時間點 (在這種情況下獲勝) 或變換 7, 在這種情況下您會遺失。

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
  
2.  藉由執行函式來模擬單骰子的遊戲。
  
    ```R
    rollDice()
    ```
  
    您贏了還是輸了？
  
現在您已有操作腳本, 讓我們來瞭解如何使用**rxExec**多次執行函式, 以建立可協助判斷贏得機率的模擬。

## <a name="pass-rolldice-in-rxexec"></a>在 rxExec 中傳遞 rollDice ()

若要在遠端 SQL Server 的內容中執行任意函數, 請呼叫**rxExec**函數。

1. 呼叫自訂函式做為**rxExec**的引數, 以及用來修改模擬的其他參數。
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    + 使用 *timesToRun* 引數來指定函數應執行的次數。  在此案例中，您要擲骰子 20 次。
  
    + 引數 *RNGseed* 和 *RNGkind* 可以用來控制隨機數字的產生。 當 *RNGseed* 設為 [自動] 時，會在每一個背景工作上平行初始化隨機資料流。
  
2. **rxExec** 函數會建立一份清單，其中每個回合都有一個項目；不過，在清單未完成時，您都不會察覺到任何影響。 當所有的反復專案都完成時, 以**length**開頭的行將會傳回值。
  
    您即可移至下一個步驟，以取得輸贏記錄的摘要。
  
3. 使用 R 的 **unlist** 函數將傳回的清單轉換為向量，再使用 **table** 函數彙總結果。
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    結果應該如下所示：
  
     *勝利遺失* *12 8*

## <a name="conclusion"></a>結論

雖然此練習很簡單, 但它會示範在 SQL Server 上執行的 R 腳本中整合任意 R 函數的重要機制。 若要總結讓這項技術可行的重點:

+ 必須設定機器學習和 R 整合的 SQL Server:使用 R 功能[SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md), 或[SQL Server 2016 R Services (資料庫內)](../install/sql-r-services-windows-install.md)。

+ 您的函式中使用的開放原始碼或協力廠商程式庫 (包括任何相依性) 必須安裝在 SQL Server 上。 如需詳細資訊, 請參閱[安裝新的 R 套件](../r/install-additional-r-packages-on-sql-server.md)。

+ 將腳本從開發環境移至強化的生產環境, 可能會引進防火牆和網路限制。 請小心測試, 以確定您的腳本能夠如預期般執行。

## <a name="next-steps"></a>後續步驟

如需使用**rxExec**的更複雜範例, 請參閱這篇文章:[使用 foreach 和 rxExec 的粗略細微性平行處理原則](https://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)
