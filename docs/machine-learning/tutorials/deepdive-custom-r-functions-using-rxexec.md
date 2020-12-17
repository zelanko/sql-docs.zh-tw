---
title: 使用 rxExec 自訂 R 函數
description: 了解如何使用模擬資料，示範如何執行在遠端伺服器上執行的自訂 R 函式。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: 3088409167e41aa478ef831c72eee100650919a1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470579"
---
# <a name="run-custom-r-functions-on-sql-server-using-rxexec-sql-server-and-revoscaler-tutorial"></a>使用 rxExec 在 SQL Server 上執行自訂 R 函式 (SQL Server 和 RevoScaleR 教學課程)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

這是 [RevoScaleR 教學課程系列](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)的教學課程 14；此教學課程系列說明如何搭配 SQL Server 使用 [RevoScaleR 函式](/machine-learning-server/r-reference/revoscaler/revoscaler) \(英文\)。

在此教學課程中，您將會使用模擬資料來示範如何執行在遠端伺服器上執行的自訂 R 函式。

您可以藉由透過 [rxExec](/machine-learning-server/r-reference/revoscaler/rxexec) 傳遞函數的方式，在 SQL Server 的內容中執行自訂 R 函數，前提是指令碼所需的任何程式庫也安裝在此伺服器，而且這些程式庫與 R 的基礎映像發佈相容。 

**RevoScaleR** 中的 **rxExec** 函數會提供一個機制來執行您所需的任何 R 指令碼。 此外，**rxExec** 能夠在單一伺服器中明確地將工作散發到多個核心，擴充受限於原生 R 引擎資源限制式的指令碼。

## <a name="prerequisites"></a>Prerequisites

+ [SQL Server 機器學習服務 (含 R)](../install/sql-machine-learning-services-windows-install.md) 或 [SQL Server 2016 R Services (資料庫內)](../install/sql-r-services-windows-install.md)
  
+ [資料庫權限](../security/user-permission.md) 和 SQL Server 資料庫使用者登入

+ [具有 RevoScaleR 程式庫的開發工作站](../r/set-up-a-data-science-client.md)

用戶端工作站上的 R 散發會提供內建的 **Rgui** 工具，讓您在本教學課程中用來執行 R 指令碼。 您也可以使用 IDE，例如 RStudio 或 Visual Studio R 工具。

## <a name="create-the-remote-compute-context"></a>建立遠端計算內容

在用戶端工作站上執行下列 R 命令。 舉例來說，如果您正在使用 **Rgui**，請從以下位置啟動它：C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64\.

1. 指定要執行計算的 SQL Server 執行個體連接字串。 必須設定伺服器的 R 整合作業。 本練習不會使用此資料庫名稱，但是連接字串需要。 如果您有測試或範例資料庫便可以使用。

    **使用 SQL 登入**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>; Database=<database-name>;Uid=<SQL-user-name>;Pwd=<password>"
    ```

    **使用 Windows 驗證**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>;Database=<database-name>;Trusted_Connection=True"
    ```

2. 將遠端計算內容建立至連接字串中所參考的 SQL Server 執行個體。

    ```R
    sqlCompute <- RxInSqlServer(connectionString = sqlConnString)
    ```

3. 啟動計算內容，然後傳回物件定義做為確認步驟。 您應該會看到計算內容物件的屬性。

    ```R
    rxSetComputeContext(sqlCompute)
    rxGetComputeContext()
    ```

## <a name="create-the-custom-function"></a>建立自訂函數

在本練習中，您將建立自訂的 R 函數，模擬包含擲一對骰子的一般賭場。 遊戲規則會決定輸贏結果：

+ 在第一把擲出 7 或 11，您就贏了。
+ 擲出 2、3 或 12，您就輸了。
+ 擲出 4、5、6、8、9 或 10，該數字會變成您的決勝點，您可以繼續擲到擲出同個決勝點 (若擲出，您就算贏)；如果擲出 7，您就算輸。

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
  
2.  請執行此函數，模擬一場單一的骰子遊戲。
  
    ```R
    rollDice()
    ```
  
    您贏了還是輸了？
  
現在您已經有操作指令碼，讓我們來看看如何使用 **rxExec** 多次執行函數，以建立模擬並協助判斷獲勝的機率。

## <a name="pass-rolldice-in-rxexec"></a>在 rxExec 中傳遞 rollDice()

若要在遠端 SQL Server 的內容中執行任意函數，請呼叫 **rxExec** 函數。

1. 呼叫自訂函數做為 **rxExec** 的引數，以及可修改模擬的其他參數。
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    + 使用 *timesToRun* 引數來指定函數應執行的次數。  在此案例中，您要擲骰子 20 次。
  
    + 引數 *RNGseed* 和 *RNGkind* 可以用來控制隨機數字的產生。 當 *RNGseed* 設為 [自動]  時，會在每一個背景工作上平行初始化隨機資料流。
  
2. **rxExec** 函數會建立一份清單，其中每個回合都有一個項目；不過，在清單未完成時，您都不會察覺到任何影響。 當所有反覆運算次數完成時，開頭為 **length** 的那一行會傳回值。
  
    您即可移至下一個步驟，以取得輸贏記錄的摘要。
  
3. 使用 R 的 **unlist** 函數將傳回的清單轉換為向量，再使用 **table** 函數彙總結果。
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    結果應該如下所示：
  
     *Loss  Win* *12  8*

## <a name="conclusion"></a>結論

雖然本練習很簡單，但卻示範了在 SQL Server 執行的 R 指令碼中，整合任意 R 函數的重要機制。 總結實現這項技術的重點：

+ 必須設定 SQL Server 的機器學習和 R 整合作業：使用 R 功能的 [SQL Server 機器學習服務](../install/sql-machine-learning-services-windows-install.md)，或 [SQL Server 2016 R Services (資料庫內)](../install/sql-r-services-windows-install.md)。

+ 您函數中使用的開放原始碼或協力廠商程式庫 (包括任何相依性) 必須安裝在 SQL Server 上。 如需詳細資訊，請參閱[安裝新的 R 套件](../package-management/install-additional-r-packages-on-sql-server.md)。

+ 將指令碼從開發環境移至強化的生產環境，可能會引進防火牆和網路限制。 請小心測試，確保您的指令碼能夠依預期執行。

## <a name="next-steps"></a>後續步驟

如需更複雜 **rxExec** 使用範例，請參閱以下文章：[使用 Foreach 和 rxExec 的粗略平行處理原則 (英文)](https://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)