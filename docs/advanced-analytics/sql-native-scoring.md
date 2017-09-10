---
title: "原生計分 |Microsoft 文件"
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e1cb06223e5274c1fa439eb9f7d82a005e93a47d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---

# <a name="native-scoring"></a>原生計分

本主題說明在 SQL Server 2017 功能，可提供幾近即時的機器學習模型上的 計分。

+ 什麼是原生與即時計分計分
+ 運作方式
+ 支援的平台和需求

## <a name="what-is-native-scoring-and-how-is-it-different-from-realtime-scoring"></a>什麼是原生計分，以及如何與不同即時計分？

在 SQL Server 2016 中，Microsoft 建立擴充性架構，可讓從 T-SQL 中執行 R 指令碼。 此架構支援 R，範圍從簡單的函式到定型複雜機器學習模型中，您可能會執行任何作業。 不過，組 R 與 SQL Server 的雙重同處理序架構表示必須在每次呼叫，不論作業的複雜度叫用外部 R 處理序。 如果您從資料表和計分對它已經在 SQL Server 中的資料載入預先定型的模型，呼叫外部 R 處理序的負擔會代表不必要的效能成本。

_計分_是兩個步驟的程序： 從資料表中，載入預先定型的模型和新輸入的資料、 表格式或單一資料列，會傳遞到模型，會產生新的值 (或_分數_)。 輸出可能是單一資料行值代表機率或數個值，包括信賴區間、 錯誤或其他有用的補數與預測。

計分的資料有多個資料列，當新的值通常插入資料表計分的程序的一部分。  不過，您也可以擷取即時的單一分數。 當計分連續輸入，以便快速記憶體載入可能會快取模型。

若要支援快速計分，SQL Server 機器學習服務 （和 Microsoft 機器學習 Server） 提供內建在計分，可以在 R 中或在 T-SQL 中的程式庫。 有不同的選項，在您有版本而定。

**原生計分**

+ 在 TRANSACT-SQL 中的 PREDICT 函數可用於_原生計分_從 SQL Server 2017 任何執行個體。 它只需要您具有已經定型，並儲存在資料表中的模型中或透過 T-SQL 進行呼叫。 它是一種即時計分使用原生 T-SQL 函式。不需要其他組態。

   不會呼叫 R 執行階段，並不需要安裝。

**即時計分**

+ **sp_rxPredict**是預存程序的即時計分，可用來從任何支援的模型型別，產生分數，而不需要呼叫 R 執行階段。

  此選項可使用即時計分也會提供在 SQL Server 2016 中，如果您升級使用 Microsoft R Server 的獨立安裝程式的 R 元件。 sp_rxPredict 也適用於 SQL Server 2017，而且可能很好的選項，如果您計分預測函式不支援的模型型別上。

+ RxPredict 函式可用於快速計分的 R 程式碼中。

針對所有的這些計分方法，您必須使用使用其中一種支援的 RevoScaleR 或 MicrosoftML 演算法來定型模型。

如需即時動作的計分方法的範例，請參閱[端對端貸款 ChargeOff 預測建置使用 Azure HDInsight Spark 叢集和 SQL Server 2016 R 服務](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

## <a name="how-native-scoring-works"></a>計分的原生如何運作

原生計分會使用原生 c + + 程式庫，microsoft 可從一種特殊的二進位格式讀取模型和產生分數。 因為模型可以發行，而且用於計分不必呼叫 R 解譯器，會降低額外負荷的多個處理程序互動。 這在企業生產案例中支援多更快的預測效能。

若要產生分數，使用這個程式庫，您呼叫計分函式，並傳遞下列必要的輸入：

+ 相容的模型。 請參閱[需求](#Requirements)如需詳細資訊。
+ 通常定義為 SQL 查詢的輸入的資料

函數會傳回輸入的資料，以及您想要傳遞的來源資料的任何資料行的預測。

如需程式碼範例，以及如何準備所需的二進位格式的模型，請參閱這篇文章的指示：

+ [如何執行即時計分](r/how-to-do-realtime-scoring.md)

## <a name="requirements"></a>需求

支援的平台如下所示：

+ SQL Server 2017 機器學習服務 （包括 Microsoft R Server 9.1.0）
    
    原生計分使用預測需要 SQL Server 2017。
    它適用於任何版本的 SQL Server 2017，包括 Linux。

    您也可以執行即時計分使用 sp_rxPredict，需要啟用 SQL CLR。

+ SQL Server 2016

   即時計分使用 sp_rxPredict 可與 SQL Server 2016，而也可以在 Microsoft R Server 上執行。 此選項需要 SQLCLR 啟用，以及您安裝 Microsoft R Server 升級。
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
  + [rxdForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

如果您要使用從 MicrosoftML 模型，請使用即時 sp_rxPredict 與計分。

### <a name="restrictions"></a>限制

不支援下列模型類型：

+ 包含其他不受支援的 R 轉換類型的模型
+ 模型使用`rxGlm`或`rxNaiveBayes`RevoScaleR 的演算法
+ PMML 模型
+ 使用 CRAN 或其他儲存機制從其他 R 程式庫建立的模型
+ 模型包含任何其他種類的 R 轉換

