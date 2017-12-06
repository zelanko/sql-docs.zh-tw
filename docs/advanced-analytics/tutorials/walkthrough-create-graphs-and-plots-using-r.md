---
title: "建立圖形和繪圖使用 SQL 與 R （逐步解說） |Microsoft 文件"
ms.date: 11/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 5f70f0a6-fd4a-410f-9f44-1605503f77ec
caps.latest.revision: "16"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 8cf83243f4c2c9dd5d114799166160d53573c90f
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="create-graphs-and-plots-using-sql-and-r-walkthrough"></a>建立圖形和繪圖使用 SQL 與 R （逐步解說）

在這部分的逐步解說中，您會學習技巧產生繪圖和使用 R 與 SQL Server 資料的對應。 建立簡單的長條圖，以取得一些練習，，然後開發更複雜的對應圖。

### <a name="create-a-histogram"></a>建立長條圖

1. 使用 [rxHistogram](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) 函數來產生第一個繪圖。  RxHistogram 函式提供的功能類似於在開放原始碼 R 封裝，但是可以在遠端執行內容中執行。

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
    > 您的圖表看起來不同？
    >  
    > 這是因為_inDataSource_會使用前 1000 個資料列。 使用 TOP 資料列的順序是不具決定性，ORDER BY 子句不存在，所以預期的資料和結果的圖形可能會不同。
    > 這個特定的影像是使用約 10,000 列資料列的資料所產生的。 建議您試驗不同數目的資料列來取得不同的圖形，並注意您的環境中傳回結果需要多長的時間。

### <a name="create-a-map-plot"></a>建立對應圖

一般而言，資料庫伺服器封鎖網際網路存取。 使用需要下載對應或其他影像，以便產生繪圖的 R 封裝時，這可以是很不方便。 不過，沒有可能有幫助開發自己的應用程式時的因應措施。 基本上，您產生地圖表示法，在用戶端，並接著在地圖上重疊的點會儲存為 SQL Server 資料表中的屬性。

1. 定義來建立 R 繪圖物件的函式。 自訂函式*mapPlot*建立散佈圖的使用計程車收取位置，並繪製了開始的每個位置的數目。 它會使用應該已安裝並載入的 **ggplot2** 和  **ggmap** 套件。

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

    + *MapPlot*函數會採用兩個引數： 現有的資料物件，您定義之前使用 RxSqlServerData，並從用戶端傳遞地圖表示法。
    + 在行首*ds*變數 rxImport 用來載入先前建立的資料來源的記憶體資料*inDataSource*。 （該資料來源包含只 1000 個資料列; 如果您想要建立具有多個資料點的對應，您可以替代不同的資料來源）。
    + 每當您使用**開放原始碼**R 函數，資料必須載入本機記憶體中的資料框架。 不過，藉由呼叫[rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport)函式，您可以在遠端計算內容的記憶體中執行。

2. 將計算內容變更為本機，並載入所需的建立對應的程式庫。

    ```R
    rxSetComputeContext("local")
    library(ggmap)
    library(mapproj)
    gc <- geocode("Times Square", source = "google")
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color');
    ```

    + `gc` 變數會儲存紐約時代廣場的一組座標。

    + 開頭為 `googmap` 的行會在所指定座標的中心產生地圖。

3. 切換至 SQL Server 計算內容中，並藉由包裝中的繪圖函式轉譯結果， [rxExec](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexec)如下所示。 RxExec 函式是一部分**RevoScaleR**封裝，並支援任意的 R 函數，在遠端計算內容中執行。

    ```R
    rxSetComputeContext(sqlcc)
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)
    plot(myplots[[1]][["myplot"]]);
    ````

    + 中的地圖資料`googMap`做為引數傳遞至遠端執行的函式*mapPlot*。 本機環境中所產生的對應，因為它們必須傳遞至函式才能建立 SQL Server 的內容中的繪圖。

    + 當行首`plot`執行時，轉譯的資料會序列化回到本機的 R 環境，以便您可以在您的 R 用戶端中檢視。

    > [!NOTE]
    > 如果您使用 SQL Server 在 Azure 虛擬機器，您可能在此時會發生錯誤。 這是因為在 Azure 中的預設防火牆規則封鎖網路存取的 R 程式碼。 如需如何修正此錯誤的詳細資訊，請參閱[Azure VM 中安裝 R Services](../r/installing-sql-server-r-services-on-an-azure-virtual-machine.md)。

4. 下圖顯示輸出繪圖。 計程車上車位置會以紅點新增到地圖上。 您的影像看起來可能不同，視多少位置在您使用的資料來源中。

    ![使用自訂 R 函數繪製的計程車乘車點](media/rsql-e2e-mapplot.png "使用自訂 R 函數繪製的計程車乘車點")

## <a name="next-lesson"></a>下一課

[建立使用 R 和 SQL 資料功能](/walkthrough-create-data-features.md)

## <a name="previous-lesson"></a>上一課

[使用 R 的資料摘要](/walkthrough-view-and-summarize-data-using-r.md)
