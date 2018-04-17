---
title: 課程 3 瀏覽及視覺化資料 |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 4be76ebbb8f082e84a00bfe93b36c9bd8c2c0a81
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="lesson-3-explore-and-visualize-the-data"></a>第 3 課： 探索和視覺化資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章是有關如何在 SQL Server 中使用 R 的 SQL 開發人員的教學課程的一部分。

在這一課中，將檢視範例資料，並接著產生某些繪圖 R 函式的使用。 中已經包含這些 R 函式[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。 您可以呼叫 R 函式，從[!INCLUDE[tsql](../../includes/tsql-md.md)]。

## <a name="review-the-data"></a>檢視資料

開發資料科學方案通常會包含大量資料瀏覽和資料視覺化。 如果您還沒有這麼做，首先花點時間檢閱資料範例。

在原始資料集中，計程車識別碼和車程記錄會提供在不同的檔案中。 不過，若要讓您更輕鬆地使用範例資料，兩個原始資料集已加入的資料行上_medallion_， _hack\_授權_，和_收取\_datetime_。  也會對記錄進行抽樣，只取得 1% 的原始記錄數目。 產生的向下取樣資料集有 1,703,957 個資料列和 23 個資料行。

**計程車識別碼**
  
-   _medallion_ 資料行代表計程車的唯一識別碼。
  
-   _Hack\_授權_資料行包含計程車驅動程式的授權數量 （匿名）。
  
**車程和小費記錄**
  
-   每筆車程記錄都會包含上車和下車位置與時間，以及車程距離。
  
-   每筆費用記錄都會包括付款資訊，例如付款類型、總付款金額和小費金額。
  
-   最後三個資料行可以用於各種機器學習工作。  _提示\_量_資料行包含連續數值，可用來當作**標籤**迴歸分析的資料行。 _tipped_ 資料行只有是/否值，並且用於二元分類。 _提示\_類別_資料行有多個**類別標籤**，因此可以用於做為標籤多級分類工作。
  
    這個逐步解說只會示範二元分類工作；您可以自由地嘗試建立其他兩個機器學習工作 (迴歸和多類別分類) 的模型。
  
-   用於標籤資料行的值都以基礎_提示\_量_資料行中，使用這些商務規則：
  
    |衍生的資料行名稱|規則|
    |-|-|
     |tipped|If tip_amount > 0, tipped = 1, otherwise tipped = 0|
    |tip_class|Class 0: tip_amount = $0<br /><br />Class 1: tip_amount > $0 and tip_amount <= $5<br /><br />Class 2: tip_amount > $5 and tip_amount <= $10<br /><br />Class 3: tip_amount > $10 and tip_amount <= $20<br /><br />Class 4: tip_amount > $20|

## <a name="create-plots-using-r-in-t-sql"></a>建立 T-SQL 中使用 R 的繪圖

因為視覺效果是可了解資料和極端值分佈的功能強大工具，所以 R 提供許多套件可以將資料視覺化。 R 的標準開放原始碼發佈也包括許多函數，可建立長條圖、散佈圖、盒狀圖以及其他資料瀏覽圖形。

R 通常會使用 R 裝置建立影像，以進行圖形輸出。 您可以擷取這個裝置的輸出，以及將影像儲存為 **varbinary** 資料類型以在應用程式中轉譯，也可以將影像儲存為任何支援檔案格式 (.JPG、.PDF 等)。

在本節中，您將了解如何使用預存程序來處理每種類型的輸出。 整個程序如下所示：

- 建立預存程序來產生 R 繪圖，做為 varbinary 資料

- 產生的繪圖，並將它儲存至影像檔

- 使用預存程序將二進位資料轉換成 JPG 或 PDF 檔案

### <a name="create-the-stored-procedure-plothistogram"></a>建立預存程序 PlotHistogram

1. 若要建立繪圖，請使用`rxHistogram`，增強的 R 函數中提供的其中一個[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，若要繪製的長條圖的資料[!INCLUDE[tsql](../../includes/tsql-md.md)]查詢。 為了簡化 R 函數的呼叫，請將它包裝在 _PlotHistogram_預存程序中。

    在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，開啟新**查詢**視窗。

2. 在資料庫中包含的教學課程的資料，建立程序中使用此陳述式：

    ```SQL
    CREATE PROCEDURE [dbo].[PlotHistogram]
    AS
    BEGIN
      SET NOCOUNT ON;
      DECLARE @query nvarchar(max) =  
      N'SELECT tipped FROM nyctaxi_sample'  
      EXECUTE sp_execute_external_script @language = N'R',  
                                         @script = N'  
       image_file = tempfile();  
       jpeg(filename = image_file);  
       #Plot histogram  
       rxHistogram(~tipped, data=InputDataSet, col=''lightgreen'',   
       title = ''Tip Histogram'', xlab =''Tipped or not'', ylab =''Counts'');  
       dev.off();  
       OutputDataSet <- data.frame(data=readBin(file(image_file, "rb"), what=raw(), n=1e6));  
       ',  
       @input_data_1 = @query  
       WITH RESULT SETS ((plot varbinary(max)));  
    END
    GO
    ```

    必要時，請務必修改程式碼來使用正確的資料表名稱。
  
    -   `@query` 變數會定義查詢文字 (`'SELECT tipped FROM nyctaxi_sample'`)，以當成指令碼輸入變數 `@input_data_1`的引數傳遞給 R 指令碼。
  
    -   R 指令碼相當簡單︰定義 R 變數 (`image_file`) 來定義影像，然後呼叫 `rxHistogram` 函數來產生繪圖。
  
    -   R 裝置設定為 **off**。
  
        在 R 中，當您發出高階繪製命令時，R 將會開啟稱為「裝置」的圖形視窗。 您可以變更視窗的大小、色彩和其他層面，也可以在寫入至檔案或透過其他方法處理輸出時關閉裝置。
  
    -   R 圖形物件會序列化為 R data.frame 以進行輸出。

### <a name="generate-the-graphics-data-and-save-to-file"></a>產生圖形資料，並儲存至檔案

預存程序會以您明顯無法直接檢視的 varbinary 資料流形式傳回影像。 不過，您可以使用 **bcp** 公用程式來取得 varbinary 資料，並將它儲存為用戶端電腦上的影像檔。
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，執行下列陳述式：
  
    ```SQL
    EXEC [dbo].[PlotHistogram]
    ```
  
    **結果**
    
    *繪圖*
    *0xFFD8FFE000104A4649...*
  
2.  開啟 PowerShell 命令提示字元，並將適當的執行個體名稱、資料庫名稱、使用者名稱和認證提供為引數來執行下列命令︰
  
     ```
     bcp "exec PlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  <database name>  -U <user name> -P <password>
     ```

    > [!NOTE]
    > 如果是 bcp 命令參數會區分大小寫。
  
3.  如果連接成功，系統會提示您輸入圖形檔格式的詳細資訊。 在每個提示字元下，按 ENTER 接受預設值，但不包括這些變更：
  
    -   在 **prefix-length of field plot**中，輸入 0。
  
    -   如果您想要儲存輸出參數以供日後重複使用，請輸入 **Y** 。
  
    ```
    Enter the file storage type of field plot [varbinary(max)]:
    Enter prefix-length of field plot [8]: 0
    Enter length of field plot [0]:
    Enter field terminator [none]:
  
    Do you want to save this format information in a file? [Y/n]
    Host filename [bcp.fmt]:
    ```
  
    **結果**
    
    ```
    Starting copy...
    1 rows copied.
    Network packet size (bytes): 4096
    Clock Time (ms.) Total     : 3922   Average : (0.25 rows per sec.)
    ```

    > [!TIP]
    > 如果您將格式資訊儲存至檔案 (bcp.fmt)，則 **bcp** 公用程式會產生您未來可套用至類似命令的格式定義，而不提示您輸入圖形檔格式選項。 若要使用格式檔案，請在 password 引數之後將 `-f bcp.fmt` 新增至任何命令列結尾。
  
4.  將會在執行 PowerShell 命令的相同目錄中建立輸出檔案。 若要檢視繪圖，只需要開啟檔案 plot.jpg。
  
    ![包含與不含小費的計程車車程](media/rsql-devtut-tippedornot.jpg "包含與不含小費的計程車車程")  
  
### <a name="export-the-plot-data-to-a-viewable-file"></a>將資料繪製匯出至可檢視檔案

輸出為二進位資料的 R 繪圖類型可能會很方便，應用程式的取用，但不是非常有用的資料科學家資料瀏覽階段期間需要呈現的繪圖。 資料科學家通常會產生多個資料視覺效果，從不同的角度深入了解資料。

若要產生使用者的圖表，您可以使用建立的 R 輸出中常見的格式，例如預存程序。JPG、。PDF、 和。PNG。 在預存程序建立圖形之後，只要開啟檔案，就可以視覺化該繪圖。

1. 建立新的預存程序， _PlotInOutputFiles_，示範如何撰寫長條圖、 scatterplots 和其他 R 圖形。JPG 和。PDF 格式。

    在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，開啟新**查詢**視窗中，然後貼上的下列[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式。
  
    ```SQL
    CREATE PROCEDURE [dbo].[PlotInOutputFiles]  
    AS  
    BEGIN  
      SET NOCOUNT ON;  
      DECLARE @query nvarchar(max) =  
      N'SELECT cast(tipped as int) as tipped, tip_amount, fare_amount FROM [dbo].[nyctaxi_sample]'  
      EXECUTE sp_execute_external_script @language = N'R',  
      @script = N'  
       # Set output directory for files and check for existing files with same names   
        mainDir <- ''C:\\temp\\plots''  
        dir.create(mainDir, recursive = TRUE, showWarnings = FALSE)  
        setwd(mainDir);  
        print("Creating output plot files:", quote=FALSE)
        
        # Open a jpeg file and output histogram of tipped variable in that file.  
        dest_filename = tempfile(pattern = ''rHistogram_Tipped_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.jpg'',sep="")  
        print(dest_filename, quote=FALSE);  
        jpeg(filename=dest_filename);  
        hist(InputDataSet$tipped, col = ''lightgreen'', xlab=''Tipped'',   
            ylab = ''Counts'', main = ''Histogram, Tipped'');  
         dev.off();  

        # Open a pdf file and output histograms of tip amount and fare amount.   
        # Outputs two plots in one row  
        dest_filename = tempfile(pattern = ''rHistograms_Tip_and_Fare_Amount_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.pdf'',sep="")  
        print(dest_filename, quote=FALSE);  
        pdf(file=dest_filename, height=4, width=7);  
        par(mfrow=c(1,2));  
        hist(InputDataSet$tip_amount, col = ''lightgreen'',   
            xlab=''Tip amount ($)'',   
            ylab = ''Counts'',   
            main = ''Histogram, Tip amount'', xlim = c(0,40), 100);  
        hist(InputDataSet$fare_amount, col = ''lightgreen'',   
            xlab=''Fare amount ($)'',   
            ylab = ''Counts'',   
            main = ''Histogram,   
            Fare amount'',   
            xlim = c(0,100), 100);  
       dev.off();  
  
        # Open a pdf file and output an xyplot of tip amount vs. fare amount using lattice;  
        # Only 10,000 sampled observations are plotted here, otherwise file is large.  
        dest_filename = tempfile(pattern = ''rXYPlots_Tip_vs_Fare_Amount_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.pdf'',sep="")  
        print(dest_filename, quote=FALSE);  
        pdf(file=dest_filename, height=4, width=4);  
        plot(tip_amount ~ fare_amount,   
            data = InputDataSet[sample(nrow(InputDataSet), 10000), ],   
            ylim = c(0,50),   
            xlim = c(0,150),   
            cex=.5,   
            pch=19,   
            col=''darkgreen'',    
            main = ''Tip amount by Fare amount'',   
            xlab=''Fare Amount ($)'',   
            ylab = ''Tip Amount ($)'');   
        dev.off();',  
     @input_data_1 = @query  
     END
    ```
  
    -   預存程序內 SELECT 查詢的輸出會儲存在預設 R 資料框架 `InputDataSet`中。 接著可以呼叫各種 R 繪製函數，以產生實際圖形檔。
  
        大部分的內嵌 R 指令碼代表這些圖形函數的選項 (例如 `plot` 或 `hist`)。
  
    -   所有檔案都會儲存至本機資料夾 _C:\temp\Plots\\_。 目的地資料夾是透過執行預存程序時提供給 R 指令碼的引數所定義。  變更 `mainDir`變數的值，即可變更目的地資料夾。
  
2.  請執行陳述式以建立預存程序。

    ```SQL
    EXEC PlotInOutputFiles
    ```

    **結果**
    
    ```
    STDOUT message(s) from external script:
    [1] Creating output plot files:[1] C:\temp\plots\rHistogram_Tipped_18887f6265d4.jpg[1] 
    
    C:\temp\plots\rHistograms_Tip_and_Fare_Amount_1888441e542c.pdf[1]
    
    C:\temp\plots\rXYPlots_Tip_vs_Fare_Amount_18887c9d517b.pdf
    ```

    以確保您不能取得錯誤時嘗試寫入至現有的檔案，會隨機產生的檔案名稱中的數字。

3. 若要檢視繪圖，開啟目的地資料夾，並檢視所建立的預存程序中的 R 程式碼的檔案。

    + 檔案`rHistogram_Tipped.jpg`顯示收到的提示與有沒有提示往返的往返次數。 （這個長條圖是非常類似您在上一個步驟中產生的一個）。

    + 檔案`rHistograms_Tip_and_Fare_Amount.pdf`顯示的提示數量，根據價位金額繪製分佈。
    
    ![長條圖顯示 tip_amount 和 fare_amount](media/rsql-devtut-tipamtfareamt.PNG "長條圖顯示 tip_amount 和 fare_amount")

    + 檔案`rXYPlots_Tip_vs_Fare_Amount.pdf`包含 scatterplot 價位量 x 軸和 y 軸上的提示數量。

    ![提示量繪製超過價位量](media/rsql-devtut-tipamtbyfareamt.PNG "提示量繪製超過價位量")

2.  若要將檔案輸出至不同的資料夾，請變更預存程序中所內嵌 R 指令碼內的 `mainDir` 變數值。 您也可以修改指令碼來輸出不同的格式、多個檔案等。

## <a name="next-lesson"></a>下一課

[第 4 課： 建立使用 T-SQL 資料功能](../tutorials/sqldev-create-data-features-using-t-sql.md)

## <a name="previous-lesson"></a>上一課

[第 2 課： 將資料匯入 SQL Server 使用 PowerShell](../r/sqldev-import-data-to-sql-server-using-powershell.md)
