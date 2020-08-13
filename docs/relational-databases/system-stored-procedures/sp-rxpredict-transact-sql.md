---
title: sp_rxPredict |Microsoft Docs
ms.date: 03/31/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: machine-learning-services
ms.topic: language-reference
f1_keywords:
- sp_rxPredict
- sp_rxPredict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_rxPredict procedure
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: dd1359fa3430e45ae54cadacd75f9ee261021b8d
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2020
ms.locfileid: "88173051"
---
# <a name="sp_rxpredict"></a>sp_rxPredict  
[!INCLUDE [SQL Server 2016 Windows only](../../includes/applies-to-version/sqlserver2016-windows-only.md)]

產生給定輸入的預測值，其中包含以二進位格式儲存在 SQL Server 資料庫中的機器學習模型。

以近乎即時的方式，提供 R 和 Python 機器學習模型的評分。 `sp_rxPredict`是提供做為 `rxPredict` [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)和[MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)中 R 函數包裝函式的預存程式，以及[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)和[MicrosoftML](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)中的[rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) Python 函式。 它是以 c + + 撰寫，並已針對評分作業特別優化。

雖然模型必須使用 R 或 Python 來建立，但在目標資料庫引擎實例上序列化並儲存為二進位格式之後，即使未安裝 R 或 Python 整合，也可以從該資料庫引擎實例取用。 如需詳細資訊，請參閱[使用 sp_rxPredict 的即時評分](https://docs.microsoft.com/sql/machine-learning/predictions/real-time-scoring)。

## <a name="syntax"></a>語法

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>引數

**model**

支援的格式的預先定型模型。 

**input**

有效的 SQL 查詢

### <a name="return-values"></a>傳回值

會傳回分數資料行，以及輸入資料來源中的任何傳遞資料行。
如果演算法支援產生這類值，則可以傳回額外的分數資料行，例如信賴區間。

## <a name="remarks"></a>備註

若要啟用預存程式的使用，必須在實例上啟用 SQLCLR。

> [!NOTE]
> Enabing 此選項有安全性的影響。 如果無法在伺服器上啟用 SQLCLR，請使用替代的執行方式，例如[TRANSACT-SQL PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql?view=sql-server-2017)函數。

使用者需要 `EXECUTE` 資料庫的許可權。

### <a name="supported-algorithms"></a>支援的演算法

若要建立和定型模型，請使用適用于 R 或 Python 的其中一種支援的演算法， [SQL Server Machine Learning Services (R 或 python) ](https://docs.microsoft.com/sql/machine-learning/sql-server-machine-learning-services)、 [SQL Server 2016 R Services](https://docs.microsoft.com/sql/machine-learning/r/sql-server-r-services)、 [SQL Server Machine Learning Server (獨立)  (R 或 Python) ](https://docs.microsoft.com/sql/machine-learning/r/r-server-standalone)，或 SQL Server [2016 r Server (獨立) ](https://docs.microsoft.com/sql/machine-learning/r/r-server-standalone?view=sql-server-2016)。

#### <a name="r-revoscaler-models"></a>R： RevoScaleR 模型

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree)
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest)

#### <a name="r-microsoftml-models"></a>R： MicrosoftML 模型

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

#### <a name="r-transformations-supplied-by-microsoftml"></a>R： MicrosoftML 所提供的轉換

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

#### <a name="python-revoscalepy-models"></a>Python： revoscalepy 模型

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit)
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees)
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree)
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest)


#### <a name="python-microsoftml-models"></a>Python： microsoftml 模型

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

#### <a name="python-transformations-supplied-by-microsoftml"></a>Python： microsoftml 所提供的轉換

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)
  
### <a name="unsupported-model-types"></a>不支援的模型類型

不支援下列模型類型：

+ `rxGlm` `rxNaiveBayes` 在 RevoScaleR 中使用或演算法的模型
+ R 中的 PMML 模型
+ 使用其他協力廠商程式庫建立的模型 

## <a name="examples"></a>範例

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

除了做為有效的 SQL 查詢， * \@ inputData*中的輸入資料也必須包含與預存模型中的資料行相容的資料行。

`sp_rxPredict`僅支援下列 .NET 資料行類型： double、float、short、ushort、long、ulong 和 string。 您可能需要在輸入資料中篩選掉不支援的類型，才能使用它來進行即時評分。 

  如需相對應 SQL 類型的詳細資訊，請參閱 [SQL-CLR 類型對應](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping)或[對應 CLR 參數資料](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。

