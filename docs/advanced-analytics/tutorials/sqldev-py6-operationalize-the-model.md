---
title: "步驟 6： 實施 Python 模型使用 SQL Server |Microsoft 文件"
ms.custom: 
ms.date: 10/17/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: python-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 7dcda2d17413e6c660510498c4b3ea770bb0b09d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="step-6-operationalize-the-python-model-using-sql-server"></a>步驟 6： 實施 Python 模型使用 SQL Server

這篇文章的教學課程中，屬於[SQL 開發人員的資料庫中的 Python 分析](sqldev-in-database-python-for-sql-developers.md)。 

在此步驟中，您學會*實施*定型，且在先前步驟中儲存的模型。

實施這個案例中，表示將模型部署到生產環境適用於計分。 與 SQL Server 的整合可讓此相當簡單，因為您可以在預存程序中內嵌的 Python 程式碼。 若要從模型根據新的輸入取得預測，只要應用程式呼叫預存程序，並傳遞新的資料。

這一課會示範兩種建立 Python 模型為基礎的預測方法： 批次計分，和計分的資料列。

- **批次計分：**若要提供多個輸入資料列，將選取的查詢當做引數傳遞至預存程序。 結果會是對應於輸入案例的觀察值的資料表。
- **個別計分：**將一組個別的參數值傳遞做為輸入。  此預存程序會傳回單一資料列或值。

所需的計分的 Python 程式碼會提供預存程序的一部分。

| 預存程序名稱 | 批次或單一 | 模型的來源|
|----|----|----|
|PredictTipRxPy|批次 (batch)| revoscalepy 模型|
|PredictTipSciKitPy|批次 (batch) |scikit-了解模型|
|PredictTipSingleModeRxPy|單一資料列| revoscalepy 模型|
|PredictTipSingleModeSciKitPy|單一資料列| scikit-了解模型|

## <a name="batch-scoring"></a>批次計分

前兩個預存程序說明了 Python 預測呼叫包裝在預存程序的基本語法。 這兩個預存程序需要資料的資料表做為輸入。

- 做為輸入參數，預存程序提供精確的模型使用的名稱。 預存程序會從資料庫資料表中載入序列化的模型`nyc_taxi_models`.table，在預存程序中使用 SELECT 陳述式。
- 序列化的模型儲存在 Python 變數`mod`以便進一步處理使用 Python。
- 要計分的新案例所取自[!INCLUDE[tsql](../../includes/tsql-md.md)]中指定查詢`@input_data_1`。 讀取查詢資料之後，這些資料列會儲存在預設資料框架 `InputDataSet`中。
- 這兩個預存程序使用函式從`sklearn`來計算精確度的度量，AUC （曲線底下區域）。 如果您也可以提供目標標籤，可以只會產生精確度度量，例如 AUC (_傾斜_資料行)。 預測不需要目標標籤 (變數`y`)，但精確度度量計算。

    因此，如果您沒有目標標籤要計分的資料，您可以修改預存程序，移除 AUC 計算，並傳回提示機率從功能 (變數`X`預存程序)。

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

預存程序應該已經建立了。 如果您找不到它，請執行下列 T-SQL 陳述式來建立預存程序。

此預存程序需要 scikit 所根據的模型-了解封裝，因為它會使用該套件的特定函式：

+ 包含輸入資料框架會傳遞至`predict_proba`羅吉斯迴歸模型中，函式`mod`。 `predict_proba`函式 (`probArray = mod.predict_proba(X)`) 傳回**float**表示的機率，將指定的提示 （的任何數量）。

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

這個預存程序會使用相同的輸入並且會建立相同類型的分數為先前的預存程序，但會使用函式從**revoscalepy**隨附 SQL Server 機器學習的封裝。

> [!NOTE] 
> 這個預存程序的程式碼已稍微變更早期發行版本和 RTM 版本，以反映變更 revoscalepy 封裝之間。 請參閱[變更](#changes)如需詳細資訊的資料表。

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

## <a name="run-batch-scoring-using-a-select-query"></a>執行批次計分使用 SELECT 查詢

預存程序**PredictTipSciKitPy**和**PredictTipRxPy**需要兩個輸入參數： 

- 擷取計分的資料的查詢
- 定型模型的名稱

將這些引數傳遞給預存程序之後，您可以選取特定的模型，或變更用於計分的資料。

1. 若要使用**scikit-了解**的計分模型，請呼叫預存程序**PredictTipSciKitPy**、 傳遞模型名稱和查詢字串做為輸入。

    ```SQL
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    預存程序會傳回傳入的輸入查詢的一部分的每個路線的預測的機率。 
    
    如果您使用 SSMS (SQL Server Management Studio) 來執行查詢，機率會顯示為中的資料表**結果**窗格。 **訊息**窗格具有值為大約 0.56 輸出 （AUC 或曲線底下區域） 的精確度度量。

2. 若要使用**revoscalepy**的計分模型，請呼叫預存程序**PredictTipRxPy**、 傳遞模型名稱和查詢字串做為輸入。

    ```SQL
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="single-row-scoring"></a>單一資料列計分

有時候，而不是批次計分，您可以將在單一的情況下，從應用程式中，取得值，並傳回單一結果，根據這些值。 例如，您無法設定 Excel 工作表、 web 應用程式或報表來呼叫預存程序，並將傳遞給它的輸入型別或由使用者選取。

在本節中，您將學習如何建立單一預測，藉由呼叫兩個預存程序：

+ [PredictTipSingleModeSciKitPy](#PredictTipSingleModeSciKitPy)針對單一資料列計分使用 scikit-學習模型。
+ [PredictTipSingleModeRxPy](#PredictTipSingleModeRxPy)針對單一資料列計分使用 revoscalepy 模型。
+ 如果您尚未尚未定型模型，傳回至[步驟 5](sqldev-py5-train-and-save-a-model-using-t-sql.md)！

這兩種模型會採用做為輸入一系列的單一值，例如旅客計數、 旅行距離等等。 資料表值函式， `fnEngineerFeatures`，用來從一項新功能的輸入轉換緯度與經度值、 直接距離。 [第 4 課](sqldev-py4-create-data-features-using-t-sql.md)包含這個資料表值函式的描述。

這兩個預存程序建立 Python 模型為基礎的分數。

> [!NOTE]
> 
> 請務必您提供當您從外部應用程式呼叫預存程序時，Python 模型所需的所有輸入的功能。 若要避免錯誤，您可能需要轉型或轉換的輸入的資料 Python 資料型別，除了驗證的資料類型和資料長度。

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

花點時間檢閱程式碼會執行計分使用預存程序**scikit-了解**模型。

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

下列預存程序執行計分使用**revoscalepy**模型。

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

### <a name="generate-scores-from-models"></a>若要從模型產生分數

建立預存程序之後，很容易產生分數，根據這兩種模式。 只要開啟 新**查詢**視窗，並針對每個特徵資料行的輸入或貼上參數。 第七個所需的值為這些特徵資料行，順序為：
    
+ *passenger_count*
+ *trip_distance* v*trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. 使用來產生預測**revoscalepy**模型中，執行此陳述式：
  
    ```SQL
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

2. 若要使用產生的分數**scikit-了解**模型中，執行此陳述式：

    ```SQL
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'linear_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

兩個程序的輸出是提示的機率為要支付計程車旅程功能或指定的參數。

### <a name="changes"></a>變更

此區段會列出此教學課程中使用的程式碼變更。 這些變更會反映最新**revoscalepy**版本。 應用程式開發介面的協助，請參閱[Python 函式程式庫參考](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)。

| 變更詳細資料 | 注意|
| ----|----|
| 刪除`import pandas`中所有的範例| 預設立即載入熊|
| 函式`rx_predict_ex`變更為`rx_predict`| RTM 和發行前版本需要`rx_predict_ex`|
| 函式`rx_logit_ex`變更為`rx_logit`| RTM 和發行前版本需要`rx_logit_ex`|
| ` probList.append(probArray._results["tipped_Pred"])`變更為`prob_list = prob_array["tipped_Pred"].values`| 更新應用程式開發介面|

如果您安裝 Python 的服務使用發行前版本的 SQL Server 2017，我們建議您升級。 您也可以使用最新版的機器學習伺服器升級的 Python 和 R 元件。 如需詳細資訊，請參閱[繫結使用的 SQL Server 執行個體升級](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

## <a name="conclusions"></a>結論

在本教學課程中，您學到如何使用預存程序中內嵌的 Python 程式碼。 與整合[!INCLUDE[tsql](../../includes/tsql-md.md)]可以更容易部署 Python 模型來進行預測，並納入企業資料工作流程的模型定型。

## <a name="previous-step"></a>上一個步驟

[步驟 5： 定型和儲存 Python 模型](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="see-also"></a>另請參閱

[使用 Python 的機器學習服務](../python/sql-server-python-services.md)
