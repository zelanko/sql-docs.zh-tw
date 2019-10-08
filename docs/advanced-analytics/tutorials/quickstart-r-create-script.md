---
title: 建立和執行簡單的 R 腳本
titleSuffix: SQL Server Machine Learning Services
description: 在具有 SQL Server Machine Learning 服務的 SQL Server 實例中，建立並執行簡單的 R 腳本。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e49b01d3c3a4ac743d6614d66cc7864aee946460
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2019
ms.locfileid: "72006037"
---
# <a name="quickstart-create-and-run-simple-r-scripts-with-sql-server-machine-learning-services"></a>快速入門：使用 SQL Server Machine Learning 服務來建立和執行簡單的 R 腳本
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本快速入門中，您將使用[SQL Server Machine Learning 服務](../what-is-sql-server-machine-learning.md)，建立並執行一組簡單的 R 腳本。 您將瞭解如何在預存程式[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)中包裝語式正確的 R 腳本，並在 SQL Server 實例中執行腳本。

## <a name="prerequisites"></a>必要條件

- 本快速入門需要使用已安裝 R 語言的[SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)，來存取 SQL Server 的實例。

  您的 SQL Server 實例可以位於 Azure 虛擬機器或內部部署中。 請注意，預設會停用外部腳本功能，因此您可能需要[啟用外部腳本](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)，並在開始之前確認**SQL Server Launchpad 服務**正在執行。

- 您也需要工具來執行包含 R 腳本的 SQL 查詢。 您可以使用任何資料庫管理或查詢工具來執行這些腳本，只要它可以連接到 SQL Server 實例，並執行 T-SQL 查詢或預存程式即可。 本快速入門使用[SQL Server Management Studio （SSMS）](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="run-a-simple-script"></a>執行簡單的腳本

若要執行 R 腳本，您會將它當做引數傳遞至系統預存程式[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。
這個系統預存程式會在 SQL Server 內容中啟動 R 執行時間、將資料傳遞至 R、安全地管理 R 使用者會話，並將任何結果傳回用戶端。

在下列步驟中，您將在 SQL Server 實例中執行此範例 R 腳本：

```r
a <- 1
b <- 2
c <- a/b
d <- a*b
print(c(c, d))
```

1. 開啟**SQL Server Management Studio** ，並連接到您的 SQL Server 實例。

1. 將完整的 R 腳本傳遞至 @no__t 0 預存程式。

   腳本會透過 `@script` 引數傳遞。 @No__t-0 引數內的所有專案都必須是有效的 R 程式碼。

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
    a <- 1
    b <- 2
    c <- a/b
    d <- a*b
    print(c(c, d))
    '
    ```

1. 會計算正確的結果，且 R `print` 函數會將結果傳回至 [**訊息**] 視窗。

   看起來應該會像這樣。

    **結果**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>執行 Hello World 腳本

典型的範例腳本只會輸出字串 "Hello World"。 執行下列命令。

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'OutputDataSet<-InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

@No__t-0 預存程式的輸入包括：

| | |
|-|-|
| @language | 定義要呼叫的語言擴充功能，在此案例中為 R |
| @script | 定義傳遞至 R 執行時間的命令。 您的整個 R 指令碼必須以 Unicode 文字的格式包含在此引數中。 您也可以將文字新增至**Nvarchar**類型的變數，然後呼叫變數 |
| @input_data_1 | 查詢所傳回的資料，傳遞至 R 執行時間，會將資料傳回 SQL Server 做為資料框架 |
|WITH RESULT SETS | 子句會定義 SQL Server 的傳回資料表的架構，並加入 "Hello World" 做為資料行名稱，並將**int**用於資料類型 |

此命令會輸出下列文字：

| 世界您好 |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>使用輸入和輸出

根據預設，`sp_execute_external_script` 會接受單一資料集做為輸入，這通常是您以有效 SQL 查詢的形式提供。 然後，它會傳回單一 R 資料框架作為輸出。

現在，讓我們使用 `sp_execute_external_script` 的預設輸入和輸出變數：**InputDataSet**和**OutputDataSet**。

1. 建立測試資料的小型資料表。

    ```sql
    CREATE TABLE RTestData (col1 INT NOT NULL)
    
    INSERT INTO RTestData
    VALUES (1);
    
    INSERT INTO RTestData
    VALUES (10);
    
    INSERT INTO RTestData
    VALUES (100);
    GO
    ```

1. 使用 `SELECT` 語句來查詢資料表。
  
    ```sql
    SELECT *
    FROM RTestData
    ```

    **結果**

    ![RTestData 資料表的內容](./media/select-rtestdata.png)

1. 執行下列 R 腳本。 它會使用 `SELECT` 語句來抓取資料表中的資料，並透過 R 執行時間傳遞，然後傳回資料做為資料框架。 @No__t-0 子句會定義針對 SQL 傳回之資料表的架構，並加入資料行名稱*NewColName*。

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **結果**

    ![從資料表傳回資料的 R 腳本輸出](./media/r-output-rtestdata.png)

1. 現在讓我們來變更輸入和輸出變數的名稱。 預設的輸入和輸出變數名稱為**InputDataSet**和**OutputDataSet**，此腳本會將名稱變更為**SQL_in**和**SQL_out**：

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N' SQL_out <- SQL_in;'
        , @input_data_1 = N' SELECT 12 as Col;'
        , @input_data_1_name = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    請注意，R 會區分大小寫。 R 腳本中使用的輸入和輸出變數（**SQL_out**、 **SQL_in**）必須符合以 `@input_data_1_name` 和 `@output_data_1_name` （包括大小寫）定義的名稱。

   > [!TIP]
   > 只有一個輸入資料集可以當作參數傳遞，您只能傳回一個資料集。 不過，您可以從 R 程式碼內部呼叫其他資料集，而且除了資料集之外，您還可以傳回其他類型的輸出。 您也可以將 OUTPUT 關鍵字新增至任何參數，讓它傳回結果。

1. 您也可以使用沒有輸入資料的 R 腳本來產生值（`@input_data_1` 會設定為空白）。

   下列腳本會輸出 "hello" 和 "world" 文字。

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
    mytextvariable <- c("hello", " ", "world");
    OutputDataSet <- as.data.frame(mytextvariable);
    '
        , @input_data_1 = N''
    WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
    ```

    **結果**

    ![使用 @script 做為輸入的查詢結果](./media/r-data-generated-output.png)

## <a name="check-r-version"></a>檢查 R 版本

如果您想要查看 SQL Server 實例中所安裝的 R 版本，請執行下列腳本。

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(version)';
GO
```

R `print` 函數會將版本傳回至 [**訊息**] 視窗。 在下面的範例輸出中，您可以看到，在此情況下，已安裝 R 版本3.4.4。

**結果**

```text
STDOUT message(s) from external script:
                   _
platform       x86_64-w64-mingw32
arch           x86_64
os             mingw32
system         x86_64, mingw32
status
major          3
minor          4.4
year           2018
month          03
day            15
svn rev        74408
language       R
version.string R version 3.4.4 (2018-03-15)
nickname       Someone to Lean On
```

## <a name="list-r-packages"></a>列出 R 套件

Microsoft 提供許多與 SQL Server Machine Learning 服務預先安裝的 R 套件。

若要查看已安裝的 R 套件清單（包括版本、相依性、授權和程式庫路徑資訊），請執行下列腳本。

```SQL
EXEC sp_execute_external_script @language = N'R'
    , @script = N'
OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
WITH result sets((
            Package NVARCHAR(255)
            , Version NVARCHAR(100)
            , Depends NVARCHAR(4000)
            , License NVARCHAR(1000)
            , LibPath NVARCHAR(2000)
            ));
```

輸出來自于 R 中的 `installed.packages()`，並以結果集的形式傳回。

**結果**

![R 中已安裝的套件](./media/rsql-installed-packages.png) 

## <a name="next-steps"></a>後續步驟

若要瞭解如何在 SQL Server Machine Learning 服務中使用 R 時使用資料結構，請遵循此快速入門：

> [!div class="nextstepaction"]
> [在 SQL Server Machine Learning 服務中使用 R 處理資料類型和物件](quickstart-r-data-types-and-objects.md)

如需在 SQL Server Machine Learning 服務中使用 R 的詳細資訊，請參閱下列文章：

- [使用 SQL Server Machine Learning 服務撰寫 advanced R 函數](quickstart-r-functions.md)
- [使用 SQL Server Machine Learning 服務在 R 中建立預測模型並為其評分](quickstart-r-train-score-model.md)
- [什麼是 SQL Server Machine Learning 服務（Python 和 R）？](../what-is-sql-server-machine-learning.md)
