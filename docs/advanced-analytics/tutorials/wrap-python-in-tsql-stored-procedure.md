---
title: "Python 程式碼包裝在預存程序 |Microsoft 文件"
titleSuffix: SQL Server
ms.custom: 
ms.date: 02/28/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2017
dev_langs:
- Python
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 11b5b649a942b1d1804b799426530a1b82ee9458
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="wrap-python-code-in-a-stored-procedure"></a>Python 程式碼包裝在預存程序
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在[上一課](run-python-using-t-sql.md)，您學到如何向 SQL Server 的 Python。 在這一課，您會學習如何在預存程序，從 Python 範例資料集，取得資料，並且該資料寫入 SQL Server 資料表中內嵌的 Python 程式碼。

系統預存程序[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)提供的 SQL 變數和 SQL 資料集傳遞至 Python 包裝函式。 也會處理 Python 的結果輸出，並將其傳遞至 SQL Server 的格式與 SQL 資料類型相容。

讓我們查看其運作方式。

## <a name="prepare-the-database-and-tables"></a>準備資料庫和資料表

雖然可以設定的遠端用戶端，並執行 Python 程式碼使用 Visual Studio 程式碼、 Visual Studio、 PyCharm 或其他工具，來簡化這個案例，在這一課的所有程式碼應該做為預存程序的一部分。

1. 啟動 SQL Server Management Studio，並開啟新**查詢**視窗。  

2. 建立此專案中，新的資料庫和變更的內容程式**查詢**視窗，以使用新的資料庫。

    ```sql
    CREATE DATABASE sqlpy;
    GO;
    USE sqlpy;
    GO;
    ```

    > [!TIP] 
    > 如果您還不熟悉 SQL Server，或使用您自己的伺服器上時，常見的錯誤是登入並開始使用，而不會注意您是在**主要**資料庫。 若要確定您使用正確的資料庫，永遠指定內容中使用`USE <database name>`陳述式。

3. 加入一些空的資料表： 一個用來儲存資料，以及一個用來儲存您訓練模型。 稍後您填入使用 Python 的資料表。

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

    如果您不熟悉 t-sql，它付款記`DROP...IF`陳述式。 當您嘗試建立的資料表已經存在，SQL Server 會傳回錯誤: 「 已有名稱為 'iris_data' 資料庫中的物件。" 若要避免這類錯誤的一個方式是刪除任何現有的資料表或其他物件做為您的程式碼的一部分。

4. 執行下列程式碼來建立用來儲存已定型的模型資料表。 若要儲存模型 Python （或 R） SQL Server 中，它們必須序列化和類型的資料行中儲存**varbinary （max)**。 

    ```sql
    DROP TABLE IF EXISTS iris_models;
    GO
    
    CREATE TABLE iris_models (
      model_name VARCHAR(50) NOT NULL DEFAULT('default model') PRIMARY KEY,
      model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

    除了模型的內容，一般而言，您會也加入其他有用的中繼資料，例如模型的名稱，它來定型，日期來源演算法和參數，來源資料的資料行等等。 現在我們將保持簡單，並使用 模型名稱。

## <a name="populate-the-table"></a>填入的資料表

若要將來自 Python 的定型資料移至 SQL Server 資料表是包含多個步驟的程序：

+ 您設計取得您想要的資料的預存程序。
+ 您執行預存程序，以取得實際的資料。
+ 您可以使用 INSERT 陳述式來指定用來儲存所擷取的資料。

1. 建立下列預存程序包含 Python 程式碼。 

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

    當您執行此程式碼時，您應該會收到訊息 「 命令成功完成。 」 這表示所有是預存程序確認已建立根據您的規格。

2. 若要實際填入的資料表，執行預存程序並指定寫入資料的資料表。 當執行時，預存程序執行的 Python 程式碼，從內建的 Python 範例資料載入光圈資料集。

    ```sql
    INSERT INTO iris_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species", "SpeciesId")
    EXEC dbo.get_iris_dataset;
    ```

    如果您還不熟悉 T-SQL，請注意，INSERT 陳述式只會將新的資料。它不會檢查現有的資料，或刪除並重建此資料表。 若要避免在資料表中取得多份相同的資料，您可以先執行此陳述式： `TRUNCATE TABLE iris_data`。 T-SQL [TRUNCATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/truncate-table-transact-sql)陳述式會刪除現有的資料，但會保留資料表的結構不變。

    > [!TIP]
    > 若要修改預存程序之後，您不需要卸除並重新建立。 使用[ALTER PROCEDURE](https://docs.microsoft.com/sql/t-sql/statements/alter-procedure-transact-sql)陳述式。 

3. 若要確認已正確地載入資料，您可以執行一些簡單的查詢：

    ```sql
    SELECT TOP(10) * FROM iris_data;
    SELECT COUNT(*) FROM iris_data;
    ```

在[下一課](../tutorials/train-score-using-python-in-tsql.md)，建立機器學習模型，並將它儲存到資料表。

### <a name="further-reading-about-stored-procedures"></a>深入了解預存程序

如果您不熟悉 SQL Server，您可能會發現在第一個複雜的預存程序。 但是，預存程序是功能強大且靈活的介面，如應用程式和伺服器之間傳遞資料。 使用預存程序，您可以動態地定義輸入，就可輕鬆將新的模型名稱、 新的參數和新的資料，而不會變更您的 Python 程式碼。

如需如何在預存程序工作的概觀，請參閱[預存程序 (Database Engine)](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine)，或本教學課程：[撰寫 TRANSACT-SQL 陳述式](https://docs.microsoft.com/sql/t-sql/tutorial-writing-transact-sql-statements)。

也有一些很好的教學課程社群網站在例如[SQL Server Central](http://www.sqlservercentral.com/)或[SQL 團隊](http://www.sqlteam.com/)。

當您考慮如何最封裝 T-SQL 中的 Python 程式碼，也請考慮使用這些功能：

+ 定義預存程序的預設值
+ 透過輸入變數使用 OUTPUT 關鍵字
+ 建立結構描述定義使用與結果，以確保該應用程式所使用的資料具有正確的資料類型和資料行名稱
+ 提供提示來改善批次處理
+ 模擬不同的使用者，以測試您的程式碼，使用 EXECUTE AS 子句

## <a name="next-lesson"></a>下一課

[Python 模型定型和產生 SQL Server 中的分數](../tutorials/train-score-using-python-in-tsql.md)