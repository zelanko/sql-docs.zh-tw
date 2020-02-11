---
title: Python + T-SQL：執行預測
description: 示範如何使用 T-SQL 函數在 SQL Server 預存程序中讓內嵌 PYthon 指令碼的教學課程
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/02/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 00e4ba99b23abff0147627239093328e6f483ffb
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "74901868"
---
# <a name="run-predictions-using-python-embedded-in-a-stored-procedure"></a>在預存程序中使用 Python 內嵌執行預測
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文是[適用於 SQL 開發人員的資料庫內 Python 分析](sqldev-in-database-python-for-sql-developers.md)教學課程的一部分。 

在此步驟中，您將瞭解如何*運作*您在上一個步驟中定型並儲存的模型。

在此案例中，運作化表示將模型部署至生產環境以進行評分。 與 SQL Server 的整合讓這項操作變得相當簡單，因為您可以在預存程序中內嵌 Python 程式碼。 若要根據新的輸入從模型取得預測，請直接從應用程式呼叫預存程序，並傳遞新的資料。

這個課程將示範兩種建立以 Python 模型為基礎之預測的方法：批次評分，以及依資料列評分資料列。

- **批次評分：** 若要提供輸入資料的多個資料列，請將 SELECT 查詢做為引數傳遞給預存程序。 結果是對應至輸入案例的觀察值資料表。
- **個別評分：** 傳遞一組個別參數值作為輸入。  此預存程序會傳回單一資料列或值。

評分所需的所有 Python 程式碼都是在預存程序中提供。

## <a name="batch-scoring"></a>批次評分

前兩個預存程序說明將預測呼叫包裝在 Python 預存程序中的基本語法。 這兩個預存程序都需要資料表做為輸入。

- 要使用的確切模型名稱會做為預存程序的輸入參數來提供。 預存程序會使用預存程序中的 SELECT 陳述式，從資料庫資料表中載入序列化模型`nyc_taxi_models`資料表。
- 序列化模型會儲存在 Python 變數 `mod` 中，以使用 Python 進行進一步處理。
- 需要評分的新案例是從 `@input_data_1` 中指定的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢取得。 讀取查詢資料之後，這些資料列會儲存在預設資料框架 `InputDataSet`中。
- 這兩個預存程序都會使用 `sklearn` 的函數來計算精確度計量 AUC (曲線下的區域)。 只有當您也提供目標標籤 (_獲得小費_資料行) 時，才可以產生精確度計量 (例如 AUC)。 預測不需要目標標籤 (變數 `y`)，但精確度計量計算會需要。

    因此，如果要計分的資料沒有目標標籤，您可以修改預存程序來移除 AUC 計算，並且只傳回功能的小費機率 (預存程序中的變數 `X`)。

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

執行下列 T-SQL 陳述式來建立預存程序。 這個預存程序需要以 scikit-learn 為基礎的模型，因為它使用該封裝的特定函數：

+ 包含輸入的資料框架會傳遞至羅吉斯回歸模型 `mod` 的 `predict_proba` 函數。 `predict_proba` 函數 (`probArray = mod.predict_proba(X)`) 傳回**浮點數**，代表給小費 (任何金額) 的機率。

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

這個預存程序會使用相同的輸入，並建立與先前預存程序相同的分數類型，但會使用 SQL Server 機器學習服務提供的 **revoscalepy** 套件中的函數。

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

預存程序 **PredictTipSciKitPy** 和 **PredictTipRxPy** 需要兩個輸入參數： 

- 擷取評分的資料所用的查詢
- 定型模型的名稱

藉由將這些引數傳遞給預存程序，您可以選取特定的模型，也可以變更用於評分的資料。

1. 若要使用 **scikit-learn** 模型進行評分，請呼叫預存程序 **PredictTipSciKitPy**，傳遞模型名稱和查詢字串做為輸入。

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    預存程序會針對傳入做為輸入查詢中的每趟車程，傳回預測的機率。 
    
    如果您使用 SSMS (SQL Server Management Studio) 執行查詢，則機率會顯示為 [結果]  窗格中的資料表。 [訊息]  窗格會輸出精確度計量 (AUC (曲線下的區域))，其值為 0.56。

2. 若要使用 **revoscalepy** 模型進行評分，請呼叫預存程序 **PredictTipRxPy**，傳遞模型名稱和查詢字串做為輸入。

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="single-row-scoring"></a>單一資料列評分

有時候，您可能會想要傳入單一案例，並從應用程式取得值，然後根據這些值傳回單一結果，而不是批次評分。 例如，您可以設定 Excel 工作表、Web 應用程式或報表來呼叫預存程序，並傳遞使用者鍵入或選取的輸入。

在本節中，您將瞭解如何叫用兩個預存程序來建立單一預測：

+ [PredictTipSingleModeSciKitPy](#predicttipsinglemodescikitpy) 是針對使用 scikit-learn 模型的單一資料列評分所設計。
+ [PredictTipSingleModeRxPy](#predicttipsinglemoderxpy) 是針對使用 revoscalepy 模型的單一資料列評分所設計。
+ 如果您尚未定型模型，請返回[步驟 5](sqldev-py5-train-and-save-a-model-using-t-sql.md)！

這兩種模型都接受一系列的單一值，例如乘客計數、路程距離等等。 資料表值函數 `fnEngineerFeatures` 是用來將緯度和經度值從輸入轉換成新功能的直接距離。 [第 4 課](sqldev-py4-create-data-features-using-t-sql.md)包含此資料表值函數的描述。

這兩個預存程序都會根據 Python 模型建立分數。

> [!NOTE]
> 
> 您從外部應用程式呼叫預存程序時，請務必提供 Python 模型所需的所有輸入功能。 若要避免發生錯誤，除了驗證資料類型和資料長度以外，您可能還需要將輸入資料轉型或轉換成 Python 資料類型。

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

請花幾分鐘的時間，使用 **scikit-learn** 模型來審查執行計分的預存程序程式碼。

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

下列預存程序會使用 **revoscalepy** 模型來執行評分。

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

建立預存程序之後，就可以輕鬆地根據其中一個模型來產生分數。 直接開啟新的 [查詢]  視窗，並針對每個特徵資料行輸入或貼上參數。 以下為這些特徵資料行所需的七個值，依序為：
    
+ *passenger_count*
+ *trip_distance* v*trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. 若要使用 **revoscalepy** 模型來產生預測，請執行下列陳述式：
  
    ```sql
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

2. 若要使用 **scikit-learn** 模型來產生分數，請執行下列陳述式：

    ```sql
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'SciKit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

這兩個程式的輸出是使用指定的參數或特徵，來計算計程車車程獲得小費的機率。

## <a name="conclusions"></a>結論

在本教學課程中，您已瞭解如何使用內嵌在預存程序中的 Python 程式碼。 與 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的整合可讓您更輕鬆地部署 Python 模型進行預測，並納入模型重新定型作為企業資料工作流程的一部分。

## <a name="previous-step"></a>上一個步驟

[定型及儲存 Python 模型](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="see-also"></a>另請參閱

[SQL Server 中的 Python 延伸模組](../concepts/extension-python.md)
