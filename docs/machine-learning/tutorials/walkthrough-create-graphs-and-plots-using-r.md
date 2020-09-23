---
title: R 教學課程：建立圖表及繪圖
description: 了解搭配使用 R 語言與 SQL Server 資料產生繪圖和地圖的技術。 建立簡單的長條圖，接著再開發更複雜的地圖繪圖。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5b6643cec32cc3581c0f91e4479fff0d908e7532
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178425"
---
# <a name="create-graphs-and-plots-using-sql-and-r-walkthrough"></a>使用 SQL 和 R 建立圖表和繪圖 (逐步解說)
[!INCLUDE [SQL Server 2016](../../includes/applies-to-version/sqlserver2016.md)]

在本逐步解說的這個部份中，您將學習使用 R 與 SQL Server 資料產生繪圖和地圖的技巧。 您將建立簡單的長條圖，接著再開發更複雜的地圖繪圖。

## <a name="prerequisites"></a>先決條件

此步驟會假設您有以本逐步解說中先前步驟為基礎的進行中 R 工作階段。 它會使用在那些步驟中建立的連接字串和資料來源物件。 會使用下列工具和套件來執行指令碼。

+ Rgui.exe 來執行 R 命令
+ Management Studio 來執行 T-SQL
+ googMap
+ ggmap 套件
+ mapproj 套件

## <a name="create-a-histogram"></a>建立長條圖

1. 使用 [rxHistogram](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) 函數來產生第一個繪圖。  rxHistogram 函數會提供類似開放原始碼 R 套件中的功能，但是可以在遠端執行內容中執行。

    ```R
    # Plot fare amount on SQL Server and return the plot
    start.time <- proc.time()
    rxHistogram(~fare_amount, data = inDataSource, title = "Fare Amount Histogram")
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2), " seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate plot.", sep=""))
    ```

2. 針對開發環境，在 R 圖形裝置中傳回影像。  例如，在 RStudio 中，按一下 [繪製] **** 視窗。  在 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]中，開啟個別的圖形視窗。

    ![使用 rxHistogram 繪製費用金額](media/rsql-e2e-rxhistogramresult.png "使用 rxHistogram 繪製費用金額")

    > [!NOTE]
    > 您的圖表看起來不同嗎？
    >  
    > 這是因為 _inDataSource_ 只會使用前 1000 列。 在不使用 ORDER BY 子句的情況下，使用 TOP 的資料列順序不具決定性，所以資料和產生的圖形可能會有所不同。
    > 這個特定的影像是使用約 10,000 列資料列的資料所產生的。 建議您試驗不同數目的資料列來取得不同的圖形，並注意您的環境中傳回結果需要多長的時間。

## <a name="create-a-map-plot"></a>建立地圖繪圖

一般而言，資料庫伺服器會封鎖網際網路存取。 但如果您使用需要下載地圖或其他影像以產生繪圖的 R 套件，這就會造成不便。 不過，有一個實用的因應措施或許可以幫助您的應用程式開發工作。 基本上，您可以在用戶端中產生地圖展示，然後將儲存為 SQL Server 資料表中屬性的點重疊在地圖上。

1. 定義可建立 R 繪圖物件的函數。 自訂函數 *mapPlot* 會建立散佈圖，而這個散佈圖會使用計程車上車位置來繪製從每個位置開始的乘車次數。 它會使用應該已[安裝並載入](walkthrough-data-science-end-to-end-walkthrough.md#add-packages)的 **ggplot2** 和 **ggmap**。

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

    + 自訂函數 *mapPlot* 採用兩個引數︰您先前使用 RxSqlServerData 所定義的現有資料物件，以及從用戶端傳遞的地圖表示法。
    + 在以 *ds* 變數開頭的行當中，rxImport 用來從先前建立的資料來源 *inDataSource* 載入記憶體資料。 (該資料來源只包含 1000 列；如果您想要建立具有更多資料點的對應，可以用不同的資料來源替代。)
    + 只要使用開放原始碼 R 函數，就必須將資料載入至本機記憶體中的資料框架。 不過，您可透過呼叫 [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) 函數，藉此在遠端計算內容的記憶體中執行工作。

2. 將計算內容變更為本機，並載入建立地圖所需的程式庫。

    ```R
    rxSetComputeContext("local")
    library(ggmap)
    library(mapproj)
    gc <- geocode("Times Square", source = "google")
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color');
    ```

    + `gc` 變數會儲存紐約時代廣場的一組座標。

    + 開頭為 `googmap` 的行會在所指定座標的中心產生地圖。

3. 切換至 SQL Server 計算內容，然後將繪圖函數包裝在 [rxExec](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexec) 中呈現結果，如下所示。 rxExec 函數是 **RevoScaleR** 套件的一部分，並支援在遠端計算內容中執行任意 R 函數。

    ```R
    rxSetComputeContext(sqlcc)
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)
    plot(myplots[[1]][["myplot"]]);
    ````

    + `googMap` 中的地圖資料將做為引數傳遞給遠端執行的函數 *mapPlot*。 由於已在本機環境中產生地圖，因此必須將地圖傳遞給函數，以在 SQL Server 的內容中建立繪圖。

    + 當開頭為 `plot` 的行執行作業時，轉譯的資料會序列化回本機 R 環境，讓您可以在 R 用戶端中查看。

    > [!NOTE]
    > 如果您在 Azure 虛擬機器中使用 SQL Server，系統在此時就可能出現錯誤。 當 Azure 中的預設防火牆規則封鎖 R 程式碼的網路存取時，系統就會發生錯誤。 如需錯誤修正的相關詳細資訊，請參閱 [在 Azure VM 上安裝 Machine Learning (R) 服務](../install/sql-machine-learning-azure-virtual-machine.md)。

4. 下圖顯示輸出繪圖。 計程車上車位置會以紅點新增到地圖上。 您的影像取決於您使用資料來源的位置數量，可能看起來會有所不同。

    ![使用自訂 R 函數繪製計程車乘車點](media/rsql-e2e-mapplot.png "使用自訂 R 函數繪製計程車乘車點")

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 R 和 SQL 建立資料特徵](walkthrough-create-data-features.md)
