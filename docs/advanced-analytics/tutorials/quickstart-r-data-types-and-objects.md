---
title: R 和 SQL 資料類型和物件的快速入門
description: 在本快速入門中, 瞭解如何使用 R 和 SQL Server 中的資料類型和資料物件。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: eb007525834c312952f9eb02809edadebaefa305
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715435"
---
# <a name="quickstart-handle-data-types-and-objects-using-r-in-sql-server"></a>快速入門：在 SQL Server 中使用 R 處理資料類型和物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本快速入門中, 取得在 R 與 SQL Server 之間移動資料時常見問題的實際操作簡介。 當您在自己的腳本中使用資料時, 您在此練習中取得的體驗會提供基本的背景。

事先知道的常見問題包括:

+ 資料類型有時不相符
+ 可能會發生隱含轉換
+ 有時需要轉型和轉換作業
+ R 和 SQL 會使用不同的資料物件

## <a name="prerequisites"></a>先決條件

先前的快速入門[中, 驗證 R 存在於 SQL Server 中](quickstart-r-verify.md), 提供設定本快速入門所需之 R 環境的相關資訊和連結。

## <a name="always-return-a-data-frame"></a>一律傳回資料框架

當您的指令碼將結果從 R 傳回到 SQL Server 時，它必須傳回資料做為 **data.frame**。 您在腳本中產生的任何其他物件類型 (無論是清單、因數、向量或二進位資料), 如果您想要將其輸出為預存程式結果的一部分, 則必須將它轉換為數據框架。 幸好有多個 R 函數可用來支援將其他物件變更為資料框架。 您甚至可將二進位模型序列化，並在資料框架中傳回它，您將在本教學課程稍後執行此動作。

首先, 讓我們使用一些 R 基本 R 物件 (向量、矩陣和清單) 來進行實驗, 並瞭解轉換至資料框架如何變更傳遞至 SQL Server 的輸出。

在 R 中比較這兩個「Hello World」腳本。腳本看起來幾乎完全相同, 但第一個會傳回三個值的單一資料行, 而第二個會傳回三個數據行, 每個都有單一值。

**範例 1**

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
     , @script = N' mytextvariable <- c("hello", " ", "world");
       OutputDataSet <- as.data.frame(mytextvariable);'
     , @input_data_1 = N' ';
```

**範例 2**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' OutputDataSet<- data.frame(c("hello"), " ", c("world"));'
      , @input_data_1 = N'  ';
```

## <a name="identify-schema-and-data-types"></a>識別架構和資料類型

為何結果如此不同？ 

您通常可以使用 R `str()` 命令來找到答案。 在 R 指令碼中的任一處加入函數 `str(object_name)`，以傳回指定 R 物件的資料結構描述做為資訊訊息。 若要檢視訊息，可查看 Visual Studio Code 的 [訊息] 窗格，或 SSMS 中的 [訊息] 索引標籤。

若要了解為什麼範例 1 和範例 2 會有如此不同的結果，在每個陳述式中 _@script_ 變數定義的結尾插入一行 `str(OutputDataSet)`，如下：

**範例1已加入 str 函數**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' mytextvariable <- c("hello", " ", "world");
      OutputDataSet <- as.data.frame(mytextvariable);
      str(OutputDataSet);'
      , @input_data_1 = N'  '
;
```

**範例 2 (已加入 str 函數)**

```sql
EXECUTE sp_execute_external_script
  @language = N'R', 
  @script = N' OutputDataSet <- data.frame(c("hello"), " ", c("world"));
    str(OutputDataSet);' , 
  @input_data_1 = N'  ';
```

現在，檢視 [訊息] 中的文字，以查看為何會有不同的輸出。

**結果 - 範例 1**

```sql
STDOUT message(s) from external script:
'data.frame':   3 obs. of  1 variable:
$ mytextvariable: Factor w/ 3 levels " ","hello","world": 2 1 3
```

**結果 - 範例 2**

```sql
STDOUT message(s) from external script:
'data.frame':   1 obs. of  3 variables:
$ c..hello..: Factor w/ 1 level "hello": 1
$ X...      : Factor w/ 1 level " ": 1
$ c..world..: Factor w/ 1 level "world": 1
```

如您所見，稍微變化一下 R 語法，就會對結果的結構描述產生極大的影響。 我們不會介紹原因, 但 R 資料類型的差異會在[Hadley wickham 針對的 "Advanced R](http://adv-r.had.co.nz)" 中的*資料結構*一節中詳細說明。

現在只需注意，您需要在將 R 物件強制轉型為資料框架時檢查預期的結果。

> [!TIP]
> 您也可以使用 R 身分識別函數 (例如`is.matrix`) `is.vector`來傳回內部資料結構的相關資訊。

## <a name="implicit-conversion-of-data-objects"></a>資料物件的隱含轉換

如果這兩個資料物件具有相同數目的維度，或者如果任一個資料類型包含異質資料類型，則每個 R 資料物件都會有自己的規則，用於在結合其他資料物件時如何處理資料。

例如, 假設您執行下列語句, 使用 R 執行矩陣乘法。您可以將單一資料行矩陣乘以具有四個值的陣列, 並預期會產生4x3 矩陣。

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
    , @script = N'
        x <- as.matrix(InputDataSet);
        y <- array(12:15);
    OutputDataSet <- as.data.frame(x %*% y);'
    , @input_data_1 = N' SELECT [Col1]  from RTestData;'
    WITH RESULT SETS (([Col1] int, [Col2] int, [Col3] int, Col4 int));
```

其中，具有三個值的資料行會轉換成單一資料行矩陣。 因為矩陣只是 R 中的特殊陣列案例，所以，陣列 `y` 會隱含地強制轉型為單一資料行的矩陣，以使這兩個引數相符。

**結果**

|Col1|Col2|Col3|Col4|
|---|---|---|---|
|12|13|14|15|
|120|130|140|150|
|1200|1300|1400|1500|

不過, 請注意當您變更陣列`y`的大小時, 會發生什麼事。

```sql
execute sp_execute_external_script
   @language = N'R'
   , @script = N'
        x <- as.matrix(InputDataSet);
        y <- array(12:14);
   OutputDataSet <- as.data.frame(y %*% x);'
   , @input_data_1 = N' SELECT [Col1]  from RTestData;'
   WITH RESULT SETS (([Col1] int ));
```

R 現在會傳回單一值做為結果。

**結果**
    
|Col1|
|---|
|1542|

為什麼？ 在此情況下, 因為這兩個引數可以當做相同長度的向量來處理, 所以 R 會傳回內部產品做為矩陣。  根據線性代數的規則，這是預期的行為；不過，如果下游應用程式預期輸出結構描述永遠不會變更，則它可能會造成問題！

> [!TIP]
> 
> 收到錯誤？ 這些範例需要資料表**RTestData**。 如果您尚未建立測試資料表, 請回到本主題以建立資料表:[處理輸入和輸出](../tutorials/rtsql-working-with-inputs-and-outputs.md)。
> 
> 如果您已建立資料表, 但仍然收到錯誤, 請確定您是在包含資料表的資料庫內容中執行預存程式, 而不是在**master**或其他資料庫中。
> 
> 此外, 我們建議您避免在這些範例中使用臨時表。 有些 R 用戶端會終止批次之間的連接, 並刪除臨時表。

## <a name="merge-or-multiply-columns-of-different-length"></a>合併或相乘不同長度的資料行

R 提供很大的彈性來處理不同大小的向量, 以及將這些資料行的結構結合成資料框架。 向量的清單看起來像是一個資料表，但它們不遵循用以管理資料庫資料表的所有規則。

例如，下列指令碼定義長度為 6 的數值陣列，並將它儲存在 R 變數 `df1` 中。 然後, 數值陣列會與 RTestData 資料表的整數結合, 其中包含三 (3) 個值, 以建立新的資料框架`df2`。

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
    , @script = N'
               df1 <- as.data.frame( array(1:6) );
               df2 <- as.data.frame( c( InputDataSet , df1 ));
               OutputDataSet <- df2'
    , @input_data_1 = N' SELECT [Col1]  from RTestData;'
    WITH RESULT SETS (( [Col2] int not null, [Col3] int not null ));
```

為了填滿資料框架，R 會根據比對陣列 `df1` 中元素數目所需的次數，多次重複使用擷取自 RTestData 的元素。

**結果**
    
|*Col2*|*Col3*|
|----|----|
|1|1|
|10|2|
|100|3|
|1|4|
|10|5|
|100|6|

請記住，資料框架只是看起來像資料表，其實是一個向量清單。

## <a name="cast-or-convert-sql-server-data"></a>轉型或轉換 SQL Server 資料

R 和 SQL Server 不會使用相同的資料類型，因此，當您在 SQL Server 中執行查詢來取得資料，然後將該資料傳遞至 R 執行階段時，通常會發生某些類型的隱含轉換。 當您將資料從 R 傳回至 SQL Server 時，將發生另一組轉換。

- SQL Server 會將查詢中的資料推送至啟動列服務所管理的 R 進程, 並將它轉換成內部表示, 以提高效率。
- R 執行階段會將資料載入 data.frame 變數，並對資料執行自己的作業。
- 資料庫引擎會使用受保護的內部連線來將資料傳回至 SQL server，並根據 SQL Server 資料類型顯示資料。
- 藉由使用可發出 SQL 查詢並處理表格式資料集的用戶端或網路程式庫來連接到 SQL Server，您就能取得資料。 此用戶端應用程式可能會以其他方式影響資料。

若要查看其運作方式, 請在[AdventureWorksDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)資料倉儲上執行此查詢, 例如這一項。 此檢視會傳回用來建立預測的銷售資料。

```sql
USE AdventureWorksDW
GO

SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = 'M200 Europe'
           ORDER BY ReportingDate ASC
```

> [!NOTE]
> 
> 您可以使用任何版本的 AdventureWorks, 或使用您自己的資料庫建立不同的查詢。 重點是嘗試處理一些包含文字、日期時間和數值的資料。

現在, 請嘗試將此查詢貼入預存程式的輸入。

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
      , @script = N' str(InputDataSet);
      OutputDataSet <- InputDataSet;'
      , @input_data_1 = N'
           SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = ''M200 Europe''
           ORDER BY ReportingDate ASC ;'
WITH RESULT SETS undefined;
```

如果您收到錯誤，您可能需要對查詢文字進行一些編輯。 例如，WHERE 子句中的字串述詞必須以兩組單引號括住。

讓查詢能夠正常運作之後，檢閱 `str` 函數的結果，以查看 R 如何處理輸入資料。

**結果**

```sql
STDOUT message(s) from external script: 'data.frame':    37 obs. of  3 variables:
STDOUT message(s) from external script: $ ReportingDate: POSIXct, format: "2010-12-24 23:00:00" "2010-12-24 23:00:00"
STDOUT message(s) from external script: $ ProductSeries: Factor w/ 1 levels "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1
STDOUT message(s) from external script: $ Amount       : num  3400 16925 20350 16950 16950
```

+ 已使用 R 資料類型 **POSIXct** 來處理 datetime 資料行。
+ 文字資料行 "ProductSeries" 已識別為**因素**, 這表示類別變數。 預設會處理字串值以做為因數。 如果您將字串傳遞至 R，則會將它轉換為整數，以供內部使用，接著對應回輸出上的字串。

### <a name="summary"></a>總結

從這些簡短的範例中, 您可以看到在傳遞 SQL 查詢做為輸入時, 檢查資料轉換效果的需求。 由於 R 不支援某些 SQL Server 資料類型, 因此請考慮使用下列方式來避免發生錯誤:

+ 事先測試您的資料, 並確認架構中的資料行或值在傳遞至 R 程式碼時可能會發生問題。
+ 個別指定輸入資料來源中的資料行，而不是使用 `SELECT *`，並了解將如何處理每個資料行。
+ 在準備輸入資料時視需要執行明確的轉型，以避免出現意外狀況。
+ 避免傳遞造成錯誤且不適用於模型化的資料行 (例如 GUID 或 rowguids)。

如需支援和不支援之資料類型的詳細資訊, 請參閱[R 程式庫和資料類型](../r/r-libraries-and-data-types.md)。

如需有關執行時間將字串轉換為數值因數之效能影響的詳細資訊, 請參閱[SQL Server R Services 效能微調](../r/sql-server-r-services-performance-tuning.md)。

## <a name="next-step"></a>下一步

在下一個快速入門中, 您將瞭解如何將 R 函數套用至 SQL Server 資料。

> [!div class="nextstepaction"]
> [入門搭配 SQL Server 資料使用 R 函數](quickstart-r-functions.md)
