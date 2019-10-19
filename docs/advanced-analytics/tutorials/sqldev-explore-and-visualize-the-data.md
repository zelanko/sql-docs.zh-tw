---
title: 第1課：使用 R 和 T-sql 探索資料並加以視覺化
description: 教學課程示範如何使用 R 函數探索 SQL Server 資料並加以視覺化。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2c204e06edd830d8036b6d0119ce1aff1a9c6833
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/17/2019
ms.locfileid: "68715374"
---
# <a name="lesson-1-explore-and-visualize-the-data"></a>第1課：探索資料並加以視覺化
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文是有關如何在 SQL Server 中使用 R 的 SQL 開發人員教學課程的一部分。

在此步驟中，您將會查看範例資料，然後使用[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) from [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)和 base R 中的泛型[歷程](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/hist)函式來產生一些繪圖。這些 R 函數已包含在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中。

本課程的主要目標是示範如何從預存程式中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 呼叫 R 函數，並將結果儲存為應用程式檔案格式：

+ 使用**RxHistogram**建立預存程式，以產生 R 繪圖做為 Varbinary 資料。 使用**bcp**將二進位資料流程匯出至影像檔案。
+ 使用**歷程**建立預存程式來產生繪圖，並將結果儲存為 JPG 和 PDF 輸出。

> [!NOTE]
> 因為視覺效果是用來瞭解資料圖形和分佈的強大工具，所以 R 提供了各種函式和封裝來產生長條圖、散佈圖、盒狀圖和其他資料流覽圖形。 R 通常會使用適用于圖形化輸出的 R 裝置來建立影像，您可以將其捕捉並儲存為**Varbinary**資料類型，以便在應用程式中呈現。 您也可以將影像儲存為任何支援檔案格式（。JPG、。PDF 等等）。

## <a name="review-the-data"></a>檢查資料

開發資料科學方案通常會包含大量資料瀏覽和資料視覺化。 首先，請花幾分鐘的時間來審查範例資料（如果您尚未這麼做）。

在原始的公用資料集中，計程車識別碼和旅程記錄是在不同的檔案中提供。 不過，為了讓範例資料更容易使用，這兩個原始資料集已聯結在資料行_medallion_、_駭客 \_license_和_pickup \_datetime_上。  也會對記錄進行抽樣，只取得 1% 的原始記錄數目。 產生的向下取樣資料集有 1,703,957 個資料列和 23 個資料行。

**計程車識別碼**
  
-   _Medallion_資料行代表計程車的唯一識別碼。
  
-   [_駭客 \_license_ ] 資料行包含計程車駕駛的授權號碼（匿名）。
  
**車程和小費記錄**
  
-   每筆車程記錄都會包含上車和下車位置與時間，以及車程距離。
  
-   每筆費用記錄都會包括付款資訊，例如付款類型、總付款金額和小費金額。
  
-   最後三個資料行可以用於各種機器學習工作。 _Tip \_amount_資料行包含連續數值，而且可用來做為迴歸分析的**標籤**資料行。 _tipped_ 資料行只有是/否值，並且用於二元分類。 _Tip \_class_資料行有多個**類別標籤**，因此可用來做為多類別分類工作的標籤。
  
    這個逐步解說只會示範二元分類工作；您可以自由地嘗試建立其他兩個機器學習工作 (迴歸和多類別分類) 的模型。
  
-   標籤資料行所使用的值都是以 [ _tip \_amount_ ] 資料行為基礎，使用下列商務規則：
  
    |衍生的資料行名稱|規則|
    |-|-|
     |tipped|If tip_amount > 0, tipped = 1, otherwise tipped = 0|
    |tip_class|Class 0: tip_amount = $0<br /><br />Class 1: tip_amount > $0 and tip_amount <= $5<br /><br />Class 2: tip_amount > $5 and tip_amount <= $10<br /><br />Class 3: tip_amount > $10 and tip_amount <= $20<br /><br />Class 4: tip_amount > $20|

## <a name="create-a-stored-procedure-using-rxhistogram-to-plot-the-data"></a>使用 rxHistogram 建立預存程式以繪製資料

若要建立繪圖，請使用[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)，這是[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)中提供的其中一個增強型 R 函數。 此步驟會根據 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢中的資料來繪製長條圖。 您可以將此函式包裝在預存程式**PlotRxHistogram**中。

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的物件總管中，以滑鼠右鍵按一下**NYCTaxi_Sample**資料庫，然後選取 [追加**查詢**]。

2. 貼上下列腳本，以建立繪製長條圖的預存程式。 這個範例名為 **RPlotRxHistogram*。

    ```sql
    CREATE PROCEDURE [dbo].[RxPlotHistogram]
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

在此腳本中可瞭解的重點包括下列各項： 
  
+ `@query` 變數會定義查詢文字 (`'SELECT tipped FROM nyctaxi_sample'`)，以當成指令碼輸入變數 `@input_data_1`的引數傳遞給 R 指令碼。 針對當做外部進程執行的 R 腳本，您應該在腳本的輸入之間有一對一的對應，以及在 SQL Server 上啟動 R 會話的[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)系統預存程式的輸入。
  
+ 在 R 腳本中，會定義變數（`image_file`）來儲存影像。 

+ 會呼叫 RevoScaleR 程式庫中的**rxHistogram**函式來產生繪圖。
  
+ R 裝置設定為**off** ，因為您是以 SQL Server 的外部腳本執行此命令。 一般來說，在 R 中，當您發出高階繪製命令時，R 會開啟一個圖形視窗，稱為「*裝置*」。 如果您要寫入檔案或以其他方式處理輸出，您可以關閉裝置。
  
+ R 圖形物件會序列化為 R data.frame 以進行輸出。

### <a name="execute-the-stored-procedure-and-use-bcp-to-export-binary-data-to-an-image-file"></a>執行預存程式，並使用 bcp 將二進位資料匯出至影像檔案

預存程序會以您明顯無法直接檢視的 varbinary 資料流形式傳回影像。 不過，您可以使用 **bcp** 公用程式來取得 varbinary 資料，並將它儲存為用戶端電腦上的影像檔。
  
1. 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，執行下列陳述式：
  
    ```sql
    EXEC [dbo].[RxPlotHistogram]
    ```
  
    **結果**
    
    *繪製* *0xFFD8FFE000104A4649 ...*
  
2. 開啟 PowerShell 命令提示字元，並執行下列命令，並提供適當的實例名稱、資料庫名稱、使用者名稱和認證做為引數。 對於使用 Windows 身分識別的使用者，您可以使用- **T**取代 **-U**和 **-P** 。
  
    ```powershell
    bcp "exec RxPlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  NYCTaxi_Sample  -U <user name> -P <password> -T
    ```

    > [!NOTE]
    > Bcp 的命令參數會區分大小寫。
  
3. 如果連接成功，系統會提示您輸入圖形檔格式的詳細資訊。 

   在每個提示字元下，按 ENTER 接受預設值，但不包括這些變更：
    
   + 在 **prefix-length of field plot**中，輸入 0。
  
   + 如果您想要儲存輸出參數以供日後重複使用，請輸入 **Y** 。
  
    ```powershell
    Enter the file storage type of field plot [varbinary(max)]: 
    Enter prefix-length of field plot [8]: 0
    Enter length of field plot [0]:
    Enter field terminator [none]:
  
    Do you want to save this format information in a file? [Y/n]
    Host filename [bcp.fmt]:
    ```
  
    **結果**
    
    ```powershell
    Starting copy...
    1 rows copied.
    Network packet size (bytes): 4096
    Clock Time (ms.) Total     : 3922   Average : (0.25 rows per sec.)
    ```

    > [!TIP]
    > 如果您將格式資訊儲存至檔案 (bcp.fmt)，則 **bcp** 公用程式會產生您未來可套用至類似命令的格式定義，而不提示您輸入圖形檔格式選項。 若要使用格式檔案，請在 password 引數之後將 `-f bcp.fmt` 新增至任何命令列結尾。
  
4.  將會在執行 PowerShell 命令的相同目錄中建立輸出檔案。 若要檢視繪圖，只需要開啟檔案 plot.jpg。
  
    ![計程車行程和沒有秘訣](media/rsql-devtut-tippedornot.jpg "計程車行程和沒有秘訣")  
  
## <a name="create-a-stored-procedure-using-hist-and-multiple-output-formats"></a>使用歷程和多個輸出格式來建立預存程式

一般而言，資料科學家會產生多個資料視覺效果，以從不同的角度取得資料的深入解析。 在此範例中，您將建立名為**RPlotHist**的預存程式，以將長條圖、散佈圖和其他 R 圖形寫入至。JPG 和。PDF 格式。

這個預存程式會使用**歷程**函數來建立長條圖，將二進位資料匯出為常用的格式，例如。JPG、。PDF 和。PNG. 

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的物件總管中，以滑鼠右鍵按一下**NYCTaxi_Sample**資料庫，然後選取 [追加**查詢**]。

2. 貼上下列腳本，以建立繪製長條圖的預存程式。 這個範例的名稱是**RPlotHist** 。
  
    ```sql
    CREATE PROCEDURE [dbo].[RPlotHist]  
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
  
+ 所有檔案都會儲存到本機資料夾 C:\temp\Plots。 目的地資料夾是透過執行預存程序時提供給 R 指令碼的引數所定義。  變更 `mainDir`變數的值，即可變更目的地資料夾。

+ 若要將檔案輸出至不同的資料夾，請變更預存程序中所內嵌 R 指令碼內的 `mainDir` 變數值。 您也可以修改指令碼來輸出不同的格式、多個檔案等。

### <a name="execute-the-stored-procedure"></a>執行預存程序

執行下列語句，將二進位繪圖資料匯出為 JPEG 和 PDF 檔案格式。

```sql
EXEC RPlotHist
```

**結果**
    
```sql
STDOUT message(s) from external script:
[1] Creating output plot files:[1] C:\temp\plots\rHistogram_Tipped_18887f6265d4.jpg[1] 

C:\temp\plots\rHistograms_Tip_and_Fare_Amount_1888441e542c.pdf[1]

C:\temp\plots\rXYPlots_Tip_vs_Fare_Amount_18887c9d517b.pdf
```

檔案名中的數位會隨機產生，以確保您在嘗試寫入至現有的檔案時，不會收到錯誤。

### <a name="view-output"></a>視圖輸出 

若要觀看繪圖，請開啟 [目的地] 資料夾，然後在預存程式中檢查 R 程式碼所建立的檔案。

1. 移至 STDOUT 訊息中指示的資料夾（在此範例中為 C:\temp\plots \)

2. 開啟 `rHistogram_Tipped.jpg` 以顯示有提示的行程數與沒有提示的行程。 （此長條圖與您在上一個步驟中產生的類似。）

3. 開啟 `rHistograms_Tip_and_Fare_Amount.pdf` 以查看 tip 金額的分佈，並根據費用金額繪製。
    
  ![顯示 tip_amount 和 fare_amount 的長條圖](media/rsql-devtut-tipamtfareamt.PNG "顯示 tip_amount 和 fare_amount 的長條圖")

4. 開啟 `rXYPlots_Tip_vs_Fare_Amount.pdf` 以在 X 軸上查看費用量，並在 y 軸上散佈圖的刀尖數量。

   ![以費用金額繪製的秘訣數量](media/rsql-devtut-tipamtbyfareamt.PNG "以費用金額繪製的秘訣數量")

## <a name="next-lesson"></a>下一課

[第2課：使用 T-sql 建立資料特徵](sqldev-create-data-features-using-t-sql.md)

## <a name="previous-lesson"></a>上一課

[設定 NYC 計程車示範資料](demo-data-nyctaxi-in-sql.md)
