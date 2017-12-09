---
title: "即時計分 |Microsoft 文件"
ms.custom: 
ms.date: 11/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 766dd16b8c716ee42e316400b7aed4f9cf6bc06a
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="realtime-scoring"></a>即時計分

本主題說明在 SQL Server 2016 和 SQL Server 2017 支援 幾近即時的機器學習模型中的 計分中提供的功能。

> [!TIP]
> 原生計分是即時計分的特殊實作計分的速度非常快，使用原生的 T-SQL 預測函式，並僅適用於 SQL Server 2017。 如需詳細資訊，請參閱[原生計分](sql-native-scoring.md)。

## <a name="how-realtime-scoring-works"></a>即時計分的運作方式

即時計分支援在 SQL Server 2017 和 SQL Server 2016 中，使用支援 RevoScaleR 或 MicrosoftML 演算法所建立的特定模型類型。 它會使用原生 c + + 程式庫產生分數，根據提供的機器學習模型儲存在特殊的二進位格式的使用者輸入。

因為定型的模型可以用於計分不必呼叫外部語言執行階段，多個處理序的額外負荷也隨著降低。 這支援計分案例的實際執行更快的預測效能。 因為資料永遠不會離開 SQL Server，可以產生並插入新的資料表，而不需任何 R 與 SQL 之間的資料轉譯結果。

即時計分是多步驟程序：

1. 未計分的預存程序必須啟用每個資料庫為基礎。
2. 您載入預先定型的模型，以二進位格式。
3. 您可以提供新的輸入的資料，表格式或單一資料列，做為模型的輸入。
4. 若要產生分數，請呼叫 sp_rxPredict 預存程序。

## <a name="get-started"></a>快速入門

如需程式碼範例和指示，請參閱[如何執行原生計分或即時計分](r/how-to-do-realtime-scoring.md)。

如範例 rxPredict 如何用於計分，請參閱 <<c0> [ 端對端貸款 ChargeOff 預測建置使用 Azure HDInsight Spark 叢集和 SQL Server 2016 R 服務](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

> [!TIP]
> 如果您正在以獨佔方式在 R 程式碼中，您也可以使用[rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict)快速計分函式。

## <a name="requirements"></a>需求

即時計分支援在這些平台：

+ SQL Server 2017 Machine Learning 服務
+ SQL Server R Services 2016 中，與 Microsoft R server 9.1.0 R 服務執行個體的升級或更新版本
+ Machine Learning 伺服器 (獨立式)

SQL Server 上，您必須啟用即時事先計分功能。 這是因為此功能需要以 CLR 為基礎的程式庫安裝到 SQL Server。

如需有關即時資訊計分在分散式環境中根據 Microsoft R Server，請參閱[publishService](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)函式用於[mrsDeploy 封裝](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)，支援發行為新計分 R 伺服器上執行的 web 服務的即時的模型。

### <a name="restrictions"></a>限制

+ 在此模型必須事先使用其中一個支援定型**rx**演算法。 如需詳細資訊，請參閱[支援演算法](#bkmk_rt_supported_algos)。 即時與計分`sp_rxPredict`支援 RevoScaleR 和 MicrosoftML 演算法。

+ 必須使用新的序列化函式儲存模型： [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)和[rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) python。 這些序列化函式已經過最佳化，支援快速計分。

+ 即時計分，不會使用解譯器解譯器。因此，任何可能需要解譯器的功能不支援在計分的步驟。  這些情況可能包括：

  + 模型使用`rxGlm`或`rxNaiveBayes`目前不支援的演算法

  + 使用 R 轉換函式中或包含一個轉換，例如公式的 RevoScaleR 模型<code>A ~ log(B)</code>不支援即時計分。 若要使用此類型的模型，我們建議您在上執行轉換輸入資料，再將資料傳遞至即時計分。

+ 即時計分目前已針對較小的資料集，範圍從幾個資料列的資料列千上百部快速預測最佳化。 在極大型資料集，使用[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)可能會比較快。

### <a name="a-namebkmkrtsupportedalgosalgorithms-that-support-realtime-scoring"></a><a name="bkmk_rt_supported_algos">支援即時計分的演算法

+ RevoScaleR 模型

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)\*
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)\*
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)\*
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree)\*
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest)\*
  
  模型標示\*也支援使用預測函數的原生計分。

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
  + [類別](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

### <a name="unsupported-model-types"></a>不支援的模型型別

不支援下列模型類型：

+ 包含其他不受支援的 R 轉換類型的模型
+ 模型使用`rxGlm`或`rxNaiveBayes`RevoScaleR 的演算法
+ PMML 模型
+ 使用 CRAN 或其他儲存機制從其他 R 程式庫建立的模型
+ 包含 R 轉換此處所列以外的任何其他種類的模型

### <a name="known-issues"></a>已知問題

+ `sp_rxPredict`當做模型傳遞 NULL 值時，傳回不正確的訊息: 「 System.Data.SqlTypes.SqlNullValueException:Data 中 Null 」。

## <a name="next-steps"></a>後續的步驟

[如何執行即時計分](r/how-to-do-realtime-scoring.md)
