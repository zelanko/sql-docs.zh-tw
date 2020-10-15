---
title: 原生評分與 T-SQL PREDICT
titleSuffix: SQL machine learning
description: 了解如何使用原生評分搭配 PREDICT T-SQL 函式，以近乎即時方式產生新資料輸入的預測值。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/29/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=azuresqldb-mi-current||=azure-sqldw-latest||=sqlallproducts-allversions'
ms.openlocfilehash: 9d8f65baaec3038431455712d64803459a96e45c
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956956"
---
# <a name="native-scoring-using-the-predict-t-sql-function-with-sql-machine-learning"></a>使用 PREDICT T-SQL 函式與 SQL 機器學習進行原生評分

[!INCLUDE [sqlserver2017-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2017-asdb-asdbmi-asa.md)]

了解如何使用原生評分搭配 [PREDICT T-SQL 函式](../../t-sql/queries/predict-transact-sql.md)，以近乎即時方式產生新資料輸入的預測值。 原生評分需要有已定型的模型。

`PREDICT` 函式會使用 [SQL 機器學習](../index.yml)中的原生 C++ 延伸模組功能。 此方法提供最快的預測和預測工作負載處理速度，並支援使用 [Open Neural Network Exchange (ONNX)](https://onnx.ai/get-started.html) 格式的模型，或使用 [RevoScaleR](../r/ref-r-revoscaler.md) 和 [revoscalepy](../python/ref-py-revoscalepy.md) 套件定型的模型。

## <a name="how-native-scoring-works"></a>原生評分的運作方式

原生評分會使用可讀取 ONNX 或預先定義二進位格式模型的程式庫，並針對您所提供的新資料輸入產生分數。 因為模型已定型、部署和儲存，所以可用於評分，而不必呼叫 R 或 Python 解譯器。 這表示可減少多個程序互動的額外負荷，因而獲得更快的預測效能。

若要使用原生評分，請呼叫 `PREDICT` T-SQL 函式並傳遞下列必要的輸入：

+ 以所支援模型和演算法為基礎的合規模型。
+ 輸入資料，通常會定義為 T-SQL 查詢。

函式會傳回輸入資料的預測，以及您想要傳遞的任何來源資料行。

## <a name="prerequisites"></a>Prerequisites

`PREDICT` 適用於：

+ Windows 和 Linux 的 SQL Server 2017 所有版本及更新版本
+ Azure SQL 受控執行個體
+ Azure SQL Database
+ Azure SQL Edge
+ Azure Synapse Analytics

根據預設，會啟用函式。 您不需要安裝 R 或 Python，或啟用其他功能。

## <a name="supported-models"></a>支援的模型

`PREDICT` 函式所支援模型格式取決於您執行原生評分的 SQL 平台。 請參閱下表，以了解哪些平台支援哪些模型格式。

| 平台 | ONNX 模型格式 | RevoScale 模型格式 |
|-|-|-|
| SQL Server | 否 | 是 |
| Azure SQL 受控執行個體 | 是 | 是 |
| Azure SQL Database | 否 | 是 |
| Azure SQL Edge | 是 | 否 |
| Azure Synapse Analytics | 是 | 否 |

::: moniker range="=azuresqldb-mi-current||=azure-sqldw-latest||=sqlallproducts-allversions"
### <a name="onnx-models"></a>ONNX 模型

模型必須是 [Open Neural Network Exchange (ONNX)](https://onnx.ai/get-started.html) 模型格式。
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current||=azuresqldb-current||=sqlallproducts-allversions"
### <a name="revoscale-models"></a>RevoScale 模型

您必須先使用 [RevoScaleR](../r/ref-r-revoscaler.md) 或 [revoscalepy](../python/ref-py-revoscalepy.md) 套件，以下列其中一種支援的 **rx** 演算法來定型模型。

使用適用於 R 的 [rxSerialize](/machine-learning-server/r-reference/revoscaler/rxserializemodel) 及適用於 Python 的 [rx_serialize_model](/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) 來序列化模型。 這些序列化函式已經過最佳化，可支援快速評分。

<a name="bkmk_native_supported_algos"></a> 

#### <a name="supported-revoscale-algorithms"></a>支援的 RevoScale 演算法

revoscalepy 和 RevoScaleR 支援下列演算法。

+ revoscalepy 演算法

  + [rx_lin_mod](/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](/machine-learning-server/python-reference/revoscalepy/rx-logit) 
  + [rx_btrees](/machine-learning-server/python-reference/revoscalepy/rx-btrees) 
  + [rx_dtree](/machine-learning-server/python-reference/revoscalepy/rx-dtree) 
  + [rx_dforest](/machine-learning-server/python-reference/revoscalepy/rx-dforest) 

+ RevoScaleR 演算法

  + [rxLinMod](/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](/r-server/r-reference/revoscaler/rxdforest)

如果必須使用 MicrosoftML 或 microsoftml 中的演算法，請使用[即時評分搭配 sp_rxPredict](../predictions/real-time-scoring.md)。

不支援的模型類型包括下列類型：

+ 包含其他轉換的模型
+ 在 RevoScaleR 或 revoscalepy 對等項目中使用 `rxGlm` 或 `rxNaiveBayes` 演算法的模型
+ PMML 模型
+ 使用其他開放原始碼或第三方程式庫建立的模型
::: moniker-end

## <a name="examples"></a>範例
::: moniker range="=azuresqldb-mi-current||=azure-sqldw-latest||=sqlallproducts-allversions"
### <a name="predict-with-an-onnx-model"></a>PREDICT 與 ONNX 模型

這個範例示範如何使用 `dbo.models` 資料表中儲存的 ONNX 模型進行原生評分。

```sql
DECLARE @model VARBINARY(max) = (
        SELECT DATA
        FROM dbo.models
        WHERE id = 1
        );

WITH predict_input
AS (
    SELECT TOP (1000) [id]
        , CRIM
        , ZN
        , INDUS
        , CHAS
        , NOX
        , RM
        , AGE
        , DIS
        , RAD
        , TAX
        , PTRATIO
        , B
        , LSTAT
    FROM [dbo].[features]
    )
SELECT predict_input.id
    , p.variable1 AS MEDV
FROM PREDICT(MODEL = @model, DATA = predict_input, RUNTIME=ONNX) WITH (variable1 FLOAT) AS p;
```

> [!NOTE]
> 由於 **PREDICT** 所傳回的資料行和值可能會因為模型類型而有差異，所以您必須使用 **WITH** 子句來定義傳回資料的結構描述。
::: moniker-end

::: moniker range=">=sql-server-2017||=azuresqldb-mi-current||>=sql-server-linux-2017||=sqlallproducts-allversions"
### <a name="predict-with-revoscale-model"></a>PREDICT 與 RevoScale 模型

在此範例中，您會在 R 中使用 **RevoScaleR** 建立模型，然後從 T-SQL 呼叫即時預測函式。

#### <a name="step-1-prepare-and-save-the-model"></a>步驟 1： 準備及儲存模型

執行下列程式碼，以建立範例資料庫和必要的資料表。

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

使用下列陳述式，在資料表中填入 **iris** 資料集的資料。

```sql
INSERT INTO iris_rx_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width" , "Species")
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

現在，請建立用以儲存模型的資料表。

```sql
DROP TABLE IF EXISTS ml_models;
GO
CREATE TABLE ml_models ( model_name nvarchar(100) not null primary key
  , model_version nvarchar(100) not null
  , native_model_object varbinary(max) not null);
GO
```

下列程式碼會根據 **iris** 資料集建立模型，並將其儲存至名為 **models** 的資料表。

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
> 請務必使用來自 RevoScaleR 的 [rxSerializeModel](/machine-learning-server/r-reference/revoscaler/rxserializemodel) 函式來儲存模型。 標準 R `serialize` 函式無法產生所需的格式。

您可以執行如下所示的陳述式，檢視以二進位格式儲存的模型：

```sql
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

#### <a name="step-2-run-predict-on-the-model"></a>步驟 2： 在模型上執行 PREDICT

下列簡單的 PREDICT 陳述式會使用**原生評分**函式，從決策樹模型取得分類。 該函式會根據您提供的屬性、花瓣長度和寬度來預測 iris (鳶尾花) 的品種。

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

如果您收到錯誤：「執行 'PREDICT' 函式時發生錯誤。 模型已損毀或無效」，通常表示您的查詢未傳回模型。 請檢查您輸入的模型名稱是否正確，或模型資料表是否為空白。

> [!NOTE]
> 由於 **PREDICT** 所傳回的資料行和值可能會因為模型類型而有差異，所以您必須使用 **WITH** 子句來定義傳回資料的結構描述。
::: moniker-end

## <a name="next-steps"></a>後續步驟

+ [PREDICT T-SQL 函式](../../t-sql/queries/predict-transact-sql.md)
+ [SQL 機器學習文件](../index.yml)
+ [SQL Edge 中採用 ONNX 格式的機器學習和 AI](/azure/azure-sql-edge/onnx-overview)
+ [在 Azure SQL Edge 中使用 ONNX 模型部署及預測](/azure/azure-sql-edge/deploy-onnx)