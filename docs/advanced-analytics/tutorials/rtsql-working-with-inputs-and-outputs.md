---
title: 處理輸入和輸出 (SQL Server Machine Learning) 使用的快速入門 |Microsoft Docs
description: 此快速入門中的 SQL Server 中的 R 指令碼，了解如何建構輸入和輸出至 sp_execute_external_script 的系統預存程序。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/15/2018
ms.topic: quickstart
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b41a8c30cd0ecbe040819478c0cadece1b9eb704
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086580"
---
# <a name="quickstart-handle-inputs-and-outputs-using-r-in-sql-server"></a>快速入門： 處理輸入及輸出在 SQL Server 中使用 R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

當您想要在 SQL Server 中執行 R 程式碼時，您必須在預存程序中包裝 R 指令碼。 您可以將寫入其中一個，或傳遞至 R 指令碼[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 此系統預存程序用以啟動 SQL Server，其會將資料傳遞至 R，內容中的 R 執行階段安全地管理 R 使用者工作階段，並傳回給用戶端的任何結果。

## <a name="prerequisites"></a>先決條件

先前的快速入門中， [Hello World R 與 SQL](rtsql-using-r-code-in-transact-sql-quickstart.md)，提供資訊並連結設定本快速入門所需的 R 環境。

<a name="bkmk_SSMSBasics"></a>

## <a name="create-some-simple-test-data"></a>建立一些簡單的測試資料

執行下列 T-SQL 陳述式，以建立小型測試資料的資料表：

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

![RTestData 資料表的內容](media/quickstart-r-working-input-outputs-results-1.png)


## <a name="get-the-same-data-using-r-script"></a>使用 R 指令碼取得相同的資料

建立資料表之後，請執行下列陳述式：

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N' OutputDataSet <- InputDataSet;'
    , @input_data_1 = N' SELECT *  FROM RTestData;'
    WITH RESULT SETS (([NewColName] int NOT NULL));
```

從資料表取得資料、 進行來回在 R 執行階段，以及傳回的資料行名稱，值*NewColName*。

**結果**

![rsql_basictut_getsamedataR](media/rsql-basictut-getsamedatar.PNG)


**註解**

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

您有收到錯誤，「 物件 SQL\_中找不到"？ 這是因為 R 有區分大小寫！ 在範例中，R 指令碼是使用 *SQL_in* 和 *SQL_out* 變數，但是針對預存程序的參數是使用 *SQL_In* 和 *SQL_Out* 變數。

請嘗試更正**僅** *SQL_In*變數*@script*並重新執行預存程序。

現在你**不同**錯誤：

```Error
EXECUTE statement failed because its WITH RESULT SETS clause specified 1 result set(s), but the statement only sent 0 result set(s) at run time.
```

我們將顯示這個錯誤因為您可以預期測試新的 R 程式碼時，通常會看到。 這表示 R 指令碼執行成功，但 SQL Server 不收到任何資料，或接收到錯誤或非預期的資料。

在此案例中，輸出結構描述 (以 **WITH** 開頭的行) 指定應傳回一個資料行的整數資料，但由於 R 把資料放在不同的變數中，因此沒有將任何資料傳回至 SQL Server，因而出現該錯誤。 若要修正錯誤，更正第二個變數的名稱。

**請記住這些需求 ！**

- 變數名稱必須遵循有效 SQL 識別項的規則。
- 參數的順序很重要。 若要使用選擇性的參數 *@input_data_1_name* 和 *@output_data_1_name*，您必須先指定必要的參數 *@input_data_1*和 *@output_data_1*。
- 只有一個輸入資料集可以當作參數傳遞，您只能傳回一個資料集。 不過，您可以從 R 程式碼內部呼叫其他資料集，而且除了資料集之外，您還可以傳回其他類型的輸出。 您也可以將 OUTPUT 關鍵字新增至任何參數，讓它傳回結果。 本教學課程稍後會提供簡單的範例。
- 為了 SQL Server，`WITH RESULT SETS` 陳述式會定義資料的結構描述。 您必須針對從 R 傳回的每個資料行，提供 SQL 相容的資料類型。您也可以使用結構描述定義來提供新的資料行名稱，您並不須要使用 R 資料框架的資料行名稱。 在某些情況下，這個子句是選擇性的;嘗試省略它，看看結果如何。

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

![使用查詢結果@script做為輸入](media/quickstart-r-working-input-outputs-results-3.png)

## <a name="next-steps"></a>後續步驟

檢查 R 和 SQL Server 之間傳遞資料，例如隱含轉換，以及 R 與 SQL 之間的差異在表格式資料時，可能會遇到的問題。

> [!div class="nextstepaction"]
> [快速入門： 處理資料型別和物件](../tutorials/rtsql-r-and-sql-data-types-and-data-objects.md)