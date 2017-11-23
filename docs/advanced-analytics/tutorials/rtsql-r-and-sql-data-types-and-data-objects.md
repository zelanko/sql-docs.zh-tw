---
title: "R 與 SQL 資料類型和資料物件 (SQL 快速入門中的 R) |Microsoft 文件"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
- SQL
ms.assetid: 1a17fc5b-b8c5-498f-b8b1-3b7b43a567e1
caps.latest.revision: "8"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 4207d26b2f38e3f13a45c21ab40293cf0dc95219
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="r-and-sql-data-types-and-data-objects-r-in-sql-quickstart"></a>R 與 SQL 資料類型和資料物件 (SQL 快速入門中的 R)

在此步驟中，您會了解 R 與 SQL Server 之間移動資料時，會發生的一些常見問題：

+ 資料類型有時不相符
+ 可能會發生隱含轉換
+ 有時需要轉型和轉換作業
+ R 和 SQL 會使用不同的資料物件

## <a name="always-return-r-data-as-a-data-frame"></a>一律傳回 R 資料做為資料框架

當您的指令碼將結果從 R 傳回到 SQL Server 時，它必須傳回資料做為 **data.frame**。 您在指令碼中產生的任何其他類型物件 (不論是清單、因數、向量或二進位資料)，如果您想要輸出它以做為預存程序結果的一部分，就必須將它轉換為資料框架。 幸好有多個 R 函數可用來支援將其他物件變更為資料框架。 您甚至可將二進位模型序列化，並在資料框架中傳回它，您將在本教學課程稍後執行此動作。

首先，讓我們來試驗某些 R 基本 R 物件 — 向量、 矩陣和清單，並查看如何轉換成資料框架變更傳遞至 SQL Server 的輸出。

比較這些兩個"Hello World"指令碼指令碼看起來幾乎完全相同，但第一個會傳回單一資料行的三個值，而第二個則傳回單一的三個資料行值，每個。

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

## <a name="identifying-the-schema-and-data-types-of-r-data"></a>識別 R 資料的結構描述和資料類型

為何結果如此不同？

您通常可以使用 R `str()` 命令來找到答案。 在 R 指令碼中的任一處加入函數 `str(object_name)`，以傳回指定 R 物件的資料結構描述做為資訊訊息。 若要檢視訊息，可查看 Visual Studio Code 的 [訊息] 窗格，或 SSMS 中的 [訊息] 索引標籤。

若要了解為什麼範例 1 和範例 2 會有如此不同的結果，在每個陳述式中 _@script_ 變數定義的結尾插入一行 `str(OutputDataSet)`，如下：

**範例 1 使用 str 函式加入**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' mytextvariable <- c("hello", " ", "world");
      str(OutputDataSet);'
      , @input_data_1 = N'  '
;
```

**範例 2 使用 str 函式加入**

```sql
EXECUTE sp_execute_external_script
  @language = N'R', 
  @script = N' OutputDataSet <- data.frame(c("hello"), " ", c("world"));
    str(OutputDataSet)' , 
  @input_data_1 = N'  ';
```

現在，檢視 [訊息] 中的文字，以查看為何會有不同的輸出。

**結果 - 範例 1**

```
STDOUT message(s) from external script:
'data.frame':   3 obs. of  1 variable:
$ mytextvariable: Factor w/ 3 levels " ","hello","world": 2 1 3
```

**結果 - 範例 2**

```
STDOUT message(s) from external script:
'data.frame':   1 obs. of  3 variables:
$ c..hello..: Factor w/ 1 level "hello": 1
$ X...      : Factor w/ 1 level " ": 1
$ c..world..: Factor w/ 1 level "world": 1
```

如您所見，稍微變化一下 R 語法，就會對結果的結構描述產生極大的影響。 我們將不會進入為何，因為 R 資料類型的差異會更詳盡地在本文中說明的 Hadley Wickham: [R 資料結構](http://adv-r.had.co.nz/Data-structures.html)。

現在只需注意，您需要在將 R 物件強制轉型為資料框架時檢查預期的結果。

> [!TIP]
> 
> 您可以也使用 R identity 函數，例如`is.matrix`，`is.vector`等等。

## <a name="implicit-conversion-of-data-objects"></a>資料物件的隱含轉換

如果這兩個資料物件具有相同數目的維度，或者如果任一個資料類型包含異質資料類型，則每個 R 資料物件都會有自己的規則，用於在結合其他資料物件時如何處理資料。

例如，假設您執行下列陳述式，以使用 R 執行矩陣相乘。您將含有三個值的單一資料行矩陣乘以含有四個值的陣列，並預期會得到一個 4x3 矩陣。

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

不過，請注意當您變更陣列的大小，會發生什麼事`y`。

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

為什麼？ 在此情況下，由於兩個引數可以處理相同的長度向量，R 會傳回內部乘積矩陣形式。  根據線性代數的規則，這是預期的行為；不過，如果下游應用程式預期輸出結構描述永遠不會變更，則它可能會造成問題！

> [!TIP]
> 
> 發生錯誤嗎？ 這些範例需要資料表**RTestData**。 如果您尚未建立測試資料的資料表，請回到本主題：[處理輸入和輸出](../tutorials/rtsql-working-with-inputs-and-outputs.md)。
> 
> 如果您已經建立資料表，但是仍然收到錯誤，請確定您在內容包含資料表的資料庫，而不是在執行預存程序**主要**或另一個資料庫。
> 
> 此外，我們建議您避免使用這些範例的暫存資料表。 某些 R 用戶端會終止批次刪除暫存資料表之間的連線。

## <a name="merge-or-multiply-columns-of-different-length"></a>合併或相乘不同長度的資料行

R 提供使用向量大小不同，以及將這些資料行類似結構結合成資料框架的絕佳彈性。 向量的清單看起來像是一個資料表，但它們不遵循用以管理資料庫資料表的所有規則。

例如，下列指令碼定義長度為 6 的數值陣列，並將它儲存在 R 變數 `df1` 中。 數字的陣列會在與 RTestData 資料表，其中包含三 （3） 值的整數，以便在新的資料範圍內，結合`df2`。

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

- SQL Server 將資料從查詢推送到啟動控制板服務所管理 R 處理序，並將它轉換成更高的效率的內部表示法。
- R 執行階段會將資料載入 data.frame 變數，並對資料執行自己的作業。
- 資料庫引擎會使用受保護的內部連線來將資料傳回至 SQL server，並根據 SQL Server 資料類型顯示資料。
- 藉由使用可發出 SQL 查詢並處理表格式資料集的用戶端或網路程式庫來連接到 SQL Server，您就能取得資料。 此用戶端應用程式可能會以其他方式影響資料。

若要查看其運作方式，請在 AdventureWorksDW 資料倉儲上執行這類查詢。 此檢視會傳回用來建立預測的銷售資料。

```sql
SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW2014].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = 'M200 Europe'
           ORDER BY ReportingDate ASC
```

> [!NOTE]
> 
> 您可以使用任何版本的 AdventureWorks，或建立不同的查詢使用您自己的資料庫。 重點是要再試一次來處理某些包含文字、 日期時間和數字值的資料。

現在，請嘗試貼上此查詢，做為預存程序的輸入。

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
      , @script = N' str(InputDataSet);
      OutputDataSet <- InputDataSet;'
      , @input_data_1 = N'
           SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW2014].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = ''M200 Europe''
           ORDER BY ReportingDate ASC ;'
WITH RESULT SETS undefined;
```

如果您收到錯誤，您可能需要對查詢文字進行一些編輯。 例如，WHERE 子句中的字串述詞必須以兩組單引號括住。

讓查詢能夠正常運作之後，檢閱 `str` 函數的結果，以查看 R 如何處理輸入資料。

**結果**

```
STDOUT message(s) from external script: 'data.frame':    37 obs. of  3 variables:
STDOUT message(s) from external script: $ ReportingDate: POSIXct, format: "2010-12-24 23:00:00" "2010-12-24 23:00:00"
STDOUT message(s) from external script: $ ProductSeries: Factor w/ 1 levels "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1
STDOUT message(s) from external script: $ Amount       : num  3400 16925 20350 16950 16950
```

+ 已使用 R 資料類型 **POSIXct** 來處理 datetime 資料行。
+ 文字資料行 」 ProductSeries"已被識別為**因素**，這表示類別變數。 預設會處理字串值以做為因數。 如果您將字串傳遞至 R，則會將它轉換為整數，以供內部使用，接著對應回輸出上的字串。

### <a name="summary"></a>摘要

即使這些簡短的範例中，從您所見不必做為輸入傳遞 SQL 查詢時，請檢查資料轉換的效果。 由於 R 不支援某些 SQL Server 資料類型的請考慮下列方式以避免發生錯誤：

+ 事先測試您的資料，並確認資料行或您可能有問題時傳遞至 R 程式碼的結構描述中的值。
+ 個別指定輸入資料來源中的資料行，而不是使用 `SELECT *`，並了解將如何處理每個資料行。
+ 在準備輸入資料時視需要執行明確的轉型，以避免出現意外狀況。
+ 避免傳遞的資料行 （例如 GUID 或 rowguids 的資料） 會導致錯誤，而且不適合用於模型化。

如需有關支援與不支援資料類型的詳細資訊，請參閱[R 程式庫和資料型別](../r/r-libraries-and-data-types.md)。

執行階段字串轉換成數值的因素的效能影響的相關資訊，請參閱[SQL Server R 服務效能微調](../r/sql-server-r-services-performance-tuning.md)。

## <a name="next-lesson"></a>下一課

在下一個步驟中，您要學習如何將 R 函數套用至 SQL Server 資料。

[使用 R 函式搭配 SQL Server 資料](../../advanced-analytics/tutorials/rtsql-using-r-functions-with-sql-server-data.md)
