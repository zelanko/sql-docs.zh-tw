---
title: "使用輸入和輸出 (SQL 快速入門中的 R) |Microsoft 文件"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
- SQL
ms.assetid: 75480e5c-f37f-45b9-a176-67e08e9a9daf
caps.latest.revision: 7
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: a5ffcfafc29f0b741d8e6ada0d50ef6f94fecc7f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# <a name="working-with-inputs-and-outputs-r-in-sql-quickstart"></a>使用輸入和輸出 (SQL 快速入門中的 R)

當您想要在 SQL Server 中執行 R 程式碼時，您必須包裝 R 指令碼中的系統預存程序， [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 這個預存程序是用來在 SQL Server 內容中啟動 R 執行階段，這會將資料傳遞到 R，安全地管理 R 使用者工作階段，並將任何結果傳回用戶端。

## <a name="bkmk_SSMSBasics"></a>建立一些簡單的測試資料

建立測試資料的小型資料表，執行下列 T-SQL 陳述式：

```sql
CREATE TABLE RTestData ([col1] int not null) ON [PRIMARY]
INSERT INTO RTestData   VALUES (1);
INSERT INTO RTestData   VALUES (10);
INSERT INTO RTestData   VALUES (100) ;
GO
```

建立資料表之後，請使用下列陳述式來查詢資料表：
  
```sql
SELECT * FROM RTestData
```

**結果**

|col1|
|------|
|*1*|
|*10*|
|*100*|

## <a name="get-the-same-data-using-r-script"></a>使用 R 指令碼取得相同的資料

建立資料表之後，請執行下列陳述式：

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N' OutputDataSet <- InputDataSet;'
    , @input_data_1 = N' SELECT *  FROM RTestData;'
    WITH RESULT SETS (([NewColName] int NOT NULL));
```

從資料表中取得資料、 來回存取透過 R 執行階段，以及傳回值的資料行名稱， *NewColName*。

**結果**

![rsql_basictut_getsamedataR](media/rsql-basictut-getsamedatar.PNG)


**註解**

+ 在 Management Studio 中，表格式結果會在 [值] 窗格中傳回。 R 執行階段所傳回的訊息，會在 [訊息] 窗格中會提供 。
+ *@language* 參數會定義要呼叫的語言擴充功能，在本例中為 R。
+ 在 *@script* 參數中，您可以定義命令以傳遞至 R 執行階段。 您的整個 R 指令碼必須以 Unicode 文字的格式包含在此引數中。 您也可以將文字新增至 **nvarchar** 類型的變數，並呼叫該變數。
+ 查詢所傳回的資料會傳遞到 R 執行階段，它會以資料框架的格式將資料傳回 SQL Server。
+ WITH RESULT SETS 子句會針對 SQL Server 定義傳回資料表的結構描述。

## <a name="change-input-or-output-variables"></a>變更輸入或輸出變數

上述範例使用預設的輸入及輸出變數名稱 (_InputDataSet_ 和 _OutputDataSet_)。 若要定義與 _InputDatSet_ 相關聯的輸入資料，您必須使用 *@input_data_1* 變數。

在本範例中，預存程序的輸出和輸入變數名稱已分別變更為 *SQL_Out* 和 *SQL_In*︰

```sql
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N' SQL_out <- SQL_in;'
  , @input_data_1 = N' SELECT 12 as Col;'
  , @input_data_1_name  = N'SQL_In'
  , @output_data_1_name =  N'SQL_Out'
  WITH RESULT SETS (([NewColName] int NOT NULL));
```

您是否已收到錯誤，「 物件 SQL\_中找不到 」？ 這是因為 R 有區分大小寫！ 在範例中，R 指令碼是使用 *SQL_in* 和 *SQL_out* 變數，但是針對預存程序的參數是使用 *SQL_In* 和 *SQL_Out* 變數。

這是因為 R 會區分大小寫。 在範例中，R 指令碼是使用 *SQL_in* 和 *SQL_out* 變數，但是針對預存程序的參數是使用 *SQL_In* 和 *SQL_Out* 變數。
嘗試更正**只** *SQL_In*變數，並重新執行預存程序。

現在您取得**不同**錯誤：

```Error
EXECUTE statement failed because its WITH RESULT SETS clause specified 1 result set(s), but the statement only sent 0 result set(s) at run time.
```

我們顯示您這個錯誤因為可預期會測試新的 R 程式碼時，通常請參閱。 這表示在 R 指令碼執行成功，但 SQL Server 接收到的任何資料，或接收到錯誤或非預期的資料。

在此案例中，輸出結構描述 (以 **WITH** 開頭的行) 指定應傳回一個資料行的整數資料，但由於 R 把資料放在不同的變數中，因此沒有將任何資料傳回至 SQL Server，因而出現該錯誤。 若要修正此錯誤，更正第二個變數的名稱。

**請記住這些需求 ！**

- 變數名稱必須遵循有效 SQL 識別項的規則。
- 參數的順序很重要。 若要使用選擇性的參數 *@input_data_1_name* 和 *@output_data_1_name*，您必須先指定必要的參數 *@input_data_1*和 *@output_data_1*。
- 只有一個輸入資料集可以當作參數傳遞，您只能傳回一個資料集。 不過，您可以從 R 程式碼內部呼叫其他資料集，而且除了資料集之外，您還可以傳回其他類型的輸出。 您也可以將 OUTPUT 關鍵字新增至任何參數，讓它傳回結果。 本教學課程稍後會提供簡單的範例。
- 為了 SQL Server，`WITH RESULT SETS` 陳述式會定義資料的結構描述。 您必須針對從 R 傳回的每個資料行，提供 SQL 相容的資料類型。您也可以使用結構描述定義來提供新的資料行名稱，您並不須要使用 R 資料框架的資料行名稱。 在某些情況下，這個子句是選擇性的;請省略它，並查看 會發生什麼事。

## <a name="generate-results-using-r"></a>使用 R 產生結果

您也可以只使用 R 指令碼產生值，並將 _@input_data_1_ 中的輸入查詢字串保持空白。 或者，使用有效的 SQL SELECT 陳述式做為預留位置，而不使用 R 指令碼中的 SQL 結果。

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
   , @script = N' mytextvariable <- c("hello", " ", "world");
       OutputDataSet <- as.data.frame(mytextvariable);'
   , @input_data_1 = N' SELECT 1 as Temp1'
   WITH RESULT SETS (([Col1] char(20) NOT NULL));
```

**結果**

*Col1*
*hello*
<code>   </code>
*world*

## <a name="next-lesson"></a>下一課

您會檢查一些在 R 和 SQL Server 之間傳遞資料時可能會遇到的問題，例如隱含轉換，以及 R 和 SQL 之間的表格式資料差異。

[R 與 SQL 資料類型及資料物件](../tutorials/rtsql-r-and-sql-data-types-and-data-objects.md)

