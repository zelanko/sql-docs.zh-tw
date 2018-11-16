---
title: R 和 SQL 資料類型和物件 (SQL Server Machine Learning) 的相關快速入門 |Microsoft Docs
description: 在本快速入門，了解如何使用資料類型與 R 和 SQL Server 中的資料物件。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/15/2018
ms.topic: quickstart
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 2e861bf2d8daf2460fbffcf2d92fcd33f859cd78
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51699111"
---
# <a name="quickstart-handle-data-types-and-objects-using-r-in-sql-server"></a>快速入門： 處理資料類型與 SQL Server 中使用 R 的物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本快速入門，取得實際操作簡介 R 與 SQL Server 之間移動資料時，會發生的常見問題。 使用您自己的指令碼中的資料時，您可以透過這個練習中此體驗會提供必要的背景。

若要事先知道常見的問題包括：

+ 資料類型有時不相符
+ 可能會發生隱含轉換
+ 有時需要轉型和轉換作業
+ R 和 SQL 會使用不同的資料物件

## <a name="prerequisites"></a>先決條件

先前的快速入門中， [Hello World R 與 SQL](rtsql-using-r-code-in-transact-sql-quickstart.md)，提供資訊並連結設定本快速入門所需的 R 環境。

## <a name="always-return-a-data-frame"></a>一律會傳回資料框架

當您的指令碼將結果從 R 傳回到 SQL Server 時，它必須傳回資料做為 **data.frame**。 您在指令碼中產生的任何其他類型物件 (不論是清單、因數、向量或二進位資料)，如果您想要輸出它以做為預存程序結果的一部分，就必須將它轉換為資料框架。 幸好有多個 R 函數可用來支援將其他物件變更為資料框架。 您甚至可將二進位模型序列化，並在資料框架中傳回它，您將在本教學課程稍後執行此動作。

首先，讓我們來試驗一些 R 的基本 R 物件 — 向量、 矩陣和清單，並查看轉換成資料框架如何變更傳遞至 SQL Server 的輸出。

比較在 r 中的這些兩個 「 Hello World 」 指令碼指令碼看起來幾乎完全相同，但第一個會傳回單一資料行的三個值，而第二個則傳回單一的三個資料行值，每個。

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

## <a name="identify-schema-and-data-types"></a>識別結構描述和資料類型

為何結果如此不同？ 

您通常可以使用 R `str()` 命令來找到答案。 在 R 指令碼中的任一處加入函數 `str(object_name)`，以傳回指定 R 物件的資料結構描述做為資訊訊息。 若要檢視訊息，可查看 Visual Studio Code 的 [訊息] 窗格，或 SSMS 中的 [訊息] 索引標籤。

若要了解為什麼範例 1 和範例 2 會有如此不同的結果，在每個陳述式中 _@script_ 變數定義的結尾插入一行 `str(OutputDataSet)`，如下：

**範例 1 使用 str 函式新增**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' mytextvariable <- c("hello", " ", "world");
      OutputDataSet <- as.data.frame(mytextvariable);
      str(OutputDataSet);'
      , @input_data_1 = N'  '
;
```

**範例 2 使用 str 函式新增**

```sql
EXECUTE sp_execute_external_script
  @language = N'R', 
  @script = N' OutputDataSet <- data.frame(c("hello"), " ", c("world"));
    str(OutputDataSet);' , 
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

如您所見，稍微變化一下 R 語法，就會對結果的結構描述產生極大的影響。 我們不會詳述原因，因為 R 資料類型的差異會更詳盡的說明這篇文章中 Hadley Wickham 所著： [R 資料結構](https://adv-r.had.co.nz/Data-structures.html)。

現在只需注意，您需要在將 R 物件強制轉型為資料框架時檢查預期的結果。

> [!TIP]
> 
> 您可以也使用 R 識別函數，例如`is.matrix`， `is.vector`，以傳回內部資料結構的相關資訊。

## <a name="implicit-conversion-of-data-objects"></a>資料物件的隱含轉換

如果這兩個資料物件具有相同數目的維度，或者如果任一個資料類型包含異質資料類型，則每個 R 資料物件都會有自己的規則，用於在結合其他資料物件時如何處理資料。

例如，假設您執行下列陳述式執行矩陣乘法使用。您具有三個值的單一資料行矩陣乘以的陣列，具有四個值，並因此預期 4x3 矩陣。

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

為什麼？ 在此情況下，因為兩個引數可以處理為相同長度的向量，R 會傳回內積作為矩陣。  根據線性代數的規則，這是預期的行為；不過，如果下游應用程式預期輸出結構描述永遠不會變更，則它可能會造成問題！

> [!TIP]
> 
> 發生錯誤嗎？ 這些範例需要資料表**RTestData**。 如果您尚未建立測試資料資料表，請回到本主題以建立資料表：[處理輸入和輸出](../tutorials/rtsql-working-with-inputs-and-outputs.md)。
> 
> 如果您已經建立資料表，但仍收到錯誤，請確定您的資料庫包含資料表，而不是在內容中執行預存程序**主要**或另一個資料庫。
> 
> 此外，我們建議您避免使用這些範例中的暫存資料表。 有些 R 用戶端將會終止批次刪除暫存資料表之間的連線。

## <a name="merge-or-multiply-columns-of-different-length"></a>合併或相乘不同長度的資料行

R 提供絕佳的彈性，使用不同的大小的向量，以及將這些類似資料行的結構結合成資料框架。 向量的清單看起來像是一個資料表，但它們不遵循用以管理資料庫資料表的所有規則。

例如，下列指令碼定義長度為 6 的數值陣列，並將它儲存在 R 變數 `df1` 中。 此數值陣列接著會與 RTestData 資料表，其中包含三 （3） 值的整數，以建立新的資料框架，結合`df2`。

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

- SQL Server 將資料從查詢發送至 Launchpad 服務所管理的 R 處理序，並將它轉換成內部表示法更高的效率。
- R 執行階段會將資料載入 data.frame 變數，並對資料執行自己的作業。
- 資料庫引擎會使用受保護的內部連線來將資料傳回至 SQL server，並根據 SQL Server 資料類型顯示資料。
- 藉由使用可發出 SQL 查詢並處理表格式資料集的用戶端或網路程式庫來連接到 SQL Server，您就能取得資料。 此用戶端應用程式可能會以其他方式影響資料。

若要查看其運作方式，請在上執行這類查詢[AdventureWorksDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)資料倉儲。 此檢視會傳回用來建立預測的銷售資料。

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
> 您可以使用任何版本的 AdventureWorks，或建立不同的查詢，使用您自己的資料庫。 重點是，嘗試處理一些包含文字、 日期時間和數字值的資料。

現在，嘗試將此查詢貼做為預存程序的輸入。

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

```
STDOUT message(s) from external script: 'data.frame':    37 obs. of  3 variables:
STDOUT message(s) from external script: $ ReportingDate: POSIXct, format: "2010-12-24 23:00:00" "2010-12-24 23:00:00"
STDOUT message(s) from external script: $ ProductSeries: Factor w/ 1 levels "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1
STDOUT message(s) from external script: $ Amount       : num  3400 16925 20350 16950 16950
```

+ 已使用 R 資料類型 **POSIXct** 來處理 datetime 資料行。
+ 「 ProductSeries"已被識別為文字資料行**因素**，這表示類別變數。 預設會處理字串值以做為因數。 如果您將字串傳遞至 R，則會將它轉換為整數，以供內部使用，接著對應回輸出上的字串。

### <a name="summary"></a>總結

即使這些簡短的範例中，您可以看到不必做為輸入傳遞 SQL 查詢時，請檢查資料轉換的效果。 由於 R 不支援某些 SQL Server 資料類型的請考慮這些方式來避免發生錯誤：

+ 事先測試您的資料，並確認資料行或您可能有問題時傳遞至 R 程式碼的結構描述中的值。
+ 個別指定輸入資料來源中的資料行，而不是使用 `SELECT *`，並了解將如何處理每個資料行。
+ 在準備輸入資料時視需要執行明確的轉型，以避免出現意外狀況。
+ 避免傳遞的資料行 （例如 GUID 或 rowguids 的資料） 會導致錯誤，而且不適合用於模型化。

如需有關支援與不支援的資料類型的詳細資訊，請參閱[R 程式庫和資料類型](../r/r-libraries-and-data-types.md)。

如需效能影響的執行階段字串轉換為數值因數的資訊，請參閱[SQL Server R Services 效能微調](../r/sql-server-r-services-performance-tuning.md)。

## <a name="next-step"></a>下一步

在下一個快速入門中，您將了解如何將 R 函數套用至 SQL Server 資料。

> [!div class="nextstepaction"]
> [SQL Server 資料的快速入門： 使用 R 函式](rtsql-using-r-functions-with-sql-server-data.md)
