---
title: 使用機器學習模型產生預測和預測
description: 使用 rxPredict 或 sp_rxPredict 進行即時計分，或預測 T-sql 以在 R 和 Python 的 SQL Server Machine Learning 中進行預測和預測。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 14ccd4beb2186213cb3d94b10031ac732224f4d9
ms.sourcegitcommit: 2f56848ec422845ee81fb84ed321a716c677aa0e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/25/2019
ms.locfileid: "71271905"
---
# <a name="how-to-generate-forecasts-and-predictions-using-machine-learning-models-in-sql-server"></a>如何在 SQL Server 中使用機器學習模型產生預測和預測
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

使用現有模型來預測或預測新資料輸入的結果是機器學習服務中的核心工作。 本文列舉在 SQL Server 中產生預測的方法。 在這些方法中, 是高速預測的內部處理方法, 其中的速度是根據執行時間相依性的累加縮減。 較少的相依性表示較快的預測。

使用內部處理基礎結構 (即時或原生評分) 隨附程式庫需求。 函式必須來自 Microsoft 程式庫。 CLR 或C++擴充功能不支援呼叫開放原始碼或協力廠商函式的 R 或 Python 程式碼。

下表摘要說明預測和預測的評分架構。 

| 方法           | 介面         | 程式庫需求 | 處理速度 |
|-----------------------|-------------------|----------------------|----------------------|
| Extensibility Framework | [rxPredict (R)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) <br/>[rx_predict (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | 無。 模型可以根據任何 R 或 Python 函數 | 數百毫秒。 <br/>在計分任何新資料之前, 載入執行時間環境會有固定的成本, 平均三到600毫秒。 |
| [即時計分 CLR 延伸模組](../real-time-scoring.md) | 序列化模型上的[sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) | RRevoScaleR、MicrosoftML <br/>Python: revoscalepy、microsoftml | 平均數十毫秒。 |
| [原生C++評分延伸模組](../sql-native-scoring.md) | 預測序列化模型上的[t-sql 函數](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) | RRevoScaleR <br/>Python: revoscalepy | 平均小於20毫秒。 | 

處理的速度和不是輸出的實質是區分功能。 假設有相同的函式和輸入, 評分的輸出不應根據您所使用的方法而有所不同。

模型必須使用支援的函式建立, 然後序列化為儲存至磁片的原始位元組資料流程, 或以二進位格式儲存在資料庫中。 使用預存程式或 T-sql, 您可以載入並使用二進位模型, 而不會產生 R 或 Python 語言執行時間的額外負荷, 並在針對新輸入產生預測分數時加快完成的時間。

CLR 和C++延伸模組的重要性就是資料庫引擎本身的鄰近程度。 資料庫引擎的原生語言是C++, 這表示以較少相依C++性在執行中撰寫的延伸模組。 相反地, CLR 延伸模組相依于 .NET Core。 

如您所預期, 平臺支援會受到這些執行時間環境的影響。 在支援關係資料庫的任何位置執行原生資料庫引擎延伸模組:Windows、Linux、Azure。 具有 .NET Core 需求的 CLR 延伸模組目前僅限 Windows。

## <a name="scoring-overview"></a>評分總覽

_評分_是一個兩個步驟的流程。 首先, 您要指定已定型的模型, 以從資料表載入。 第二, 將新的輸入資料傳遞至函數, 以產生預測值 (或_分數_)。 輸入通常是 T-SQL 查詢, 其中會傳回表格式或單一資料列。 您可以選擇輸出代表機率的單一資料行值, 或者您可能會輸出數個值, 例如信賴區間、錯誤或其他對預測的有用補數。

接下來, 準備模型並產生分數的整體程式, 可以透過這種方式來總結:

1. 使用支援的演算法建立模型。 支援會因您選擇的評分方法而異。
2. 將模型定型。
3. 使用特殊的二進位格式序列化模型。
3. 將模型儲存至 SQL Server。 這通常表示在 SQL Server 資料表中儲存序列化模型。
4. 呼叫函數或預存程式, 將模型和資料輸入指定為參數。

當輸入包含許多資料列時, 通常會更快地將預測值插入資料表, 做為計分處理的一部分。 在您從表單或使用者要求取得輸入值, 並將分數傳回給用戶端應用程式的案例中, 產生單一分數比較常見。 若要在產生連續分數時改善效能, SQL Server 可能會快取模型, 使其可以重載到記憶體中。

## <a name="compare-methods"></a>比較方法

為了保留核心資料庫引擎進程的完整性, R 和 Python 的支援會在從 RDBMS 處理中隔離語言處理的雙重架構中啟用。 從 SQL Server 2016 開始, Microsoft 加入了擴充性架構, 可讓您從 T-sql 執行 R 腳本。 在 SQL Server 2017 中, 已新增 Python 整合。 

擴充性架構支援您可能在 R 或 Python 中執行的任何作業, 範圍從簡單的函式到定型複雜的機器學習模型。 不過, 不論作業的複雜度為何, 雙重程式架構都需要針對每個呼叫叫用外部 R 或 Python 進程。 當工作負載需要從資料表載入預先定型的模型, 並針對已經在 SQL Server 中的資料進行計分時, 呼叫外部進程的額外負荷會增加在特定情況下可能無法接受的延遲。 例如, 詐騙偵測需要快速計分才能相關。

為了提高詐騙偵測之類案例的計分速度, SQL Server 將內建計分程式庫新增C++為和 CLR 延伸模組, 以消除 R 和 Python 啟動程式的額外負荷。

[**即時計分**](../real-time-scoring.md)是高效能計分的第一個解決方案。 在舊版的 SQL Server 2017 和更新版本的 SQL Server 2016 中引進, 即時評分依賴 CLR 程式庫, 其適用于 R 和 Python 處理在 RevoScaleR、MicrosoftML (R)、revoscalepy 和中由 Microsoft 控制的函式。microsoftml (Python)。 CLR 程式庫是使用**sp_rxPredict**預存程式來叫用，以從任何支援的模型類型產生分數，而不需要呼叫 R 或 Python 執行時間。

[**原生評分**](../sql-native-scoring.md)是 SQL Server 2017 功能, 實作為原生C++程式庫, 但僅適用于 RevoScaleR 和 revoscalepy 模型。 這是最快速且更安全的方法, 但支援與其他方法相關的較小功能集。

## <a name="choose-a-scoring-method"></a>選擇評分方法

平臺需求通常會規定要使用的評分方法。

| 產品版本和平臺 | 方法 |
|------------------------------|-------------|
| Windows 上的 SQL Server 2017、SQL Server 2017 Linux 及 Azure SQL Database | 使用 T-sql 預測的**原生評分** |
| SQL Server 2017 (僅限 Windows)、SQL Server 2016 R Services (位於 SP1 或更高版本) | 使用 sp\_rxPredict 預存程式的**即時評分** |

建議您使用 PREDICT 函數來進行原生評分。 您必須\_啟用 SQLCLR 整合, 才能使用 sp rxPredict。 啟用此選項之前, 請先考慮安全性含意。

## <a name="serialization-and-storage"></a>序列化和儲存

若要使用具有任一快速評分選項的模型, 請使用已針對大小和評分效率優化的特殊序列化格式來儲存模型。

+ 呼叫[rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)以將支援的模型寫入**原始**格式。
+ 呼叫[rxUnserializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)' 以重新構成要在其他 R 程式碼中使用的模型, 或用來查看模型。

**使用 SQL**

在 SQL 程式碼中，您可以使用[sp_execute_external_script](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)來定型模型，並在**Varbinary （max）** 類型的資料行中，將定型的模型直接插入資料表中。 如需簡單的範例, 請參閱[在 R 中建立 preditive 模型](../tutorials/quickstart-r-train-score-model.md)

**使用 R**

從 R 程式碼, 呼叫 RevoScaleR 封裝中的[rxWriteObject](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxwriteobject)函式, 將模型直接寫入資料庫中。 **RxWriteObject ()** 函數可以從 ODBC 資料來源 (例如 SQL Server) 取得 R 物件, 或將物件寫入 SQL Server。 API 會在簡單的索引鍵/值存放區之後進行模型化。
  
如果您使用此函式, 請務必先使用[rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)序列化模型。 然後, 將**rxWriteObject**中的*序列化*引數設定為 FALSE, 以避免重複序列化步驟。

將模型序列化為二進位格式很有用, 但如果您要在擴充性架構中使用 R 和 Python 執行時間環境評分預測, 則不需要。 您可以將原始位元組格式的模型儲存至檔案, 然後從檔案讀取到 SQL Server。 如果您要在環境之間移動或複製模型, 此選項可能會很有用。

## <a name="scoring-in-related-products"></a>相關產品中的評分

如果您使用[獨立伺服器](r-server-standalone.md)或[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), 除了預存程式和 t-sql 函數之外, 還有其他選項可快速產生預測。 獨立伺服器和 Machine Learning Server 都支援*web 服務*的概念, 以進行程式碼部署。 您可以將 R 或 Python 預先定型的模型組合成 web 服務, 在執行時間呼叫以評估新的資料輸入。 如需詳細資訊，請參閱下列文章：

+ [Machine Learning Server 中的 web 服務是什麼？](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [什麼是運算化？](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)
+ [使用 azureml-模型管理-sdk 將 Python 模型部署為 web 服務](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [將 R 程式碼區塊或即時模型發佈為新的 web 服務](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [適用于 R 的 mrsdeploy 套件](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)


## <a name="see-also"></a>另請參閱

+ [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)  
+ [rxRealTimeScoring](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxrealtimescoring)
+ [sp-rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)
+ [預測 T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)