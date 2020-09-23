---
title: 使用 sp_rxPredict 進行即時評分
description: 了解如何使用 SQL Server 中的 sp_rxPredict 系統預存程序執行即時評分，在預測工作負載中取得高效能的預測或分數。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/31/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 89e7a3e15f389de8fc696247197c9f678955ed73
ms.sourcegitcommit: 5f658b286f56001b055a8898d97e74906516dc99
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009344"
---
# <a name="real-time-scoring-with-sp_rxpredict-in-sql-server"></a>使用 SQL Server 中的 sp_rxPredict 進行即時評分
[!INCLUDE[sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

了解如何使用 SQL Server 中的 [sp_rxPredict](../../relational-databases/system-stored-procedures/sp-rxpredict-transact-sql.md) 系統預存程序執行即時評分，在預測工作負載中取得高效能的預測或分數。

使用 `sp_rxPredict` 的即時評分與語言無關，且執行時無須依賴[機器學習服務](../sql-server-machine-learning-services.md)或 [R Services](../r/sql-server-r-services.md) 中的 R 或 Python 執行階段。 假設模型是使用 Microsoft 函式來建立並定型，然後在 SQL Server 中序列化為二進位格式，您可以在未安裝 R 或 Python 附加元件的 SQL Server 執行個體上，使用即時評分來針對新的資料輸入產生預測輸出。

## <a name="how-real-time-scoring-works"></a>即時評分的運作方式

目前支援根據 [RevoScaleR](../r/ref-r-revoscaler.md) 或 [MicrosoftML](../r/ref-r-microsoftml.md) 中的函式 (R) 或是 [revoscalepy](../python/ref-py-revoscalepy.md) 或 [microsoftml](../python/ref-py-microsoftml.md) 中的函式 (Python)，對特定模型類型進行即時評分。 其根據提供給機器學習模型 (採用特殊二進位格式) 的使用者輸入，使用原生 C++ 程式庫來產生分數。

由於定型的模型可以用於評分，而且不需要呼叫[機器學習服務](../sql-server-machine-learning-services.md)或 [R Services](../r/sql-server-r-services.md) 中的外部語言執行階段，因此可減少使用多個程序的額外負荷。 

即時評分是一個多步驟的程序：

1. 執行評分的預存程序必須在每個資料庫上啟用。
2. 您會以二進位格式載入預先定型的模型。
3. 您會提供用於評分的新輸入資料 (表格式或單一資料列) 作為模型的輸入。
4. 若要產生分數，請呼叫 [sp_rxPredict](../../relational-databases/system-stored-procedures/sp-rxpredict-transact-sql.md) 預存程序。

## <a name="prerequisites"></a>Prerequisites

+ [啟用 SQL Server CLR 整合](../../relational-databases/clr-integration/clr-integration-enabling.md)

+ [啟用即時評分](#bkmk_enableRtScoring)。

+ 必須預先使用其中一個支援的 **rx** 演算法來定型模型。 針對 R，使用 `sp_rxPredict` 的即時評分會與 [RevoScaleR 和 MicrosoftML 支援的演算法](#bkmk_rt_supported_algos)搭配運作。 針對 Python，請參閱 [revoscalepy 和 microsoftml 支援的演算法](#bkmk_py_supported_algos)。

+ 使用適用於 R 的 [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) 及適用於 Python 的 [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) 來序列化模型。 這些序列化函式已經過最佳化，可支援快速評分。

+ 將模型儲存到您想要從中進行呼叫的資料庫引擎執行個體。 此執行個體不需要有 R 或 Python 執行階段延伸模組。

> [!Note]
> 即時評分目前已針對較小資料集進行快速預測的最佳化，從幾個資料列到數十萬個資料列皆涵蓋在範圍內。 在大型資料集上，使用 [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) 可能會更快。

<a name ="bkmk_enableRtScoring"></a> 

## <a name="enable-real-time-scoring"></a>啟用即時評分

您必須針對要用於評分的每個資料庫啟用這項功能。 伺服器管理員應該執行包含在 RevoScaleR 套件中的命令列公用程式 Registerrext.exe。

> [!NOTE]
> 為了讓即時評分能夠運作，執行個體中必須啟用 SQL CLR 功能；此外，資料庫必須標示為值得信任。 當您執行指令碼時，系統會為您執行這些動作。 不過，在這麼做之前，請先考慮額外的安全性影響！

1. 開啟提升權限的命令提示字元，並瀏覽至 RegisterRExt.exe 所在的資料夾。 下列路徑可以在預設安裝中使用：

    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. 執行下列命令，並以您的執行個體名稱和您要啟用擴充預存程序的目標資料庫進行替代：

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    例如，若要將擴充預存程序新增至預設執行個體上的 CLRPredict 資料庫，請輸入：

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    如果資料庫位於預設執行個體上，則執行個體名稱為選擇性。 如果您使用的是具名執行個體，則必須指定執行個體名稱。

3. RegisterRExt.exe 會建立下列物件：

    + 信任的組件
    + 預存程序 `sp_rxPredict`
    + 新的資料庫角色：`rxpredict_users`。 資料庫管理員可以使用此角色，將權限授與使用即時評分功能的使用者。

4. 將需要執行 `sp_rxPredict` 的任何使用者新增至新角色。

> [!NOTE]
>
> SQL Server 2017 和更新版本中有額外的安全性措施，可避免 CLR 整合發生問題。 這些量值也會對此預存程序的用法施加額外限制。

## <a name="disable-real-time-scoring"></a>停用即時評分

若要停用即時計分功能，請開啟提升權限的命令提示字元，然後執行下列命令：`RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

<a name="bkmk_py_supported_algos"></a>

## <a name="supported-algorithms"></a>支援的演算法

### <a name="python-algorithms-using-real-time-scoring"></a>使用即時評分的 Python 演算法

+ revoscalepy 模型

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) \(英文\) \*
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) \(英文\) \*
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) \(英文\) \*
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) \(英文\) \*
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) \(英文\) \*
  
  以 \* 標示的模型也支援使用 PREDICT 函式進行原生評分。

+ microsoftml 模型

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_net](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

+ microsoftml 提供的轉換

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)

<a name="bkmk_rt_supported_algos"></a>

### <a name="r-algorithms-using-real-time-scoring"></a>使用即時評分的 R 演算法

+ RevoScaleR 模型

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) \(英文\) \*
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) \(英文\) \*
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) \(英文\) \*
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) \(英文\) \*
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) \(英文\) \*
  
  以 \* 標示的模型也支援使用 PREDICT 函式進行原生評分。

+ MicrosoftML 模型

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

+ MicrosoftML 提供的轉換

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

### <a name="unsupported-model-types"></a>不支援的模型類型

即時評分不會使用解譯器；因此，在評分步驟執行期間，任何可能需要解譯器的功能皆不支援。  這些情況可能包括：

+ 不支援使用 `rxGlm` 或 `rxNaiveBayes` 演算法的模型。

+ 即時評分中不支援模型使用轉換函式或包含轉換的公式 (例如 `A ~ log(B`)。 若要使用此類型的模型，我們建議您先對輸入資料執行轉換，然後再將資料傳遞至即時評分。

## <a name="example"></a>範例

本節說明準備並儲存**即時**預測的模型所需的步驟，並提供如何從 T-SQL 呼叫函式的 R 範例。

### <a name="step-1-prepare-and-save-the-model"></a>步驟 1： 準備及儲存模型

sp\_rxPredict 所需的二進位格式與使用 PREDICT 函式所需的格式相同。 因此，在您的 R 程式碼中，請包含對 [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) 的呼叫，並務必指定 `realtimeScoringOnly = TRUE`，如下列範例所示：

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-2-call-sp_rxpredict"></a>步驟 2： 呼叫 sp_rxPredict

您可以像呼叫任何其他預存程序一樣地呼叫 `sp_rxPredict`。 在目前的版本中，預存程序只會採用兩個參數： _\@model_ 代表二進位格式的模型，而 _\@inputData_ 代表用於評分的資料，並定義為有效的 SQL 查詢。

因為二進位格式與 PREDICT 函式所使用的格式相同，因此您可以使用上述範例中的模型和資料表。

```sql
DECLARE @irismodel varbinary(max)
SELECT @irismodel = [native_model_object] from [ml_models]
WHERE model_name = 'iris.dtree' 
AND model_version = 'v1''

EXEC sp_rxPredict
@model = @irismodel,
@inputData = N'SELECT * FROM iris_rx_data'
```

> [!NOTE]
> 如果用於評分的輸入資料不包含符合模型需求的資料行，則呼叫 `sp_rxPredict` 的作業就會失敗。 目前僅支援下列 .NET 資料類型：double、float、short、ushort、long、ulong 和 string。
>
> 因此，您可能需要在輸入資料中篩選掉不受支援的類型，才能使用該資料來進行即時評分。
>
> 如需相對應 SQL 類型的詳細資訊，請參閱 [SQL-CLR 類型對應](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping)或[對應 CLR 參數資料](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data)。

## <a name="next-steps"></a>後續步驟

+ [使用 PREDICT T-SQL 函式與 SQL 機器學習進行原生評分](native-scoring-predict-transact-sql.md)
+ [sp_rxPredict](../../relational-databases/system-stored-procedures/sp-rxpredict-transact-sql.md)
+ [SQL 機器學習](../index.yml)
