---
title: 如何產生預測與使用 SQL Server 中的機器學習服務模型的預測 |Microsoft Docs
description: 使用原生評分的預測和預測 R 和 SQL Server Machine Learning 中的 Pythin 即時計分或預測 T-SQL rxPredict 或 sp_rxPredict。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/30/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8d1ff524a0f033c4e47d7fe7f4e366cb00f2f7b5
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2018
ms.locfileid: "46712468"
---
# <a name="how-to-generate-forecasts-and-predictions-using-machine-learning-models-in-sql-server"></a>如何產生預測與使用 SQL Server 中的機器學習服務模型的預測
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

使用現有的模型來預測或預測新的資料輸入的結果是在 machine learning 中的核心工作。 這篇文章會列舉 SQL Server 中產生預測的方法。 在方法之間高速的預測，其中速度為基礎的累加式簡化的內部處理方法執行階段相依性。 較少的相依性表示更快得到預測。

使用內部處理基礎結構 （即時或原生評分） 隨附的程式庫需求。 函式必須是從 Microsoft 程式庫。 CLR 或 c + + 延伸模組不支援呼叫開放原始碼或協力廠商的函式中的 R 或 Python 程式碼。

下表摘要說明預測和預測評分的架構。 

| 方法           | 介面         | 程式庫需求 | 處理速度 |
|-----------------------|-------------------|----------------------|----------------------|
| Extensibility Framework | [rxPredict (R)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) <br/>[rx_predict (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | 無。 模型可以根據任何 R 或 Python 函式 | 數百毫秒。 <br/>載入執行階段環境都有固定的成本之前的任何新資料計分,，平均三到六個 100 毫秒。 |
| [即時評分的 CLR 延伸模組](../real-time-scoring.md) | [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)上序列化的模型 | : RevoScaleR MicrosoftML <br/>Python: revoscalepy microsoftml | 數以萬計的平均 （毫秒）。 |
| [原生評分的 c + + 延伸模組](../sql-native-scoring.md) | [預測 T-SQL 函數](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)上序列化的模型 | : RevoScaleR <br/>Python: revoscalepy | 小於 20 毫秒，平均。 | 

處理速度和不獨特是輸出的差異的功能。 假設相同的功能和輸入，經過評分的輸出應該不會隨著您使用的方法上。

必須使用支援的函式中，建立模型，然後序列化為未經處理的位元組資料流儲存到磁碟，或儲存在資料庫中的二進位格式。 您可以使用預存程序或 T-SQL，載入和使用 R 或 Python 語言執行平台，不必二進位模型而能更快完成時產生新的輸入上的預測分數。

CLR 和 c + + 的擴充功能的重要性是鄰近的資料庫引擎本身。 Database engine 的原生語言是 c + +，這表示在執行較少的相依性的 c + + 撰寫延伸模組。 相反地，CLR 的擴充功能會相依於.NET Core。 

如您所料，平台支援將會受到這些執行的階段環境。 原生資料庫引擎延伸模組在關聯式資料庫支援的任何地方執行： Windows，Linux，Azure。 CLR 與.NET Core 需求的延伸模組目前為 Windows 只。

## <a name="scoring-overview"></a>評分的概觀

_評分_是兩個步驟的程序。 首先，您可以指定已定型的模型，以從資料表載入。 第二，傳遞新輸入資料，請在函式，來產生預測值 (或_分數_)。 輸入通常是傳回表格式或單一資料列的 T-SQL 查詢。 您可以選擇輸出單一資料行值代表機率，或您可能會輸出數個值，例如信賴區間 」、 「 錯誤 」 或 「 預測其他實用補充。

採取的步驟後，準備模型的整體程序，然後產生分數可以如此歸納：

1. 建立模型，使用支援的演算法。 支援會因您所選擇的計分方法而異。
2. 定型模型。
3. 序列化使用特殊的二進位格式的模型。
3. 將模型儲存至 SQL Server。 通常這表示已序列化的模型儲存在 SQL Server 資料表中。
4. 呼叫函式或預存程序，做為參數指定的模型和資料的輸入。

當輸入包含多個資料列時，它通常是快速插入資料表中的預測值，評分程序的一部分。 產生單一的分數是從表單或使用者的要求，取得輸入的值和傳回的分數，以用戶端應用程式的案例中較為典型的。 若要產生連續的分數時，改善效能，SQL Server 可能會快取模型，以便載入記憶體。

## <a name="compare-methods"></a>比較方法

若要保留核心資料庫引擎處理序的完整性，隔離從 RDBMS 處理的語言處理雙架構中已啟用對 R 和 Python 支援。 從 SQL Server 2016 開始，Microsoft 會加入一種擴充性架構，可讓從 T-SQL 執行 R 指令碼。 在 SQL Server 2017 中，已新增 Python 整合。 

擴充性架構支援以 R 或 Python，範圍從簡單的函數到訓練複雜機器學習服務模型，您可能會執行任何作業。 不過，雙同處理序架構需要叫用每個呼叫，不論作業的複雜度外部 R 或 Python 處理序。 當工作負載需要從資料表載入預先定型的模型，並針對它評分已在 SQL Server 中的資料時，呼叫外部處理序的額外工作將可以在某些情況下無法接受的延遲。 例如，詐騙偵測需要快速評分相關性。

若要增加評分的速度，像是詐騙偵測案例，SQL Server 會將內建生計分庫成為消除的 R 和 Python 的啟動程序的額外負荷的 c + + 和 CLR 的延伸模組。

[**即時計分**](../real-time-scoring.md)是高效能評分的第一個解決方案。 舊版的 SQL Server 2017 和更新版本的更新中，導入 SQL Server 2016，即時評分依賴內就能對 R 和 Python 處理而不受 Microsoft 管制 RevoScaleR、 MicrosoftML (R)、 revoscalepy 中的函式的 CLR 程式庫和microsoftml (Python)。 CLR 程式庫會使用叫用**sp_rxPredict**預存程序從任何支援的模型型別，產生分數，而不需要呼叫 R 或 Python 執行階段。

[**原生評分**](../sql-native-scoring.md)是 SQL Server 2017 功能，實為原生的 c + + 程式庫，但僅適用於 RevoScaleR 與 revoscalepy 模式。 它是最快且更安全的方式，但是支援較少的相對於其他方法的函式。

## <a name="choose-a-scoring-method"></a>選擇計分方法

平台需求通常會指定要使用哪一個評分方法。

| 產品版本及平台 | 方法 |
|------------------------------|-------------|
| Windows、 SQL Server 2017 Linux 和 Azure SQL Database 上的 SQL Server 2017 | **原生評分**與 T-SQL 的預測 |
| SQL Server 2017 (Windows 只)，SQL Server 2016 R Services SP1 或更高版本 | **即時計分**sp\_rxPredict 預存程序 |

我們建議使用 PREDICT 函式的原生評分。 使用預存程序\_rxPredict，您必須啟用 SQLCLR 整合。 啟用此選項之前，請考慮安全性隱含意義。

## <a name="serialization-and-storage"></a>序列化與儲存體

若要使用其中一個快速的評分選項模型，將儲存模型使用特殊的序列化的格式，這已針對大小最佳化和評分的效率。

+ 呼叫[rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)寫入到支援的模型**原始**格式。
+ 呼叫[rxUnserializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)' 來重新構成其他 R 程式碼中使用的模型或檢視模型。

**使用 SQL**

從 SQL 程式碼中，您可以訓練模型使用[sp_execute_external_script](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)，並直接插入至資料表，類型的資料行中的 定型的模型**varbinary （max)**。 如需簡單的範例，請參閱[在 R 中建立 preditive 模型](../tutorials/rtsql-create-a-predictive-model-r.md)

**使用 R**

從 R 程式碼，呼叫[rxWriteObject](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxwriteobject)模型直接寫入至資料庫的 RevoScaleR 封裝中的函式。 **RxWriteObject()** 函式可以擷取從 ODBC 資料來源，例如 SQL Server 的 R 物件或物件寫入 SQL Server。 API 被仿造的簡單索引鍵-值存放區。
  
如果您使用此函式時，務必模型使用序列化[rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)第一次。 然後，設定*序列化*中的引數**rxWriteObject**設為 FALSE，以避免重複序列化步驟。

序列化成二進位格式的模型非常有用，但並非必要，如果您計分預測使用 R 和 Python 執行階段環境中的擴充性架構。 您可以將模型儲存至檔案的原始位元組格式，並從檔案中讀取 SQL server。 如果您要移動或複製環境之間的模型，此選項可能會很有用。

## <a name="scoring-in-related-products"></a>相關產品中的評分

如果您使用[獨立主機](r-server-standalone.md)或[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)，您有其他選項，除了預存程序和 T-SQL 函式，來快速產生預測。 獨立伺服器和 Machine Learning Server 支援的概念*web 服務*程式碼部署。 您可以組合 R 或 Python 預先定型模型，為 web 服務，在評估新的資料輸入的執行階段呼叫。 如需詳細資訊，請參閱下列文章：

+ [在 Machine Learning Server 中的 web 服務是什麼？](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [什麼是作業？](https://docs.microsoft.com/machine-learning-server/operationalize/concept-operationalize-deploy-consume)
+ [將 Python 模型部署為 web 服務使用 azureml 模型-管理 sdk](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [將 R 程式碼區塊或即時模型發佈為新的 web 服務](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [適用於 R 的 mrsdeploy 套件](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)


## <a name="see-also"></a>另請參閱

+ [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)  
+ [rxRealTimeScoring](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxrealtimescoring)
+ [預存程序 rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)
+ [預測 T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)