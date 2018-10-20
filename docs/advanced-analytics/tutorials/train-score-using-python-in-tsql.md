---
title: SQL Server 中使用 Python 模型訓練和預測 |Microsoft Docs
description: 建立並定型模型，使用 Python 和傳統的鳶尾花資料集。 將模型儲存至 SQL Server，然後使用它來產生預測的結果。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/18/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 839bcecdeaf7b5e2a7ea1297fe941353bffed20e
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461834"
---
# <a name="use-a-python-model-in-sql-server-for-training-and-scoring"></a>使用 SQL Server 中的 Python 模型訓練和評分
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在 Python 練習中，了解常見的模式，來建立、 定型和使用 SQL Server 中的模型。 這個練習中建立兩個預存程序。 第一個會產生預測根據花卉特性鳶尾花品種的貝氏機率分類模型。 第二個程序是用於評分。 它會呼叫第一個程序輸出一組預測中所產生的模型。 透過逐步執行本練習，您將學習為基礎的 SQL Server 資料庫引擎執行個體上執行 Python 程式碼的基本技巧。

此練習中所使用的範例資料[鳶尾花資料集](demo-data-iris-in-sql.md)中**irissql**資料庫。

## <a name="create-a-model-using-a-sproc"></a>使用預存程序建立模型

1. 開啟新的 [查詢] 視窗，在 Management Studio 連接到**irissql**資料庫。 

    ```sql
    USE irissql
    GO
    ```

2. 在新的 [查詢] 視窗，建立預存程序，建立並定型的模型執行下列程式碼。 會儲存在 SQL Server 中重複使用的模型會序列化為位元組資料流，並儲存在資料庫資料表中的 varbinary （max） 資料行。 一旦建立模型時，定型、 序列化，並儲存至資料庫，它可以呼叫其他程序或計分工作負載預測 T-SQL 函式。

   這個程式碼會使用序列化，序列化的模型和 scikit-learn 提供貝氏機率分類演算法。 此模型會使用從 0 到 4 中的資料行的資料定型**iris_data**資料表。 您在程序的第二部分中看到的參數說明資料輸入和模型輸出。 

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

3. 驗證預存程序存在。 如果沒有發生錯誤，執行 T-SQL 指令碼，從上一個步驟，新的預存程序稱為**generate_iris_model**會建立並加入至**irissql**資料庫。 您可以在 Management Studio 中找到預存程序**物件總管**下方**可程式性**。

## <a name="execute-the-sproc-to-create-and-train-models"></a>執行預存程序建立並定型模型

1. 建立預存程序之後，執行下列程式碼來執行它。 執行預存程序的特定陳述式是`EXEC`第五個列。

   這個指令碼會刪除現有的模型，相同的名稱 （"貝氏機率分類 」） 以挪出空間給新的重新執行相同的程序所建立。 不用模型刪除，就會發生錯誤，指出此物件已經存在。 

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes '
    SELECT @new_model_name 
    EXEC generate_iris_model @model OUTPUT;
    DELETE iris_models WHERE model_name = @new_model_name;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    GO
    ```

2. 在 [輸出] 區域中檢視結果。 指令碼包含 SELECT 陳述式顯示模型存在。 傳回模型的清單中的另一個方法是`SELECT * FROM iris_models`中**irissql**。

    **結果**

    |   | （沒有資料行名稱 |
    |---|-----------------|
    | 1 | 貝氏機率分類     | 


## <a name="create-and-execute-a-sproc-for-generating-predictions"></a>建立和執行的預存程序來產生預測

既然您已建立、 定型，並儲存模型中，移至下一個步驟： 建立預存程序，會產生預測。 所呼叫的 sp_execute_external_script 來啟動 Python，然後將傳遞載入序列化的模型，您在上一個練習中，建立，然後提供它要評分的資料輸入的 Python 指令碼中，您會執行這項操作。

1. 執行下列程式碼建立預存程序執行評分。 在執行階段，此程序會將二進位模型載入，請使用資料行`[1,2,3,4]`做為輸入，並指定資料行`[0,5,6]`做為輸出。

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

2. 執行預存程序，讓模型名稱"貝氏機率分類 」，讓此程序知道要使用哪一個模型。 

    ```sql
    EXEC predict_species 'Naive Bayes';
    GO
    ```

    當您執行預存程序時，它會傳回 Python data.frame。 T-SQL 的這一行會指定傳回的結果結構描述： `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`。 您可以將結果插入到新的資料表，或返回應用程式。

    ![結果集，無法執行預存程序](media/train-score-using-python-NB-model-results.png)

    結果是 150 預測物種利用花卉的特性做為輸入。 對於大部分的觀察值，預測的指定比對實際的動物種類。

    此範例已發出簡單使用 Python 鳶尾花資料集進行定型和計分。 更常見的方法會牽涉到執行 SQL 查詢，以取得新的資料，並將它傳遞至 Python `InputDataSet`。 

## <a name="conclusion"></a>結論

在這個練習中，您已了解如何建立預存程序，針對不同的工作，每個預存程序使用的系統預存程序的地方[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)啟動 Python 處理序。 Python 程序的輸入會當做參數傳遞至 sp_execute_external 指令碼。 在 Python 指令碼本身和 SQL Server 資料庫中的資料變數會傳遞做為輸入。

如果您是用來使用 Python 中，您可能習慣手動載入資料、 建立一些摘要和圖形，然後定型模型及產生一些分數，全都放在相同的 250 行程式碼。 這篇文章會有所不同組織成個別的程序作業的慣用方法。 這種做法會很有幫助以多種等級。

其中一個優點是您可以分隔成可以使用參數進行修改的可重複執行步驟的程序。 盡量，您想清楚定義輸入和對應至預存程序輸入的輸出和輸出可以在執行階段傳入預存程序中執行的 Python 程式碼。 在此練習中，建立模型 （名為在此範例中的"貝氏機率分類 」） 的 Python 程式碼會傳遞做為第二個預存程序，在 計分程序中呼叫模型的輸入。

第二個優點是訓練並可最佳化評分程序，利用 SQL Server 的功能，例如平行處理，資源控管，或使用中的演算法[revoscalepy](../python/what-is-revoscalepy.md)或[MicrosoftML](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) ，支援資料流，並平行執行。 藉由分隔定型和計分，您可以針對特定工作負載的最佳化。

## <a name="next-steps"></a>後續步驟

先前的教學課程著重於本機執行。 不過，您也可以執行 Python 程式碼從用戶端工作站，作為遠端計算內容中使用 SQL Server。 如需設定用戶端工作站連接到 SQL Server 的詳細資訊，請參閱[設定 Python 用戶端工具](../python/setup-python-client-tools-sql.md)。

+ [從 Python 用戶端建立 revoscalepy 模型](use-python-revoscalepy-to-create-model.md)
