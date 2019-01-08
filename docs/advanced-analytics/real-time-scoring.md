---
title: 進行即時評分使用 sp_rxPredict 預存程序-SQL Server Machine Learning 服務
description: 產生使用 sp_rxPredict，評分資料輸入，針對預先定型的模型，以 R 撰寫 SQL Server 上的預測。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: def60a6de7d5a6f3641a6de88410543e9e592ba4
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645157"
---
# <a name="real-time-scoring-with-sprxpredict-in-sql-server-machine-learning"></a>使用 SQL Server machine learning 中的 sp_rxPredict 進行即時評分
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

進行即時評分用法[sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)系統預存程序和 CLR 擴充功能在 SQL Server 的高效能預測或預測的工作負載中的分數。 即時評分與語言無關，並執行 R 或 Python 執行時間不含相依性。 假設模型建立並定型使用 Microsoft 函式，然後序列化為 SQL Server 中的二進位格式，您可以使用即時評分來產生新的資料輸入，並沒有 R 或 Python 的附加元件的 SQL Server 執行個體上的預測的結果安裝。

## <a name="how-real-time-scoring-works"></a>如何進行即時評分運作方式

即時評分支援在 SQL Server 2017 和 SQL Server 2016[支援的模型型別](#bkmk_py_supported_algos)用於線性及羅吉斯迴歸 」 和 「 決策樹模型。 它會使用原生 c + + 程式庫產生分數，根據使用者輸入提供給 machine learning 的特殊的二進位格式儲存的模型。

因為可以使用定型的模型進行評分，而不需要呼叫外部語言執行階段，則會減少多個處理序的額外負荷。 這可用於評分案例的生產環境支援更快的預測效能。 因為資料絕不會離開 SQL Server，就可以產生並插入新的資料表，而不需要任何 R 與 SQL 之間的資料轉譯結果。

即時評分是多步驟程序：

1. 未評分的預存程序必須啟用每個資料庫為基礎。
2. 您載入預先定型的模型，以二進位格式。
3. 您提供新的輸入的資料評分，表格式或單一資料列，做為模型的輸入。
4. 若要產生分數，請呼叫[sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)預存程序。

> [!TIP]
> 如需範例的作用中的即時評分，請參閱[端對端貸款壞帳預測建置使用 Azure HDInsight Spark 叢集和 SQL Server 2016 R 服務](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

## <a name="prerequisites"></a>先決條件

+ [啟用 SQL Server CLR 整合](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration)。

+ [啟用即時評分](#bkmk_enableRtScoring)。

+ 必須事先使用其中一個支援訓練模型**rx**演算法。 針對 R，使用即時評分`sp_rxPredict`配合[RevoScaleR 和 MicrosoftML 支援演算法](#bkmk_rt_supported_algos)。 對於 Python，請參閱[revoscalepy 和 microsoftml 支援的演算法](#bkmk_py_supported_algos)

+ 模型使用序列化[rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)針對 R，以及[rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)適用於 Python。 這些序列化函式已經過最佳化，支援快速評分。

+ 將模型儲存至資料庫引擎執行個體，您要呼叫它。 這個執行個體不需要擁有 R 或 Python 執行階段延伸模組。

> [!Note]
> 即時評分目前已針對較小的資料集，範圍從幾個資料列到數十萬個資料列上的快速預測最佳化。 使用的巨量資料集[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)可能會比較快。

<a name="bkmk_py_supported_algos"></a>

## <a name="supported-algorithms"></a>支援的演算法

### <a name="python-algorithms-using-real-time-scoring"></a>Python 演算法使用即時評分

+ revoscalepy 模型

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) \*
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) \*
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) \*
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) \*
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) \*
  
  模型標示為\*也支援原生評分 PREDICT 函式。

+ microsoftml 模型

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_net](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

+ Microsoftml 所提供的轉換

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)


<a name="bkmk_rt_supported_algos"></a>

### <a name="r-algorithms-using-real-time-scoring"></a>使用即時計分的 R 演算法

+ RevoScaleR 模型

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) \*
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) \*
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) \*
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) \*
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) \*
  
  模型標示為\*也支援原生評分 PREDICT 函式。

+ MicrosoftML 模型

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

+ MicrosoftML 所提供的轉換

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

### <a name="unsupported-model-types"></a>不支援的模型型別

即時評分，不會使用解譯器;因此，可能需要解譯器的任何功能不支援在評分的步驟。  這些情況可能包括：

  + 模型使用`rxGlm`或`rxNaiveBayes`演算法不支援。

  + 模型使用的轉換函式或公式包含轉換，例如<code>A ~ log(B)</code>不支援即時評分。 若要使用這種模型，建議您在輸入資料上執行轉換，再將資料傳遞給即時評分。


## <a name="example-sprxpredict"></a>範例： sp_rxPredict

本節說明設定所需的步驟**即時**預測，並提供如何從 T-SQL 呼叫函數的範例。

<a name ="bkmk_enableRtScoring"></a> 

### <a name="step-1-enable-the-real-time-scoring-procedure"></a>步驟 1： 啟用即時評分程序

您必須啟用此功能的每個您想要用於評分的資料庫。 伺服器系統管理員應該執行的命令列公用程式，RegisterRExt.exe 隨附的 RevoScaleR 封裝。

> [!NOTE]
> 必須在執行個體中啟用 SQL CLR 功能以進行即時評分工作順序，此外，資料庫必須標示為值得信任。 當您執行指令碼時，為您執行這些動作。 不過，這麼做之前考量的額外的安全性影響 ！

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
    + 新的資料庫角色， `rxpredict_users`。 資料庫管理員可以使用此角色，授與權限給使用者使用即時評分的功能。

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
> 
> 預存程序呼叫\_rxPredict 失敗時，如果評分的輸入的資料不包含資料行符合模型的需求。 目前支援只有下列.NET 資料類型： double、 float、 short、 ushort、 long、 ulong 和字串。
> 
> 因此，您可能需要進行即時評分使用之前，先篩選出不支援的類型，在您的輸入資料。
> 
> 如需對應的 SQL 類型的資訊，請參閱[SQL-CLR 類型對應](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping)或是[對應 CLR 參數資料](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data)。

## <a name="disable-real-time-scoring"></a>停用即時評分

若要停用即時評分的功能，請開啟提升權限的命令提示字元，並執行下列命令： `RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="next-steps"></a>後續步驟

如需如何使用 rxPredict，用於評分的範例，請參閱[端對端貸款壞帳預測建置使用 Azure HDInsight Spark 叢集和 SQL Server 2016 R 服務](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)。

如需有關 SQL Server 中的評分的詳細背景，請參閱[如何在 SQL Server machine learning 產生預測](r/how-to-do-realtime-scoring.md)。
