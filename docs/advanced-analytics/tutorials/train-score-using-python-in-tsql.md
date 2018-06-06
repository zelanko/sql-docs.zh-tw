---
title: 使用 Python 模型進行定型和計分 SQL 中的 |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b7f5883356ff6878f869ee10f915bcb93a2dba17
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="use-python-model-in-sql-for-training-and-scoring"></a>在 SQL 中使用 Python 模型，用於定型和計分
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在[上一課](wrap-python-in-tsql-stored-procedure.md)，您學到使用 Python 與 SQL 的常見模式。 您已了解您的 Python 程式碼應該會輸出一個清楚定義的 data.frame，並可以選擇性地輸出多個純量或二進位的變數。 您已學到的 SQL 預存程序應該設計成可正確類型的資料傳入 Python，以及處理結果。

本節中，您可以使用這個相同的模式來定型模型，您已加入 SQL Server 的資料，並將模型儲存至 SQL Server 資料表：

+ 您設計呼叫 Python 機器學習服務函數的預存程序。
+ 預存程序需要從用於定型此模型中的 SQL Server 的資料。
+ 預存程序會以二進位變數輸出定型的模型。 
+ 插入資料表變數的模型，您可儲存定型的模型。 

## <a name="create-the-stored-procedure-and-train-a-python-model"></a>建立預存程序和 Python 模型定型

1. 若要建立的預存程序會建立模型的 SQL Server Management Studio 中執行下列程式碼。

    ```sql
    CREATE PROCEDURE generate_iris_model (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'Python',
    @script = N'
    import pickle
    from sklearn.naive_bayes import GaussianNB
    GNB = GaussianNB()
    trained_model = pickle.dumps(GNB.fit(iris_data[[0,1,2,3]], iris_data[[4]]))
    '
    , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
    , @input_data_1_name = N'iris_data'
    , @params = N'@trained_model varbinary(max) OUTPUT'
    , @trained_model = @trained_model OUTPUT;
    END;
    GO
    ```

2. 如果這個命令會執行不會發生錯誤，新的預存程序建立，並加入至資料庫。 您可以在 Management Studio 中找到預存程序**物件總管 中**下**可程式性**。

3. 現在，執行預存程序。

    ```sql
    EXEC generate_iris_model
    ```

    您應該取得發生錯誤，因為您未提供需要輸入預存程序。

    「 程序或函數 'generate_iris_model' 必須有參數 '@trained_model'，但未提供。"

4. 若要產生模型，以必要的輸入，並將它儲存至資料表需要一些額外的陳述式：

    ```sql
    DECLARE @model varbinary(max);
    EXEC generate_iris_model @model OUTPUT;
    INSERT INTO iris_models (model_name, model) values('Naive Bayes', @model);
    ```

5. 現在，再試一次執行模型產生程式碼。 

    您應該會收到錯誤: 「 主索引鍵條件約束違規無法插入重複的索引鍵物件 'dbo.iris_models' 中。 重複的索引鍵值是 （貝氏機率分類） 」。

    這是因為提供的模型名稱是以手動方式輸入"貝氏機率分類 」 中做為 INSERT 陳述式的一部分。 假設您計劃建立大量模型，每次執行上使用不同的參數或不同的演算法，您應該考慮的中繼資料結構描述的設定，讓您可以自動命名模型，並更輕鬆地找到它們。

6. 若要解決這個錯誤，您可以修改一些次要 SQL 包裝函式。 這個範例會產生唯一的模型名稱，藉由附加目前日期和時間：

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes ' + CAST(GETDATE()as varchar)
    SELECT @new_model_name 
    EXEC generate_iris_model @model OUTPUT;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    ```

7. 若要檢視模型，執行簡單的 SELECT 陳述式。

    ```sql
    SELECT * FROM iris_models;
    GO
    ```

    **結果**

    |model_name | model |
    |------|------|
    | 貝氏機率分類 | 0x800363736B6C656172... |
    | 貝氏機率分類 01 2018 上午 9:39 年 1 月 | 0x800363736B6C656172... |
    | 貝氏機率分類 Feb 01 2018 10:51 AM | 0x800363736B6C656172... |

## <a name="generate-scores-from-the-model"></a>從模型產生分數

最後，讓我們從資料表載入變數，此模型，並將它傳遞回 Python 產生分數。

1. 執行下列的程式碼建立預存程序執行計分。 

    ```sql
    CREATE PROCEDURE predict_species (@model varchar(100))
    AS
    BEGIN
    DECLARE @nb_model varbinary(max) = (SELECT model FROM iris_models WHERE model_name = @model);
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'
    import pickle
    irismodel = pickle.loads(nb_model)
    species_pred = irismodel.predict(iris_data[[1,2,3,4]])
    iris_data["PredictedSpecies"] = species_pred
    OutputDataSet = iris_data.query( ''PredictedSpecies != SpeciesId'' )[[0, 5, 6]]
    print(OutputDataSet)
    '
    , @input_data_1 = N'select id, "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
    , @input_data_1_name = N'iris_data'
    , @params = N'@nb_model varbinary(max)'
    , @nb_model = @nb_model
    WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));
    END;
    GO
    ```

    預存程序會從資料表中取得貝氏機率分類模型，並使用與模型相關聯的函式產生分數。 在此範例中，預存程序會取得模型中使用的模型名稱的資料表。 不過，根據模型儲存的中繼資料種類，您可以也取得最新的模型或模型最高的精確度。

2. 執行下列幾行來傳遞的模型名稱"貝氏機率分類"計分的程式碼會執行預存程序。 

    ```sql
    EXEC predict_species 'Naive Bayes';
    GO
    ```

    當您執行預存程序時，它會傳回 Python data.frame。 T-SQL 的這一行會指定傳回的結果的結構描述： `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`

    您可以將結果插入新的資料表，或將其傳回應用程式。

    此範例中，已對簡單使用來自 Python 光圈資料集的資料進行計分。 (請參閱行`iris_data[[1,2,3,4]])`。)不過，通常會執行 SQL 查詢，以取得新的資料，然後傳遞到為 Python `InputDataSet`。 

### <a name="remarks"></a>備註

如果您習慣使用 Python，您可能會是習慣於載入資料、 建立一些摘要和圖形，然後定型模型和所有在相同的 250 行程式碼中產生一些分數。

不過，如果您的目標來實施 SQL Server 中的程序 （模型建立、 計分等），務必考慮您可以為可重複的步驟，可以使用參數來修改分隔處理序的方式。 盡量，您想您已經清楚地定義輸入和輸出對應至預存程序的輸入和輸出的預存程序中執行 Python 程式碼。

此外，您通常可以藉由分隔資料瀏覽處理序的處理程序的模型定型，或產生分數提升效能。 

計分和定型程序可以通常最佳化利用 SQL Server 的功能，如平行處理，或使用中的演算法[revoscalepy](../python/what-is-revoscalepy.md)或[MicrosoftML](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)該支援資料流和平行執行，而不使用標準的 Python 程式庫。 

## <a name="next-lesson"></a>下一課

在最後一課，您可以執行 Python 程式碼從遠端用戶端，使用 SQL Server 當成計算內容。 這是選擇性步驟，如果您沒有 Python 用戶端，或不想要的預存程序之外執行 Python。

+ [Python 用戶端從建立 revoscalepy 模型](use-python-revoscalepy-to-create-model.md)
