---
title: "步驟 3：瀏覽及視覺化資料 (資料庫內進階分析教學課程) | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
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
  - "TSQL"
ms.assetid: 7fe670f3-5e62-43ef-97eb-b9af54df9128
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# 步驟 3：瀏覽及視覺化資料 (資料庫內進階分析教學課程)
開發資料科學方案通常會包含大量資料瀏覽和資料視覺化。 在這個步驟中，您將檢閱範例資料，然後使用 R 函數產生一些繪圖。 這些 R 函數已經包含在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中；在這個逐步解說中，您將練習從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 呼叫 R 函數。  
  
## 檢閱資料  
首先，需要一分鐘的時間來檢閱範例資料 (如果您還沒有這麼做)。  
  
在原始資料集中，計程車識別碼和車程記錄會提供在不同的檔案中。 不過，為了更輕鬆地使用範例資料，已根據 _medallion_、_hack_license_ 和 _pickup_datetime_ 資料行來聯結兩個原始資料集。  也會對記錄進行抽樣，只取得 1% 的原始記錄數目。 產生的向下取樣資料集有 1,703,957 個資料列和 23 個資料行。  
  
**計程車識別碼**  
  
-   _medallion_ 資料行代表計程車的唯一識別碼。  
  
-   _hack_license_ 資料行包含計程車司機駕照號碼 (匿名)。  
  
**車程和小費記錄**  
  
-   每筆車程記錄都會包含上車和下車位置與時間，以及車程距離。  
  
-   每筆費用記錄都會包括付款資訊，例如付款類型、總付款金額和小費金額。  
  
-   最後三個資料行可以用於各種機器學習工作。  _tip_amount_ 資料行包含連續數值，而且可以當成 **label** 資料行來進行迴歸分析。 _tipped_ 資料行只有是/否值，並且用於二元分類。 _tip_class_ 資料行有多個**類別標籤**，因此可以當成多類別分類工作的標籤使用。  
  
    這個逐步解說只會示範二元分類工作；您可以自由地嘗試建立其他兩個機器學習工作 (迴歸和多類別分類) 的模型。  
  
-   使用這些商務規則，用於 label 資料行的值都是根據 _tip_amount_ 資料行︰  
  
    |衍生的資料行名稱|規則|  
    |-|-|  
     |tipped|If tip_amount > 0, tipped = 1, otherwise tipped = 0|  
    |tip_class|Class 0: tip_amount = $0<br /><br />Class 1: tip_amount > $0 and tip_amount <= $5<br /><br />Class 2: tip_amount > $5 and tip_amount <= $10<br /><br />Class 3: tip_amount > $10 and tip_amount <= $20<br /><br />Class 4: tip_amount > $20|  
  
## 在 T-SQL 中使用 R 建立繪圖  
因為視覺效果是可了解資料和極端值分佈的功能強大工具，所以 R 提供許多套件可以將資料視覺化。 R 的標準開放原始碼發佈也包括許多函數，可建立長條圖、散佈圖、盒狀圖以及其他資料瀏覽圖形。  
  
R 通常會使用 R 裝置建立影像，以進行圖形輸出。 您可以擷取這個裝置的輸出，以及將影像儲存為 **varbinary** 資料類型以在應用程式中轉譯，也可以將影像儲存為任何支援檔案格式 (.JPG、.PDF 等)。  
  
在本節中，您將了解如何使用預存程序來處理每種類型的輸出。  
  
-   將繪圖儲存為 varbinary 資料類型  
  
-   將繪圖儲存至伺服器上的檔案 (.JPG、.PDF)  
  
### 將繪圖儲存為 varbinary 資料類型  
您將使用 `rxHistogram` ([!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中所提供的一個加強 R 函數)，以根據 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢中的資料來繪製長條圖。 為了簡化 R 函數的呼叫，請將它包裝在 _PlotHistogram_ 預存程序中。  
  
預存程序會以您明顯無法直接檢視的 varbinary 資料流形式傳回影像。 不過，您可以使用 **bcp** 公用程式來取得 varbinary 資料，並將它儲存為用戶端電腦上的影像檔。  
  
##### 建立預存程序 PlotHistogram  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，開啟新的查詢視窗。  
  
2.  選取逐步解說的資料庫，然後使用此陳述式建立程序。  
  
    ```  
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
  
    -   `@query` 變數會定義查詢文字 (`'SELECT tipped FROM nyctaxi_sample'`)，以當成指令碼輸入變數 `@input_data_1` 的引數傳遞給 R 指令碼。  
  
    -   R 指令碼相當簡單︰定義 R 變數 (`image_file`) 來定義影像，然後呼叫 `rxHistogram` 函數來產生繪圖。  
  
    -   R 裝置設定為 **off**。  
  
        在 R 中，當您發出高階繪製命令時，R 將會開啟稱為「裝置」的圖形視窗。 您可以變更視窗的大小、色彩和其他層面，也可以在寫入至檔案或透過其他方法處理輸出時關閉裝置。  
  
    -   R 圖形物件會序列化為 R data.frame 以進行輸出。 這是 CTP3 的暫時因應措施。  
  
##### 將 varbinary 資料輸出至可檢視的圖形檔  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，執行下列陳述式：  
  
    ```  
    EXEC [dbo].[PlotHistogram]  
    ```  
  
**結果**  
  
*plot*  
*0xFFD8FFE000104A4649...*  
  
2.  開啟 PowerShell 命令提示字元，並將適當的執行個體名稱、資料庫名稱、使用者名稱和認證提供為引數來執行下列命令︰  
  
    ```  
    bcp "exec PlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  <database name>  -U <user name> -P <password>  
  
    ```  
  
    > [!NOTE]  
    > **bcp** 的命令參數區分大小寫。  
  
3.  如果連接成功，系統會提示您輸入圖形檔格式的詳細資訊。 在每個提示字元下，按 ENTER 接受預設值，但不包括這些變更：  
  
    -   在 **prefix-length of field plot** 中，輸入 0。  
  
    -   如果您想要儲存輸出參數以供日後重複使用，請輸入 **Y**。  
  
    ```  
    Enter the file storage type of field plot [varbinary(max)]:  
    Enter prefix-length of field plot [8]: 0  
    Enter length of field plot [0]:  
    Enter field terminator [none]:  
  
    Do you want to save this format information in a file? [Y/n]  
    Host filename [bcp.fmt]:  
  
    ```  
  
**結果**  
  
*Starting copy...*  
*1 rows copied.*  
*Network packet size (bytes): 4096*  
*Clock Time (ms.)Total     : 3922   Average : (0.25 rows per sec.)*  
   
> [!TIP]  
 > 如果您將格式資訊儲存至檔案 (bcp.fmt)，則 **bcp** 公用程式會產生您未來可套用至類似命令的格式定義，而不提示您輸入圖形檔格式選項。 若要使用格式檔案，請在 password 引數之後將 `-f bcp.fmt` 新增至任何命令列結尾。  
  
4.  將會在執行 PowerShell 命令的相同目錄中建立輸出檔案。 若要檢視繪圖，只需要開啟檔案 plot.jpg。  
  
    ![taxi trips with and without tips](../../advanced-analytics/r-services/media/rsql-devtut-tippedornot.jpg "taxi trips with and without tips")  
  
### 將繪圖儲存至伺服器上的檔案 (jpg、pdf)  
將 R 繪圖輸出至二進位資料類型可能十分方便供應用程式使用，但不大適用於在資料瀏覽階段期間需要所轉譯繪圖的資料科學家。 資料科學家通常會產生多個資料視覺效果，從不同的角度深入了解資料。  
  
若要產生更容易檢視的圖形，您可以使用以常見格式 (例如 .JPG、.PDF 和 .PNG) 建立 R 輸出的預存程序。 在預存程序建立圖形之後，只要開啟檔案，就可以視覺化該繪圖。  
  
在這個步驟中，您將建立新的預存程序 _PlotInOutputFiles_，以示範如何使用 R 繪製函數來建立長條圖、散佈圖，以及 .JPG 和 .PDF 格式的其他圖形。 圖形檔會儲存至本機檔案；亦即，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資料夾中。  
  
##### 建立預存程序 PlotInOutputFiles  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，開啟新的查詢視窗，並貼入下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
    ```  
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
  
    -   預存程序內 SELECT 查詢的輸出會儲存在預設 R 資料框架 `InputDataSet` 中。 接著可以呼叫各種 R 繪製函數，以產生實際圖形檔。  
  
        大部分的內嵌 R 指令碼代表這些圖形函數的選項 (例如 `plot` 或 `hist`)。  
  
    -   所有檔案都會儲存至本機資料夾 _C:\temp\Plots\\_。  
  
        目的地資料夾是透過執行預存程序時提供給 R 指令碼的引數所定義。  變更 `mainDir` 變數的值，即可變更目的地資料夾。  
  
2.  請執行陳述式以建立預存程序。  
  
  
##### 產生圖形檔  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，執行下列 SQL 查詢：  
  
    ```  
    EXEC PlotInOutputFiles  
  
    ```  
  
**結果**  
  
*STDOUT message(s) from external script:*  
*[1] Creating output plot files:[1]* *C:\\\temp\\\plots\\\rHistogram_Tipped_18887f6265d4.jpg[1]* *C:\\\temp\\\plots\\\rHistograms_Tip_and_Fare_Amount_1888441e542c.pdf[1]* *C:\\\temp\\\plots\\\rXYPlots_Tip_vs_Fare_Amount_18887c9d517b.pdf*  
  
2.  開啟目的地資料夾，並檢閱預存程序中 R 程式碼所建立的檔案。 (檔案名稱中的數字會隨機產生)。  
  
*  rHistogram_Tipped_*nnnn*.jpg：顯示收到小費 (1) 與未收到小費 (0) 的車程數目。 這個長條圖與您在上一個步驟中所產生的長條圖十分類似。  
  
*  rHistograms_Tip_and_Fare_Amount_*nnnn*.pdf：顯示 tip_amount 和 fare_amount 資料行中值的分佈。  
  
        ![histogram showing tip_amount and fare_amount](../../advanced-analytics/r-services/media/rsql-devtut-tipamtfareamt.PNG "histogram showing tip_amount and fare_amount")  
  
*  rXYPlots_Tip_vs_Fare_Amount_*nnnn*.pdf：x 軸為費用金額且 y 軸為小費金額的散佈圖。  
  
        ![tip amount plotted over fare amount](../../advanced-analytics/r-services/media/rsql-devtut-tipamtbyfareamt.PNG "tip amount plotted over fare amount")  
  
3.  若要將檔案輸出至不同的資料夾，請變更預存程序中所內嵌 R 指令碼內的 `mainDir` 變數值。  
  
    您也可以修改指令碼來輸出不同的格式、多個檔案等。  
  
## 下一個步驟  
[步驟 4︰使用 T-SQL 建立資料特徵](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md)  
  
## 上一個步驟  
[步驟 2︰使用 PowerShell 將資料匯入 SQL Server](../../advanced-analytics/r-services/step-2-import-data-to-sql-server-using-powershell.md)  
  
## 另請參閱  
[適用於 SQL 開發人員的資料庫內進階分析 &#40;教學課程&#41;](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
[SQL Server R 服務教學課程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
