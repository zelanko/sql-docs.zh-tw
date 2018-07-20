---
title: 使用 Python 模型訓練和評分的 SQL 中 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 02ffd5a25c076ef5a65a6e3a998aae485e37d982
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39085020"
---
# <a name="use-python-model-in-sql-for-training-and-scoring"></a>在 SQL 中使用 Python 模型訓練和評分
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在 [上一課](wrap-python-in-tsql-stored-procedure.md)，您已了解使用 Python 與 SQL 的常見模式。 您已了解您的 Python 程式碼應該會輸出一條明確定義的 data.frame，並可選擇性地輸出多個純量或二進位的變數。 您已了解 SQL 預存程序，應該將正確的資料類型傳遞至 Python，並處理結果所設計。

在本節中，您可以使用此相同的模式，根據您已新增至 SQL Server 的資料來定型模型，並將模型儲存至 SQL Server 資料表：

+ 您設計呼叫 Python 機器學習服務函式的預存程序。
+ 預存程序必須從用於定型模型的 SQL Server 的資料。
+ 預存程序會將定型的模型輸出做為二進位的變數。 
+ 您可以插入資料表變數的模型，以節省定型的模型。 

## <a name="create-the-stored-procedure-and-train-a-python-model"></a>建立預存程序，並將 Python 模型定型

1. 建立預存程序，建立模型的 SQL Server Management Studio 中執行下列程式碼。

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

2. 如果此命令會執行不會發生錯誤，新的預存程序建立，並加入至資料庫。 您可以在 Management Studio 中找到預存程序**物件總管**下方**可程式性**。

3. 現在，執行預存程序。

    ```sql
    EXEC generate_iris_model
    ```

    因為您尚未提供輸入預存程序需要，您應該取得發生錯誤。

    「 程序或函數 'generate_iris_model' 必須有參數 '\@trained_model'，但未提供。 」

4. 若要產生必要的輸入使用的模型，並將它儲存至資料表，需要一些其他的陳述式：

    ```sql
    DECLARE @model varbinary(max);
    EXEC generate_iris_model @model OUTPUT;
    INSERT INTO iris_models (model_name, model) values('Naive Bayes', @model);
    ```

5. 現在，請再試一次執行的模型產生程式碼。 

    您應該會收到錯誤: 「 PRIMARY KEY 條件約束的違規情形無法插入重複的索引鍵在物件 'dbo.iris_models'。 重複的索引鍵值是 （貝氏機率分類） 」。

    這是因為模型名稱由以手動方式輸入 「 貝氏機率分類 」 做為 INSERT 陳述式的一部分提供。 假設您想要建立許多模型，在每次執行使用不同的參數或不同的演算法，您應該考慮的中繼資料結構描述的設定，讓您可以自動命名模型，並更輕鬆地找到它們。

6. 若要解決這個錯誤，您可以稍做一些修改 SQL 包裝函式。 此範例會產生唯一的模型名稱，藉由附加目前日期和時間：

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes ' + CAST(GETDATE()as varchar)
    SELECT @new_model_name 
    EXEC generate_iris_model @model OUTPUT;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    ```

7. 若要檢視的模型，執行簡單的 SELECT 陳述式。

    ```sql
    SELECT * FROM iris_models;
    GO
    ```

    **結果**

    |model_name | model |
    |------|------|
    | 貝氏機率分類 | 0x800363736B6C656172... |
    | 貝氏機率分類 Jan 01 2018 上午 9:39 | 0x800363736B6C656172... |
    | 貝氏機率分類 Feb 01 2018 上午 10:51 | 0x800363736B6C656172... |

## <a name="generate-scores-from-the-model"></a>從模型產生分數

最後，讓我們從資料表載入變數中，此模型，並將它傳遞至 Python 來產生分數。

1. 執行下列程式碼建立預存程序執行評分。 

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

    預存程序會從資料表取得貝氏機率分類模型，並使用與模型相關聯的函式產生分數。 在此範例中，預存程序會使用模型名稱的資料表中取得的模型。 不過，視何種中繼資料會儲存與模型，您可以也取得最新的模型或模型具有最高精確度。

2. 執行下列幾行，將執行評分的程式碼的預存程序的模型名稱"貝氏機率分類 」。 

    ```sql
    EXEC predict_species 'Naive Bayes';
    GO
    ```

    當您執行預存程序時，它會傳回 Python data.frame。 T-SQL 的這一行會指定傳回的結果結構描述： `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`

    您可以將結果插入到新的資料表，或返回應用程式。

    此範例已發出簡單使用 Python 鳶尾花資料集的資料進行評分。 (請參閱行`iris_data[[1,2,3,4]])`。)不過，通常您會執行 SQL 查詢，以取得新的資料，並將它傳遞至 Python `InputDataSet`。 

### <a name="remarks"></a>備註

如果您是用來使用 Python 中，您可能習慣手動載入資料、 建立一些摘要和圖形，然後定型模型及產生一些分數，全都放在相同的 250 行程式碼。

不過，如果您的目標是讓 SQL Server 中的程序 （模型建立、 評分、 等） 來運作，則務必納入考量，您可以分成程序可以使用參數進行修改的可重複執行步驟的方式。 盡量，您想要清楚定義輸入和輸出對應至預存程序的輸入和輸出的預存程序中所執行的 Python 程式碼。

此外，您通常可以在資料瀏覽處理序開來的定型模型，或產生分數的處理程序，改善效能。 

Scoring 和訓練程序可以通常最佳化運用 SQL Server 的功能，例如平行處理，或使用中的演算法[revoscalepy](../python/what-is-revoscalepy.md)或是[MicrosoftML](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)該支援資料流和平行執行，而不使用標準 Python 程式庫。 

## <a name="next-lesson"></a>下一課

在最後一課中，您可以執行 Python 程式碼從遠端用戶端，使用 SQL Server 作為計算內容。 這是選擇性步驟，如果您沒有 Python 用戶端，或不想要的預存程序之外執行 Python。

+ [從 Python 用戶端建立 revoscalepy 模型](use-python-revoscalepy-to-create-model.md)
