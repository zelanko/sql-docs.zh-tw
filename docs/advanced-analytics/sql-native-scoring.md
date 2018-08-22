---
title: 在 SQL Server machine learning 中的原生評分 |Microsoft Docs
description: 產生使用預測 T-SQL 函式，評分 dta 的輸入，針對 SQL Server 上以 R 或 Python 撰寫的預先定型模型的預測。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: bf8f9a6362b72efddccbf5c2b0e54096c6e86aa7
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2018
ms.locfileid: "40393620"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>使用預測 T-SQL 函式的原生評分
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

預先定型的模型之後，您可以將新的輸入的資料傳遞至產生的預測值的函式或*分數*。 在 SQL Server 2017 Windows 或 Linux，或 Azure SQL Database 中，您可以在 TRANSACT-SQL 中使用 PREDICT 函式，以支援原生評分項目。 它只需要有模型已經定型，都可以使用 T-SQL 進行呼叫。 

+ 什麼是原生評分與即時評分
+ 運作方式
+ 支援的平台和需求

## <a name="what-is-native-scoring-and-how-is-it-different-from-real-time-scoring"></a>什麼是原生評分，以及如何與不同即時評分？

在 SQL Server 2016 中，Microsoft 建立了一個擴充性架構，可允許從 T-SQL 執行 R 指令碼。 此架構支援在 R 中，範圍從簡單的函數到訓練複雜機器學習服務模型，您可能會執行任何作業。 不過，雙同處理序架構需要叫用外部 R 處理序的每個呼叫，不論作業的複雜度。 如果您從資料表和評分對它已在 SQL Server 中的資料載入預先定型的模型，呼叫外部 R 處理序的額外負荷會表示產生不必要的效能成本。

_評分_是兩個步驟的程序。 首先，您會指定從資料表載入預先定型的模型。 第二，傳遞新輸入資料，請在函式，來產生預測值 (或_分數_)。 輸入可以是表格式或單一資料列。 您可以選擇輸出單一資料行值代表機率，或您可能會輸出數個值，例如信賴區間 」、 「 錯誤 」 或 「 預測其他實用補充。

當輸入包含多個資料列時，它通常是快速插入資料表中的預測值，評分程序的一部分。  產生單一的分數是從表單或使用者的要求，取得輸入的值和傳回的分數，以用戶端應用程式的案例中較為典型的。 若要產生連續的分數時，改善效能，SQL Server 可能會快取模型，以便載入記憶體。

若要支援快速評分，SQL Server Machine Learning 服務 （和 Microsoft Machine Learning Server） 提供內建在評分，可以在 R 中，或在 T-SQL 中的程式庫。 有不同的選項，在您有版本而定。

**原生評分**

+ PREDICT 函式在 TRANSACT-SQL 支援_原生評分_中任何的 SQL Server 2017 執行個體。 它只需要有模型已經定型，都可以使用 T-SQL 進行呼叫。 使用 T-SQL 的原生評分，具有下列優點：

    + 不需要進行其他組態設定。
    + 不會呼叫 R 執行階段。 不需要安裝。

**即時評分**

+ **sp_rxPredict**即時評分，可以用來從任何支援的模型型別，產生分數而不需要呼叫 R 執行階段為預存程序。

  這個預存程序也會提供在 SQL Server 2016 中，如果您升級使用的 Microsoft R Server 獨立安裝的 R 元件。 SQL Server 2017 也支援 sp_rxPredict。 因此，您可以使用此函式時使用 PREDICT 函式不支援的模型型別產生分數。

+ RxPredict 函式可以用於 R 程式碼中的快速評分。

針對所有的這些計分方法，您必須使用已在使用其中一種支援的 RevoScaleR 或 MicrosoftML 演算法定型的模型。

如需範例的作用中的即時評分，請參閱[端對端貸款壞帳預測建置使用 Azure HDInsight Spark 叢集和 SQL Server 2016 R 服務](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

## <a name="how-native-scoring-works"></a>原生評分的運作方式

原生評分，就會使用來自 Microsoft 的可進行特殊的二進位格式讀取模型及產生分數的原生 c + + 程式庫。 因為可以發行模型，並將它用於計分不必呼叫 R 解譯器中，會減少多個處理程序互動的額外負荷。 在企業生產環境案例中，原生評分支援因此，更快的預測效能。

若要產生分數，使用此程式庫，您會呼叫評分函式，，並傳遞下列必要的輸入：

+ 相容的模型。 請參閱[需求](#Requirements)一節以取得詳細資料。
+ 輸入的資料，通常會定義為 SQL 查詢

此函數會傳回輸入資料，以及您想要通過的來源資料的任何資料行的預測。

如需程式碼範例，以及如何準備所需的二進位格式中的模型，請參閱這篇文章的指示：

+ [如何執行即時評分](r/how-to-do-realtime-scoring.md)

完整的解決方案，其中包含原生評分，請參閱 SQL Server 開發小組的這些範例：

+ 部署您的 ML 指令碼：[使用 Python 模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ 部署您的 ML 指令碼：[使用 R 模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)

## <a name="requirements"></a>需求

支援的平台如下所示：

+ SQL Server 2017 Machine Learning 服務 （包括 Microsoft R Server 9.1.0）
    
    原生評分使用 PREDICT 需要 SQL Server 2017。
    它適用於任何版本的 SQL Server 2017 中，包括 Linux。

    您也可以執行即時評分使用 sp_rxPredict。 若要使用此預存程序，您必須啟用[SQL Server CLR 整合](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration)。

+ SQL Server 2016

   進行即時評分使用 sp_rxPredict 可以使用 SQL Server 2016，並也可以在 Microsoft R Server 上執行。 此選項需要 SQLCLR 已啟用，以及您安裝 Microsoft R Server 升級。
   如需詳細資訊，請參閱[即時評分](Real-time-scoring.md)

### <a name="model-preparation"></a>模型的準備

+ 必須事先使用其中一個支援訓練模型**rx**演算法。 如需詳細資訊，請參閱 <<c0> [ 支援的演算法](#bkmk_native_supported_algos)。
+ 必須使用新的序列化函數提供 Microsoft R Server 9.1.0 中儲存模型。 序列化函式最佳化，以支援快速評分。

### <a name="bkmk_native_supported_algos"></a> 支援原生評分的演算法

+ RevoScaleR 模型

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

如果您需要使用從 MicrosoftML 的模型，使用與 sp_rxPredict 即時評分。

### <a name="restrictions"></a>限制

不支援下列模型類型：

+ 包含其他不受支援的 R 轉換類型的模型
+ 模型使用`rxGlm`或`rxNaiveBayes`RevoScaleR 中的演算法
+ PMML 模型
+ 使用其他的 R 程式庫，從 CRAN 或其他存放庫中建立的模型
+ 模型包含任何其他 R 轉換

## <a name="see-also"></a>另請參閱

[即時 SQL Server machine learning 中評分 ](real-time-scoring.md)