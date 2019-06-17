---
title: 處理輸入和輸出 Python-SQL Server Machine Learning 中的快速入門
description: 此快速入門中的 SQL Server 中的 Python 指令碼，了解如何建構輸入和輸出至 sp_execute_external_script 的系統預存程序。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: fe60197671e40317f56a62ad98ea364a238df174
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "67033399"
---
# <a name="quickstart-handle-inputs-and-outputs-using-python-in-sql-server"></a>快速入門：處理輸入及輸出在 SQL Server 中使用 Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本快速入門示範如何處理輸入及輸出時使用 SQL Server Machine Learning 服務中的 Python。

根據預設， [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)接受單一輸入資料集，這通常是您提供有效的 SQL 查詢的形式。

其他類型的輸入可以當做 SQL 變數： 比方說，您可以傳遞定型的模型為變數，例如使用序列化函式[pickle](https://docs.python.org/3.0/library/pickle.html)或是[rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)中撰寫模型二進位格式。

預存程序傳回單一的 Python [pandas](https://pandas.pydata.org/pandas-docs/stable/index.html)資料框架做為輸出，但您也可以輸出純量和做為變數的模型。 例如，您可以輸出定型的模型，做為二進位的變數，並將它傳遞至 T-SQL INSERT 陳述式，以寫入該模型的資料表。 您也可以產生繪圖 （以二進位格式） 或純量 （個別的值，例如日期和時間，所經過的時間來定型模型，等等）。

## <a name="prerequisites"></a>先決條件

先前的快速入門中，[確認 Python 存在於 SQL Server](quickstart-python-verify.md)，提供資訊並連結設定本快速入門所需的 Python 環境。

## <a name="create-the-source-data"></a>建立來源資料

執行下列 T-SQL 陳述式，以建立小型測試資料的資料表：

```sql
CREATE TABLE PythonTestData (col1 INT NOT NULL)
INSERT INTO PythonTestData VALUES (1);
INSERT INTO PythonTestData VALUES (10);
INSERT INTO PythonTestData VALUES (100);
GO
```

建立資料表之後，請使用下列陳述式來查詢資料表：
  
```sql
SELECT * FROM PythonTestData
```

**結果**

![PythonTestData 資料表的內容](./media/select-pythontestdata.png)

## <a name="inputs-and-outputs"></a>[指令碼轉換編輯器]

讓我們看看預設值的 sp_execute_external_script 的輸入和輸出變數：`InputDataSet`和`OutputDataSet`。

1. 您可以從資料表取得資料，做為您的 Python 指令碼輸入。 執行以下陳述式。 從資料表取得資料、 進行來回透過 Python 執行階段，以及傳回的資料行名稱的值*NewColName*。

    查詢所傳回的資料會傳遞至 Python 執行階段，傳回至 SQL Database 的資料，當做 pandas 資料框架。 WITH RESULT SETS 子句會定義傳回的資料表的結構描述，SQL database。

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **結果**

    ![從資料表傳回資料的 Python 指令碼輸出](./media/python-output-pythontestdata.png)

2. 讓我們變更輸入或輸出變數的名稱。 上述指令碼使用預設的輸入和輸出變數名稱， _InputDataSet_並_OutputDataSet_。 若要定義輸入的資料與相關聯_InputDataSet_，您使用 *@input_data_1* 變數。

    此指令碼，在預存程序的輸出和輸入的變數名稱已變更為*SQL_out*並*SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'Python'
      , @script = N'SQL_out = SQL_in'
      , @input_data_1 = N' SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    中的輸入和輸出變數的大小寫`@input_data_1_name`並`@output_data_1_name`一定要相符的項目中的 Python 程式碼中的大小寫`@script`，因為 Python 是區分大小寫。

    只有一個輸入資料集可以當作參數傳遞，您只能傳回一個資料集。 不過，您可以在您的 Python 程式碼內呼叫從其他資料集，而且您可以傳回其他類型，除了資料集的輸出。 您也可以將 OUTPUT 關鍵字新增至任何參數，讓它傳回結果。 

    `WITH RESULT SETS`陳述式在 SQL Server 中定義資料用的結構描述。 您需要提供 SQL 相容的資料類型，您即可從 Python 傳回每個資料行。 您可以使用的結構描述定義來提供新的資料行名稱太，因為您不需要使用 Python data.frame 的資料行名稱。

3. 您也可以使用 Python 指令碼產生值，並保留中的輸入的查詢字串 _@input_data_1_ 空白。

    ```sql
    EXECUTE sp_execute_external_script
    @language = N'Python'
    , @script = N'
    import pandas as pd
    mytextvariable = pandas.Series(["hello", " ", "world"]);
    OutputDataSet = pd.DataFrame(mytextvariable);'
    , @input_data_1 = N''
    WITH RESULT SETS (([Col1] CHAR(20) NOT NULL));
    ```

    **結果**

    ![使用查詢結果@script做為輸入](./media/python-data-generated-output.png)

## <a name="next-steps"></a>後續步驟

檢查傳遞 Python 與 SQL Server 之間的表格式資料時，可能會遇到的問題。

> [!div class="nextstepaction"]
> [快速入門：SQL Server 中的 Python 資料結構](quickstart-python-data-structures.md)
