---
title: 使用預存程式進行定型和預測的 Python 模型快速入門
description: 在 SQL Server 預存程式中內嵌 Python 程式碼, 以建立、定型和使用具有傳統鳶尾花資料集的 Python 模型。 將定型的模型儲存至 SQL Server, 然後使用它來產生預測的結果。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 47ee23d945ded9fac97fe3eddc2137eeead00ae1
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469507"
---
# <a name="quickstart-create-train-and-use-a-python-model-with-stored-procedures-in-sql-server"></a>快速入門：在 SQL Server 中使用預存程式來建立、定型和使用 Python 模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本快速入門中, 您將會建立和執行兩個預存程式。 第一個使用傳統的鳶尾花花資料集, 並產生一個一般的貝氏機率分類模型, 以根據花卉特性來預測鳶尾花物種。 第二個程式是用於計分。 它會呼叫第一個程式中產生的模型, 以輸出一組預測。 藉由將程式碼放入預存程式中, 其他預存程式和用戶端應用程式就可以包含、可重複使用和呼叫作業。 

藉由完成本快速入門, 您將瞭解:

> [!div class="checklist"]
> * 如何在預存程式中內嵌 Python 程式碼
> * 如何透過預存程式上的輸入, 將輸入傳遞至您的程式碼
> * 如何使用預存程式來讓模型

## <a name="prerequisites"></a>必要條件

先前的快速入門中, 請[確認 Python 存在於 SQL Server](quickstart-python-verify.md)中, 提供設定本快速入門所需之 python 環境的相關資訊和連結。

此練習中使用的範例資料是[**irissql**](demo-data-iris-in-sql.md)資料庫。

## <a name="create-a-stored-procedure-that-generates-models"></a>建立會產生模型的預存程式

SQL Server 開發的常見模式是將可程式化作業組織成不同的預存程式。 在此步驟中, 您將建立一個預存程式, 以產生預測結果的模型。 

1. 在 Management Studio 中開啟新的查詢視窗, 並連接到**irissql**資料庫。 

    ```sql
    USE irissql
    GO
    ```

2. 複製下列程式碼, 以建立新的預存程式。 

   執行時, 此程式會呼叫[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)來啟動 Python 會話。 
   
   您的 Python 程式碼所需的輸入會當做此預存程式上的輸入參數來傳遞。 輸出將會是經過訓練的模型, 以適用于機器學習服務演算法的 Python **scikit-learn-瞭解**程式庫為基礎。 

   這段程式碼會使用[**pickle**](https://docs.python.org/2/library/pickle.html)來序列化模型。 此模型將使用來自**iris_data**資料表的資料行0到4來定型。 
   
   您在程式的第二個部分中看到的參數會詳述資料輸入和模型輸出。 您可能會想要在預存程式中執行的 Python 程式碼, 有清楚定義的輸入和輸出, 其對應至在執行時間傳入的預存程式輸入和輸出。 

    ```sql
    CREATE PROCEDURE generate_iris_model (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'Python',
    @script = N'
    import pickle
    from sklearn.naive_bayes import GaussianNB
    GNB = GaussianNB()
    trained_model = pickle.dumps(GNB.fit(iris_data[[0,1,2,3]], iris_data[[4]].values.ravel()))
    '
    , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
    , @input_data_1_name = N'iris_data'
    , @params = N'@trained_model varbinary(max) OUTPUT'
    , @trained_model = @trained_model OUTPUT;
    END;
    GO
    ```

3. 確認預存程式存在。 

   如果上一個步驟中的 T-sql 腳本執行時沒有錯誤, 則會建立名為**generate_iris_model**的新預存程式, 並將其新增至**irissql**資料庫。 您可以在 [可程式性] 底下的 Management Studio **物件總管**中找到預存程式。

## <a name="execute-the-procedure-to-create-and-train-models"></a>執行建立和定型模型的程式

在此步驟中, 執行程式來執行內嵌程式碼, 並建立定型和序列化模型做為輸出。 儲存以在 SQL Server 中重複使用的模型會序列化為位元組資料流程, 並儲存在資料庫資料表的 VARBINARY (MAX) 資料行中。 建立、定型、序列化模型並儲存到資料庫之後, 其他程式或評分工作負載中的[預測 t-sql 函式](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)可以呼叫它。

1. 複製下列程式碼以執行程式。 執行預存程式的特定語句位於`EXEC`第五行。

   此特定腳本會刪除相同名稱 ("貝氏貝氏機率分類") 的現有模型, 以騰出空間給透過重新執行相同程式所建立的新。 若未刪除模型, 就會發生錯誤, 指出物件已經存在。 模型會儲存在名為**iris_models**的資料表中 (當您建立**irissql**資料庫時布建)。

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes'
    EXEC generate_iris_model @model OUTPUT;
    DELETE iris_models WHERE model_name = @new_model_name;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    GO
    ```

2. 確認已插入另一個傳回模型清單的方法

    ```sql
    SELECT * FROM dbo.iris_models
    ```

    **結果**

    | model_name  | model |
    |---|-----------------|
    | 貝氏機率分類 | 0x800363736B6C6561726E2E6E616976655F62617965730A... | 

## <a name="create-and-execute-a-stored-procedure-for-generating-predictions"></a>建立和執行預存程式以產生預測

現在您已建立、定型及儲存模型, 請繼續進行下一個步驟: 建立會產生預測的預存程式。 若要這麼做, 您可以呼叫 sp_execute_external_script 來啟動 Python, 然後傳入 Python 腳本來載入您在上一個練習中建立的序列化模型, 然後將它的資料輸入提供給分數。

1. 執行下列程式碼, 以建立執行計分的預存程式。 在執行時間, 此程式會載入二進位模型、使用資料行`[1,2,3,4]`做為輸入, 並指定`[0,5,6]`資料行做為輸出。

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
    OutputDataSet = iris_data[[0,5,6]] 
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

2. 執行預存程式, 並提供模型名稱 "貝氏貝氏機率分類", 讓程式知道要使用哪一個模型。 

    ```sql
    EXEC predict_species 'Naive Bayes';
    GO
    ```

    當您執行預存程式時, 它會傳回 Python 資料。框架。 這一行 T-sql 會指定傳回結果的架構: `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`。 您可以將結果插入新的資料表中, 或將其傳回至應用程式。

    ![執行預存程式的結果集](media/train-score-using-python-NB-model-results.png)

    結果是使用花卉特性做為輸入的物種的150預測。 對於大部分的觀察, 預測的物種會符合實際的物種。

    這個範例是使用 Python 鳶尾花資料集進行定型和評分的簡單方法。 較常見的方法牽涉到執行 SQL 查詢來取得新的資料, 並將其當成 Python `InputDataSet`傳入。 

## <a name="conclusion"></a>結論

在此練習中, 您已瞭解如何建立專門用來執行不同工作的預存程式, 其中每個預存程式都使用系統預存程式[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)來啟動 Python 進程。 Python 處理常式的輸入會當做參數傳遞至 sp_execute_external 腳本。 Python 腳本本身和 SQL Server 資料庫中的資料變數都會當做輸入傳遞。

一般來說, 您應該只打算使用具有精美 Python 程式碼的 SSMS, 或簡單的 Python 程式碼, 以傳回以資料列為基礎的輸出。 SSMS 是一種工具, 可支援 T-sql 之類的查詢語言, 並傳回簡維資料列集。 如果您的程式碼會產生像是散佈圖或長條圖的視覺效果輸出, 您需要可呈現影像的工具或使用者應用程式。

對於用來撰寫處理各種作業之全內含腳本的 Python 開發人員而言, 將工作組織成不同的程式可能看似不必要。 但定型和計分有不同的使用案例。 藉由分隔它們, 您可以將每個工作放在不同的排程上, 並將許可權設為作業的範圍。

同樣地, 您也可以利用 SQL Server 的資源功能, 例如平行處理、資源管理, 或撰寫腳本以在支援資料流程處理和平行執行的[revoscalepy](../python/ref-py-revoscalepy.md)或[microsoftml](../python/ref-py-microsoftml.md)中使用演算法。 藉由分隔定型和評分, 您可以將特定工作負載的優化設為目標。

最後一項優點是可以使用參數來修改進程。 在此練習中, 已將建立模型的 Python 程式碼 (在此範例中名為 "貝氏貝氏機率分類") 當做輸入傳遞至第二個預存程式, 以在計分進程中呼叫模型。 此練習只會使用一個模型, 但您可以想像如何在評分工作中將模型參數化, 讓該腳本更有用。

## <a name="next-steps"></a>後續步驟

如果您是 SQL developer 的 Python 新手, 請參閱在本機使用 Python 程式碼的步驟和工具, 以及從本機會話將執行轉移至遠端 SQL Server 實例的能力。

> [!div class="nextstepaction"]
> [設定 Python 用戶端工作站](../python/setup-python-client-tools-sql.md)。

