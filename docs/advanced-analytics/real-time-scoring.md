---
title: 在 SQL Server machine learning 中的即時評分 |Microsoft Docs
description: 產生使用 sp_rxPredict，評分 dta 的輸入，針對預先定型的模型，以 R 撰寫 SQL Server 上的預測。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d5a3d0318f925918ef98ae18744e4287d6b81108
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2018
ms.locfileid: "40396077"
---
# <a name="real-time-scoring-with-sprxpredict-in-sql-server-machine-learning"></a>使用 SQL Server machine learning 中的 sp_rxPredict 進行即時評分
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章說明如何在 SQL Server 關聯式資料的近乎即時 works 評分，使用機器學習服務模型以 r 撰寫 

> [!Note]
> 原生評分是使用原生的 T-SQL 預測函式進行非常快速評分的即時評分的特殊實作。 如需詳細資訊和可用性，請參閱 <<c0> [ 原生評分](sql-native-scoring.md)。

## <a name="how-real-time-scoring-works"></a>如何進行即時評分運作方式

即時評分支援在 SQL Server 2017 和 SQL Server 2016 中，特定模型類型，例如根據 RevoScaleR 或 MicrosoftML functions [rxLinMod (RevoScaleR)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)或[rxNeuralNet (MicrosoftML)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet). 它會使用原生 c + + 程式庫產生分數，根據使用者輸入提供給 machine learning 的特殊的二進位格式儲存的模型。

因為可以使用定型的模型進行評分，而不需要呼叫外部語言執行階段，則會減少多個處理序的額外負荷。 這可用於評分案例的生產環境支援更快的預測效能。 因為資料絕不會離開 SQL Server，就可以產生並插入新的資料表，而不需要任何 R 與 SQL 之間的資料轉譯結果。

即時評分是多步驟程序：

1. 未評分的預存程序必須啟用每個資料庫為基礎。
2. 您載入預先定型的模型，以二進位格式。
3. 您可以提供新的輸入的資料，表格式或單一資料列，做為模型的輸入。
4. 若要產生分數，請呼叫 sp_rxPredict 預存程序。

## <a name="get-started"></a>開始使用

程式碼範例和指示，請參閱[如何執行原生評分或即時評分](r/how-to-do-realtime-scoring.md)。

如需如何使用 rxPredict，用於評分的範例，請參閱[端對端貸款壞帳預測建置使用 Azure HDInsight Spark 叢集和 SQL Server 2016 R 服務](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

> [!TIP]
> 如果您正在以獨佔方式在 R 程式碼中，您也可以使用[rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict)快速評分函式。

## <a name="requirements"></a>需求

支援這些平台上的即時評分：

+ SQL Server 2017 Machine Learning 服務
+ SQL Server R Services 2016 中，以升級至 9.1.0 或更新版本的 R 元件

在 SQL Server，您必須啟用以 CLR 為基礎的程式庫加入 SQL Server 即時評分的功能。

如需 Microsoft R Server 為基礎的分散式環境中的即時評分資訊，請參閱[publishService](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)中可用的函式[mrsDeploy 套件](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)，支援發行進行即時評分為新的 R 伺服器上執行的 web 服務的模型。

### <a name="restrictions"></a>限制

+ 必須事先使用其中一個支援訓練模型**rx**演算法。 如需詳細資訊，請參閱 <<c0> [ 支援的演算法](#bkmk_rt_supported_algos)。 使用即時評分`sp_rxPredict`支援 RevoScaleR 和 MicrosoftML 演算法。

+ 必須儲存模型，使用新的序列化函式： [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)針對 R，以及[rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)適用於 Python。 這些序列化函式已經過最佳化，支援快速評分。

+ 即時評分，不會使用解譯器;因此，可能需要解譯器的任何功能不支援在評分的步驟。  這些情況可能包括：

  + 模型使用`rxGlm`或`rxNaiveBayes`目前不支援的演算法

  + 使用 R 轉換函數或包含的轉換，例如公式的 RevoScaleR 模型<code>A ~ log(B)</code>不支援即時評分。 若要使用這種模型，我們建議您在上執行的轉換輸入資料，再將資料傳遞給即時評分。

+ 即時評分目前已針對較小的資料集，範圍從幾個資料列到數十萬個資料列上的快速預測最佳化。 使用的巨量資料集[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)可能會比較快。

### <a name="a-namebkmkrtsupportedalgosalgorithms-that-support-real-time-scoring"></a><a name="bkmk_rt_supported_algos">支援即時評分的演算法

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

上一節中的 R 轉換非明確列出不支援即時評分。 

對於習慣使用 RevoScaleR 和 Microsoft R 特有的其他程式庫的開發人員，包括不受支援的函式`rxGlm`或`rxNaiveBayes`RevoScaleR，PMML 模型中的演算法和其他模型，建立使用其他的 R 程式庫，從 CRAN 或其他存放庫。

### <a name="known-issues"></a>已知問題

+ `sp_rxPredict` NULL 值傳遞做為模型時，會傳回不正確訊息: 「 System.Data.SqlTypes.SqlNullValueException:Data 中 Null 」。

## <a name="next-steps"></a>後續步驟

[如何進行即時評分](r/how-to-do-realtime-scoring.md)
