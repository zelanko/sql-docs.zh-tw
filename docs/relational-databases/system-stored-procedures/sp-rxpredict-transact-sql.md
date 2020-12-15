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
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 55514f89487a06e16413f199f744013d2c4f8c90
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461499"
---
# <a name="sp_rxpredict"></a>sp_rxPredict  
[!INCLUDE [SQL Server 2016 Windows only](../../includes/applies-to-version/sqlserver2016-windows-only.md)]

產生指定輸入的預測值，包含以二進位格式儲存在 SQL Server 資料庫中的機器學習模型。

以近乎即時的方式提供 R 和 Python 機器學習模型的評分。 `sp_rxPredict`是在 RevoScaleR 和 MicrosoftML 中提供作為 R 函式包裝函式的預存程式 `rxPredict` [](/r-server/r-reference/revoscaler/revoscaler) ，以及[revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)和[MicrosoftML](/machine-learning-server/python-reference/microsoftml/microsoftml-package)中的[rx_predict](/machine-learning-server/python-reference/revoscalepy/rx-predict) Python 函數。 [](/r-server/r-reference/microsoftml/microsoftml-package) 它是以 c + + 撰寫，專門針對計分作業進行優化。

雖然模型必須使用 R 或 Python 來建立，但在目標資料庫引擎實例上序列化並儲存為二進位格式後，即使未安裝 R 或 Python 整合，也可以從該資料庫引擎實例取用。 如需詳細資訊，請參閱 [使用 sp_rxPredict 的即時評分](../../machine-learning/predictions/real-time-scoring.md)。

## <a name="syntax"></a>語法

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>引數

**model**

支援格式的預先定型模型。 

**input**

有效的 SQL 查詢

### <a name="return-values"></a>傳回值

會傳回分數資料行，以及輸入資料來源中的任何傳遞資料行。
如果演算法支援產生這類值，則可以傳回其他分數資料行，例如信賴區間。

## <a name="remarks"></a>備註

若要允許使用預存程式，必須在實例上啟用 SQLCLR。

> [!NOTE]
> 啟用此選項有安全性含意。 如果無法在您的伺服器上啟用 SQLCLR，請使用替代的執行，例如 [TRANSACT-SQL PREDICT](../../t-sql/queries/predict-transact-sql.md?view=sql-server-2017) 函數。

使用者需要 `EXECUTE` 資料庫的許可權。

### <a name="supported-algorithms"></a>支援的演算法

若要建立和定型模型，請使用其中一個支援的 R 或 Python 演算法（由 [SQL Server Machine Learning Services (r 或 python) ](../../machine-learning/sql-server-machine-learning-services.md)、 [SQL Server 2016 R Services](../../machine-learning/r/sql-server-r-services.md)、 [SQL Server Machine Learning Server (獨立)  (R 或 Python) ](../../machine-learning/r/r-server-standalone.md)，或 SQL Server [2016 R Server (獨立) ](../../machine-learning/r/r-server-standalone.md?view=sql-server-2016)。

#### <a name="r-revoscaler-models"></a>R： RevoScaleR 模型

  + [rxLinMod](/machine-learning-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](/machine-learning-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](/machine-learning-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](/machine-learning-server/r-reference/revoscaler/rxdtree)
  + [rxdForest](/machine-learning-server/r-reference/revoscaler/rxdforest)

#### <a name="r-microsoftml-models"></a>R： MicrosoftML 模型

  + [rxFastTrees](/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](/machine-learning-server/r-reference/microsoftml/rxfastlinear)

#### <a name="r-transformations-supplied-by-microsoftml"></a>R： MicrosoftML 提供的轉換

  + [featurizeText](/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](/machine-learning-server/r-reference/microsoftml/selectFeatures)

#### <a name="python-revoscalepy-models"></a>Python： revoscalepy 模型

  + [rx_lin_mod](/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](/machine-learning-server/python-reference/revoscalepy/rx-logit)
  + [rx_btrees](/machine-learning-server/python-reference/revoscalepy/rx-btrees)
  + [rx_dtree](/machine-learning-server/python-reference/revoscalepy/rx-dtree)
  + [rx_dforest](/machine-learning-server/python-reference/revoscalepy/rx-dforest)


#### <a name="python-microsoftml-models"></a>Python： microsoftml 模型

  + [rx_fast_trees](/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_network](/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

#### <a name="python-transformations-supplied-by-microsoftml"></a>Python： microsoftml 提供的轉換

  + [featurize_text](/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [concat](/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](/machine-learning-server/python-reference/microsoftml/categorical-hash)
  
### <a name="unsupported-model-types"></a>不支援的模型類型

不支援下列模型類型：

+ 使用 `rxGlm` RevoScaleR 中的或演算法的模型 `rxNaiveBayes`
+ 在 R 中 PMML 模型
+ 使用其他協力廠商程式庫建立的模型 

## <a name="examples"></a>範例

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

除了成為有效的 SQL 查詢以外， *\@ inputData* 中的輸入資料還必須包含與預存模型中的資料行相容的資料行。

`sp_rxPredict` 僅支援下列 .NET 資料行類型： double、float、short、ushort、long、ulong 和 string。 您可能需要在輸入資料中篩選出不受支援的類型，才能使用它來進行即時評分。 

  如需相對應 SQL 類型的詳細資訊，請參閱 [SQL-CLR 類型對應](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping)或[對應 CLR 參數資料](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。