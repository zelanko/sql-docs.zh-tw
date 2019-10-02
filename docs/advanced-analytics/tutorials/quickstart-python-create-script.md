---
title: 建立和執行簡單的 Python 腳本
titleSuffix: SQL Server Machine Learning Services
description: 在具有 SQL Server Machine Learning 服務的 SQL Server 實例中，建立並執行簡單的 Python 腳本。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a6f7fe62f746a8f6e74ebdf9f766b76c0edc720a
ms.sourcegitcommit: 9221a693d4ab7ae0a7e2ddeb03bd0cf740628fd0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2019
ms.locfileid: "71204295"
---
# <a name="quickstart-create-and-run-simple-python-scripts-with-sql-server-machine-learning-services"></a>快速入門：使用 SQL Server Machine Learning 服務來建立及執行簡單的 Python 腳本
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本快速入門中，您將使用[SQL Server Machine Learning 服務](../what-is-sql-server-machine-learning.md)，建立並執行一組簡單的 Python 腳本。 您將瞭解如何在預存程式[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)中包裝格式正確的 Python 腳本，並在 SQL Server 實例中執行腳本。

## <a name="prerequisites"></a>必要條件

- 本快速入門需要使用已安裝 Python 語言的[SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)，來存取 SQL Server 的實例。

- 您也需要工具來執行包含 Python 腳本的 SQL 查詢。 您可以使用任何資料庫管理或查詢工具來執行這些腳本，只要它可以連接到 SQL Server 實例，並執行 T-SQL 查詢或預存程式即可。 本快速入門使用[SQL Server Management Studio （SSMS）](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="run-a-simple-script"></a>執行簡單的腳本

若要執行 Python 腳本，您會將它當做引數傳遞至系統預存程式[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。
這個系統預存程式會在 SQL Server 內容中啟動 Python 執行時間、將資料傳遞至 Python、安全地管理 Python 使用者會話，並將任何結果傳回用戶端。

在下列步驟中，您將在 SQL Server 實例中執行此 Python 腳本範例：

```python
a = 1
b = 2
c = a/b
d = a*b
print(c, d)
```

1. 在連接到您的 SQL Server 實例的**SQL Server Management Studio**中，開啟新的查詢視窗。

1. 將完整的 Python 腳本傳遞給`sp_execute_external_script`預存程式。

   腳本會透過`@script`引數傳遞。 引數內`@script`的所有專案都必須是有效的 Python 程式碼。

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

1. 會計算正確的結果，且 Python `print`函式會將結果傳回至 [**訊息**] 視窗。

   看起來應該會像這樣。

    **結果**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>執行 Hello World 腳本

典型的範例腳本只會輸出字串 "Hello World"。 執行下列命令。

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'OutputDataSet = InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

預存程式`sp_execute_external_script`的輸入包括：

| | |
|-|-|
| @language | 定義要呼叫的語言擴充功能，在此案例中為 Python |
| @script | 定義傳遞至 Python 執行時間的命令<br>您的整個 Python 腳本必須以 Unicode 文字的形式包含在此引數中。 您也可以將文字新增至**Nvarchar**類型的變數，然後呼叫變數 |
| @input_data_1 | 查詢所傳回的資料，傳遞至 Python 執行時間，這會將資料傳回 SQL Server 做為資料框架 |
|WITH RESULT SETS | 子句會定義 SQL Server 所傳回之資料表的架構，在此案例中，會加入 "Hello World" 做為資料行名稱，並將**int**用於資料類型 |

此命令會輸出下列文字：

| 世界您好 |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>使用輸入和輸出

根據預設， `sp_execute_external_script`會接受單一資料集做為輸入，這通常是您以有效 SQL 查詢的形式提供。 然後，它會傳回單一 Python 資料框架作為輸出。

現在，讓我們使用的預設輸入和輸出變數`sp_execute_external_script`：**InputDataSet**和**OutputDataSet**。

1. 建立測試資料的小型資料表。

    ```sql
    CREATE TABLE PythonTestData (col1 INT NOT NULL)
    
    INSERT INTO PythonTestData
    VALUES (1);
    
    INSERT INTO PythonTestData
    VALUES (10);
    
    INSERT INTO PythonTestData
    VALUES (100);
    GO
    ```

1. `SELECT`使用語句來查詢資料表。
  
    ```sql
    SELECT *
    FROM PythonTestData
    ```

    **結果**

    ![PythonTestData 資料表的內容](./media/select-pythontestdata.png)

1. 執行下列 Python 腳本。 它會使用`SELECT`語句來抓取資料表中的資料、透過 Python 執行時間傳遞，然後傳回資料做為資料框架。 子句會定義針對 SQL 傳回之資料表的架構，並加入資料行名稱*NewColName。* `WITH RESULT SETS`

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **結果**

    ![從資料表傳回資料的 Python 腳本輸出](./media/python-output-pythontestdata.png)

1. 現在，變更輸入和輸出變數的名稱。 預設的輸入和輸出變數名稱為**InputDataSet**和**OutputDataSet**，下列腳本會將名稱變更為**SQL_in**和**SQL_out**：

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'SQL_out = SQL_in;'
        , @input_data_1 = N'SELECT 12 as Col;'
        , @input_data_1_name  = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    請注意，Python 會區分大小寫。 Python 腳本中使用的輸入和輸出變數（**SQL_out**、 **SQL_in**）必須符合以`@input_data_1_name`和`@output_data_1_name`定義的名稱，包括大小寫。

   > [!TIP]
   > 只有一個輸入資料集可以當作參數傳遞，您只能傳回一個資料集。 不過, 您可以從 Python 程式碼內部呼叫其他資料集, 而且除了資料集之外, 您還可以傳回其他類型的輸出。 您也可以將 OUTPUT 關鍵字新增至任何參數，讓它傳回結果。

1. 您也可以使用不含輸入資料的 Python 腳本（`@input_data_1`設為空白）來產生值。

   下列腳本會輸出 "hello" 和 "world" 文字。

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   mytextvariable = pandas.Series(["hello", " ", "world"]);
   OutputDataSet = pd.DataFrame(mytextvariable);
   '
       , @input_data_1 = N''
   WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
   ```

   **結果**

   ![使用@script作為輸入的查詢結果](./media/python-data-generated-output.png)

> [!NOTE]
> Python 會使用開頭的空格來分組語句。 因此，當內嵌的 Python 腳本跨越多行（如上述腳本所示）時，請勿嘗試將 Python 命令縮排到與 SQL 命令相同的行。 例如，此腳本將會產生錯誤：

  ```text
  EXECUTE sp_execute_external_script @language = N'Python'
      , @script = N'
      import pandas as pd
      mytextvariable = pandas.Series(["hello", " ", "world"]);
      OutputDataSet = pd.DataFrame(mytextvariable);
      '
      , @input_data_1 = N''
  WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
  ```

## <a name="check-python-version"></a>檢查 Python 版本

如果您想要查看 SQL Server 實例中所安裝的 Python 版本，請執行下列腳本。

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import sys
print(sys.version)
'
GO
```

Python `print`函式會將版本傳回至 [**訊息**] 視窗。 在下面的範例輸出中，您可以看到，在此情況下，已安裝 Python 版本3.5.2。

**結果**

```text
STDOUT message(s) from external script: 
3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
```

## <a name="list-python-packages"></a>列出 Python 套件

Microsoft 提供一些在您的 SQL Server 實例中，預先安裝 SQL Server Machine Learning 服務的 Python 套件。

若要查看已安裝的 Python 套件清單（包括版本），請執行下列腳本。

```SQL
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import pip
for i in pip.get_installed_distributions():
    print(i)
'
GO
```

輸出來自`pip.get_installed_distributions()`于 Python 中的，並以`STDOUT`訊息的形式傳回。

**結果**

```text
STDOUT message(s) from external script:
xlwt 1.2.0
XlsxWriter 0.9.6
xlrd 1.0.0
win-unicode-console 0.5
widgetsnbextension 2.0.0
wheel 0.29.0
Werkzeug 0.12.1
wcwidth 0.1.7
unicodecsv 0.14.1
traitlets 4.3.2
tornado 4.4.2
toolz 0.8.2
. . .
```

## <a name="next-steps"></a>後續步驟

若要在 SQL Server 中使用 Python 建立機器學習模型，請遵循此快速入門：

> [!div class="nextstepaction"]
> [使用 SQL Server Machine Learning 服務在 Python 中建立預測模型並為其評分](quickstart-python-train-score-model.md)

如需 SQL Server Machine Learning 服務的詳細資訊，請參閱下列文章。

- [在 SQL Server Machine Learning 服務中使用 Python 處理資料類型和物件](quickstart-python-data-structures.md)
- [什麼是 SQL Server Machine Learning 服務（Python 和 R）？](../what-is-sql-server-machine-learning.md)
