---
title: "使用 R 建立圖形和繪圖 (資料科學端對端逐步解說) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
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
ms.assetid: 5f70f0a6-fd4a-410f-9f44-1605503f77ec
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# 使用 R 建立圖形和繪圖 (資料科學端對端逐步解說)
在這一課，您將學習搭配使用 R 與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來產生繪圖和地圖的技巧。  您將會看到檢視在伺服器上所建立的繪圖多麼簡單，以及如何將圖形物件傳遞給伺服器。  
  
## <a name="creating-graphics"></a>建立圖形
在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中，會序列化您電腦與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦內容之間的圖形物件以及模型和結果。

使用 SQL Server 計算內容時，您可能無法下載地圖表示法，因為大部分實際執行的資料庫伺服器會完全封鎖網際網路存取。  因此，若要建立第二組繪圖，您將會在用戶端中產生地圖表示法，然後將儲存為 *nyctaxi_sample* 資料表中屬性的點重疊在地圖上。   

若要這樣做，您會先呼叫 Google 地圖來建立地圖表示法，然後將地圖表示法傳遞至 SQL 內容。  
  
這是開發專屬應用程式時可能有用的模式。   
  
### <a name="create-a-histogram"></a>建立長條圖  
若要建立長條圖，您將使用稍早建立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源，以及 R Services 中所提供的 `rxHistogram` 函數。  
  
1.  使用 *rxHistogram* 函數來產生第一個繪圖。  *rxHistogram* 函數會提供類似開放原始碼 R 封裝中的功能，但是可以在遠端執行內容中執行。 
  
    ```R  
    #Plot fare amount on SQL Server and return the plot  
    start.time <- proc.time()  
    rxHistogram(~fare_amount, data = inDataSource, title = "Fare Amount Histogram")  
    used.time <- proc.time() - start.time  
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2), " seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))    
    ```         
  
2.  針對開發環境，在 R 圖形裝置中傳回影像。  例如，在 RStudio 中，按一下 [繪製] 視窗。  在 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]中，開啟個別的圖形視窗。  
  
    ![using rxHistogram to plot fare amounts](../../advanced-analytics/r-services/media/rsql-e2e-rxhistogramresult.png "using rxHistogram to plot fare amounts")  
  
    > [!NOTE]  因為在不使用 ORDER BY 子句的情況下，使用 TOP 的資料列順序不具決定性，所以您可能會看到非常不同的結果。 建議您試驗不同數目的資料列來取得不同的圖形，並注意您的環境中傳回結果需要多長的時間。  這個特定的影像是使用 ~10,000 個資料列的資料所產生。
  
### <a name="create-a-map-plot"></a>建立地圖  
在此範例中，您將會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體作為計算內容來產生繪圖物件，然後將繪圖物件傳回給本機計算內容來進行轉譯。  
   
1.  首先，定義可建立繪圖物件的函數。  

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
    + 自訂 R 函數 *mapPlot* 會建立散佈圖，這個散佈圖會使用計程車上車位置來繪製從每個位置開始的乘車次數。 它會使用應該已安裝並載入的 **ggplot2** 和  **ggmap** 套件。  
    + 自訂函數 *mapPlot* 採用兩個引數︰您先前使用 *RxSqlServerData* 所定義的現有資料物件，以及從用戶端傳遞的地圖表示法。    
    + 請記得使用 *ds* 變數來載入先前所建立資料來源 *inDataSource* 中的資料。  只要使用開放原始碼 R 函數，就必須將資料載入至記憶體中的資料框架。 做法是使用 **RevoScaleR** 封裝中的 *rxImport* 函數。  不過，此函數會在先前定義的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內容中於記憶體中執行。 亦即，這個函數不會使用本機工作站的記憶體。  
  
2.  接下來，載入在本機 R 環境中建立這些地圖所需的程式庫。  
  
    ```R  
    library(ggmap)  
    library(mapproj)  
    gc <- geocode("Times Square", source = "google")  
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color';    
    ```  
    + 這個程式碼是在 R 用戶端上執行。 請注意， **ggmap** 和 **mapproj**程式庫的重複呼叫。 原因是前一個函數定義已在伺服器內容中執行，而且絕不會在本機載入程式庫；現在，您要將繪製作業帶回工作站。  
  
    -   *gc* 變數會儲存紐約時代廣場的一組座標。  
  
    -   開頭為 *googmap* 的行會在所指定座標的中心產生地圖。  
          
  
3.  執行繪製函數，並在本機 R 環境中轉譯結果。 若要這樣做，請在 *rxExec* 中包裝繪製函數，如下所示。  *rxExec* 函數包含在 **RevoScaleR** 封裝中，並支援在遠端計算內容中執行任意 R 函數。 
  
    ```R  
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)  
    plot(myplots[[1]][["myplot"]]);  
  
    ```  
    + 在第一行中，您可以看到將地圖資料當成引數 (*googMap*) 傳遞給遠端執行的函數 *mapPlot*。 原因是已在本機環境中產生地圖，並且已將地圖傳遞給函數，以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的內容中建立繪圖。   
  
        轉譯的資料接著會序列化回本機 R 環境，讓您可以使用 RStudio 中的 [繪製] 視窗或其他 R 圖形裝置來進行檢視。  
  
  
4.  以下是輸出繪圖，會在地圖上以紅點顯示上車位置。  
  
    ![plotting taxi rides using a custom R function](../../advanced-analytics/r-services/media/rsql-e2e-mapplot.png "plotting taxi rides using a custom R function")  
  
## <a name="next-lesson"></a>下一課  
[第 3 課︰建立資料特徵 &#40;資料科學端對端逐步解說&#41;](../../advanced-analytics/r-services/lesson-3-create-data-features-data-science-end-to-end-walkthrough.md)  
  
  
  
