---
title: 處理輸入和輸出，R-SQL Server Machine Learning 中的快速入門
description: 此快速入門中的 SQL Server 中的 R 指令碼，了解如何建構輸入和輸出至 sp_execute_external_script 的系統預存程序。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 56d2eb65ca95dd4f153f3c7a6ebb00e926465687
ms.sourcegitcommit: baca29731a1be4f8fa47567888278394966e2af7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046751"
---
# <a name="quickstart-handle-inputs-and-outputs-using-r-in-sql-server"></a>快速入門：處理輸入及輸出在 SQL Server 中使用 R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本快速入門示範如何處理輸入及輸出時使用 SQL Server Machine Learning 服務中的 R 或 R 服務。

當您想要在 SQL Server 中執行 R 程式碼時，您必須在預存程序中包裝 R 指令碼。 您可以將寫入其中一個，或傳遞至 R 指令碼[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 此系統預存程序用以啟動 SQL Server，其會將資料傳遞至 R，內容中的 R 執行階段安全地管理 R 使用者工作階段，並傳回給用戶端的任何結果。

根據預設， [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)接受單一輸入資料集，這通常是您提供有效的 SQL 查詢的形式。 其他類型的輸入可以當做 SQL 變數。

預存程序傳回單一的 R 資料框架做為輸出，但您也可以輸出純量和做為變數的模型。 例如，您可以輸出定型的模型，做為二進位的變數，並將它傳遞至 T-SQL INSERT 陳述式，以寫入該模型的資料表。 您也可以產生繪圖 （以二進位格式） 或純量 （個別的值，例如日期和時間，所經過的時間來定型模型，等等）。

## <a name="prerequisites"></a>先決條件

先前的快速入門中，[確認 R 存在於 SQL Server](quickstart-r-verify.md)，提供資訊並連結設定本快速入門所需的 R 環境。

## <a name="create-the-source-data"></a>建立來源資料

執行下列 T-SQL 陳述式，以建立小型測試資料的資料表：

```sql
CREATE TABLE RTestData (col1 INT NOT NULL)
INSERT INTO RTestData VALUES (1);
INSERT INTO RTestData VALUES (10);
INSERT INTO RTestData VALUES (100);
GO
```

建立資料表之後，請使用下列陳述式來查詢資料表：
  
```sql
SELECT * FROM RTestData
```

**結果**

![RTestData 資料表的內容](./media/select-rtestdata.png)

## <a name="inputs-and-outputs"></a>[指令碼轉換編輯器]

讓我們看看預設值的 sp_execute_external_script 的輸入和輸出變數：`InputDataSet`和`OutputDataSet`。

1. 您可以從資料表取得資料，做為 R 指令碼輸入。 執行以下陳述式。 從資料表取得資料、 進行來回在 R 執行階段，以及傳回的資料行名稱的值*NewColName*。

    查詢所傳回的資料會傳遞至 R 執行階段，傳回的資料到 SQL Database 做為資料框架。 WITH RESULT SETS 子句會定義傳回的資料表的結構描述，SQL database。

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **結果**

    ![從資料表傳回資料的 R 指令碼輸出](./media/r-output-rtestdata.png)

2. 讓我們變更輸入或輸出變數的名稱。 上述指令碼使用預設的輸入和輸出變數名稱， _InputDataSet_並_OutputDataSet_。 若要定義輸入的資料與相關聯_InputDatSet_，您使用*@input_data_1*變數。

    此指令碼，在預存程序的輸出和輸入的變數名稱已變更為*SQL_out*並*SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'R'
      , @script = N' SQL_out <- SQL_in;'
      , @input_data_1 = N'SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    請注意，R 區分大小寫，所以案例中的輸入和輸出變數`@input_data_1_name`並`@output_data_1_name`一定要相符的項目中的 R 程式碼中`@script`。 

    此外，參數的順序很重要的。 若要使用選擇性的參數 *@input_data_1_name* 和 *@output_data_1_name*，您必須先指定必要的參數 *@input_data_1*和 *@output_data_1*。

    只有一個輸入資料集可以當作參數傳遞，您只能傳回一個資料集。 不過，您可以從 R 程式碼內部呼叫其他資料集，而且除了資料集之外，您還可以傳回其他類型的輸出。 您也可以將 OUTPUT 關鍵字新增至任何參數，讓它傳回結果。 

    `WITH RESULT SETS`陳述式在 SQL Server 中定義資料用的結構描述。 您必須提供每個資料行從 r 傳回的 SQL 相容的資料類型您可以使用的結構描述定義來提供新的資料行名稱太，因為您不需要使用 R 資料框架的資料行名稱。

3. 您也可以使用 R 指令碼產生值，並保留中的輸入的查詢字串_@input_data_1_空白。

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N' mytextvariable <- c("hello", " ", "world");
            OutputDataSet <- as.data.frame(mytextvariable);'
        , @input_data_1 = N''
    WITH RESULT SETS (([Col1] CHAR(20) NOT NULL));
    ```

    **結果**

    ![使用查詢結果@script做為輸入](./media/r-data-generated-output.png)

## <a name="next-steps"></a>後續步驟

檢查 R 和 SQL Server 之間傳遞資料，例如隱含轉換，以及 R 與 SQL 之間的差異在表格式資料時，可能會遇到的問題。

> [!div class="nextstepaction"]
> [快速入門：處理資料型別和物件](quickstart-r-data-types-and-objects.md)