---
title: 使用預測 T-SQL 陳述式-SQL Server Machine Learning 服務的原生評分
description: 產生使用預測 T-SQL 函式，評分 dta 的輸入，針對 SQL Server 上以 R 或 Python 撰寫的預先定型模型的預測。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a14a4b188aa27acdef0bc836e939a7df0021e522
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645127"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>使用預測 T-SQL 函式的原生評分
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

原生評分會使用[預測 T-SQL 函式](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)和 原生 c + + 延伸模組功能在 SQL Server 2017 中的產生預測值或*分數*中近乎即時的新資料輸入。 這種方法提供預測和預測的工作負載，可能的處理速度最快，但隨附平台和程式庫的需求： 只有來自 RevoScaleR 與 revoscalepy 函式具有 c + + 實作。

原生評分，您需要已定型的模型。 在 SQL Server 2017 Windows 或 Linux，或 Azure SQL Database 中，您可以呼叫 PREDICT 函數中 TRANSACT-SQL 來叫用原生對您提供做為輸入參數的新資料評分。 PREDICT 函式會傳回分數，透過您提供的資料輸入。

## <a name="how-native-scoring-works"></a>原生評分的運作方式

原生評分使用原生 c + + 程式庫可以讀取已定型的模型，microsoft 先前儲存在特殊的二進位格式或儲存至磁碟以原始位元組資料流，並產生新的資料輸入您所提供的分數。 已定型的模型，因為已發行，並儲存，它可以用於評分不必呼叫 R 或 Python 解譯器。 因此，多個處理程序互動的額外負荷已降低，導致更快的預測效能，在生產環境的企業案例。

若要使用原生評分，呼叫預測 T-SQL 函數並傳遞下列必要的輸入：

+ 相容的模型，用來根據支援的演算法。
+ 輸入的資料，通常會定義為 SQL 查詢。

此函數會傳回輸入資料，以及您想要通過的來源資料的任何資料行的預測。

## <a name="prerequisites"></a>先決條件

預測所有版本的 SQL Server 2017 資料庫引擎上可用並已啟用，根據預設，包括 SQL Server 2017 Machine Learning 服務在 Windows、 SQL Server 2017 (Windows)、 SQL Server 2017 (Linux) 或 Azure SQL Database。 您不需要安裝 R、 Python、 或啟用其他功能。

+ 必須事先使用其中一個支援訓練模型**rx**下面所列的演算法。

+ 模型使用序列化[rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)針對 R，以及[rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)適用於 Python。 這些序列化函式已經過最佳化，支援快速評分。

<a name="bkmk_native_supported_algos"></a> 

## <a name="supported-algorithms"></a>支援的演算法

+ revoscalepy 模型

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) 
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) 
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) 
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) 

+ RevoScaleR 模型

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

如果您需要使用從 MicrosoftML 或 microsoftml 的模型，使用[即時評分 sp_rxPredict](real-time-scoring.md)。

不支援的模型類型包括下列類型：

+ 模型包含其他轉換
+ 模型使用`rxGlm`或`rxNaiveBayes`RevoScaleR 或 revoscalepy 對等項目中的演算法
+ PMML 模型
+ 使用其他開放原始碼或協力廠商程式庫所建立的模型

## <a name="example-predict-t-sql"></a>範例預測 (T-SQL)

在此範例中，您可以建立模型時，並接著從 T-SQL 呼叫即時的預測函數。

### <a name="step-1-prepare-and-save-the-model"></a>步驟 1： 準備和儲存模型

執行下列的程式碼，以建立範例資料庫和必要的資料表。

```sql
CREATE DATABASE NativeScoringTest;
GO
USE NativeScoringTest;
GO
DROP TABLE IF EXISTS iris_rx_data;
GO
CREATE TABLE iris_rx_data (
  "Sepal.Length" float not null, "Sepal.Width" float not null
  , "Petal.Length" float not null, "Petal.Width" float not null
  , "Species" varchar(100) null
);
GO
```

使用下列陳述式來填入資料的資料表**鳶尾花**資料集。

```sql
INSERT INTO iris_rx_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width" , "Species")
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

現在，建立儲存模型的資料表。

```sql
DROP TABLE IF EXISTS ml_models;
GO
CREATE TABLE ml_models ( model_name nvarchar(100) not null primary key
  , model_version nvarchar(100) not null
  , native_model_object varbinary(max) not null);
GO
```

下列程式碼會建立模型，根據**鳶尾花**資料集並將它儲存到名為資料表**模型**。

```sql
DECLARE @model varbinary(max);
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'
    iris.sub <- c(sample(1:50, 25), sample(51:100, 25), sample(101:150, 25))
    iris.dtree <- rxDTree(Species ~ Sepal.Length + Sepal.Width + Petal.Length + Petal.Width, data = iris[iris.sub, ])
    model <- rxSerializeModel(iris.dtree, realtimeScoringOnly = TRUE)
    '
  , @params = N'@model varbinary(max) OUTPUT'
  , @model = @model OUTPUT
  INSERT [dbo].[ml_models]([model_name], [model_version], [native_model_object])
  VALUES('iris.dtree','v1', @model) ;
```

> [!NOTE] 
> 請務必使用[rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)從儲存模型的 RevoScaleR 函式。 標準 R`serialize`函式無法產生所需的格式。

您可以執行下列命令來檢視預存的模型，以二進位格式等陳述式：

```sql
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>步驟 2： 在模型上執行預測

下列簡單的預測陳述式從決策樹模型使用取得分類**原生評分**函式。 它可預測的鳶尾花品種根據您提供的屬性、 花瓣長度和寬度。

```sql
DECLARE @model varbinary(max) = (
  SELECT native_model_object
  FROM ml_models
  WHERE model_name = 'iris.dtree'
  AND model_version = 'v1');
SELECT d.*, p.*
  FROM PREDICT(MODEL = @model, DATA = dbo.iris_rx_data as d)
  WITH(setosa_Pred float, versicolor_Pred float, virginica_Pred float) as p;
go
```

如果您收到錯誤，「 執行期間發生錯誤的函式 PREDICT。 模型已損毀或無效 」，通常表示您的查詢未傳回模型。 請檢查是否輸入模型名稱正確，或如果是空的模型資料表。

> [!NOTE]
> 因為所傳回的資料行和值**PREDICT**可能會因模型類型，您必須使用來定義傳回資料的結構描述**WITH**子句。

## <a name="next-steps"></a>後續步驟

完整的解決方案，其中包含原生評分，請參閱 SQL Server 開發小組的這些範例：

+ 部署您的 ML 指令碼：[使用 Python 模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ 部署您的 ML 指令碼：[使用 R 模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)