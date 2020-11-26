---
title: R 教學課程：探索及視覺化資料
titleSuffix: SQL machine learning
description: 探索範例資料並產生一些繪圖，以準備使用 R 的二元分類搭配 SQL 機器學習。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/15/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||>=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: cba06a816e57189cb69f9680542452d2788b233e
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "92412525"
---
# <a name="r-tutorial-explore-and-visualize-data"></a>R 教學課程：探索及視覺化資料
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

在這個五部分教學課程系列的第二部分中，您已探索範例資料並產生一些繪圖。 稍後，您將了解如何在 Python 中序列化繪圖物件，然後將這些物件還原序列化並製作繪圖。

在這五集教學課程系列的第二集中，您要檢閱範例資料，然後使用基礎 R 中的泛型 `barplot` 和 `hist` 函數產生一些繪圖。

本文的主要目標是示範如何從預存程序中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 呼叫 R 函式，並將結果儲存為應用程式檔案格式：

+ 使用 `barplot` 來建立預存程序，以產生 R 繪圖做為 Varbinary 資料。 使用 **bcp** 將二進位資料流匯出至影像檔案。
+ 使用 `hist` 建立預存程序以產生繪圖，並將結果儲存為 JPG 和 PDF 輸出。

> [!NOTE]
> 由於可透過視覺效果這項強大工具了解資料圖形和分佈，因此 R 提供了各種函數和封裝來產生長條圖、散佈圖、盒狀圖及其他資料探索圖表。 R 通常會使用 R 裝置來建立影像以進行圖形化輸出，您可以擷取後儲存為 **Varbinary** 資料類型，以便在應用程式中轉譯。 您也可以將影像儲存為任何支援的檔案格式 (.JPG、.PDF 等)。

在本文中，您將：

> [!div class="checklist"]
> + 檢閱範例資料
> + 在 T-SQL 中使用 R 建立繪圖
> + 以多種檔案格式輸出繪圖

在[第一部分](r-taxi-classification-introduction.md)中，您已安裝必要條件並還原範例資料庫。

在[第三部分](r-taxi-classification-create-features.md)中，您將了解如何使用 Transact-SQL 函式，從未經處理的資料建立特徵。 接著您將從預存程序呼叫該函數，以建立包含特徵值的資料表。

在[第四部分](r-taxi-classification-train-model.md)中，您將載入模組，並呼叫所需的函式，以使用 SQL Server 預存程序來建立和定型模型。

在[第五部分](r-taxi-classification-deploy-model.md)中，您將了解如何運作您在第四部分中定型並儲存的模型。

## <a name="review-the-data"></a>檢閱資料

開發資料科學方案通常會包含大量資料瀏覽和資料視覺化。 首先，需要一分鐘的時間來檢閱範例資料 (如果您還沒檢閱)。

在原始的公用資料集中，計程車識別碼和車程記錄會以不同檔案提供。 不過，為了更輕鬆地使用範例資料，已根據 _medallion_、_hack\_license_ 和 _pickup\_datetime_ 資料行來聯結兩個原始資料集。  也會對記錄進行抽樣，只取得 1% 的原始記錄數目。 產生的向下取樣資料集有 1,703,957 個資料列和 23 個資料行。

**計程車識別碼**
  
+ _medallion_ 資料行代表計程車的唯一識別碼。
  
+ _hack\_license_ 資料行包含計程車司機駕照號碼 (匿名)。
  
**車程和小費記錄**
  
+ 每筆車程記錄都會包含上車和下車位置與時間，以及車程距離。
  
+ 每筆費用記錄都會包括付款資訊，例如付款類型、總付款金額和小費金額。
  
+ 最後三個資料行可以用於各種機器學習工作。 _tip\_amount_ 資料行包含連續數值，而且可以當成 **label** 資料行來進行迴歸分析。 _tipped_ 資料行只有是/否值，並且用於二元分類。 _tip\_class_ 資料行有多個 **類別標籤**，因此可以當成多類別分類工作的標籤使用。
  
  這個逐步解說只會示範二元分類工作；您可以自由地嘗試建立其他兩個機器學習工作 (迴歸和多類別分類) 的模型。
  
+ 使用以下商務規則而用於標籤資料行的值都是根據 _tip\_amount_ 資料行：
  
  |衍生的資料行名稱|規則|
  |-|-|
  |tipped|If tip_amount > 0, tipped = 1, otherwise tipped = 0|
  |tip_class|Class 0: tip_amount = $0<br /><br />Class 1: tip_amount > $0 and tip_amount <= $5<br /><br />Class 2: tip_amount > $5 and tip_amount <= $10<br /><br />Class 3: tip_amount > $10 and tip_amount <= $20<br /><br />Class 4: tip_amount > $20|

## <a name="create-plots-using-r-in-t-sql"></a>在 T-SQL 中使用 R 建立繪圖

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!IMPORTANT]
> 從 SQL Server 2019 開始，隔離機制會要求您授與繪圖檔案儲存所在目錄的適當權限。 如需有關如何設定這些權限的詳細資訊，請參閱 [Windows 上 SQL Server 2019 中的檔案權限區段：機器學習服務的隔離變更](../install/sql-server-machine-learning-services-2019.md#file-permissions)
::: moniker-end

請使用 R 函數 `barplot` 建立繪圖。 此步驟會根據 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢提供的資料繪製長條圖。 您可以將此函數包裝在預存程序 **RPlotHistogram** 中。

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的物件總管中，以滑鼠右鍵按一下 **NYCTaxi_Sample** 資料庫，然後選取 [新查詢]  。 或者，在 Azure Data Studio 中，從 [檔案] 功能表中選取 [新增筆記本]，然後連線到資料庫。

2. 貼上下列指令碼，建立繪製長條圖的預存程序。 此範例名為 **RPlotHistogram**。

   ```sql
   CREATE PROCEDURE [dbo].[RPlotHistogram]
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
      barplot(table(InputDataSet$tipped), main = "Tip Histogram", col="lightgreen", xlab="Tipped or not", ylab = "Counts", space=0)
      dev.off();  
      OutputDataSet <- data.frame(data=readBin(file(image_file, "rb"), what=raw(), n=1e6));  
      ',  
      @input_data_1 = @query  
      WITH RESULT SETS ((plot varbinary(max)));  
   END
   GO
   ```

此指令碼中需了解的重點包括下列各項：
  
+ `@query` 變數會定義查詢文字 (`'SELECT tipped FROM nyctaxi_sample'`)，以當成指令碼輸入變數 `@input_data_1`的引數傳遞給 R 指令碼。 若是以外部程序執行的 R 指令碼，在指令碼輸入，以及在 SQL Server 上啟動 R 工作階段的 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 系統預存程序輸入之間，應該要有一對一的對應。
  
+ 在 R 指令碼中，會定義變數 (`image_file`) 以儲存影像。

+ 呼叫 `barplot` 函數可產生繪圖。
  
+ R 裝置設定為 [關閉]  ，因為您是以 SQL Server 中的外部指令碼執行此命令。 一般來說，當您在 R 中發出高階繪製命令時，R 將會開啟稱為「裝置」  的圖形視窗。 如果您要寫入檔案或以其他方式處理輸出，可以關閉裝置。
  
+ R 圖形物件會序列化為 R data.frame 以進行輸出。

### <a name="execute-the-stored-procedure-and-use-bcp-to-export-binary-data-to-an-image-file"></a>執行預存程序，並使用 bcp 將二進位資料匯出至影像檔案

預存程序會以您明顯無法直接檢視的 varbinary 資料流形式傳回影像。 不過，您可以使用 **bcp** 公用程式來取得 varbinary 資料，並將它儲存為用戶端電腦上的影像檔。
  
1. 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，執行下列陳述式：
  
    ```sql
    EXEC [dbo].[RPlotHistogram]
    ```
  
    **結果**
    
    *plot* *0xFFD8FFE000104A4649...*
  
2. 開啟 PowerShell 命令提示字元，並將適當的執行個體名稱、資料庫名稱、使用者名稱和認證提供為引數來執行下列命令。 若是使用 Windows 身分識別的使用者，您可以使用 **-T** 取代 **-U** 和 **-P**。
  
   ```powershell
   bcp "exec RPlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  NYCTaxi_Sample  -U <user name> -P <password> -T
   ```

   > [!NOTE]
   > bcp 的命令參數區分大小寫。
  
3. 如果連接成功，系統會提示您輸入圖形檔格式的詳細資訊。

   在每個提示字元下，按 ENTER 接受預設值，但不包括這些變更：

   + 針對 **prefix-length of field plot**，輸入 0。
  
   + 如果您想要儲存輸出參數以供日後重複使用，請輸入 **Y** 。
  
   ```text
   Enter the file storage type of field plot [varbinary(max)]: 
   Enter prefix-length of field plot [8]: 0
   Enter length of field plot [0]:
   Enter field terminator [none]:
  
   Do you want to save this format information in a file? [Y/n]
   Host filename [bcp.fmt]:
   ```
  
   **結果**

   ```text
   Starting copy...
   1 rows copied.
   Network packet size (bytes): 4096
   Clock Time (ms.) Total     : 3922   Average : (0.25 rows per sec.)
   ```

   > [!TIP]
   > 如果您將格式資訊儲存至檔案 (bcp.fmt)，則 **bcp** 公用程式會產生您未來可套用至類似命令的格式定義，而不提示您輸入圖形檔格式選項。 若要使用格式檔案，請在 password 引數之後將 `-f bcp.fmt` 新增至任何命令列結尾。
  
4. 將會在執行 PowerShell 命令的相同目錄中建立輸出檔案。 若要檢視繪圖，只需要開啟檔案 plot.jpg。
  
   ![含/不含小費的計程車車程](media/rsql-devtut-tippedornot.jpg "含/不含小費的計程車車程")  
  
## <a name="create-a-stored-procedure-using-hist"></a>使用 `hist` 建立預存程序

資料科學家通常會產生多個資料視覺效果，從不同的角度深入了解資料。 在此範例中，您將建立名為 **RPlotHist** 的預存程序，並且將長條圖、散佈圖及其他 R 圖形寫成 .JPG 和 .PDF 格式。

這個預存程序會使用 `hist` 函數來建立長條圖，將二進位資料匯出成常用的格式，例如 .JPG、.PDF 及 .PNG。

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
  
此指令碼中需了解的重點包括下列各項：

+ 預存程序內 SELECT 查詢的輸出會儲存在預設 R 資料框架 `InputDataSet`中。 接著可以呼叫各種 R 繪製函數，以產生實際圖形檔。 大部分的內嵌 R 指令碼代表這些圖形函數的選項 (例如 `plot` 或 `hist`)。
  
+ R 裝置設定為 [關閉]  ，因為您是以 SQL Server 中的外部指令碼執行此命令。 一般來說，當您在 R 中發出高階繪製命令時，R 將會開啟稱為「裝置」  的圖形視窗。 如果您要寫入檔案或以其他方式處理輸出，可以關閉裝置。
  
+ 所有檔案都會儲存至本機資料夾 C:\temp\Plots。 目的地資料夾是透過執行預存程序時提供給 R 指令碼的引數所定義。 若要將檔案輸出至不同的資料夾，請變更預存程序中所內嵌 R 指令碼內的 `mainDir` 變數值。 您也可以修改指令碼來輸出不同的格式、多個檔案等。

### <a name="execute-the-stored-procedure"></a>執行預存程序

執行下列陳述式，將二進位繪圖資料匯出成 JPEG 和 PDF 檔案格式。

```sql
EXEC RPlotHist
```

**結果**

```text
STDOUT message(s) from external script:
[1] Creating output plot files:[1] C:\temp\plots\rHistogram_Tipped_18887f6265d4.jpg[1] 

C:\temp\plots\rHistograms_Tip_and_Fare_Amount_1888441e542c.pdf[1]

C:\temp\plots\rXYPlots_Tip_vs_Fare_Amount_18887c9d517b.pdf
```

檔案名稱中的字數會隨機產生，確保不會因嘗試寫入現有檔案而發生錯誤。

### <a name="view-output"></a>檢視輸出

若要檢視繪圖，請開啟目的地資料夾，並檢閱預存程序中 R 程式碼所建立的檔案。

1. 前往 STDOUT 訊息中指示的資料夾 (在此範例中是 C:\temp\plots\)

2. 開啟 `rHistogram_Tipped.jpg` 以顯示收到小費及未收到小費的車程數 (此長條圖與您在上個步驟中產生的長條圖類似)。

3. 開啟 `rHistograms_Tip_and_Fare_Amount.pdf`，查看根據費用金額繪製的小費金額分佈狀況。

   ![顯示 tip_amount 和 fare_amount 的長條圖](media/rsql-devtut-tipamtfareamt.PNG "顯示 tip_amount 和 fare_amount 的長條圖")

4. 開啟 `rXYPlots_Tip_vs_Fare_Amount.pdf`，檢視 x 軸為費用金額且 y 軸為小費金額的散佈圖。

   ![根據費用金額繪製的小費金額](media/rsql-devtut-tipamtbyfareamt.PNG "根據費用金額繪製的小費金額")

## <a name="next-steps"></a>後續步驟

在本文章中，您將：

> [!div class="checklist"]
> + 已檢閱範例資料
> + 已在 T-SQL 中使用 R 建立繪圖
> + 以多種檔案格式輸出繪圖

> [!div class="nextstepaction"]
> [R 教學課程：建立資料特徵](r-taxi-classification-create-features.md)