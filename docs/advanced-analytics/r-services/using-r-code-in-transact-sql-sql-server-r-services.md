---
title: "在 Transact-SQL 中使用 R 程式碼 (SQL Server R Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/10/2017"
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
ms.assetid: 4e6fe30d-a105-4d5b-bc05-5e5204753847
caps.latest.revision: 36
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 28
---
# 在 Transact-SQL 中使用 R 程式碼 (SQL Server R Services)
本教學課程提供非常簡短的範例，說明在 SQL Server R 服務中使用 R 的語法。    
    
    
如果您不熟悉 SQL Server R 服務，但想要了解如何定義 T-SQL 預存程序中的 R 指令碼、如何使用資料作為輸入及如何定義輸出的基本概念，這是不錯的起點。    
    
**必要條件**︰若要在 SQL Server R 服務中執行 R 程式碼，您必須連接到已安裝 R 服務的 SQL Server 執行個體。     
    
## 第 1 部分 - 基本作業  

在下列各節中，您將了解如何透過新增參數來擴充預存程序，以及如何設定輸入和輸出。   
  
### 1.1. 檢查 R 在 SQL Server 中是否運作正常  

此查詢使用系統預存程序 [sp_execute_external_script](https://msdn.microsoft.com/library/mt604368.aspx)，這是您在 SQL Server 的內容中呼叫 R 的方式。 此範例會將 SQL 查詢當作輸入傳遞至 R，再由 R 將該資料框架傳回 SQL Server。     
    
1. 在 Windows [開始] 功能表中，找出 Microsoft SQL Server Management Studio。     
2. 如果找不到，您可能需要加以安裝︰[下載 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)。    
3. 在 [連接到伺服器] 對話方塊中，輸入已啟用 SQL Server R 服務的伺服器或執行個體名稱。 如需這些範例，請確定使用能夠建立新資料庫的帳戶進行登入、執行 SELECT 陳述式並檢視資料表。  開啟新的 [查詢] 視窗並貼入此陳述式，檢查一切是否運作正常：    
    
    ```sql   
    exec sp_execute_external_script  
      @language =N'R',    
      @script=N'OutputDataSet<-InputDataSet',      
      @input_data_1 =N'select 1 as hello'    
      with result sets (([hello] int not null));    
    go    
    ```   
       
       
  
### <a name="bkmk_SSMSBasics"></a>1.2. 建立一些簡單的測試資料  
    
開發複雜的資料科學解決方案之前，請務必了解 SQL Server 與 R 之間的差異。    
  
1. 執行下列 T-SQL 陳述式以建立暫存資料表。     
   
    ```sql    
    CREATE TABLE #MyData ([Col1] int not null) ON [PRIMARY]    
    INSERT INTO #MyData   VALUES (1);    
    INSERT INTO #MyData   Values (10);    
    INSERT INTO #MyData   Values (100) ;    
    GO    
    ```    
5. 建立資料表之後，請使用下列陳述式來查詢資料表：  
    ```sql  
    SELECT * from #MyData  
    ```  

**結果**  
  
|Col1 |   
|----|   
|1|   
|10|   
|100|   
  
    
### 1.3. 使用 R 指令碼取得測試資料    
  
建立資料表之後，請執行下列陳述式：  
  
  ```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' OutputDataSet <- InputDataSet;'    
    , @input_data_1 = N' SELECT *  FROM #MyData;'    
    WITH RESULT SETS (([NewColName] int NOT NULL));
  ```    
    
它應該會傳回相同的值，但具有新的資料行名稱。  
  
**注意**    
- *@Language* 參數會定義要呼叫的語言擴充功能，在本例中為 R。    
- 在 *@script* 參數中，您可以定義命令以 Unicode 文字形式傳遞至 R 執行階段。 您也可以將此文字新增至 **nvarchar** 類型的變數，並呼叫此變數。    
- `N'OutputDataSet <- InputDataSet;'` 行會將預設變數名稱 **InputDataSet** 中包含的輸入資料傳遞至 R，然後傳回結果，而不需要執行任何進一步的作業。 請注意，R 區分大小寫，因此輸入和輸出變數名稱都必須使用正確的大小寫，否則將會引發錯誤。    
   
    
若要指定不同的輸入或輸出變數，請使用 *@input_data_1_name* 參數，然後輸入有效的 SQL 識別碼。 例如，本例中的輸出和輸入變數名稱已分別變更為 *SQLOut* 和 *SQLIn*︰    
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' SQLOut <- SQLIn;'    
    , @input_data_1 = N' SELECT 12 as Col;'    
    , @input_data_1_name  = N'SQLIn'    
    , @output_data_1_name =  N'SQLOut'    
    WITH RESULT SETS (([NewColName] int NOT NULL));    
```    
    
**注意**    
- 您必須先指定必要的參數 *@input_data_1* 和 *@output_data_1*，才能使用選擇性參數 *@input_data_1_name* 和 *@output_data_1_name*。    
- SQL 和 R 不支援相同的資料類型；因此，將資料從 SQL Server 傳送至 R 時通常會發生類型轉換，反之亦然。 如需詳細資訊，請參閱[使用 R 資料類型](../../advanced-analytics/r-services/working-with-r-data-types.md)。    
- 只有一個輸入資料集可以當作參數傳遞，您只能傳回一個資料集。 不過，您可以從 R 程式碼內部呼叫其他資料集，而且除了資料集之外，您還可以傳回其他類型的輸出。 您也可以將 OUTPUT 關鍵字新增至任何參數，讓它傳回結果。      
- 所傳回資料集 (R data.frame) 的結構描述是由 `WITH RESULT SETS` 陳述式定義的。 請嘗試省略此項目，看看會有什麼結果。    
- [值] 窗格中會傳回表格式結果。 [訊息] 中會提供 R 執行階段所傳回的訊息     
  
### 1.4. 使用 R 產生結果    
    
您也可以只使用 R 指令碼產生值，將 _@input_data_1_ 的輸入查詢字串保持空白。 或者，您可以使用有效的 SQL SELECT 陳述式作為預留位置，而不使用 R 指令碼中的 SQL 結果。    
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' mytextvariable <- c("hello", " ", "world");    
                         OutputDataSet <- as.data.frame(mytextvariable);'    
    , @input_data_1 = N' SELECT 1 as Temp1'    
    WITH RESULT SETS (([col] char(20) NOT NULL));    
```    
    
**結果**    
    
    
 |*col* |    
 |-----|    
 |*hello*|    
 |     |    
 |*world*|    
    

現在，請嘗試上方提供的不同版本 Hello World 範例。     
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' OutputDataSet<- data.frame(c("hello"), " ", c("world"));'    
    , @input_data_1 = N'  '    
    WITH RESULT SETS (([col1] varchar(20) , [col2] char(1), [col3] varchar(20) ));    
```    
    
    
**結果**    
    
    
 |*col1* | *col2* | *col3*|    
 |-------|-------|-------    
 |*hello*|  |*world*|    
    
請注意，這兩個陳述式都會建立具有三個值的向量，但第二個範例會傳回三個資料行和單一資料列，而第一個範例會傳回單一資料行和三個資料列。 為什麼？
    
這是因為 R 提供許多方式來處理多個資料行的值︰向量、矩陣、陣列和清單。 這些作業雖然很強大且有彈性，但不一定符合 SQL 開發人員的期望。  有些 R 函數會對清單和矩陣執行隱含的資料物件轉換。

> [!TIP] 
> 
> 請務必確認您的結果，並判斷 R 程式碼將會傳回多少資料行，以及資料類型為何。    
>     
> 不論 R 程式碼使用的是矩陣、向量還是其他資料結構，請記住，R 指令碼輸出到預存程序的結果必須是 **data.frame**。      
  
  
## 第 2 部分 - 資料轉換和其他問題  
  
本節快速概覽在 SQL Server 中執行 R 程式碼時要留意的某些問題。  
  
+ 資料類型：了解 cast 和 convert 選項以及隱含轉換  
+ 表格式結果集：預期 R 變更資料行和資料列的方式    
  
### 2.1 資料類型的隱含強制型轉  
    
R 和 SQL Server 使用不同的資料類型，因此當您在 R 和資料庫之間移動資料時，必須注意相關限制。 下列範例說明這些常見問題。   
    
    
1. 執行下列陳述式，使用 R 執行矩陣乘法。在此指令碼中，三個值的單一資料行會轉換成單一資料行矩陣。  然後，R 會將第二個變數 `y` 隱含強制轉型為單一資料行矩陣，讓兩個引數相符。  
    
    ```sql    
    execute sp_execute_external_script    
      @language = N'R'    
      , @script = N'    
        x <- as.matrix(InputDataSet);    
        y <- array(12:15);    
      OutputDataSet <- as.data.frame(x %*% y);'    
     , @input_data_1 = N' SELECT [Col1]  from #MyData;'    
      WITH RESULT SETS (([Col1] int, [Col2] int, [Col3] int, Col4 int));    
    ```    
**結果**

|Col1|Col2|Col3|Col4|
|---|---|---|---|
|12|13|14|15|
|120|130|140|150|
|1200|1300|1400|1500|
 
  
      
2. 現在執行下一個指令碼，程序差不多，看看當您變更陣列長度時會有什麼結果。 
   
    ```sql    
    execute sp_execute_external_script    
      @language = N'R'    
      , @script = N'    
        x <- as.matrix(InputDataSet);    
        y <- array(12:14);    
      OutputDataSet <- as.data.frame(y %*% x);'    
      , @input_data_1 = N' SELECT [Col1]  from #MyData;'    
      WITH RESULT SETS (([Col1] int ));    
    ```    

**結果**    
    
|Col1|
|---|    
|1542|    
  
  R 這次會傳回單一值作為結果。 此結果有效，因為兩個引數是長度相同的向量；因此，R 將會傳回內積作為矩陣。    
    
   
  
### 2.2 合併或相乘不同長度的資料行    
    
  
下列指令碼會說明 R 某些不符合資料庫開發人員預期的行為。   
  
此指令碼定義長度為 6 的新數值陣列，並將它儲存在 R 變數 `df1` 中。 此數值陣列接著會與 #MyData 資料表 (含有 3 個值) 的整數結合，以建立新的資料框架 `df2`。   
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N'    
               df1 <- as.data.frame( array(1:6) );    
               df2 <- as.data.frame( c( InputDataSet , df1 ));    
               OutputDataSet <- df2'    
    , @input_data_1 = N' SELECT [Col1]  from #MyData;'    
    WITH RESULT SETS (( [Col2] int not null, [Col3] int not null ));    
```    
    
**結果**    
    
|*Col2*|*Col3*|    
|----|----|    
|1|1|    
|10|2|    
|100|3|    
|1|4|    
|10|5|    
|100|6|    
    
R 中有許多函數，可建立表格式輸出，並根據 R 資料物件對值執行相當不同的運算。 由於此 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序需要將輸入和輸出當作 data.frame 傳遞，因此您經常會使用函數將資料行和資料列轉換成資料框架及從中轉換出。    
    
如果您不確定要使用哪個 R 資料物件，請新增 R `str()` 函數或其中一個識別函數 (`is.matrix`、`is.vector` 等) 來檢查結果，並取得實際的結構描述和實值型別。    
  
  
如需詳細資訊，請參閱 Hadley Wickham 針對 [R 資料結構](http://adv-r.had.co.nz/Data-structures.html)所撰寫的這篇文章。    
    
### 2.3 識別資料類型並確認結構描述   
您會發現確實了解從 R 程式碼傳回的資料行數目，以及每個資料行的資料類型，是很重要的一件事。     
    
  
您可以在 R 指令碼中使用函數 `str()`，以傳回 R 物件的資料結構描述作為資訊訊息。 

例如，下列陳述式會傳回 #MyData 資料表的結構描述。    
        
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' str(InputDataSet);'    
    , @input_data_1 = N' SELECT *  FROM #MyData;'    
      WITH RESULT SETS undefined;    
```    
    
    
**結果**    
    
*STDOUT message (s) from external script:*    
*'data.frame': 3 obs. of 1 variable:*    
*STDOUT message (s) from external script:*    
*$ Col1: int 1   10   100*    
    
  
  
### 2.4 轉型或轉換資料行   
  
當您將資料從 SQL Server 傳送至 R 時，您經常需要轉換 (cast 或 convert) 資料類型，以確保可以適當處理這些類型。    
  
當您使用 SQL 查詢當作 R 程式碼的輸入時，會發生多個資料轉換：    
- SQL Server 將資料從查詢發送至 Launchpad 服務所管理的 R 處理序，並將其轉換為內部表示法。    
- R 執行階段會將資料載入 data.frame 變數，並對資料執行自己的作業。    
- 資料庫引擎會將資料傳回 Management Studio 或其他使用 SQL Server 資料類型的用戶端。  
    
1. 在 AdventureWorksDW 資料倉儲上執行下列查詢。 輸入資料查詢會定義用來建立預測之銷售資料的資料表。   
  
    ```sql    
    execute sp_execute_external_script    
       @language = N'R'    
      , @script = N' str(InputDataSet);'    
      , @input_data_1 = N'
           SELECT ReportingDate    
         , CAST(ModelRegion as varchar(50)) as ProductSeries    
         , Amount    
           FROM [AdventureworksDW2016CTP3].[dbo].[vTimeSeries]     
           WHERE [ModelRegion] = ''M200 Europe''    
           ORDER BY ReportingDate ASC ;'    
        WITH RESULT SETS undefined;    
    ```    
  
2. 現在檢閱 `str` 函數的結果，以查看 R 如何處理輸入資料。
      
**結果**    
    
  *STDOUT message(s) from external script: 'data.frame':    37 obs. of  3 variables:*    
  *STDOUT message(s) from external script: $ ReportingDate: POSIXct, format: "2010-12-24 23:00:00" "2010-12-24 23:00:00"*    
  *STDOUT message(s) from external script: $ ProductSeries: Factor w/ 1 levels "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1 ...*    
  *STDOUT message(s) from external script: $ Amount       : num  3400 16925 20350 16950 16950*    
    
    
**注意**    
    
- R 不支援某些 SQL Server 資料類型。因此，為了避免錯誤，您應該個別指定資料行並轉換某些資料行。    
- WHERE 子句中的字串述詞必須以兩組單引號括住。    
- datetime 資料行已傳回作為 R 資料類型 **POSIXct**。    
- 資料行 [ProductSeries] 已 (正確) 識別為**因素**。    
     
  
### 2.5 使用多個輸入   
只有一個輸入資料集可以當作參數傳遞。 不過，您可以使用 RODBC，從 R 程式碼內部呼叫其他資料集。     
  
例如，下列範例會呼叫 RODBC 套件，並在 SELECT 陳述式中指定此資料。    
    
```sql    
    @script = N' 
       <other R code here>;    
       library(RODBC);    
       connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");        dbhandle <- odbcDriverConnect(connStr)    
       OutputDataSet <- sqlQuery(dbhandle, "SELECT * from <table_name>");    
       <more R code combining the data>'    
```

建議您使用 RODBC 取得較小的資料集，例如查閱或因素清單，並使用 @input_data 參數從 SQL Server 取得較大的資料集，例如用於將模型定型的資料集。 


### 2.6 產生多個輸出

在 SQL Server 2016 中，來自預存程序 sp_execute_external_script 的 R 輸出會限制為單一 data.frame 或資料集 (未來可能會移除這項限制)。   
不過，除了資料集之外，您還可以傳回其他類型的輸出。 例如，您可能會使用單一資料集作為輸入來定型模型，但傳回統計資料的資料表作為輸出，再加上定型的模型作為物件。    
    
此外，您可以將 `OUTPUT` 關鍵字新增到任何輸入參數，讓它傳回結果。   
    
### 2.7 平行處理    
    
如果您使用大型資料集，而且取得資料的 SQL 查詢可以產生平行查詢計劃，您可以將 *@parallel* 參數設定為 1，以平行方式執行 R 指令碼。 如果您想要對大型結果集計分，這通常會很有用。 如果使用此選項，您必須事先使用 WITH RESULT SETS 指定輸出結果結構描述。    
    
不過，如果您必須定型使用所有資料列的模型，此參數不會有任何作用；在此情況下，建議您使用 **ScaleR** 套件。 這些套件可以自動散發處理，而不需要在 sp_execute_external_script 呼叫中指定 *@parallel =1*。    
    
      
  
## 第 3 部分 - 在預存程序中包裝 R 函數  
  
R 可以執行許多進階統計函數，而使用 T-SQL 可能需要複雜的程式碼才能重新產生這些函數。  不過，有了 R 服務，您在預存程序中執行 R 公用程式即可支援以下類似工作：   
    
- 將 R 的數學和統計函數套用至 SQL Server 資料    
    
- 建立使用 R 程式碼的資料表值函式或純量函數    
     

 通常會將這些 R 函數的呼叫封裝在預存程序中，使其更容易傳入參數。 為說明此程序，R 程式碼、sp_execute_external_script 的臨機操作預存程序呼叫及可用以參數化 R 函數的預存程序，都會提供相同的函數。
 
      
### 3.1. 產生亂數  
  
下列陳述式使用 `stats` 套件中的其中一個 R 函數，預設會在安裝 R 服務時載入此套件。 此處所示的 `rnorm` 函數在指定平均值 100 的情況下，使用常態分佈產生亂數 20。    

以下是執行工作的 R 程式碼。

```r
as.data.frame(rnorm(20, mean = 100));
```

這個陳述式會從 T-SQL 呼叫函數，將結果輸出至 SQL Server。  
   
```sql    
EXEC sp_execute_external_script    
      @language = N'R'    
    , @script = N' 
         OutputDataSet <- as.data.frame(rnorm(20, mean = 100));'    
    , @input_data_1 = N'   ;'    
      WITH RESULT SETS (([Density] float NOT NULL));    
```    

接下來，將預存程序包裝在另一個預存程序中，使其更容易傳入參數。 您必須定義 _@params_ 引數中的每一個輸入參數，並依名稱對應各個參數及其對應的 R 參數。

```sql
CREATE PROCEDURE MyRNorm (@mynorm int, @mymean int)
AS
    EXEC sp_execute_external_script    
      @language = N'R'    
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynorm, mymean));'    
    , @input_data_1 = N'   ;' 
    , @params = N' @mynorm int, @mymean int'  
    , @mynorm = @mynorm
    , @mymean = @mymean
    WITH RESULT SETS (([Density] float NOT NULL));    
```

呼叫新的預存程序並傳入值。

```sql
exec MyRNorm @mynorm = 20,@mymean = 100
```  
    
### 3.2 R 公用程式函數的更多用途  
  
此範例會呼叫其中一個 R 公用程式套件，並使用其 `memory.limit()` 函數來取得目前環境的記憶體。 預設會安裝 `utils` 套件，但不會載入。    
    
```sql    
execute sp_execute_external_script    
      @language = N'R'    
    , @script = N'    
        library(utils);    
        mymemory <- memory.limit();    
        OutputDataSet <- as.data.frame(mymemory);'    
    , @input_data_1 = N' ;'    
     WITH RESULT SETS (([Col1] int not null));    
```    

下例會使用 R .Machine 函數取得目前電腦支援的整數最大長度，再將其輸出到主控台。

```R
localmax <- .Machine$integer.max;
localmax;
```

```sql
execute sp_execute_external_script
  @language = N'R'
  , @script = N'
      localmax <- .Machine$integer.max;
      OutputDataSet <- as.data.frame(localmax);'
  , @input_data_1 = N'select [Col1]  from #MyData;'
  WITH RESULT SETS (([MaxIntValue] int not null));
```     
    
但不是只有 R 能做好此項工作。 SQL Server 中的集合式作業在處理某些作業上，可能比資料科學家慣常使用的 R 更有效率。如需 R 函數和 T-SQL 自訂函數的效能比較範例，請參閱[資料科學端對端逐步解說](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)。 

建議您依個別情況，評估是使用 R、T-SQL 或其他工具來執行指定作業，會較為合理。    
    
    
    
### 其他資源    
    
[資料科學深入探討︰使用 RevoScaleR 套件](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)︰此逐步解說提供常見資料科學工作的實際操作體驗    
[資料科學端對端解決方案](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)︰此逐步解說說明在 SQL 和 R 方法之間取得平衡的開發和部署程序       
[SQL 開發人員的進階分析](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)︰向 SQL 開發人員說明完整模型作業     
    
    
    
    
