---
title: 使用 T-SQL PREDICT 進行原生評分
description: 使用 PREDICT T-SQL 函式產生預測，並根據 SQL Server 上以 R 或 Python 撰寫的預先定型模型來評分資料輸入。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 766adecbc91f88ed0796e4214b7e4074fc564f01
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727292"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>使用 PREDICT T-SQL 函式進行原生評分
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

原生評分會在 SQL Server 2017 中使用 [PREDICT T-SQL 函式](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)和 C++ 擴充功能，近乎即時地產生新資料輸入的預測值或「分數」  。 此方法可以為預測工作負載提供最快的可能處理速度，但附帶平台和程式庫需求：只有來自 RevoScaleR 和 revoscalepy 的函式具有 C++ 實作。

原生評分需要您具有已定型的模型。 在 SQL Server 2017 Windows 或 Linux 中，或是在 Azure SQL Database 中，您可以透過 Transact-SQL 呼叫 PREDICT 函式，以針對您提供為輸入參數的新資料叫用原生評分。 PREDICT 函式會傳回您所提供資料輸入的分數。

## <a name="how-native-scoring-works"></a>原生評分的運作方式

原生評分會使用 Microsoft 中的原生 C++ 程式庫，以讀取先前以特殊二進位格式儲存，或以原始位元組串流形式儲存至磁碟的已定型模型，並為您提供的新資料輸入產生分數。 由於模型已定型、發佈和儲存，所以可以在不需要呼叫 R 或 Python 解譯器的情況下用於評分。 因此可減少多個程序互動的額外負荷，讓企業生產案例中的預測效能更快速。

若要使用原生評分，請呼叫 PREDICT T-SQL 函數並傳遞下列必要的輸入：

+ 以所支援演算法為基礎的相容模型。
+ 輸入資料，通常會定義為 SQL 查詢。

函式會傳回輸入資料的預測，以及您想要傳遞的任何來源資料行。

## <a name="prerequisites"></a>Prerequisites

PREDICT 適用於所有版本的 SQL Server 2017 資料庫引擎，且預設為啟用，包括 Windows 上的 SQL Server 機器學習服務、SQL Server 2017 (Windows)、SQL Server 2017 (Linux) 或 Azure SQL Database。 您不需要安裝 R、Python 或啟用其他功能。

+ 必須預先使用下列其中一個支援的 **rx** 演算法來定型模型。

+ 使用適用於 R 的 [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) 及適用於 Python 的 [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) 來序列化模型。 這些序列化函式已經過最佳化，可支援快速評分。

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

如果您需要使用 MicrosoftML 或 microsoftml 中的模型，請使用[搭配 sp_rxPredict 的即時評分](real-time-scoring.md)。

不支援的模型類型包括下列類型：

+ 包含其他轉換的模型
+ 在 RevoScaleR 或 revoscalepy 對等項目中使用 `rxGlm` 或 `rxNaiveBayes` 演算法的模型
+ PMML 模型
+ 使用其他開放原始碼或第三方程式庫建立的模型

## <a name="example-predict-t-sql"></a>範例：PREDICT (T-SQL)

在此範例中，您會建立模型，然後從 T-SQL 呼叫即時預測函式。

### <a name="step-1-prepare-and-save-the-model"></a>步驟 1： 準備及儲存模型

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
> 請務必使用來自 RevoScaleR 的 [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) 函式來儲存模型。 標準 R `serialize` 函式無法產生所需的格式。

您可以執行如下所示的陳述式，檢視以二進位格式儲存的模型：

```sql
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>步驟 2： 在模型上執行 PREDICT

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

## <a name="next-steps"></a>後續步驟

如需包含原生評分的完整解決方案，請參閱 SQL Server 開發小組中的這些範例：

+ 部署您的 ML 指令碼：[使用 Python 模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ 部署您的 ML 指令碼：[使用 R 模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)