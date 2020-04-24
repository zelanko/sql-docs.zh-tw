---
title: 快速入門：執行 R 指令碼
description: 使用 SQL Server 機器學習服務執行一組簡單的 R 指令碼。 了解如何使用預存程序 sp_execute_external_script 在 SQL Server 執行個體中執行指令碼。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/27/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 33baeba807711c1eb65b3a9c972066bb384e2542
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487293"
---
# <a name="quickstart-run-simple-r-scripts-with-sql-server-machine-learning-services"></a>快速入門：使用 SQL Server 機器學習服務執行簡單的 R 指令碼
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在此快速入門中，您將會使用 [SQL Server 機器學習服務](../sql-server-machine-learning-services.md)來執行一組簡單的 R 指令碼。 您將會了解如何使用預存程序 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 在 SQL Server 執行個體中執行指令碼。

## <a name="prerequisites"></a>Prerequisites

- 本快速入門需使用已安裝 R 語言的 [SQL Server 機器學習服務](../install/sql-machine-learning-services-windows-install.md)來存取 SQL Server 的執行個體。

  您的 SQL Server 執行個體可以位於 Azure 虛擬機器或內部部署中。 請注意，外部指令碼功能預設為停用，因此可能需要[啟用外部指令碼](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)，並在開始之前確認 **SQL Server Launchpad 服務**正在執行。

- 您也需要工具來執行包含 R 指令碼的 SQL 查詢。 您可以使用任何資料庫管理或查詢工具來執行這些指令碼，只要該工具可以連線到 SQL Server 執行個體，並執行 T-SQL 查詢或預存程序即可。 本快速入門使用 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="run-a-simple-script"></a>執行簡單的指令碼

若要執行 R 指令碼，請將它當做引數傳遞至系統預存程式，[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。
此系統預存程序會在 SQL Server 內容中啟動 R 執行階段、將資料傳遞到 R、安全地管理 R 使用者工作階段，並將任何結果傳回用戶端。

在下列步驟中，您將在 SQL Server 執行個體中執行此範例 R 指令碼：

```r
a <- 1
b <- 2
c <- a/b
d <- a*b
print(c(c, d))
```

1. 開啟 **SQL Server Management Studio** 並連線至 SQL Server 執行個體。

1. 將完整的 R 指令碼傳遞至 `sp_execute_external_script` 預存程序。

   指令碼會透過 `@script` 引數傳遞。 `@script` 引數內的所有一切都必須是有效的 R 程式碼。

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

1. 系統會計算正確的結果，且 R `print` 函數會將結果傳回至 [訊息]  視窗。

   其外觀應該如下所示。

    **結果**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>執行 Hello World 指令碼

典型的範例指令碼只會輸出字串 "Hello World"。 執行下列命令。

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'OutputDataSet<-InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

`sp_execute_external_script` 預存程序的輸入包括：

| | |
|-|-|
| @language | 定義要呼叫的語言擴充功能，在本例中為 R |
| @script | 定義要傳遞至 R 執行階段的命令。 整個 R 指令碼都必須包含在這個引數中 (作為 Unicode 文字)。 您也可以將文字新增至 **Nvarchar** 類型的變數，並呼叫該變數 |
| @input_data_1 | 查詢所傳回的資料會傳遞到 R 執行階段，它會以資料框架的格式將資料傳回 SQL Server |
|使用結果集 | 子句會定義 SQL Server 傳回資料表的結構描述，然後加入 "Hello World" 做為資料行名稱，並將 **int** 用於資料類型 |

此命令會輸出下列文字：

| Hello World |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>使用者輸入和輸出

在預設情況下，`sp_execute_external_script` 會接受單一資料集做為輸入，這通常由您以有效的 SQL 查詢形式提供。 然後，它會傳回單一 R 資料框架做為輸出。

現在，讓我們使用 `sp_execute_external_script` 的預設輸入和輸出變數：**InputDataSet** 和 **OutputDataSet**。

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

1. 使用 `SELECT` 陳述式查詢資料表。
  
    ```sql
    SELECT *
    FROM RTestData
    ```

    **結果**

    ![RTestData 資料表的內容](./media/select-rtestdata.png)

1. 請執行下列 R 指令碼。 它會使用 `SELECT` 陳述式來擷取資料表中的資料、透過 R 執行階段傳遞，然後傳回資料做為資料框架。 `WITH RESULT SETS` 子句會為 SQL 定義傳回資料表的結構描述，新增資料行名稱 *NewColName*。

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **結果**

    ![從資料表傳回資料的 R 指令碼輸出](./media/r-output-rtestdata.png)

1. 現在讓我們變更輸入和輸出變數的名稱。 預設的輸入和輸出變數名稱是 **InputDataSet** 和 **OutputDataSet**，此指令碼會將名稱變更為 **SQL_in** 和 **SQL_out**：

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N' SQL_out <- SQL_in;'
        , @input_data_1 = N' SELECT 12 as Col;'
        , @input_data_1_name = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    請注意，R 區分大小寫。 R 指令碼 (**SQL_out** **SQL_in**) 中所使用的輸入和輸出變數必須比對以 `@input_data_1_name` 和 `@output_data_1_name` 定義的名稱，包括大小寫。

   > [!TIP]
   > 只有一個輸入資料集可以傳入作為參數，而且您只能傳回一個資料集。 不過，您可以從 R 程式碼內呼叫其他資料集，而且可以在資料集以外傳回其他類型的輸出。 您也可以為任何參數加上 OUTPUT 關鍵字，使其與結果一起傳回。

1. 您也可以在無輸入資料的情況下 (`@input_data_1` 設為空白)，只使用 R 指令碼產生值。

   下列指令碼輸出文字 "hello" 和 "world"。

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

    ![使用 @script 做為輸入查詢結果](./media/r-data-generated-output.png)

## <a name="check-r-version"></a>檢查 R 版本

如果您想要查看在 SQL Server 執行個體中所安裝的 R 版本，請執行下列指令碼。

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(version)';
GO
```

R `print` 函數會將版本傳回到 [訊息]  視窗。 在下方的範例輸出中，您可以看到在此案例中安裝的是 R 3.4.4 版。

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

Microsoft 提供一些透過 SQL Server 機器學習服務預先安裝的 R 套件。

若要查看已安裝 R 套件的清單 (包括版本、相依性、授權及程式庫路徑資訊)，請執行下列指令碼。

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

輸出來自 R 中的 `installed.packages()`，並以結果集的形式傳回。

**結果**

![R 中已安裝的套件](./media/rsql-installed-packages.png) 

## <a name="next-steps"></a>後續步驟

若要瞭解如何在 SQL Server 機器學習服務中使用 R 來使用資料結構，請遵循本快速入門：

> [!div class="nextstepaction"]
> [在 SQL Server 機器學習服務中使用 R 處理資料類型和物件](quickstart-r-data-types-and-objects.md)

如需在 SQL Server 機器學習服務中使用 R 的詳細資訊，請參閱下列文章：

- [使用 SQL Server 機器學習服務撰寫進階 R 函數](quickstart-r-functions.md)
- [使用 SQL Server 機器學習服務在 R 中建立預測模型並計算其分數](quickstart-r-train-score-model.md)
- [什麼是 SQL Server 機器學習服務 (Python 和 R)？](../sql-server-machine-learning-services.md)
