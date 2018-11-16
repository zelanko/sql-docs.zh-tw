---
title: SQL Server 中的 Python 模型訓練和預測使用預存程序 |Microsoft Docs
description: 若要建立、 定型和使用 Python 模型與傳統的鳶尾花資料集的 SQL Server 預存程序中內嵌 Python 程式碼。 將定型的模型儲存至 SQL Server，然後使用它來產生預測的結果。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/23/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 17b51d695a923b6db1661e6e15605a1f05d08178
ms.sourcegitcommit: 0f7cf9b7ab23df15624d27c129ab3a539e8b6457
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2018
ms.locfileid: "51293154"
---
# <a name="create-train-and-use-a-python-model-with-stored-procedures-in-sql-server"></a>建立、 定型和使用 SQL Server 中的預存程序中的 Python 模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這個練習中示範的 Python 與 SQL Server 的整合，當您將新增[Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)資料庫引擎執行個體的功能。 這類執行個體上，您可以將內部的 Python 程式碼包裝[預存程序](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)以利作業化您的指令碼，對於生產工作負載。 能夠將程式碼內嵌在預存程序中有如何設計、 測試及管理資料科學與機器學習服務工作中的獲益良多。 它能讓您的指令碼和模型到任何可以連線到 SQL Server 的應用程式。

在 Python 練習中，您將建立和執行兩個預存程序。 第一個使用傳統的鳶尾花資料集，並產生預測根據花卉特性鳶尾花品種的貝氏機率分類模型。 第二個程序是用於評分。 它會呼叫第一個程序輸出一組預測中所產生的模型。 藉由將程式碼放在預存程序中，作業會為自主、 可重複使用，和可呼叫其他預存程序和用戶端應用程式。 

藉由完成本教學課程中，您將了解：

> [!div class="checklist"]
> * 如何在預存程序中內嵌 Python 程式碼
> * 如何將您的程式碼，透過輸入的輸入傳遞預存程序
> * 如何讓模型來使用預存程序

## <a name="prerequisites"></a>先決條件

此練習中所使用的範例資料[ **irissql** ](demo-data-iris-in-sql.md)資料庫。

您也需要 T-SQL 編輯器中，例如[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017)。

## <a name="create-a-stored-procedure-that-generates-models"></a>建立會產生模型的預存程序

SQL Server 開發的常見模式是組織成不同的預存程序的可程式化作業。 在此步驟中，您將建立產生的模型來預測結果的預存程序。 

1. 開啟新的 [查詢] 視窗，在 Management Studio 連接到**irissql**資料庫。 

    ```sql
    USE irissql
    GO
    ```

2. 複製下列程式碼來建立新的預存程序。 

   此程序執行時，呼叫[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)啟動 Python 工作階段。 
   
   輸入所需的 Python 程式碼會傳遞做為輸入參數，此預存程序。 輸出會是定型的模型，並根據 Python **scikit-learn-了解**適用於機器學習演算法程式庫。 

   此程式碼會使用[ **pickle** ](https://docs.python.org/2/library/pickle.html)序列化模型。 此模型會使用從 0 到 4 中的資料行的資料定型**iris_data**資料表。 
   
   您在程序的第二部分中看到的參數說明資料輸入和模型輸出。 盡量，您想要清楚定義輸入預存程序中執行的 Python 程式碼，並將輸出對應至預存程序輸入和輸出，在執行階段中傳遞。 

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

3. 驗證預存程序存在。 

   如果沒有發生錯誤，執行 T-SQL 指令碼，從上一個步驟，新的預存程序稱為**generate_iris_model**會建立並加入至**irissql**資料庫。 您可以在 Management Studio 中找到預存程序**物件總管**下方**可程式性**。

## <a name="execute-the-procedure-to-create-and-train-models"></a>執行程序建立並定型模型

在此步驟中，執行程序執行的內嵌程式碼，建立定型和序列化的模型，做為輸出。 會儲存在 SQL Server 中重複使用的模型會序列化為位元組資料流，並儲存在資料庫資料表中的 varbinary （max） 資料行。 一旦模型建立、 定型、 序列化，並儲存至資料庫，它可以呼叫其他程序，或由[預測 T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)計分工作負載的函式。

1. 下列程式碼複製到執行程序。 執行預存程序的特定陳述式是`EXEC`第五個列。

   這個指令碼會刪除現有的模型，相同的名稱 （"貝氏機率分類 」） 以挪出空間給新的重新執行相同的程序所建立。 不用模型刪除，就會發生錯誤，指出此物件已經存在。 模型會儲存在名為資料表**iris_models**，您所建立時佈建**irissql**資料庫。

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


## <a name="create-and-execute-a-stored-procedure-for-generating-predictions"></a>建立及執行預存程序來產生預測

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

在此練習中，您已了解如何建立不同的工作，其中每個預存程序會使用系統預存程序專用的預存程序[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)啟動 Python 處理序。 Python 程序的輸入會當做參數傳遞至 sp_execute_external 指令碼。 在 Python 指令碼本身和 SQL Server 資料庫中的資料變數會傳遞做為輸入。

一般而言，您只應在 SSMS 中使用外觀精美的 Python 程式碼或簡單的 Python 程式碼會傳回資料列為主的輸出。 作為工具，SSMS 支援 T-SQL 這類的查詢語言，並傳回扁平化資料列集。 如果您的程式碼會產生類似的散佈圖或長條圖的視覺化輸出，您會需要一個工具或使用者的應用程式，可以呈現影像。

針對某些 Python 開發人員用來撰寫全部包含的指令碼處理作業的範圍，將工作組織成個別的程序看起來不必要。 但定型和計分有不同的使用案例。 藉由分隔它們，您可以將每個工作放上不同的排程和作業的 「 範圍 」 權限。

同樣地，您也可以利用資源配置的 SQL Server 功能，例如平行處理，資源控管，或撰寫您的指令碼，以使用中的演算法[revoscalepy](../python/what-is-revoscalepy.md)或是[MicrosoftML](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) ，支援資料流處理和平行執行。 藉由分隔定型和計分，您可以針對特定工作負載的最佳化。

最後一個好處是可以使用參數來修改處理程序。 在此練習中，建立模型 （在此範例中，名為"貝氏機率分類 」） 的 Python 程式碼傳遞做為第二個預存程序呼叫模型評分程序中的輸入。 這個練習中只會使用一個模型，但您可以想像如何參數化的評分的工作中的模型會使該指令碼更加實用。

## <a name="next-steps"></a>後續步驟

如果您不熟悉 Python 的 SQL 開發人員，檢閱的步驟和工具來處理在本機，Python 程式碼能夠轉移到遠端的 SQL Server 執行個體從本機工作階段執行。

> [!div class="nextstepaction"]
> [設定 Python 用戶端工作站](../python/setup-python-client-tools-sql.md)。

