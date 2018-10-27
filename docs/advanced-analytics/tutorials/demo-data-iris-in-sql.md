---
title: 鳶尾花示範資料集，SQL Server Python 和 R 教學課程 |Microsoft Docs
Description: Create a database containing the Iris dataset and a table for storing models. This dataset is used in exercises showing how to wrap R language or Python code in a SQL Server stored procedure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 74e4cbe97d64f922de2cdfe1f67eae5d3a3e24bd
ms.sourcegitcommit: 70e47a008b713ea30182aa22b575b5484375b041
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2018
ms.locfileid: "49806668"
---
#  <a name="iris-demo-data-for-sql-server-python-and-r-tutorials"></a>如需 SQL Server Python 和 R 教學課程的鳶尾花示範資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在此練習中，建立將資料從 SQL Server 資料庫[鳶尾花資料集](https://en.wikipedia.org/wiki/Iris_flower_data_set)和相同的資料為基礎的模型。 鳶尾花資料包含在 SQL Server 所安裝的 R 和 Python 散發套件，並會在機器學習服務教學課程適用於 SQL Server。 

若要完成此練習中，您應該具備[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017)或其他工具，可執行 T-SQL 查詢。

教學課程和快速入門使用此資料集包含下列項目：

+  [使用 SQL Server 中的 Python 模型訓練和評分](train-score-using-python-in-tsql.md)

## <a name="create-the-database"></a>建立資料庫

1. 啟動 SQL Server Management Studio，並開啟新**查詢**視窗。  

2. 建立新的資料庫，此專案中，並將內容變更您**查詢**視窗，以使用新的資料庫。

    ```sql
    CREATE DATABASE irissql
    GO
    USE irissql
    GO
    ```

    > [!TIP] 
    > 如果您還不熟悉 SQL Server，或使用您自己的伺服器上時，常見的錯誤是登入，並啟動工作，不會注意到您位於**主要**資料庫。 若要確定您使用的正確的資料庫，永遠指定內容中使用`USE <database name>`陳述式 (例如`use irissql`)。

3. 新增一些空白的資料表： 一個用來儲存資料，以及一個用來儲存已定型的模型。 **Iris_models**資料表用於儲存在其他的練習中所產生的序列化的模型。

    下列程式碼會建立定型資料的資料表。

    ```sql
    DROP TABLE IF EXISTS iris_data;
    GO
    CREATE TABLE iris_data (
      id INT NOT NULL IDENTITY PRIMARY KEY
      , "Sepal.Length" FLOAT NOT NULL, "Sepal.Width" FLOAT NOT NULL
      , "Petal.Length" FLOAT NOT NULL, "Petal.Width" FLOAT NOT NULL
      , "Species" VARCHAR(100) NOT NULL, "SpeciesId" INT NOT NULL
    );
    ```

    > [!TIP] 
    > 如果您不熟悉 T-SQL，值得記住`DROP...IF`陳述式。 當您嘗試建立資料表，並已經存在時，SQL Server 會傳回錯誤: 「 有 」 已經名為 'iris_data' 資料庫中的物件。 若要避免這類錯誤的一個方式是刪除任何現有的資料表或其他物件做為您的程式碼的一部分。

4. 執行下列程式碼來建立用來儲存已定型的模型資料表。 若要儲存 SQL Server 中的 Python （或 R） 模型，他們必須序列化及儲存在類型的資料行**varbinary （max)**。 

    ```sql
    DROP TABLE IF EXISTS iris_models;
    GO
    
    CREATE TABLE iris_models (
      model_name VARCHAR(50) NOT NULL DEFAULT('default model') PRIMARY KEY,
      model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

    除了模型的內容，一般而言，您就也加入其他實用的中繼資料，例如模型的名稱、 已受過訓練，日期的來源演算法和參數，來源資料的資料行等等。 現在，我們會保持簡單，並使用模型名稱。

## <a name="populate-the-table"></a>填入資料表

您可以從 R 或 Python 來取得內建的鳶尾花資料。 您可以使用 Python 或 R 將資料載入至資料框架，並將它插入資料庫中的資料表。 將訓練資料從外部的工作階段移至 SQL Server 資料表是一個多步驟的程序：

+ 設計預存程序可取得您想要的資料。
+ 執行預存程序，以取得實際資料。
+ 建構的 INSERT 陳述式，來指定應儲存擷取的資料。

1. 在系統上使用 Python 整合，建立下列預存程序將資料載入使用 Python 程式碼。

    ```sql
    CREATE PROCEDURE get_iris_dataset
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'
    from sklearn import datasets
    iris = datasets.load_iris()
    iris_data = pandas.DataFrame(iris.data)
    iris_data["Species"] = pandas.Categorical.from_codes(iris.target, iris.target_names)
    iris_data["SpeciesId"] = iris.target
    ', 
    @input_data_1 = N'', 
    @output_data_1_name = N'iris_data'
    WITH RESULT SETS (("Sepal.Length" float not null, "Sepal.Width" float not null, "Petal.Length" float not null, "Petal.Width" float not null, "Species" varchar(100) not null, "SpeciesId" int not null));
    END;
    GO
    ```

    當您執行此程式碼時，您應該會收到訊息 「 命令成功完成。 」 這都表示為預存程序，已建立根據您的規格。

2. 或者，在具有 R 整合的系統，建立改為使用 R 的程序。

    ```sql
    CREATE PROCEDURE get_iris_dataset
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'R', 
    @script = N'
    library(RevoScaleR)
    data(iris)
    iris$SpeciesID <- c(unclass(iris$Species))
    iris_data <- iris
    ', 
    @input_data_1 = N'', 
    @output_data_1_name = N'iris_data'
    WITH RESULT SETS (("Sepal.Length" float not null, "Sepal.Width" float not null, "Petal.Length" float not null, "Petal.Width" float not null, "Species" varchar(100) not null, "SpeciesId" int not null));
    END;
    GO
    ```

3. 若要實際填入資料表，執行預存程序，並指定寫入資料的位置的資料表。 當執行時，預存程序執行的 Python 或 R 程式碼載入內建的鳶尾花資料集，並再將資料插入**iris_data**資料表。

    ```sql
    INSERT INTO iris_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species", "SpeciesId")
    EXEC dbo.get_iris_dataset;
    ```

    如果您還不熟悉 T-SQL，請注意，INSERT 陳述式只會將新的資料;它不會檢查有現有的資料，或刪除並重建此資料表。 若要避免在資料表中取得多份相同的資料，您可以先執行此陳述式： `TRUNCATE TABLE iris_data`。 T-SQL [TRUNCATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/truncate-table-transact-sql)陳述式會刪除現有的資料，但會保留資料表的結構保持不變。

    > [!TIP]
    > 若要修改預存程序之後，您不需要卸除並重新建立它。 使用[ALTER PROCEDURE](https://docs.microsoft.com/sql/t-sql/statements/alter-procedure-transact-sql)陳述式。 


## <a name="query-the-data"></a>查詢資料

驗證步驟中，執行查詢，以確認資料已上傳。

1. 在 [物件總管] 的資料庫，以滑鼠右鍵按一下**irissql**資料庫，然後開始新的查詢。

2. 執行一些簡單的查詢：

    ```sql
    SELECT TOP(10) * FROM iris_data;
    SELECT COUNT(*) FROM iris_data;
    ```

## <a name="next-steps"></a>後續步驟

下一課，您會建立機器學習模型並將它儲存到資料表時，，然後使用模型來產生預測的結果。

+ [使用 SQL Server 中的 Python 模型訓練和評分](train-score-using-python-in-tsql.md)
