---
title: 使用 Python 模型預測潛在結果
description: 示範如何使用 T-sql 函式在 SQL Server 預存程式中讓內嵌 PYthon 腳本的教學課程
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/02/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 275981cbd4543263507415b5e7ba783f1ecbd8e5
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345849"
---
# <a name="run-predictions-using-python-embedded-in-a-stored-procedure"></a>在預存程式中使用 Python 內嵌執行預測
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文屬於[適用于 SQL 開發人員的資料庫內 Python 分析](sqldev-in-database-python-for-sql-developers.md)教學課程的一部分。 

在此步驟中, 您將瞭解如何*讓*您在上一個步驟中訓練並儲存的模型。

在此案例中, 運算化表示將模型部署至生產環境以進行計分。 與 SQL Server 的整合讓這項操作變得相當簡單, 因為您可以在預存程式中內嵌 Python 程式碼。 若要根據新的輸入從模型取得預測, 請直接從應用程式呼叫預存程式, 並傳遞新的資料。

這一課將示範兩種建立以 Python 模型為基礎之預測的方法: 批次評分, 以及依資料列評分資料列。

- **批次評分:** 若要提供輸入資料的多個資料列, 請將 SELECT 查詢當做引數傳遞給預存程式。 結果會是對應到輸入案例的觀察表。
- **個別評分:** 傳遞一組個別參數值作為輸入。  此預存程序會傳回單一資料列或值。

計分所需的所有 Python 程式碼都是在預存程式中提供。

## <a name="batch-scoring"></a>批次評分

前兩個預存程式說明將 Python 預測呼叫包裝在預存程式中的基本語法。 這兩個預存程式都需要資料表做為輸入。

- 要使用的確切模型名稱會當做預存程式的輸入參數來提供。 預存程式會使用預存程式中的 SELECT `nyc_taxi_models`語句, 從資料庫的資料表載入序列化的模型。
- 序列化的模型會儲存在 python 變數`mod`中, 以使用 python 進一步處理。
- 需要評分的新案例是從中[!INCLUDE[tsql](../../includes/tsql-md.md)] `@input_data_1`指定的查詢取得。 讀取查詢資料之後，這些資料列會儲存在預設資料框架 `InputDataSet`中。
- 這兩個預存程式`sklearn`會使用中的函式來計算精確度計量 AUC (曲線下的區域)。 只有當您也提供目標標籤 (_附屬_資料行) 時, 才可以產生精確度計量 (例如 AUC)。 預測不需要目標標籤 (變數`y`), 但精確度度量計算會執行。

    因此, 如果您沒有要計分之資料的目標標籤, 您可以修改預存程式來移除 AUC 計算, 並只傳回特徵 (預存程式中的變數`X` ) 的 tip 機率。

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

Rrun 下列 T-sql 語句來建立預存程式。 這個預存程式需要以 scikit-learn 為基礎的模型, 因為它使用該封裝的特定函式:

+ 包含輸入的資料框架會傳遞至羅吉斯`predict_proba`回歸`mod`模型的功能。 函式 (`probArray = mod.predict_proba(X)`) 會傳回**float** , 表示將會指定秘訣 (任何數量) 的機率。 `predict_proba`

```sql
DROP PROCEDURE IF EXISTS PredictTipSciKitPy;
GO

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

這個預存程式會使用相同的輸入, 並建立與先前預存程式相同的分數類型, 但會使用 SQL Server 機器學習服務所提供之**revoscalepy**套件中的函數。

```sql
DROP PROCEDURE IF EXISTS PredictTipRxPy;
GO

CREATE PROCEDURE [dbo].[PredictTipRxPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
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
probList = probArray["tipped_Pred"].values 

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

## <a name="run-batch-scoring-using-a-select-query"></a>使用 SELECT 查詢執行批次評分

預存程式**PredictTipSciKitPy**和**PredictTipRxPy**需要兩個輸入參數: 

- 抓取資料進行計分的查詢
- 定型模型的名稱

藉由將這些引數傳遞給預存程式, 您可以選取特定的模型, 或變更用於計分的資料。

1. 若要使用**scikit-learn-學習**模型進行評分, 請呼叫預存程式**PredictTipSciKitPy**, 傳遞模型名稱和查詢字串做為輸入。

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    預存程式會針對傳入做為輸入查詢一部分的每個行程, 傳回預測的機率。 
    
    如果您使用 SSMS (SQL Server Management Studio) 執行查詢, 則機率會顯示為 [**結果**] 窗格中的資料表。 [**訊息**] 窗格會以大約0.56 的值, 輸出精確度度量 (AUC 或曲線下的區域)。

2. 若要使用**revoscalepy**模型進行評分, 請呼叫預存程式**PredictTipRxPy**, 傳遞模型名稱和查詢字串做為輸入。

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="single-row-scoring"></a>單一資料列評分

有時候, 您可能會想要傳入單一案例、從應用程式取得值, 並根據這些值傳回單一結果, 而不是批次評分。 例如, 您可以設定 Excel 工作表、web 應用程式或報表來呼叫預存程式, 並將其傳遞給它輸入或由使用者選取。

在本節中, 您將瞭解如何藉由呼叫兩個預存程式來建立單一預測:

+ [PredictTipSingleModeSciKitPy](#predicttipsinglemodescikitpy)是針對使用 scikit-learn 學習模型的單一資料列評分所設計。
+ [PredictTipSingleModeRxPy](#predicttipsinglemoderxpy)是針對使用 revoscalepy 模型的單一資料列評分所設計。
+ 如果您尚未定型模型, 請返回[步驟 5](sqldev-py5-train-and-save-a-model-using-t-sql.md)!

這兩種模型都接受一系列的單一值, 例如乘客計數、路程距離等等。 資料表值`fnEngineerFeatures`函式是用來將緯度和經度值從輸入轉換成新功能的直接距離。 [第4課](sqldev-py4-create-data-features-using-t-sql.md)包含此資料表值函式的描述。

這兩個預存程式都會根據 Python 模型建立分數。

> [!NOTE]
> 
> 當您從外部應用程式呼叫預存程式時, 請務必提供 Python 模型所需的所有輸入功能。 若要避免發生錯誤, 您可能需要將輸入資料轉換或轉換成 Python 資料類型, 以及驗證資料類型和資料長度。

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

請花幾分鐘的時間來檢查預存程式的程式碼, 以使用**scikit-learn 學習**模型執行評分。

```sql
DROP PROCEDURE IF EXISTS PredictTipSingleModeSciKitPy;
GO

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
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
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

下列預存程式會使用**revoscalepy**模型執行評分。

```sql
DROP PROCEDURE IF EXISTS PredictTipSingleModeRxPy;
GO

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
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
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
probList = probArray["tipped_Pred"].values

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

建立預存程式之後, 就可以輕鬆地根據其中一個模型來產生分數。 只要開啟新的**查詢**視窗, 然後輸入或貼上每個特徵資料行的參數即可。 以下是這些功能資料行的七個必要值, 順序如下:
    
+ *passenger_count*
+ *trip_distance* v*trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. 若要使用**revoscalepy**模型產生預測, 請執行下列語句:
  
    ```sql
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

2. 若要使用**scikit-learn 學習**模型來產生分數, 請執行下列語句:

    ```sql
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'SciKit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

這兩個程式的輸出是使用指定的參數或功能來支付出租車行程的機率。

## <a name="conclusions"></a>結論

在本教學課程中, 您已瞭解如何使用內嵌在預存程式中的 Python 程式碼。 與[!INCLUDE[tsql](../../includes/tsql-md.md)]的整合可讓您更輕鬆地部署用於預測的 Python 模型, 並納入模型重新定型作為企業資料工作流程的一部分。

## <a name="previous-step"></a>上一個步驟

[定型和儲存 Python 模型](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="see-also"></a>另請參閱

[SQL Server 中的 Python 延伸模組](../concepts/extension-python.md)
