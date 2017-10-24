---
title: "如何執行即時計分或 SQL Server 中的原生計分 |Microsoft 文件"
ms.custom: 
ms.date: 10/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 175a9bc664a2032d828ca790312920339f971b9b
ms.contentlocale: zh-tw
ms.lasthandoff: 10/17/2017

---
# <a name="how-to-perform-realtime-scoring-or-native-scoring-in-sql-server"></a>如何執行即時計分或 SQL Server 中的原生計分

本主題提供如何執行即時計分和 SQL Server 2017 和 SQL Server 2016 中的原生計分功能的指示和範例程式碼。 同時即時計分和原生計分的目標是要提升以小型批次計分作業的效能。

同時即時計分和原生計分設計為可讓您使用的機器學習模型，而不需要安裝。您只需要為取得預先定型的模型，以相容的格式，並將它儲存在 SQL Server 資料庫。

## <a name="choosing-a-scoring-method"></a>選擇計分方法

下列選項可支援快速的批次預測：

+ **原生計分**: SQL Server 2017 T-SQL 預測函式
+ **即時計分**： 使用 sp\_rxPredict 中 SQL Server 2016 或 SQL Server 2017 預存程序。

> [!NOTE]
> 在 SQL Server 2017，建議使用預測函數。
> 若要使用預存程序\_rxPredict 需要啟用 SQLCLR 整合。 啟用此選項之前，請考慮的安全性含意。

正在準備模型，並接著分數的整體程序是非常類似：

1. 建立使用支援的演算法的模型。
2. 序列化使用特殊的二進位格式的模型。
3. 將模型提供給 SQL Server。 通常這表示 SQL Server 資料表中儲存的已序列化的模型。
4. 呼叫函式或預存程序，並傳遞模型和輸入的資料。

### <a name="requirements"></a>需求

+ PREDICT 函數使用的 SQL Server 2017 所有版本中，預設會啟用。 您不需要安裝 R，或啟用其他功能。

+ 如果使用預存程序\_rxPredict，一些額外的步驟所需。 請參閱[啟用即時計分](#bkmk_enableRtScoring)。

+ 此時，只有 RevoScaleR 和 MicrosoftML 可以建立相容的模型。 其他的模型型別可能會在未來。 如需目前支援的演算法的清單，請參閱[即時計分](../real-time-scoring.md)。

### <a name="serialization-and-storage"></a>序列化和儲存體

若要使用快速計分選項的其中一個模型，必須先儲存模型特殊的序列化格式，這已經過最佳化的大小和計分的效率。

+ 呼叫`rxSerializeModel`撰寫模型來支援**原始**格式。
+ 呼叫`rxUnserializeModel`deserialization 其他 R 程式碼中使用的模型或檢視模式。

如需詳細資訊，請參閱[rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)。

**使用 SQL**

從 SQL 程式碼，您可以訓練模型使用`sp_execute_external_script`，然後直接插入在資料表類型的資料行中的定型的模型**varbinary （max)**。

如需簡單的範例，請參閱[本教學課程](../tutorials/rtsql-create-a-predictive-model-r.md)

**使用 R**

從 R 程式碼中，有兩種方式可將模型儲存至資料表：

+ 呼叫`rxWriteObject`函式，從 RevoScaleR 封裝，將模型直接寫入資料庫。

  `rxWriteObject()`函式可以擷取像是 SQL Server ODBC 資料來源中的 R 物件或物件寫入 SQL Server。 API 非常簡單的索引鍵-值存放區的模式。
  
  如果您使用此函式，請務必將第一次使用新的序列化函式的模型序列化。 然後，設定*序列化*加上旗標`rxWriteObject`設為 FALSE，以避免重複序列化步驟。

+ 您可以也將模型儲存至檔案的原始格式，然後從檔案讀取至 SQL Server。 如果您要移動或複製環境之間的模型，此選項可能會很有用。

## <a name="native-scoring-with-predict"></a>原生與預測計分

在此範例中，建立模型，然後呼叫 T-SQL 即時預測函數。

### <a name="step-1-prepare-and-save-the-model"></a>步驟 1： 準備並儲存模型

執行下列程式碼來建立範例資料庫和必要的資料表。

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

使用下列陳述式來擴展資料表的資料**光圈**資料集。

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

下列程式碼會建立模型，根據**光圈**資料集，並將它儲存至模型資料表。

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
> 您必須使用[rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)從儲存模型的 RevoScaleR 函式。 標準 R`serialize`函式無法產生所需的格式。

您可以執行下列命令來檢視預存的模型，以二進位格式等陳述式：

```SQL
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>步驟 2： 在模型上執行預測

下列簡單的預測陳述式取得從決策樹模型使用分類**原生計分**函式。 根據您提供的屬性、 瓣花瓣長度及寬度光圈物種預測。

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

如果您收到錯誤，「 執行期間發生錯誤預測的函式。 模型已損毀或無效 」，通常表示您的查詢未傳回的模型。 請檢查是否輸入模型名稱正確，或如果是空的模型資料表。

> [!NOTE]
> 因為所傳回的資料行和值**預測**因模型類型而有所不同，您必須定義傳回資料的結構描述使用**WITH**子句。

## <a name="realtime-scoring-with-sprxpredict"></a>即時 sp_rxPredict 與計分

本章節描述設定所需的步驟**即時**預測，並提供如何從 T-SQL 呼叫函式的範例。

### <a name ="bkmk_enableRtScoring"></a>步驟 1。 啟用即時計分程序

您必須啟用每個資料庫，您想要用於計分這項的功能。 伺服器系統管理員應該執行的命令列公用程式，RegisterRExt.exe 隨附 RevoScaleR 封裝。

> [!NOTE]
> 為了讓即時計分工作，SQL CLR 功能，才能啟用執行個體中，資料庫必須標示為值得信任。 當您執行指令碼時，讓您執行這些動作。 不過，您應該考慮的額外的安全性含意。

1. 開啟提升權限的命令提示字元並瀏覽至 RegisterRExt.exe 所在的資料夾。 在預設安裝中可用的下列路徑：
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. 執行下列命令，並以您的執行個體和您要啟用擴充預存程序的目標資料庫的名稱取代：

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    比方說，若要將擴充預存程序加入 CLRPredict 資料庫的預設執行個體，請輸入：

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    執行個體名稱是選擇性，如果資料庫位於預設執行個體。 如果您使用具名執行個體，您必須指定執行個體名稱。

3. RegisterRExt.exe 會建立下列物件：

    + 信任的組件
    + 預存程序`sp_rxPredict`
    + 新的資料庫角色， `rxpredict_users`。 資料庫管理員可以使用此角色，授與使用即時計分功能的使用者權限。

4. 加入的任何使用者需要執行`sp_rxPredict`至新的角色。

> [!NOTE]
> 
> 在 SQL Server 2017，其他安全性量值都位於來防止 CLR 整合的問題。 這些量值會使用這個預存程序以及其他限制。

### <a name="step-2-prepare-and-save-the-model"></a>步驟 2： 準備並儲存模型

預存程序所需的二進位格式\_rxPredict 是相同的預測。 因此，在 R 程式碼中包含對[rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)，而且一定要指定_realtimeScoringOnly_ = TRUE，如此範例所示：

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sprxpredict"></a>步驟 3： 呼叫 sp_rxPredict

您呼叫 sp\_rxPredict，就像其他任何預存程序。 在目前版本中，預存程序會採用只有兩個參數：  _@model_ 的二進位格式，模型和 _@inputData_ 用於計分的資料定義為有效的 SQL 查詢.

二進位格式中都相同，以供預測函式，因為您可以使用前面範例中模型和資料的資料表。

```SQL
DECLARE @irismodel varbinary(max)
SELECT @irismodel = [native_model_object] from [ml_models]
WHERE model_name = 'iris.dtree.model' AND model_version = 'v1''

EXEC sp_rxPredict
@model = @irismodel,
@inputData = N'SELECT * FROM iris_rx_data'
```

> [!NOTE]
> 
> 預存程序呼叫\_rxPredict 失敗時，如果計分的輸入的資料不包含符合的需求之模型的資料行。 目前支援只能使用下列的.NET 資料類型： 雙精確度、 float、 short、 ushort、 long、 ulong 和字串。
> 
> 因此，您可能需要篩選出您的輸入資料中不支援的型別，才能將它用於即時計分。
> 
> 如需對應的 SQL 型別資訊，請參閱[SQL CLR 類型對應](https://msdn.microsoft.com/library/bb386947.aspx)或[對應 CLR 參數資料](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data)。

## <a name="disable-realtime-scoring"></a>停用即時計分

若要停用即時計分功能，請開啟提升權限的命令提示字元並執行下列命令：`RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="realtime-scoring-in-microsoft-r-server-or-machine-learning-server"></a>即時 Microsoft R Server 或 Server 機器學習的計分方法

機器學習 Server 支援分散式的即時計分模型發佈為 web 服務。 如需詳細資訊，請參閱下列文章：

+ [機器學習伺服器中的 web 服務有哪些？](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [實施是什麼？](https://docs.microsoft.com/machine-learning-server/operationalize/concept-operationalize-deploy-consume)
+ [Python 模型部署為 web 服務與 azureml 模型-管理 sdk](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [將 R 程式碼區塊或即時模型發行為新的 web 服務](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [R 的 mrsdeploy 封裝](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)

