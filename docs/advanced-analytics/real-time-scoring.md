---
title: 使用 sp_rxPredict 預存程式的即時計分
description: 使用 sp_rxPredict 產生預測, 針對在 SQL Server 上以 R 撰寫的預先定型模型評分資料輸入。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 2e9c9353acdc0a2641203788c8e4883a9accb021
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345685"
---
# <a name="real-time-scoring-with-sprxpredict-in-sql-server-machine-learning"></a>在 SQL Server 機器學習服務中使用 sp_rxPredict 的即時評分
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

即時計分會在 SQL Server 中使用[sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)系統預存程式和 CLR 擴充功能, 以取得預測工作負載的高效能預測或分數。 即時計分是與語言無關, 而且會在 R 或 Python 執行時間沒有相依性的情況下執行。 假設使用 Microsoft 函式建立並定型的模型, 然後在 SQL Server 中序列化為二進位格式, 您可以使用即時計分, 針對沒有 R 或 Python 附加元件 SQL Server 實例上的新資料輸入產生預測結果客戶.

## <a name="how-real-time-scoring-works"></a>即時計分的運作方式

根據 RevoScaleR 或 MicrosoftML 函數 (例如[rxLinMod (RevoScaleR)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)[rxNeuralNet (MicrosoftML))](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet), SQL Server 2017 和 SQL Server 2016 都支援即時評分。 它會使用C++原生程式庫, 根據提供給以特殊二進位格式儲存之機器學習模型的使用者輸入來產生分數。

由於定型的模型可以用於計分, 而不需要呼叫外部語言執行時間, 因此會減少多個進程的額外負荷。 針對生產評分案例, 這可支援更快速的預測效能。 由於資料永遠不會離開 SQL Server, 因此可以產生結果並插入新的資料表中, 而不需要在 R 與 SQL 之間進行任何資料轉譯。

即時計分是一個多步驟的程式:

1. 執行評分的預存程式必須針對每個資料庫啟用。
2. 您會以二進位格式載入預先定型的模型。
3. 您會提供新的輸入資料做為模型的輸入, 以表格式或單一資料列進行評分。
4. 若要產生分數, 請呼叫[sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)預存程式。

## <a name="prerequisites"></a>必要條件

+ [啟用 SQL SERVER CLR 整合](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration)。

+ [啟用即時評分](#bkmk_enableRtScoring)。

+ 模型必須使用其中一個支援的**rx**演算法預先定型。 針對 R, 與搭配`sp_rxPredict` [RevoScaleR 和 MicrosoftML 支援的演算法](#bkmk_rt_supported_algos)使用的即時評分。 針對 Python, 請參閱[revoscalepy 和 microsoftml 支援的演算法](#bkmk_py_supported_algos)

+ 使用適用于 R 的[rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)和適用于 Python 的[rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)來序列化模型。 這些序列化函數已經過優化, 可支援快速計分。

+ 將模型儲存到您想要從中呼叫它的 database engine 實例。 此實例不需要有 R 或 Python 執行時間延伸模組。

> [!Note]
> 即時計分目前已針對較小的資料集進行快速預測, 範圍從幾個資料列到數十萬個數據列。 在大型資料集上, 使用[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)可能會更快。

<a name="bkmk_py_supported_algos"></a>

## <a name="supported-algorithms"></a>支援的演算法

### <a name="python-algorithms-using-real-time-scoring"></a>使用即時評分的 Python 演算法

+ revoscalepy 模型

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) \*
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) \*
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees)\*
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) \*
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) \*
  
  標記為的\*模型也支援使用 PREDICT 函數進行原生評分。

+ microsoftml 模型

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_net](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

+ Microsoftml 提供的轉換

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)


<a name="bkmk_rt_supported_algos"></a>

### <a name="r-algorithms-using-real-time-scoring"></a>使用即時評分的 R 演算法

+ RevoScaleR 模型

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) \*
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) \*
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)\*
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) \*
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) \*
  
  標記為的\*模型也支援使用 PREDICT 函數進行原生評分。

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

即時計分不會使用解譯器;因此, 在評分步驟期間, 不支援任何可能需要解譯器的功能。  這些情況可能包括：

  + 不支援使用`rxGlm`或`rxNaiveBayes`演算法的模型。

  + 使用轉換函式或包含轉換的公式 (例如<code>A ~ log(B)</code> ) 的模型在即時計分中不受支援。 若要使用此類型的模型, 我們建議您先對輸入資料執行轉換, 然後再將資料傳遞至即時評分。


## <a name="example-sprxpredict"></a>範例: sp_rxPredict

本節說明設定**即時**預測所需的步驟, 並提供如何從 t-sql 呼叫函數的 R 範例。

<a name ="bkmk_enableRtScoring"></a> 

### <a name="step-1-enable-the-real-time-scoring-procedure"></a>步驟 1： 啟用即時計分程式

您必須針對要用於評分的每個資料庫啟用這項功能。 伺服器系統管理員應該執行包含在 RevoScaleR 套件中的命令列公用程式 Registerrext.exe。

> [!NOTE]
> 為了讓即時計分能夠運作, 必須在實例中啟用 SQL CLR 功能。此外, 資料庫必須標示為值得信任。 當您執行腳本時, 系統會為您執行這些動作。 不過, 在這麼做之前, 請先考慮額外的安全性含意!

1. 開啟提升許可權的命令提示字元, 並流覽至 Registerrext.exe 所在的資料夾。 下列路徑可以在預設安裝中使用:
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. 執行下列命令, 以您的實例名稱和您想要啟用擴充預存程式的目標資料庫來取代:

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    例如, 若要將擴充預存程式加入至預設實例上的 CLRPredict 資料庫, 請輸入:

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    如果資料庫位於預設實例上, 實例名稱就是選擇性的。 如果您使用的是已命名的實例, 則必須指定實例名稱。

3. Registerrext.exe 會建立下列物件:

    + 信任的元件
    + 預存程式`sp_rxPredict`
    + 新的資料庫角色`rxpredict_users`。 資料庫管理員可以使用這個角色, 將許可權授與使用即時評分功能的使用者。

4. 將任何需要執行`sp_rxPredict`的使用者新增至新角色。

> [!NOTE]
> 
> 在 SQL Server 2017 中, 有額外的安全性措施可避免 CLR 整合發生問題。 這些量值也會對此預存程式的用法施加額外的限制。 

### <a name="step-2-prepare-and-save-the-model"></a>步驟 2： 準備並儲存模型

Sp\_rxPredict 所需的二進位格式與使用 PREDICT 函數所需的格式相同。 因此, 在您的 R 程式碼中, 包含對[rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)的呼叫, 並務必`realtimeScoringOnly = TRUE`指定, 如下列範例所示:

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sprxpredict"></a>步驟 3： 呼叫 sp_rxPredict

您可以像\_處理任何其他預存程式一樣呼叫 sp rxPredict。 在目前的版本中, 預存程式只接受兩個 _\@_ 參數: 模型的模型 (二進位格式), 以及 _\@inputData_中要用於計分的資料, 定義為有效的 SQL 查詢。

因為二進位格式與 PREDICT 函數所使用的相同, 所以您可以使用上述範例中的模型和資料表。

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
> 如果計分的輸入\_資料不包含符合模型需求的資料行, 則呼叫 sp rxPredict 會失敗。 目前僅支援下列 .NET 資料類型: double、float、short、ushort、long、ulong 和 string。
> 
> 因此, 您可能需要在輸入資料中篩選掉不受支援的類型, 才能使用它來進行即時評分。
> 
> 如需對應 SQL 類型的詳細資訊, 請參閱[sql-CLR 類型](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping)對應或對應[CLR 參數資料](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data)。

## <a name="disable-real-time-scoring"></a>停用即時評分

若要停用即時計分功能, 請開啟提升許可權的命令提示字元, 然後執行下列命令:`RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="next-steps"></a>後續步驟

如需 SQL Server 中評分的詳細背景, 請參閱[如何在 SQL Server 機器學習服務中產生預測](r/how-to-do-realtime-scoring.md)。
