---
title: "原生計分 |Microsoft 文件"
ms.custom: 
ms.date: 09/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 8cce800526dbf89da77508713b4dd2aa2eead4ae
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="native-scoring"></a>原生計分

本主題說明在 SQL Server 2017 功能，可提供幾近即時的機器學習模型上的 計分。

+ 什麼是原生與即時計分計分
+ 運作方式
+ 支援的平台和需求

## <a name="what-is-native-scoring-and-how-is-it-different-from-realtime-scoring"></a>什麼是原生計分，以及如何與不同即時計分？

在 SQL Server 2016 中，Microsoft 建立擴充性架構，可讓從 T-SQL 中執行 R 指令碼。 此架構支援 R，範圍從簡單的函式到定型複雜機器學習模型中，您可能會執行任何作業。 不過，雙同處理序架構需要叫用外部 R 處理序每次呼叫，不論作業的複雜度。 如果您從資料表和計分對它已經在 SQL Server 中的資料載入預先定型的模型，呼叫外部 R 處理序的負擔會代表不必要的效能成本。

_計分_是兩個步驟的程序。 首先，您可以指定預先定型的模型資料表中載入。 第二，新傳遞輸入函式，來產生預測值的資料 (或_分數_)。 輸入可以是表格式或單一資料列。 您可以選擇輸出單一資料行值代表機率，或您可能會輸出數個值，例如信賴區間、 錯誤或其他有用的補數與預測。

當輸入包含多個資料列的資料時，通常是更快將預測值插入資料表，計分的程序的一部分。  產生單一的分數是更一般的案例，您的表單或使用者的要求，從取得輸入的值並傳回至用戶端應用程式的分數。 若要產生連續的分數時改善效能，SQL Server 可能會快取模型，以便載入記憶體。

若要支援快速計分，SQL Server 機器學習服務 （和 Microsoft 機器學習 Server） 提供內建在計分，可以在 R 中或在 T-SQL 中的程式庫。 有不同的選項，在您有版本而定。

**原生評分**

+ 預測函數，在 TRANSACT-SQL 支援_原生計分_中的 SQL Server 2017 任何執行個體。 它只需要您有模型已經定型過，您可以使用 T-SQL 來呼叫。 使用 T-SQL 原生計分具有下列優點：

    + 不需要進行其他組態設定。
    + 不會呼叫 R 執行階段。 不需要安裝。

**即時計分**

+ **sp_rxPredict**是預存程序的即時計分，可用來從任何支援的模型型別，產生分數，而不需要呼叫 R 執行階段。

  這個預存程序也會提供在 SQL Server 2016 中，如果您升級使用 Microsoft R Server 的獨立安裝程式的 R 元件。 SQL Server 2017 也支援 sp_rxPredict 功能。 因此，您可以使用此函式時使用預測函式不支援類型的模型產生分數。

+ RxPredict 函式可用於快速計分的 R 程式碼中。

針對所有的這些計分方法，您必須使用使用其中一種支援的 RevoScaleR 或 MicrosoftML 演算法來定型模型。

如需即時動作的計分方法的範例，請參閱[端對端貸款 ChargeOff 預測建置使用 Azure HDInsight Spark 叢集和 SQL Server 2016 R 服務](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

## <a name="how-native-scoring-works"></a>計分的原生如何運作

原生計分會使用原生 c + + 程式庫，microsoft 可從一種特殊的二進位格式讀取模型和產生分數。 因為模型可以發行，而且用於計分不必呼叫 R 解譯器，會降低額外負荷的多個處理程序互動。 因此，原生計分支援更快的預測效能企業實際執行案例中。

若要產生分數，使用這個程式庫，您呼叫計分函式，並傳遞下列必要的輸入：

+ 相容的模型。 請參閱[需求](#Requirements)如需詳細資訊。
+ 通常定義為 SQL 查詢的輸入的資料

函數會傳回輸入的資料，以及您想要傳遞的來源資料的任何資料行的預測。

如需程式碼範例，以及如何準備所需的二進位格式的模型，請參閱這篇文章的指示：

+ [如何執行即時計分](r/how-to-do-realtime-scoring.md)

完整的解決方案，其中包含原生計分，請參閱 SQL Server 開發小組的這些範例：

+ 部署您的 ML 指令碼：[使用 Python 模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ 部署您的 ML 指令碼：[使用 R 模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)

## <a name="requirements"></a>需求

支援的平台如下所示：

+ SQL Server 2017 機器學習服務 （包括 Microsoft R Server 9.1.0）
    
    原生計分使用預測需要 SQL Server 2017。
    它適用於任何版本的 SQL Server 2017，包括 Linux。

    您也可以執行即時計分使用 sp_rxPredict。 若要使用這個預存程序需要啟用[SQL Server CLR 整合](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration)。

+ SQL Server 2016

   即時計分使用 sp_rxPredict 可能有 SQL Server 2016，並也可以在 Microsoft R Server 上執行。 此選項需要 SQLCLR 啟用，以及您安裝 Microsoft R Server 升級。
   如需詳細資訊，請參閱[即時計分](Real-time-scoring.md)

### <a name="model-preparation"></a>模型的準備工作

+ 在此模型必須事先使用其中一個支援定型**rx**演算法。 如需詳細資訊，請參閱[支援演算法](#bkmk_native_supported_algos)。
+ 使用 Microsoft R Server 9.1.0 中提供新的序列化函式必須儲存模型。 序列化函式已最佳化為支援快速計分。

### <a name="bkmk_native_supported_algos"></a>支援原生計分的演算法

+ RevoScaleR 模型

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

如果您要使用從 MicrosoftML 模型，請使用即時 sp_rxPredict 與計分。

### <a name="restrictions"></a>限制

不支援下列模型類型：

+ 包含其他不受支援的 R 轉換類型的模型
+ 模型使用`rxGlm`或`rxNaiveBayes`RevoScaleR 的演算法
+ PMML 模型
+ 使用 CRAN 或其他儲存機制從其他 R 程式庫建立的模型
+ 模型包含任何其他的 R 轉換
