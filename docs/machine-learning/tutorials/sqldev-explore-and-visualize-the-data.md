---
title: R + T-SQL 教學課程：探索資料
description: 教學課程說明如何使用 R 函數探索及視覺化 SQL Server 資料。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 03/03/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: bc5434483fd6f63a73362fb42b1bd17aa749ebd3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85757105"
---
# <a name="lesson-1-explore-and-visualize-the-data"></a>第 1 課：探索及視覺化資料
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

本篇教學課程文章適用 SQL 開發人員，說明如何在 SQL Server 中使用 R。

您會在此步驟中查看範例資料，然後使用 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 提供的 [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) 以及基礎 R 中的泛型 [Hist](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/hist) 函數建立一些繪圖。這些 R 函數已包含在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中。

本課程的主要目標是示範如何從預存程序中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 呼叫 R 函數，並將結果儲存為應用程式檔案格式：

+ 使用 **RxHistogram** 來建立預存程序，以產生 R 繪圖做為 Varbinary 資料。 使用 **bcp** 將二進位資料流匯出至影像檔案。
+ 使用 **Hist** 建立預存程序以產生繪圖，並將結果儲存為 JPG 和 PDF 輸出。

> [!NOTE]
> 由於可透過視覺效果這項強大工具了解資料圖形和分佈，因此 R 提供了各種函數和封裝來產生長條圖、散佈圖、盒狀圖及其他資料探索圖表。 R 通常會使用 R 裝置來建立影像以進行圖形化輸出，您可以擷取後儲存為 **Varbinary** 資料類型，以便在應用程式中轉譯。 您也可以將影像儲存為任何支援的檔案格式 (.JPG、.PDF 等)。

## <a name="review-the-data"></a>檢閱資料

開發資料科學方案通常會包含大量資料瀏覽和資料視覺化。 首先，需要一分鐘的時間來檢閱範例資料 (如果您還沒檢閱)。

在原始的公用資料集中，計程車識別碼和車程記錄會以不同檔案提供。 不過，為了更輕鬆地使用範例資料，已根據 _medallion_、_hack\_license_ 和 _pickup\_datetime_ 資料行來聯結兩個原始資料集。  也會對記錄進行抽樣，只取得 1% 的原始記錄數目。 產生的向下取樣資料集有 1,703,957 個資料列和 23 個資料行。

**計程車識別碼**
  
-   _medallion_ 資料行代表計程車的唯一識別碼。
  
-   _hack\_license_ 資料行包含計程車司機駕照號碼 (匿名)。
  
**車程和小費記錄**
  
-   每筆車程記錄都會包含上車和下車位置與時間，以及車程距離。
  
-   每筆費用記錄都會包括付款資訊，例如付款類型、總付款金額和小費金額。
  
-   最後三個資料行可以用於各種機器學習工作。 _tip\_amount_ 資料行包含連續數值，而且可以當成 **label** 資料行來進行迴歸分析。 _tipped_ 資料行只有是/否值，並且用於二元分類。 _tip\_class_ 資料行有多個**類別標籤**，因此可以當成多類別分類工作的標籤使用。
  
    這個逐步解說只會示範二元分類工作；您可以自由地嘗試建立其他兩個機器學習工作 (迴歸和多類別分類) 的模型。
  
-   使用以下商務規則而用於標籤資料行的值都是根據 _tip\_amount_ 資料行：
  
    |衍生的資料行名稱|規則|
    |-|-|
     |tipped|If tip_amount > 0, tipped = 1, otherwise tipped = 0|
    |tip_class|Class 0: tip_amount = $0<br /><br />Class 1: tip_amount > $0 and tip_amount <= $5<br /><br />Class 2: tip_amount > $5 and tip_amount <= $10<br /><br />Class 3: tip_amount > $10 and tip_amount <= $20<br /><br />Class 4: tip_amount > $20|

## <a name="create-a-stored-procedure-using-rxhistogram-to-plot-the-data"></a>使用 rxHistogram 建立預存程序，以繪製資料

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!IMPORTANT]
> 從 SQL Server 2019 開始，隔離機制已經變更。 因此您必須授與繪圖檔案所在目錄的適當權限。 如需有關如何設定這些權限的詳細資訊，請參閱 [Windows 上 SQL Server 2019 中的檔案權限區段：機器學習服務的隔離變更](../install/sql-server-machine-learning-services-2019.md#file-permissions)
::: moniker-end

若要建立繪圖，請使用 [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)，這是 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 中提供的一個增強型 R 函數。 此步驟會根據 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢提供的資料繪製長條圖。 您可以將此函式包裝在預存程序 (**RxPlotHistogram**) 中。

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的物件總管中，以滑鼠右鍵按一下 **NYCTaxi_Sample** 資料庫，然後選取 [新查詢]  。

2. 貼上下列指令碼，建立繪製長條圖的預存程序。 此範例的名稱是 **RxPlotHistogram**。

    ```sql
    CREATE PROCEDURE [dbo].[RxPlotHistogram]
    AS
    BEGIN
      SET NOCOUNT ON;
      DECLARE @query nvarchar(max) =  
      N'SELECT tipped FROM [dbo].[nyctaxi_sample]'  
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

此指令碼中需了解的重點包括下列各項： 
  
+ `@query` 變數會定義查詢文字 (`'SELECT tipped FROM nyctaxi_sample'`)，以當成指令碼輸入變數 `@input_data_1`的引數傳遞給 R 指令碼。 若是以外部程序執行的 R 指令碼，在指令碼輸入，以及在 SQL Server 上啟動 R 工作階段的 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 系統預存程序輸入之間，應該要有一對一的對應。
  
+ 在 R 指令碼中，會定義變數 (`image_file`) 以儲存影像。 

+ 呼叫 RevoScaleR 程式庫的 **rxHistogram** 函數，以產生繪圖。
  
+ R 裝置設定為 [關閉]  ，因為您是以 SQL Server 中的外部指令碼執行此命令。 一般來說，當您在 R 中發出高階繪製命令時，R 將會開啟稱為「裝置」  的圖形視窗。 如果您要寫入檔案或以其他方式處理輸出，可以關閉裝置。
  
+ R 圖形物件會序列化為 R data.frame 以進行輸出。

### <a name="execute-the-stored-procedure-and-use-bcp-to-export-binary-data-to-an-image-file"></a>執行預存程序，並使用 bcp 將二進位資料匯出至影像檔案

預存程序會以您明顯無法直接檢視的 varbinary 資料流形式傳回影像。 不過，您可以使用 **bcp** 公用程式來取得 varbinary 資料，並將它儲存為用戶端電腦上的影像檔。
  
1. 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，執行下列陳述式：
  
    ```sql
    EXEC [dbo].[RxPlotHistogram]
    ```
  
    **結果**
    
    *plot* *0xFFD8FFE000104A4649...*
  
2. 開啟 PowerShell 命令提示字元，並將適當的執行個體名稱、資料庫名稱、使用者名稱和認證提供為引數來執行下列命令。 若是使用 Windows 身分識別的使用者，您可以使用 **-T** 取代 **-U** 和 **-P**。
  
    ```powershell
    bcp "exec RxPlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  NYCTaxi_Sample  -U <user name> -P <password> -T
    ```

    > [!NOTE]
    > bcp 的命令參數區分大小寫。
  
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
  
    ![含/不含小費的計程車車程](media/rsql-devtut-tippedornot.jpg "含/不含小費的計程車車程")  
  
## <a name="create-a-stored-procedure-using-hist-and-multiple-output-formats"></a>使用 Hist 和多種輸出格式來建立預存程序

資料科學家通常會產生多個資料視覺效果，從不同的角度深入了解資料。 在此範例中，您將建立名為 **RPlotHist** 的預存程序，並且將長條圖、散佈圖及其他 R 圖形寫成 .JPG 和 .PDF 格式。

這個預存程序會使用 **Hist** 函數來建立長條圖，將二進位資料匯出成常用的格式，例如 .JPG、.PDF 及 .PNG。 

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的物件總管中，以滑鼠右鍵按一下 **NYCTaxi_Sample** 資料庫，然後選取 [新查詢]  。

2. 貼上下列指令碼，建立繪製長條圖的預存程序。 此範例的名稱是 **RPlotHist**。
  
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
  
+ 所有檔案都會儲存至本機資料夾 C:\temp\Plots。 目的地資料夾是透過執行預存程序時提供給 R 指令碼的引數所定義。  變更 `mainDir`變數的值，即可變更目的地資料夾。

+ 若要將檔案輸出至不同的資料夾，請變更預存程序中所內嵌 R 指令碼內的 `mainDir` 變數值。 您也可以修改指令碼來輸出不同的格式、多個檔案等。

### <a name="execute-the-stored-procedure"></a>執行預存程序

執行下列陳述式，將二進位繪圖資料匯出成 JPEG 和 PDF 檔案格式。

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

檔案名稱中的字數會隨機產生，確保不會因嘗試寫入現有檔案而發生錯誤。

### <a name="view-output"></a>檢視輸出 

若要檢視繪圖，請開啟目的地資料夾，並檢閱預存程序中 R 程式碼所建立的檔案。

1. 前往 STDOUT 訊息中指示的資料夾 (在此範例中是 C:\temp\plots\)

2. 開啟 `rHistogram_Tipped.jpg`，顯示收到的小費與未收到小費的車程數目。 (這個長條圖與您在上一個步驟中所產生的長條圖十分類似。)

3. 開啟 `rHistograms_Tip_and_Fare_Amount.pdf`，查看根據費用金額繪製的小費金額分佈狀況。
    
  ![顯示 tip_amount 和 fare_amount 的長條圖](media/rsql-devtut-tipamtfareamt.PNG "顯示 tip_amount 和 fare_amount 的長條圖")

4. 開啟 `rXYPlots_Tip_vs_Fare_Amount.pdf`，檢視 x 軸為費用金額且 y 軸為小費金額的散佈圖。

   ![根據費用金額繪製的小費金額](media/rsql-devtut-tipamtbyfareamt.PNG "根據費用金額繪製的小費金額")

## <a name="next-lesson"></a>下一課

[第 2 課：使用 T-SQL 建立資料特徵](sqldev-create-data-features-using-t-sql.md)

## <a name="previous-lesson"></a>上一課

[設定紐約市計程車示範資料](demo-data-nyctaxi-in-sql.md)
