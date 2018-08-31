---
title: 課程 3 的瀏覽和使用 R 和 T-SQL (SQL Server Machine Learning) 將資料視覺化 |Microsoft Docs
description: 教學課程示範如何在 SQL Server 中內嵌 R 預存程序和 T-SQL 函數
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6b34de3c71629a1563bf0d480306680dc6253748
ms.sourcegitcommit: 320958d0f55b6974abf46f8a04f7a020ff86a0ae
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/23/2018
ms.locfileid: "42703621"
---
# <a name="lesson-3-explore-and-visualize-the-data"></a>第 3 課： 瀏覽及視覺化資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章是有關如何在 SQL Server 中使用 R 的 SQL 開發人員的教學課程的一部分。

在這一課，您將檢閱範例資料，並接著產生使用一些繪圖[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)從[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)及 泛型[Hist](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/hist)基底函式中已包含這些 R 函數[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。

索引鍵的目標示範如何呼叫 R 函數，從[!INCLUDE[tsql](../../includes/tsql-md.md)]預存程序，並儲存應用程式檔案格式中的結果：

+ 建立預存程序，使用**RxHistogram**產生 R 繪圖做為 varbinary 資料。 使用**bcp**匯出至影像檔的二進位資料流。
+ 建立預存程序，使用**Hist**來產生繪圖，將結果儲存為 JPG 和 PDF 的輸出。

> [!NOTE]
> 視覺效果是這類強大的工具來了解資料圖形和通訊群組，因為 R 提供的各種函式與封裝產生長條圖、 散佈圖、 方塊繪圖和其他資料瀏覽圖形。 R 通常會建立使用圖形化的輸出，您可以擷取並儲存為 R 裝置的映像**varbinary**轉譯應用程式中的資料類型。 您也可以將映像儲存到任何支援檔案格式 (。JPG、。PDF 等）。

## <a name="review-the-data"></a>檢閱資料

開發資料科學方案通常會包含大量資料瀏覽和資料視覺化。 因此先花點時間檢閱範例資料，如果您還沒有這麼做。

在原始資料集中，計程車識別碼和車程記錄會提供在不同的檔案中。 不過，若要讓您更輕鬆地使用的範例資料，兩個原始資料集已加入的資料行_medallion_， _hack\_授權_，和_pickup\_datetime_。  也會對記錄進行抽樣，只取得 1% 的原始記錄數目。 產生的向下取樣資料集有 1,703,957 個資料列和 23 個資料行。

**計程車識別碼**
  
-   _medallion_ 資料行代表計程車的唯一識別碼。
  
-   _Hack\_授權_資料行包含計程車司機駕照號碼 （匿名）。
  
**車程和小費記錄**
  
-   每筆車程記錄都會包含上車和下車位置與時間，以及車程距離。
  
-   每筆費用記錄都會包括付款資訊，例如付款類型、總付款金額和小費金額。
  
-   最後三個資料行可以用於各種機器學習工作。 _祕訣\_數量_資料行包含連續數值，並可用來當做**標籤**迴歸分析的資料行。 _tipped_ 資料行只有是/否值，並且用於二元分類。 _祕訣\_類別_資料行有多個**類別標籤**，因此可以使用做為標籤的多類別分類工作。
  
    這個逐步解說只會示範二元分類工作；您可以自由地嘗試建立其他兩個機器學習工作 (迴歸和多類別分類) 的模型。
  
-   用於標籤資料行的值都以_祕訣\_數量_資料行中，使用這些商務規則：
  
    |衍生的資料行名稱|規則|
    |-|-|
     |tipped|If tip_amount > 0, tipped = 1, otherwise tipped = 0|
    |tip_class|Class 0: tip_amount = $0<br /><br />Class 1: tip_amount > $0 and tip_amount <= $5<br /><br />Class 2: tip_amount > $5 and tip_amount <= $10<br /><br />Class 3: tip_amount > $10 and tip_amount <= $20<br /><br />Class 4: tip_amount > $20|

## <a name="create-a-stored-procedure-using-rxhistogram-to-plot-the-data"></a>建立預存程序使用 rxHistogram 繪製資料

若要建立繪圖，請使用[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)，其中一個增強型 R 函數中提供[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)。 此步驟中繪製的長條圖，根據資料[!INCLUDE[tsql](../../includes/tsql-md.md)]查詢。 您可以將此函式包裝在預存程序中， **PlotHistogram**。

1. 在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，請在物件總管 中以滑鼠右鍵按一下**NYCTaxi_Sample**資料庫中，展開**可程式性**，然後展開**預存程序**檢視在第 2 課建立的程序。

2. 以滑鼠右鍵按一下**PlotHistogram** ，然後選取**修改**檢視的來源。 您可以執行此程序來呼叫**rxHistogram** nyctaxi_sample 資料表已支付小費資料行中包含的資料。

3. 選擇性地學習練習中，建立您自己的複本，此預存程序，使用下列的範例。 開啟新的查詢視窗並貼上下列指令碼建立預存程序繪製的長條圖。 此範例中名為**PlotHistogram2**以避免命名衝突的既有的程序。

    ```SQL
    CREATE PROCEDURE [dbo].[PlotHistogram2]
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

預存程序**PlotHistogram2**等同於預先存在的預存程序**PlotHistogram**由`RunSQL_SQL_Walkthrough.ps1`指令碼。 
  
+ `@query` 變數會定義查詢文字 (`'SELECT tipped FROM nyctaxi_sample'`)，以當成指令碼輸入變數 `@input_data_1`的引數傳遞給 R 指令碼。
  
+ R 指令碼是相當簡單： R 變數 (`image_file`) 來定義映像，然後**rxHistogram**函式呼叫來產生繪圖。
  
+ R 裝置設定為**關閉**因為您以 SQL Server 中的外部指令碼來執行此命令。 通常在 R 中，當您發出高階繪製命令時，R 會開啟 [圖形] 視窗中，呼叫*裝置*。 您可以變更視窗的大小、色彩和其他層面，也可以在寫入至檔案或透過其他方法處理輸出時關閉裝置。
  
+ R 圖形物件會序列化為 R data.frame 以進行輸出。

### <a name="execute-the-stored-procedure-and-use-bcp-to-export-binary-data-to-an-image-file"></a>執行預存程序，並使用 bcp 匯出至影像檔的二進位資料

預存程序會以您明顯無法直接檢視的 varbinary 資料流形式傳回影像。 不過，您可以使用 **bcp** 公用程式來取得 varbinary 資料，並將它儲存為用戶端電腦上的影像檔。
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，執行下列陳述式：
  
    ```SQL
    EXEC [dbo].[PlotHistogram]
    ```
  
    **結果**
    
    *繪圖*
    *0xFFD8FFE000104A4649...*
  
2.  開啟 PowerShell 命令提示字元並執行下列命令，並提供適當的執行個體名稱、 資料庫名稱、 使用者名稱和認證做為引數。 對於使用 Windows 身分識別，您可以取代 **-U**並 **-P**具有 **-T**。
  
     ```text
     bcp "exec PlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  TaxiNYC_Sample  -U <user name> -P <password>
     ```

    > [!NOTE]
    > 如果是 bcp 命令參數會區分大小寫。
  
3.  如果連接成功，系統會提示您輸入圖形檔格式的詳細資訊。 

   在每個提示字元下，按 ENTER 接受預設值，但不包括這些變更：
    
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
  
## <a name="create-a-stored-procedure-using-hist-and-multiple-output-formats"></a>建立預存程序使用 Hist 和多個輸出格式

一般而言，資料科學家會產生多個資料視覺效果，以取得深入了解資料從不同的角度。 在此範例中，預存程序會使用 Hist 函式建立的長條圖，例如將二進位資料匯出至熱門的格式。JPG、。PDF、 和。PNG。 

1. 使用現有的預存程序， **PlotInOutputFiles**、 長條圖、 散佈和其他 R 圖形來撰寫。JPG 和。PDF 格式。 `RunSQL_SQL_Walkthrough.ps1`會建立**PlotInOutputFiles**並將它加入資料庫。 使用滑鼠右鍵按一下**修改**檢視的來源。

2. 選擇性地學習練習中，建立您自己的程序的複本**PlotInOutputFiles2**，以避免命名衝突的唯一名稱。

    在  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，開啟新**查詢**視窗中，並貼上下列[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式。
  
    ```SQL
    CREATE PROCEDURE [dbo].[PlotInOutputFiles2]  
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
  
+ 預存程序內 SELECT 查詢的輸出會儲存在預設 R 資料框架 `InputDataSet`中。 接著可以呼叫各種 R 繪製函數，以產生實際圖形檔。 大部分的內嵌 R 指令碼代表這些圖形函數的選項 (例如 `plot` 或 `hist`)。
  
+ 所有檔案都會儲存至本機資料夾 _C:\temp\Plots\\_。 目的地資料夾是透過執行預存程序時提供給 R 指令碼的引數所定義。  變更 `mainDir`變數的值，即可變更目的地資料夾。

+ 若要將檔案輸出至不同的資料夾，請變更預存程序中所內嵌 R 指令碼內的 `mainDir` 變數值。 您也可以修改指令碼來輸出不同的格式、多個檔案等。

### <a name="execute-the-stored-procedure"></a>執行預存程序

執行下列陳述式，將二進位繪圖資料匯出至 JPEG 和 PDF 檔案格式。

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

若要確保您不想要撰寫到現有的檔案時可能會發生錯誤，會隨機產生的檔案名稱中的數字。

### <a name="view-output"></a>檢視輸出 

若要檢視繪圖，開啟目的地資料夾，並檢閱檔案所建立的預存程序中的 R 程式碼。

1. 移的 STDOUT 訊息中指定的資料夾 （在此範例中，這是 C:\temp\plots\)

2. 開啟`rHistogram_Tipped.jpg`顯示收到小費的車程和小費的車程數目。 （此長條圖是十分類似您在上一個步驟中產生）。

3. 開啟`rHistograms_Tip_and_Fare_Amount.pdf`檢視發佈的小費金額、 小費金額相對繪製成圖形。
    
  ![長條圖顯示 tip_amount 和 fare_amount](media/rsql-devtut-tipamtfareamt.PNG "長條圖顯示 tip_amount 和 fare_amount")

4. 開啟`rXYPlots_Tip_vs_Fare_Amount.pdf`檢視費用金額的散佈圖 x 軸和 y 軸為小費金額。

   ![小費金額繪製費用金額 over](media/rsql-devtut-tipamtbyfareamt.PNG "繪製費用金額透過的小費金額")

## <a name="next-lesson"></a>下一課

[第 3 課： 建立使用 T-SQL 的資料特徵](sqldev-create-data-features-using-t-sql.md)

## <a name="previous-lesson"></a>上一課

[NYC 計程車示範資料的第 1 課： 設定](sqldev-download-the-sample-data.md)
