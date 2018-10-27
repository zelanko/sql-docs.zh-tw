---
title: 使用 SQL Server 的 Python 模型運算化 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d95edb081edc0f18a3734025a5902d13f8e9a295
ms.sourcegitcommit: 70e47a008b713ea30182aa22b575b5484375b041
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2018
ms.locfileid: "49806808"
---
# <a name="operationalize-the-python-model-using-sql-server"></a>使用 SQL Server 的 Python 模型運算化
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章是教學課程中，部分[適用於 SQL 開發人員的資料庫內 Python 分析](sqldev-in-database-python-for-sql-developers.md)。 

在此步驟中，您學會*操作*受過訓練，並在上一個步驟中儲存的模型。

在此案例中，實作表示將模型部署到生產環境進行評分。 與 SQL Server 的整合可讓這相當簡單，因為您可以在預存程序中內嵌 Python 程式碼。 若要取得新的輸入所根據的模型預測，只要從應用程式呼叫預存程序，並傳遞新的資料。

這一課會示範兩個方法，來建立 Python 模型為基礎的預測： 批次評分和評分的資料列。

- **批次評分：** 提供多個輸入資料列，將選取的查詢做為引數傳遞至預存程序。 結果是對應至輸入案例的觀察值的資料表。
- **個別評分：** 傳遞一組個別參數值作為輸入。  此預存程序會傳回單一資料列或值。

用於評分所需的所有 Python 程式碼都可做為預存程序的一部分。

| 預存程序名稱 | 批次或單一 | 模型的來源|
|----|----|----|
|PredictTipRxPy|批次 (batch)| revoscalepy 模型|
|PredictTipSciKitPy|批次 (batch) |scikit-learn-了解模型|
|PredictTipSingleModeRxPy|單一資料列| revoscalepy 模型|
|PredictTipSingleModeSciKitPy|單一資料列| scikit-learn-了解模型|

## <a name="batch-scoring"></a>批次評分

前兩個預存程序說明將 Python 預測呼叫包裝在預存程序的基本語法。 這兩個預存程序需要資料的資料表做為輸入。

- 要使用的精確模型的名稱被提供做為預存程序的輸入參數。 預存程序會從資料庫資料表載入序列化的模型`nyc_taxi_models`.table，預存程序中使用 SELECT 陳述式。
- 序列化的模型儲存在 Python 變數`mod`供進一步處理使用 Python。
- 需要評分的新案例所取自[!INCLUDE[tsql](../../includes/tsql-md.md)]查詢中指定`@input_data_1`。 讀取查詢資料之後，這些資料列會儲存在預設資料框架 `InputDataSet`中。
- 這兩個預存程序會使用函式從`sklearn`來計算精確度的度量，AUC （曲線下面積）。 如果您也可以提供目標的標籤，可以只會產生精確度計量，例如 AUC ( _tipped_資料行)。 預測不需要的目標標籤 (變數`y`)，但精確度公制計算。

    因此，如果您沒有要評分的資料的目標標籤，您可以修改預存程序，若要移除的 AUC 計算，並從功能傳回只小費的機率 (變數`X`預存程序)。

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

預存程序應該已經已為您建立。 如果您找不到它，請執行下列 T-SQL 陳述式來建立預存程序。

這個預存程序需要根據 scikit-learn 模型-了解封裝，因為它會使用該套件的特定函式：

+ 包含輸入資料框架會傳遞至`predict_proba`函式的羅吉斯迴歸模型， `mod`。 `predict_proba`函式 (`probArray = mod.predict_proba(X)`) 會傳回**float** ，表示要提供給小費 （任何金額） 的機率。

```SQL
CREATE PROCEDURE [dbo].[PredictTipSciKitPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
  EXEC sp_execute_external_script
    @language = N'Python',
    @script = N'
        import pickle;
        import numpy;
        from sklearn import metrics
        
        mod = pickle.loads(lmodel2)
        
        X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
        y = numpy.ravel(InputDataSet[["tipped"]])
        
        probArray = mod.predict_proba(X)
        probList = []
        for i in range(len(probArray)):
          probList.append((probArray[i])[1])
        
        probArray = numpy.asarray(probList)
        fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
        aucResult = metrics.auc(fpr, tpr)
        print ("AUC on testing data is: " + str(aucResult))
        
        OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
        ',  
    @input_data_1 = @inquery,
    @input_data_1_name = N'InputDataSet',
    @params = N'@lmodel2 varbinary(max)',
    @lmodel2 = @lmodel2
  WITH RESULT SETS ((Score float));
END
GO
```

### <a name="predicttiprxpy"></a>PredictTipRxPy

這個預存程序會使用相同的輸入，並建立先前的預存程序中，相同類型的分數，但使用從函式**revoscalepy**與 SQL Server machine learning 提供的封裝。

> [!NOTE] 
> 這個預存程序的程式碼已稍微變更早期發行版本和 RTM 版本，以反映變更 revoscalepy 套件之間。 請參閱[變更](#changes)如需詳細資訊的資料表。

```SQL
CREATE PROCEDURE [dbo].[PredictTipRxPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);

  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      from sklearn import metrics
      from revoscalepy.functions.RxPredict import rx_predict;
      
      mod = pickle.loads(lmodel2)
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      y = numpy.ravel(InputDataSet[["tipped"]])
      
      probArray = rx_predict(mod, X)
      prob_list = prob_array["tipped_Pred"].values 
      
      probArray = numpy.asarray(probList)
      fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
      aucResult = metrics.auc(fpr, tpr)
      print ("AUC on testing data is: " + str(aucResult))
      OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
      ',    
    @input_data_1 = @inquery,
    @input_data_1_name = N'InputDataSet',
    @params = N'@lmodel2 varbinary(max)',
    @lmodel2 = @lmodel2
  WITH RESULT SETS ((Score float));
END
GO
```

## <a name="run-batch-scoring-using-a-select-query"></a>執行批次評分使用 SELECT 查詢

預存程序**PredictTipSciKitPy**並**PredictTipRxPy**需要兩個輸入參數： 

- 擷取用於評分的資料的查詢
- 定型模型的名稱

將這些引數傳遞至預存程序之後，您可以選取特定的模型，或變更用於評分的資料。

1. 若要使用**scikit-learn-了解**模型進行評分，請呼叫預存程序**PredictTipSciKitPy**、 傳遞模型名稱和查詢字串做為輸入。

    ```SQL
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    預存程序傳回的輸入查詢的一部分傳入每趟車程的預測的機率。 
    
    如果您使用 SSMS (SQL Server Management Studio) 執行查詢，機率會以表格形式**結果**窗格。 **訊息**窗格具有大約 0.56 值輸出 （AUC 或曲線下的面積） 的精確度度量。

2. 若要使用**revoscalepy**模型進行評分，請呼叫預存程序**PredictTipRxPy**、 傳遞模型名稱和查詢字串做為輸入。

    ```SQL
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="single-row-scoring"></a>單一資料列評分

有時候，而不是批次評分，建議您將在單一的情況下，從應用程式時，取得值，並傳回單一結果，根據這些值。 比方說，您可以設定 Excel 工作表、 web 應用程式或報表來呼叫預存程序，並將傳遞給它的輸入型別或由使用者選取。

在本節中，您將了解如何建立單一預測，藉由呼叫兩個預存程序：

+ [PredictTipSingleModeSciKitPy](#PredictTipSingleModeSciKitPy)專為單一資料列評分使用 sscikit-learn-了解模型。
+ [PredictTipSingleModeRxPy](#PredictTipSingleModeRxPy)專為單一資料列評分使用 revoscalepy 模型。
+ 如果您還沒有尚未定型的模型，回到[步驟 5](sqldev-py5-train-and-save-a-model-using-t-sql.md)！

這兩個模型會採用做為輸入一系列的單一值，例如乘客計數、 車程距離等等。 資料表值函式， `fnEngineerFeatures`，用來從一項新功能的輸入轉換緯度和經度值、 的直線距離。 [第 4 課](sqldev-py4-create-data-features-using-t-sql.md)包含這個資料表值函式的描述。

這兩個預存程序會建立 Python 模型為基礎的分數。

> [!NOTE]
> 
> 請務必您提供從外部應用程式呼叫預存程序時，Python 模型所需的所有輸入的功能。 若要避免錯誤，您可能需要轉型，或輸入的資料轉換成 Python 資料類型，除了驗證資料類型和資料長度。

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

花點時間檢閱程式碼會執行評分使用預存程序**scikit-learn-了解**模型。

```SQL
CREATE PROCEDURE [dbo].[PredictTipSingleModeSciKitPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
  SELECT * FROM [dbo].[fnEngineerFeatures]( 
    @passenger_count,
    @trip_distance,
    @trip_time_in_secs,
    @pickup_latitude,
    @pickup_longitude,
    @dropoff_latitude,
    @dropoff_longitude)
    '
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      
      # Load model and unserialize
      mod = pickle.loads(model)
      
      # Get features for scoring from input data
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      
      # Score data to get tip prediction probability as a list (of float)
      probList = []
      probList.append((mod.predict_proba(X)[0])[1])
      
      # Create output data frame
      OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
    ',
    @input_data_1 = @inquery,
    @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
      @model = @lmodel2,
      @passenger_count =@passenger_count ,
      @trip_distance=@trip_distance,
      @trip_time_in_secs=@trip_time_in_secs,
      @pickup_latitude=@pickup_latitude,
      @pickup_longitude=@pickup_longitude,
      @dropoff_latitude=@dropoff_latitude,
      @dropoff_longitude=@dropoff_longitude
  WITH RESULT SETS ((Score float));
END
GO
```

### <a name="predicttipsinglemoderxpy"></a>PredictTipSingleModeRxPy

下列的預存程序可讓您執行使用的評分**revoscalepy**模型。

```SQL
CREATE PROCEDURE [dbo].[PredictTipSingleModeRxPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
    SELECT * FROM [dbo].[fnEngineerFeatures]( 
      @passenger_count,
      @trip_distance,
      @trip_time_in_secs,
      @pickup_latitude,
      @pickup_longitude,
      @dropoff_latitude,
      @dropoff_longitude)
    '
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      from revoscalepy.functions.RxPredict import rx_predict;
      
      # Load model and unserialize
      mod = pickle.loads(model)
      
      # Get features for scoring from input data
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      
      # Score data to get tip prediction probability as a list (of float)
      
      probArray = rx_predict(mod, X)
      
      probList = []
      prob_list = prob_array["tipped_Pred"].values
      
      # Create output data frame
      OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
      ',
    @input_data_1 = @inquery,
    @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
      @model = @lmodel2,
      @passenger_count =@passenger_count ,
      @trip_distance=@trip_distance,
      @trip_time_in_secs=@trip_time_in_secs,
      @pickup_latitude=@pickup_latitude,
      @pickup_longitude=@pickup_longitude,
      @dropoff_latitude=@dropoff_latitude,
      @dropoff_longitude=@dropoff_longitude
  WITH RESULT SETS ((Score float));
END
GO
```

### <a name="generate-scores-from-models"></a>從模型產生分數

建立預存程序之後，很容易產生分數，其中一種模型為基礎。 只要開啟 [新**查詢**] 視窗中，並針對每個特徵資料行的輸入或貼上參數。 第七個必須是這些特徵資料行順序的值：
    
+ *passenger_count*
+ *trip_distance* v*trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. 若要使用來產生預測**revoscalepy**模型中，執行此陳述式：
  
    ```SQL
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

2. 若要使用產生的分數**scikit-learn-了解**模型中，執行此陳述式：

    ```SQL
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'linear_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

這兩個程序的輸出是小費的使用指定的參數或功能在計程車車程所支付的機率。

### <a name="changes"></a> 變更

此區段會列出本教學課程使用的程式碼變更。 這些變更會反映最新**revoscalepy**版本。 如需 API 的協助，請參閱[Python 函式程式庫參考](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)。

| 變更詳細資料 | 注意|
| ----|----|
| 刪除`import pandas`中所有範例| 現在預設載入 pandas|
| 函式`rx_predict_ex`變更為 `rx_predict`| RTM 和發行前版本需要 `rx_predict_ex`|
| 函式`rx_logit_ex`變更為 `rx_logit`| RTM 和發行前版本需要 `rx_logit_ex`|
| ` probList.append(probArray._results["tipped_Pred"])` 變更為 `prob_list = prob_array["tipped_Pred"].values`| 更新 API|

如果您使用 SQL Server 2017 的發行前版本的 Python Services 安裝，我們建議您升級。 您也可以使用最新版的 Machine Learning Server 升級只是 Python 和 R 元件。 如需詳細資訊，請參閱 <<c0> [ 升級的 SQL Server 執行個體中使用繫結](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

## <a name="conclusions"></a>結論

在本教學課程中，您已了解如何使用內嵌在預存程序中的 Python 程式碼。 與整合[!INCLUDE[tsql](../../includes/tsql-md.md)]更輕鬆部署 Python 模型來進行預測，並納入模型重新定型作為企業資料工作流程的一部分。

## <a name="previous-step"></a>上一個步驟

[訓練及儲存 Python 模型](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="see-also"></a>另請參閱

[SQL Server 中的 Python 擴充功能](../concepts/extension-python.md)
