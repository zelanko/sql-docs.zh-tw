---
title: 使用 SQL 和 R 函式-SQL Server Machine Learning 建立圖形和繪圖
description: 本教學課程示範如何建立圖形和繪圖使用 SQL Server 上的 R 語言函式。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d19625ed56370a1619300c21e3822c0c3eeef484
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2018
ms.locfileid: "53597079"
---
# <a name="create-graphs-and-plots-using-sql-and-r-walkthrough"></a>使用 SQL 和 R （逐步解說） 建立圖形和繪圖
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本逐步解說的這個部分，您會學習技術來產生繪圖和使用 R 與 SQL Server 資料的對應。 您會建立簡單的長條圖，並再開發更複雜的地圖繪圖。

## <a name="prerequisites"></a>先決條件

這個步驟會假設根據先前在本逐步解說的步驟進行中的 R 工作階段。 它會使用連接字串和資料來源中建立的物件執行這些步驟。 下列工具和套件來執行指令碼。

+ 若要執行 R 命令的 Rgui.exe
+ Management Studio 來執行 T-SQL
+ googMap
+ ggmap 封裝
+ mapproj 封裝

## <a name="create-a-histogram"></a>建立長條圖

1. 使用 [rxHistogram](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) 函數來產生第一個繪圖。  RxHistogram 函式會提供類似於在開放原始碼 R 套件的功能，但可以在遠端執行內容中執行。

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
    > 您的圖形看起來不同嗎？
    >  
    > 這是因為_inDataSource_會使用前 1000 個資料列。 使用 TOP 的資料列的順序是不具決定性，ORDER BY 子句不存在，因此預計的資料和產生的圖形可能會有所不同。
    > 這個特定的影像是使用約 10,000 列資料列的資料所產生的。 建議您試驗不同數目的資料列來取得不同的圖形，並注意您的環境中傳回結果需要多長的時間。

## <a name="create-a-map-plot"></a>建立地圖

一般而言，資料庫伺服器會封鎖網際網路存取。 使用 R 套件，必須先下載對應或其他映像，以產生繪圖時，這很不方便。 不過，還有可能有幫助開發您自己的應用程式時的因應措施。 基本上，您會產生地圖表示法，在用戶端，，然後將它重疊在地圖上的點會儲存為 SQL Server 資料表中的屬性。

1. 定義可建立 R 繪圖物件的函數。 自訂函式*mapPlot*建立散佈圖使用計程車上車位置，以及繪製從每個位置開始的乘車次數。 它會使用**ggplot2**並**ggmap**套件，應該已經很[安裝並載入](walkthrough-data-science-end-to-end-walkthrough.md#add-packages)。

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

    + *MapPlot*函式會採用兩個引數： 現有的資料物件，您定義稍早使用 RxSqlServerData，並從用戶端傳遞的地圖表示法。
    + 在開頭的行會*ds*變數，rxImport 用來載入先前建立的資料來源的記憶體資料*inDataSource*。 （該資料來源包含只 1000 個資料列，如果您想要建立具有多個資料點的對應，您可以替代不同的資料來源）。
    + 每當您使用開放原始碼 R 函數，資料必須載入本機記憶體中的資料框架。 不過，藉由呼叫[rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport)函式，您可以在遠端計算內容的記憶體中執行。

2. 將計算內容變更為本機，並載入建立這些地圖所需的程式庫。

    ```R
    rxSetComputeContext("local")
    library(ggmap)
    library(mapproj)
    gc <- geocode("Times Square", source = "google")
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color');
    ```

    + `gc` 變數會儲存紐約時代廣場的一組座標。

    + 開頭為 `googmap` 的行會在所指定座標的中心產生地圖。

3. 切換至 SQL Server 計算內容，並轉譯結果，藉由包裝繪製函數，在[rxExec](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexec)如下所示。 RxExec 函式是一部分**RevoScaleR**封裝，並支援執行任意 R 函數，在遠端計算內容中。

    ```R
    rxSetComputeContext(sqlcc)
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)
    plot(myplots[[1]][["myplot"]]);
    ````

    + 中的對應資料`googMap`做為引數傳遞給遠端執行的函式*mapPlot*。 在您的本機環境中所產生的對應，因為必須將它們傳遞至函式才能建立繪圖的 SQL Server 內容中。

    + 當開頭的行會`plot`執行時，轉譯的資料會序列化回本機 R 環境，以便您可以在您的 R 用戶端中檢視。

    > [!NOTE]
    > 如果您在 Azure 虛擬機器中使用 SQL Server，您可能在此時會發生錯誤。 當預設的防火牆規則，在 Azure 中的 R 程式碼會封鎖網路存取，就會發生錯誤。 如需有關如何修正此錯誤的詳細資訊，請參閱 < [Azure VM 上的安裝 Machine Learning （R) Services](../r/installing-sql-server-r-services-on-an-azure-virtual-machine.md)。

4. 下圖顯示輸出繪圖。 計程車上車位置會以紅點新增到地圖上。 您的映像可能會有所不同，視幾個位置您所使用的資料來源。

    ![使用自訂 R 函數繪製的計程車乘車點](media/rsql-e2e-mapplot.png "使用自訂 R 函數繪製的計程車乘車點")

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 R 與 SQL 建立資料特徵](walkthrough-create-data-features.md)
