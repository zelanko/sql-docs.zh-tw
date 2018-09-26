---
title: sp_rxPredict |Microsoft Docs
ms.custom: ''
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_rxPredict
- sp_rxPredict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_rxPredict procedure
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a8b23fe592b7e7fc90f2e3229d71a805f7332f4d
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2018
ms.locfileid: "46713860"
---
# <a name="sprxpredict"></a>sp_rxPredict  
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

產生指定的輸入，機器學習模型以二進位格式儲存在 SQL Server 資料庫所組成的預測的值。

提供在 R 和 Python 機器學習服務模型中近乎即時評分。 `sp_rxPredict` 提供的包裝函式的預存程序`rxPredict`中的 R 函式[RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)並[MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)，而[rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) Python 函式，在[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)並[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)。 它以 c + + 撰寫，並已特別針對評分作業最佳化。

雖然必須使用 R 或 Python 之後它會序列化並儲存在目標資料庫引擎執行個體上的二進位格式,，建立模型，便可以從該資料庫引擎執行個體即使在未安裝 R 或 Python 整合。 如需詳細資訊，請參閱 <<c0> [ 即時評分 sp_rxPredict](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring)。


## <a name="syntax"></a>語法

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>引數

**model**

預先定型的模型支援的格式。 

**input**

有效的 SQL 查詢

### <a name="return-values"></a>傳回值

則會傳回分數資料行，以及任何傳遞的資料行，從輸入的資料來源。
其他分數資料行，例如信賴區間，如果演算法所支援的這類值產生可傳回。

## <a name="remarks"></a>備註

若要啟用使用預存程序，必須在執行個體上已啟用 SQLCLR。

> [!NOTE]
> 有安全性影響 enabing 此選項。 使用替代的實作，例如[TRANSACT-SQL 預測](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql?view=sql-server-2017)函式，如果無法在伺服器上已啟用 SQLCLR。

使用者需求`EXECUTE`資料庫的權限。


### <a name="supported-algorithms"></a>支援的演算法

若要建立並定型模型，R 或 Python，使用其中一個支援的演算法所提供[SQL Server 2016 R Services](https://docs.microsoft.com/sql/advanced-analytics/r/sql-server-r-services?view=sql-server-2017)， [SQL Server 2016 R Server （獨立式）](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone?view=sql-server-2016)， [SQL Server 2017 Machine學習 （R 或 Python） 的服務](https://docs.microsoft.com//sql/advanced-analytics/what-is-sql-server-machine-learning?view=sql-server-2017)，或[SQL Server 2017 伺服器 （獨立式） （R 或 Python）](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone?view=sql-server-2017)。


#### <a name="r-revoscaler-models"></a>: RevoScaleR 模型

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree)
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest)

#### <a name="r-microsoftml-models"></a>: MicrosoftML 模型

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

#### <a name="r-transformations-supplied-by-microsoftml"></a>： MicrosoftML 所提供的轉換

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

#### <a name="python-revoscalepy-models"></a>Python: revoscalepy 模型

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit)
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees)
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree)
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest)


#### <a name="python-microsoftml-models"></a>Python: microsoftml 模型

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

#### <a name="python-transformations-supplied-by-microsoftml"></a>Microsoftml 所提供的 Python： 轉換

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-referencee/microsoftml/categorical-hash)
  
### <a name="unsupported-model-types"></a>不支援的模型型別

不支援下列模型類型：

+ 模型使用`rxGlm`或`rxNaiveBayes`RevoScaleR 中的演算法
+ 在 R 中的 PMML 模型
+ 使用其他協力廠商程式庫所建立的模型 

## <a name="examples"></a>範例

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

有效的 SQL 查詢，輸入資料中除了*@inputData*必須在預存的模型中包含資料行與資料行相容。

`sp_rxPredict` 僅支援下列.NET 資料行類型： double、 float、 short、 ushort、 long、 ulong 和字串。 您可能需要篩選出您的輸入資料中不支援的型別才能使用它進行即時評分。 

  如需對應的 SQL 類型的資訊，請參閱[SQL-CLR 類型對應](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping)或是[對應 CLR 參數資料](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。

