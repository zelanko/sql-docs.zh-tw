---
title: "步驟 6： 實施模型 |Microsoft 文件"
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- python-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b33f3876f054d7e7150a18967d5cfa37dd2d82bf
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="step-6-operationalize-the-model"></a>步驟 6︰操作模型

在此步驟中，您將學習到*實施*定型，且在先前步驟中儲存的模型。 實施在此情況下部署模型至生產環境適用於計分 」 的方式。 這是容易如果 Python 程式碼包含在預存程序。 然後，您就可以從應用程式，以便預測新的觀察值上呼叫預存程序。

您將瞭解兩種方法來呼叫預存程序的 Python 模型：

- **批次計分模式**︰使用 SELECT 查詢來提供多個資料列。 此預存程序會傳回對應至輸入案例的觀察值資料表。
- **個別計分模式**︰傳遞一組個別參數值作為輸入。  此預存程序會傳回單一資料列或值。

## <a name="scoring-using-the-scikit-learn-model"></a>計分使用 scikit-了解模型

預存程序_PredictTipSciKitPy_使用 scikit-學習模型。 這個預存程序說明 Python 預測呼叫包裝在預存程序的基本語法。

- 若要使用模型的名稱被提供做為輸入參數，預存程序。 
- 預存程序會再從資料庫資料表載入序列化的模型`nyc_taxi_models`.table，在預存程序中使用 SELECT 陳述式。
- 序列化的模型儲存在 Python 變數`mod`以便進一步處理使用 Python。
- 要計分的新案例所取自[!INCLUDE[tsql](../../includes/tsql-md.md)]中指定查詢`@input_data_1`。 讀取查詢資料之後，這些資料列會儲存在預設資料框架 `InputDataSet`中。
- 此資料框架會傳遞至`predict_proba`羅吉斯迴歸模型中，函式`mod`，使用 scikit 建立時所-學習模型。 
- `predict_proba`函式 (`probArray = mod.predict_proba(X)`) 傳回**float**表示的機率，將指定的提示 （的任何數量）。
- 預存程序也能計算精確度的度量，AUC （曲線底下區域）。 如果您也可以提供目標標籤 （也就是 （雪人） 資料行），只會產生精確度度量，例如 AUC。 預測不需要目標標籤 (變數`y`)，但精確度度量計算。

  因此，如果您沒有目標標籤要計分的資料，您可以修改預存程序，移除 AUC 計算，並只傳回從功能的提示機率 (變數`X`預存程序)。

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
        import pandas;
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

## <a name="scoring-using-the-revoscalepy-model"></a>計分使用 revoscalepy 模型

預存程序_PredictTipRxPy_使用模型，建立使用**revoscalepy**程式庫。 它的運作方式一樣為_PredictTipSciKitPy_程序，但有一些變更，如**revoscalepy**函式。

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
      import pandas;
      from sklearn import metrics
      from revoscalepy.functions.RxPredict import rx_predict_ex;
      
      mod = pickle.loads(lmodel2)
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      y = numpy.ravel(InputDataSet[["tipped"]])
      
      probArray = rx_predict_ex(mod, X)
      probList = []
      for i in range(len(probArray._results["tipped_Pred"])):
        probList.append((probArray._results["tipped_Pred"][i]))
      
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

## <a name="batch-scoring-using-a-select-query"></a>使用 SELECT 查詢的批次計分

預存程序**PredictTipSciKitPy**和**PredictTipRxPy**需要兩個輸入參數： 

- 擷取計分的資料的查詢
- 定型模型的名稱

在本節中，您將學習如何將這些引數傳遞給預存程序，輕鬆地變更模型和用於計分的資料。

1. 定義輸入的資料，並呼叫預存程序進行評分，如下所示。 此範例中使用預存程序 PredictTipSciKitPy 計分，並傳入模型的名稱和查詢字串

    ```SQL
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    預存程序會傳回傳入的輸入查詢的一部分的每個路線的預測的機率。 如果您使用 SSMS (SQL Server Management Studio) 來執行查詢，機率會顯示為中的資料表**結果**窗格。 **訊息**窗格具有值為大約 0.56 輸出 （AUC 或曲線底下區域） 的精確度度量。

2. 若要使用**revoscalepy**的計分模型，請呼叫預存程序**PredictTipRxPy**、 模型名稱和查詢字串中傳遞。

    ```SQL
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="score-individual-rows-using-scikit-learn-model"></a>分數為個別的資料列使用 scikit-了解模型

有時候，而不是批次計分，您可能會想要在單一的情況下，傳遞從應用程式中，取得值，並根據這些值產生單一結果。 例如，您可以設定 Excel 工作表、Web 應用程式或 Reporting Services 報表來呼叫預存程序，並提供使用者鍵入或選取的輸入。

在本節中，您將學習如何透過呼叫預存程序來建立單一預測。

1. 花點時間檢閱程式碼的預存程序[PredictTipSingleModeSciKitPy](#PredictTipSingleModeSciKitPy)和[PredictTipSingleModeRxPy](#PredictTipSingleModeRxPy)，這會下載的一部分。 這些預存程序使用 scikit-了解和 revoscalepy 模型，以及執行評分，如下所示：

  - 做為輸入提供模型的名稱和多個單一值。 這些輸入包括旅客計數、 旅行距離等等。
  - 資料表值函式，`fnEngineerFeatures`會接受輸入的值，並將經緯度和直接距離的您該轉換。 [第 4 課](sqldev-py4-create-data-features-using-t-sql.md)包含這個資料表值函式的描述。
  - 如果您從外部應用程式呼叫預存程序，請確定輸入的資料符合 Python 模型的必要輸入的功能。 這可能包括轉型或轉換的輸入的資料 Python 資料型別，或驗證的資料類型和資料長度。
  - 預存程序會建立預存的 Python 模型為基礎的分數。

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

以下是執行計分使用預存程序的定義**scikit-了解**模型。

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
      import pandas;
      
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

以下是執行計分使用預存程序的定義**revoscalepy**模型。

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
      import pandas;
      from revoscalepy.functions.RxPredict import rx_predict_ex;
      
      # Load model and unserialize
      mod = pickle.loads(model)
      
      # Get features for scoring from input data
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      
      # Score data to get tip prediction probability as a list (of float)
      
      probArray = rx_predict_ex(mod, X)
      
      probList = []
      probList.append(probArray._results["tipped_Pred"])
      
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

2.  若要試試看，開啟 新**查詢**視窗中，並呼叫預存程序，每個特徵資料行的輸入參數。

    ```SQL
    -- Call stored procedure PredictTipSingleModeSciKitPy to score using SciKit-Learn model
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'linear_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    -- Call stored procedure PredictTipSingleModeRxPy to score using revoscalepy model
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```
    
    七個的值為這些特徵資料行，順序為：
    
    -   *passenger_count*
    -   *trip_distance*
    -   *trip_time_in_secs*
    -   *pickup_latitude*
    -   *pickup_longitude*
    -   *dropoff_latitude*
    -   *dropoff_longitude*

3. 提示要支付計程車旅程上述參數或功能的可能性就這兩個程序的輸出。

## <a name="conclusions"></a>結論

在本教學課程中，您學到如何使用預存程序中內嵌的 Python 程式碼。 與整合[!INCLUDE[tsql](../../includes/tsql-md.md)]可以更容易部署 Python 模型來進行預測，並納入企業資料工作流程的模型定型。

## <a name="previous-step"></a>上一個步驟
[步驟 6︰操作模型](sqldev-py6-operationalize-the-model.md)

## <a name="see-also"></a>另請參閱

[使用 Python 的機器學習服務](../python/sql-server-python-services.md)

