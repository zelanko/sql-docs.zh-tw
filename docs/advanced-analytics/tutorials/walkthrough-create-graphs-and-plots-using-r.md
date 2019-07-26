---
title: 使用 SQL 和 R 函數建立圖形和繪圖-SQL Server Machine Learning
description: 示範如何在 SQL Server 上使用 R 語言函式建立圖形和繪圖的教學課程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: f14005b8ba9d6f05d2b69deba29d83af5695f657
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470505"
---
# <a name="create-graphs-and-plots-using-sql-and-r-walkthrough"></a>使用 SQL 和 R 建立圖形和繪圖 (逐步解說)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本逐步解說的這個部分中, 您將學習使用 R 與 SQL Server 資料來產生繪圖和地圖的技巧。 您會建立簡單的長條圖, 然後開發更複雜的地圖繪圖。

## <a name="prerequisites"></a>先決條件

此步驟會根據本逐步解說中的先前步驟, 假設正在進行中的 R 會話。 它會使用在這些步驟中建立的連接字串和資料來源物件。 下列工具和封裝是用來執行腳本。

+ 執行 R 命令的 rgui.exe
+ 執行 T-sql 的 Management Studio
+ googMap
+ ggmap 套件
+ mapproj 套件

## <a name="create-a-histogram"></a>建立長條圖

1. 使用 [rxHistogram](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) 函數來產生第一個繪圖。  RxHistogram 函數提供的功能與開放原始碼 R 套件中的類似, 但可以在遠端執行內容中執行。

    ```R
    # Plot fare amount on SQL Server and return the plot
    start.time <- proc.time()
    rxHistogram(~fare_amount, data = inDataSource, title = "Fare Amount Histogram")
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2), " seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate plot.", sep=""))
    ```

2. 針對開發環境，在 R 圖形裝置中傳回影像。  例如，在 RStudio 中，按一下 [繪製]  視窗。  在 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]中，開啟個別的圖形視窗。

    ![使用 rxHistogram 繪製費用金額](media/rsql-e2e-rxhistogramresult.png "使用 rxHistogram 繪製費用金額")

    > [!NOTE]
    > 您的圖表看起來不同嗎？
    >  
    > 這是因為_inDataSource_只會使用前1000個數據列。 在沒有 ORDER BY 子句的情況下, 使用 TOP 的資料列順序是不具決定性的, 因此預期資料和產生的圖形可能會有所不同。
    > 這個特定的影像是使用約 10,000 列資料列的資料所產生的。 建議您試驗不同數目的資料列來取得不同的圖形，並注意您的環境中傳回結果需要多長的時間。

## <a name="create-a-map-plot"></a>建立地圖繪圖

一般而言, 資料庫伺服器會封鎖網際網路存取。 當您使用需要下載地圖或其他影像來產生繪圖的 R 套件時, 這會很方便。 不過, 在開發自己的應用程式時, 您可能會發現有用的因應措施。 基本上, 您會在用戶端上產生地圖標記法, 然後在地圖上重迭儲存為 SQL Server 資料表中之屬性的點。

1. 定義用來建立 R 繪圖物件的函式。 自訂函式*mapPlot*會建立使用計程車取貨位置的散佈圖, 並繪製從每個位置開始的乘車數目。 它會使用應該已[安裝並載入](walkthrough-data-science-end-to-end-walkthrough.md#add-packages)的**ggplot2**和**ggmap**套件。

    ```R
    mapPlot <- function(inDataSource, googMap){
        library(ggmap)
        library(mapproj)
        ds <- rxImport(inDataSource)
        p <- ggmap(googMap)+
        geom_point(aes(x = pickup_longitude, y =pickup_latitude ), data=ds, alpha =.5,
    color="darkred", size = 1.5)
        return(list(myplot=p))
    }
    ```

    + *MapPlot*函數接受兩個引數: 您先前使用 RxSqlServerData 所定義的現有資料物件, 以及從用戶端傳遞的地圖標記法。
    + 在以*ds*變數開頭的那一行中, rxImport 是用來從先前建立的資料來源 ( *inDataSource*) 載入記憶體資料。 (該資料來源只包含1000個數據列; 如果您想要建立具有更多資料點的對應, 可以替代不同的資料來源)。
    + 每當您使用開放原始碼 R 函數時, 必須將資料載入本機記憶體中的資料框架。 不過, 藉由呼叫[rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport)函數, 您可以在遠端計算內容的記憶體中執行。

2. 將計算內容變更為 [本機], 並載入建立對應所需的程式庫。

    ```R
    rxSetComputeContext("local")
    library(ggmap)
    library(mapproj)
    gc <- geocode("Times Square", source = "google")
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color');
    ```

    + `gc` 變數會儲存紐約時代廣場的一組座標。

    + 開頭為 `googmap` 的行會在所指定座標的中心產生地圖。

3. 切換至 SQL Server 計算內容, 並藉由將繪圖函式包裝在[rxExec](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexec)中來呈現結果, 如下所示。 RxExec 函數是**RevoScaleR**套件的一部分, 可支援在遠端計算內容中執行任意 R 函數。

    ```R
    rxSetComputeContext(sqlcc)
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)
    plot(myplots[[1]][["myplot"]]);
    ````

    + 中`googMap`的對應資料會當做引數傳遞給遠端執行的函數*mapPlot*。 因為對應是在您的本機環境中產生的, 所以必須將它們傳遞給函式, 才能在 SQL Server 的內容中建立繪圖。

    + 當以`plot`執行開頭的那一行時, 轉譯的資料會序列化回本機 R 環境, 讓您可以在 R 用戶端中進行查看。

    > [!NOTE]
    > 如果您在 Azure 虛擬機器中使用 SQL Server, 此時可能會出現錯誤。 當 Azure 中的預設防火牆規則封鎖 R 程式碼的網路存取時, 就會發生錯誤。 如需如何修正此錯誤的詳細資訊, 請參閱[在 AZURE VM 上安裝 Machine Learning (R) 服務](../install/sql-machine-learning-azure-virtual-machine.md)。

4. 下圖顯示輸出繪圖。 計程車上車位置會以紅點新增到地圖上。 視您使用的資料來源中有多少個位置而定, 您的影像可能看起來不同。

    ![使用自訂 R 函數繪製的計程車乘車點](media/rsql-e2e-mapplot.png "使用自訂 R 函數繪製的計程車乘車點")

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 R 和 SQL 建立資料特徵](walkthrough-create-data-features.md)
