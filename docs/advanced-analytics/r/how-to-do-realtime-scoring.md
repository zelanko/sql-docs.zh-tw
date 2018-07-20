---
title: 如何執行即時評分，或在 SQL Server Machine Learning 中的原生評分 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 265a40d01be772b36ce7e49d06aeef8d3f5d81e5
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39085850"
---
# <a name="how-to-perform-realtime-scoring-or-native-scoring-in-sql-server"></a>如何執行即時計分或 SQL Server 中的原生評分
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文章提供如何執行即時評分和原生評分的功能，在 SQL Server 2016 和 SQL Server 2017 的指示和範例程式碼。 即時評分和原生評分的目標是要提升以小型批次評分作業的效能。

即時評分和原生評分被設計來讓您使用的機器學習模型，而不需要安裝。您只需要是取得相容的格式，預先定型的模型，並將它儲存在 SQL Server 資料庫。

## <a name="choosing-a-scoring-method"></a>選擇計分方法

下列選項可支援快速的批次預測：

+ **原生評分**: SQL Server 2017 中的 T-SQL 預測函式
+ **即時計分**： 使用 sp\_rxPredict 預存程序，在 SQL Server 2016 或 SQL Server 2017。

> [!NOTE]
> SQL Server 2017 中，建議使用 PREDICT 函式。
> 若要使用預存程序\_rxPredict，您必須啟用 SQLCLR 整合。 啟用此選項之前，請考慮安全性隱含意義。

準備模型，並將產生分數的整體程序如下：

1. 建立模型，使用支援的演算法。
2. 序列化使用特殊的二進位格式的模型。
3. 將模型提供給 SQL Server。 通常這表示已序列化的模型儲存在 SQL Server 資料表中。
4. 呼叫的函式或預存程序，並傳遞模型和輸入的資料。

### <a name="requirements"></a>需求

+ PREDICT 函式可用於所有版本的 SQL Server 2017，並依預設會啟用。 您不需要安裝 R，或啟用其他功能。

+ 如果使用預存程序\_rxPredict，一些額外的步驟所需。 請參閱[啟用即時評分](#bkmk_enableRtScoring)。

+ 在此階段中，只有 RevoScaleR 和 MicrosoftML 可以建立相容的模型。 其他的模型型別可能會在未來。 如需目前支援的演算法的清單，請參閱[即時評分](../real-time-scoring.md)。

### <a name="serialization-and-storage"></a>序列化與儲存體

若要使用其中一個快速的評分選項模型，將儲存模型使用特殊的序列化的格式，這已針對大小最佳化和評分的效率。

+ 呼叫`rxSerializeModel`寫入至支援的模型**原始**格式。
+ 呼叫`rxUnserializeModel`才能重新組成其他 R 程式碼中使用的模型，或檢視的模型。

如需詳細資訊，請參閱 < [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)。

**使用 SQL**

從 SQL 程式碼中，您可以訓練模型使用`sp_execute_external_script`，並直接插入至資料表，類型的資料行中的 定型的模型**varbinary （max)**。

如需簡單的範例，請參閱[本教學課程](../tutorials/rtsql-create-a-predictive-model-r.md)

**使用 R**

從 R 程式碼中，有兩種方式可將模型儲存至資料表：

+ 呼叫`rxWriteObject`函式，從 RevoScaleR 封裝，將模型直接寫入資料庫。

  `rxWriteObject()`函式可以擷取從 ODBC 資料來源，例如 SQL Server 的 R 物件或物件寫入 SQL Server。 API 被仿造的簡單索引鍵-值存放區。
  
  如果您使用此函式時，請務必將序列化的第一次使用新的序列化函式的模型。 然後，設定*序列化*中的引數`rxWriteObject`設為 FALSE，以避免重複序列化步驟。

+ 您可以也將模型儲存至檔案的原始格式，並從檔案中讀取 SQL server。 如果您要移動或複製環境之間的模型，此選項可能會很有用。

## <a name="native-scoring-with-predict"></a>原生評分與預測

在此範例中，您可以建立模型時，並接著從 T-SQL 呼叫即時預測函式。

### <a name="step-1-prepare-and-save-the-model"></a>步驟 1： 準備和儲存模型

執行下列的程式碼，以建立範例資料庫和必要的資料表。

```SQL
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

```SQL
INSERT INTO iris_rx_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width" , "Species")
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

現在，建立儲存模型的資料表。

```SQL
DROP TABLE IF EXISTS ml_models;
GO
CREATE TABLE ml_models ( model_name nvarchar(100) not null primary key
  , model_version nvarchar(100) not null
  , native_model_object varbinary(max) not null);
GO
```

下列程式碼會建立模型，根據**鳶尾花**資料集並將它儲存到名為資料表**模型**。

```SQL
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

```SQL
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>步驟 2： 在模型上執行預測

下列簡單的預測陳述式從決策樹模型使用取得分類**原生評分**函式。 它可預測的鳶尾花品種根據您提供的屬性、 花瓣長度和寬度。

```SQL
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

## <a name="realtime-scoring-with-sprxpredict"></a>即時評分 sp_rxPredict

本節說明設定所需的步驟**即時**預測，並提供如何從 T-SQL 呼叫函數的範例。

### <a name ="bkmk_enableRtScoring"></a> 步驟 1。 啟用即時計分程序

您必須啟用此功能的每個您想要用於評分的資料庫。 伺服器系統管理員應該執行的命令列公用程式，RegisterRExt.exe 隨附的 RevoScaleR 封裝。

> [!NOTE]
> 必須在執行個體中啟用 SQL CLR 功能讓即時計分工作，此外，資料庫必須標示為值得信任。 當您執行指令碼時，為您執行這些動作。 不過，這麼做之前考量的額外的安全性影響 ！

1. 開啟提升權限的命令提示字元，並瀏覽至 RegisterRExt.exe 所在的資料夾。 在預設安裝中可用的下列路徑：
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. 執行下列命令，並以您的執行個體和您要啟用擴充預存程序的目標資料庫的名稱取代：

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    比方說，若要將擴充預存程序加入 CLRPredict 資料庫的預設執行個體，請輸入：

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    執行個體名稱是選擇性，如果資料庫位於預設執行個體。 如果您使用具名執行個體，您必須指定執行個體名稱。

3. RegisterRExt.exe 建立下列物件：

    + 受信任的組件
    + 預存程序 `sp_rxPredict`
    + 新的資料庫角色， `rxpredict_users`。 資料庫管理員可以使用此角色，使用即時評分功能的使用者授與權限。

4. 新增需要執行任何使用者`sp_rxPredict`至新的角色。

> [!NOTE]
> 
> 在 SQL Server 2017 中，其他安全性量值會防止使用 CLR 整合的問題。 這些量值會使用這個預存程序以及其他限制。 

### <a name="step-2-prepare-and-save-the-model"></a>步驟 2： 準備和儲存模型

預存程序所需的二進位格式\_rxPredict 是使用 PREDICT 函式所需的格式相同。 因此，R 程式碼中包含呼叫[rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)，並務必指定`realtimeScoringOnly = TRUE`，如這個範例所示：

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sprxpredict"></a>步驟 3： 呼叫 sp_rxPredict

您呼叫 sp\_rxPredict 您對任何其他預存程序。 在目前的版本中，預存程序會採用只有兩個參數： _\@模型_模型，以二進位格式，和 _\@inputData_用於評分的資料定義為有效的 SQL 查詢。

因為二進位的格式相同，可由 PREDICT 函式，您可以使用前述範例中的模型和資料的資料表。

```SQL
DECLARE @irismodel varbinary(max)
SELECT @irismodel = [native_model_object] from [ml_models]
WHERE model_name = 'iris.dtree' 
AND model_version = 'v1''

EXEC sp_rxPredict
@model = @irismodel,
@inputData = N'SELECT * FROM iris_rx_data'
```

> [!NOTE]
> 
> 預存程序呼叫\_rxPredict 失敗時，如果評分的輸入的資料不包含資料行符合模型的需求。 目前支援只有下列.NET 資料類型： double、 float、 short、 ushort、 long、 ulong 和字串。
> 
> 因此，您可能需要篩選出不支援的類型，在您的輸入資料中，才能將它用於即時評分。
> 
> 如需對應的 SQL 類型的資訊，請參閱[SQL-CLR 類型對應](https://msdn.microsoft.com/library/bb386947.aspx)或是[對應 CLR 參數資料](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data)。

## <a name="disable-realtime-scoring"></a>停用即時評分

若要停用即時評分的功能，請開啟提升權限的命令提示字元，並執行下列命令： `RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="realtime-scoring-in-microsoft-r-server-or-machine-learning-server"></a>即時計分在 Microsoft R Server 或 Machine Learning Server

Machine Learning 伺服器支援分散式的即時計分模型發佈為 web 服務。 如需詳細資訊，請參閱下列文章：

+ [在 Machine Learning Server 中的 web 服務是什麼？](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [什麼是作業？](https://docs.microsoft.com/machine-learning-server/operationalize/concept-operationalize-deploy-consume)
+ [將 Python 模型部署為 web 服務使用 azureml 模型-管理 sdk](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [將 R 程式碼區塊或即時模型發佈為新的 web 服務](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [適用於 R 的 mrsdeploy 套件](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)
