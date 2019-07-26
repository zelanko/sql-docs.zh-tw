---
title: 在 Python 中使用輸入和輸出的快速入門
description: 在 SQL Server 的 Python 腳本快速入門中, 瞭解如何將輸入和輸出結構為 sp_execute_external_script 系統預存程式。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0259a4695ab1ee6f42b92e12b47f81e9aa851469
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469609"
---
# <a name="quickstart-handle-inputs-and-outputs-using-python-in-sql-server"></a>快速入門：在 SQL Server 中使用 Python 處理輸入和輸出
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本快速入門說明在 SQL Server Machine Learning 服務中使用 Python 時, 如何處理輸入和輸出。

根據預設, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)會接受單一輸入資料集, 這通常是您以有效 SQL 查詢的形式提供。

其他類型的輸入可以當做 SQL 變數傳遞: 例如, 您可以使用[pickle](https://docs.python.org/3.0/library/pickle.html)或[rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)之類的序列化函數, 以二進位格式撰寫模型, 以將定型的模型當做變數傳遞。

預存程式會傳回單一 Python [pandas](https://pandas.pydata.org/pandas-docs/stable/index.html)資料框架做為輸出, 但您也可以將純量和模型輸出為變數。 例如, 您可以將定型的模型輸出為二進位變數, 並將它傳遞至 T-sql INSERT 語句, 以將該模型寫入資料表。 您也可以產生繪圖 (二進位格式) 或純量 (個別的值, 例如日期和時間、定型模型所經過的時間等等)。

## <a name="prerequisites"></a>先決條件

先前的快速入門中, 請[確認 Python 存在於 SQL Server](quickstart-python-verify.md)中, 提供設定本快速入門所需之 python 環境的相關資訊和連結。

## <a name="create-the-source-data"></a>建立來源資料

執行下列 T-sql 語句, 以建立測試資料的小型資料表:

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

讓我們看看 sp_execute_external_script 的預設輸入和輸出變數: `InputDataSet`和。 `OutputDataSet`

1. 您可以從資料表中取得資料, 以作為 Python 腳本的輸入。 執行下列語句。 它會從資料表取得資料、透過 Python 執行時間進行來回行程, 並傳回具有*NewColName*資料行名稱的值。

    查詢所傳回的資料會傳遞至 Python 執行時間, 這會將資料傳回 SQL Database 做為 pandas 資料框架。 WITH RESULT SETS 子句會定義所傳回之資料表的架構, 以供 SQL Database。

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **結果**

    ![從資料表傳回資料的 Python 腳本輸出](./media/python-output-pythontestdata.png)

2. 讓我們變更輸入或輸出變數的名稱。 上述腳本使用預設輸入和輸出變數名稱_InputDataSet_和_OutputDataSet_。 若要定義與_InputDataSet_相關聯的輸入資料, 您 *@input_data_1* 可以使用變數。

    在此腳本中, 預存程式的輸出和輸入變數名稱已變更為*SQL_out*和*SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'Python'
      , @script = N'SQL_out = SQL_in'
      , @input_data_1 = N' SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    和`@input_data_1_name` `@script`中的輸入和輸出變數大小寫必須符合中的 python 程式碼中的大小寫, 因為 python 會區分大小寫。 `@output_data_1_name`

    只有一個輸入資料集可以當作參數傳遞，您只能傳回一個資料集。 不過, 您可以從 Python 程式碼內部呼叫其他資料集, 而且除了資料集之外, 您還可以傳回其他類型的輸出。 您也可以將 OUTPUT 關鍵字新增至任何參數，讓它傳回結果。 

    `WITH RESULT SETS`語句會定義 SQL Server 中使用之資料的架構。 您必須為從 Python 傳回的每個資料行提供 SQL 相容的資料類型。 您也可以使用架構定義來提供新的資料行名稱, 因為您不需要使用 Python data. 框架中的資料行名稱。

3. 您也可以使用 Python 腳本來產生值, 並將輸入查詢字串 _@input_data_1_ 保留為空白。

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

    ![使用@script作為輸入的查詢結果](./media/python-data-generated-output.png)

## <a name="next-steps"></a>後續步驟

檢查在 Python 與 SQL Server 之間傳遞表格式資料時可能會遇到的一些問題。

> [!div class="nextstepaction"]
> [入門SQL Server 中的 Python 資料結構](quickstart-python-data-structures.md)
