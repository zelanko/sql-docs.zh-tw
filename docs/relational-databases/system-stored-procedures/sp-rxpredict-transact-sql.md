---
title: sp_rxPredict |微軟文件
ms.date: 03/31/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: machine-learning
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
monikerRange: '>=sql-server-2016||>= sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 45afb5e861aee7b8cf253f6c241a884b54ff9451
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2020
ms.locfileid: "80662843"
---
# <a name="sp_rxpredict"></a>sp_rxPredict  
[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

為給定的輸入生成預測值,該輸入由存儲在 SQL Server 資料庫中的二進位數位格式的機器學習模型組成。

近乎即時地在 R 和 Python 機器學習模型上提供評分。 `sp_rxPredict``rxPredict`是作為[RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)和[MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)中的 R 函數的包裝提供的儲存過程,以及 rx_predict [Python](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict)函數在[revoscaley](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)和[Microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)中提供。 它寫於C++,專為評分操作進行了優化。

儘管必須使用 R 或 Python 創建模型,但一旦模型序列化並儲存在目標資料庫引擎實例上,即使未安裝 R 或 Python 整合,也可以從該資料庫引擎實例使用該模型。 有關詳細資訊,請參閱使用[sp_rxPredict 的即時評分](https://docs.microsoft.com/sql/machine-learning/real-time-scoring)。

## <a name="syntax"></a>語法

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>引數

**model**

支援格式的預訓練模型。 

**input**

合法的 SQL 查詢

### <a name="return-values"></a>傳回值

返回分數列以及輸入數據源中的任何傳遞列。
如果演算法支援生成此類值,則可以返回其他分數列,如置信區間。

## <a name="remarks"></a>備註

要啟用儲存過程的使用,必須在實例上啟用 SQLCLR。

> [!NOTE]
> 使用此選項會產生安全影響。 如果在伺服器上無法啟用 SQLCLR,請使用替代實現,如[Transact-SQL PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql?view=sql-server-2017)函數。

使用者需要`EXECUTE`資料庫的許可權。

### <a name="supported-algorithms"></a>支援的演算法

要建立和訓練模型,請使用[SQL Server 2 電腦學習服務 (R 或 Python)、SQL](https://docs.microsoft.com/sql/machine-learning/what-is-sql-server-machine-learning) [Server 2016 R 服務](https://docs.microsoft.com/sql/machine-learning/r/sql-server-r-services)[、SQL Server 機器學習伺服器(獨立)(R 或 Python)](https://docs.microsoft.com/sql/machine-learning/r/r-server-standalone)或[SQL Server 2016 R 伺服器(獨立)](https://docs.microsoft.com/sql/machine-learning/r/r-server-standalone?view=sql-server-2016)提供的 R 或 Python 支援的演演演算法之一。

#### <a name="r-revoscaler-models"></a>R: RevoScaleR 模型

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees \(英文\) ](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree \(英文\) ](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree)
  + [rxd森林](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest)

#### <a name="r-microsoftml-models"></a>R: 微軟ML模型

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rx快速森林](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

#### <a name="r-transformations-supplied-by-microsoftml"></a>R:微軟ML提供的轉換

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

#### <a name="python-revoscalepy-models"></a>Python:重度模型

  + [rx_lin_mod \(英文\) ](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit \(英文\) ](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit)
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees)
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree)
  + [rx_dforest \(英文\) ](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest)


#### <a name="python-microsoftml-models"></a>Python:微軟模型

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

#### <a name="python-transformations-supplied-by-microsoftml"></a>Python:微軟提供的轉換

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)
  
### <a name="unsupported-model-types"></a>不支援的模型類型

不支援以下模型型態:

+ 使用 RevoScaleR`rxGlm``rxNaiveBayes`中的 或 演算法的模型
+ R 中的 PMML 型號
+ 使用其他第三方庫建立的模型 

## <a name="examples"></a>範例

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

除了是有效的 SQL 查詢外*\@,inputData*中的輸入數據還必須包括與存儲模型中的列相容的列。

`sp_rxPredict`僅支援以下 .NET 列類型:雙精度、浮點、短列、u 短型、長列、ulong 和字串。 在使用輸入資料進行即時評分之前,您可能需要篩選出輸入數據中不支援的類型。 

  如需相對應 SQL 類型的詳細資訊，請參閱 [SQL-CLR 類型對應](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping)或[對應 CLR 參數資料](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。

