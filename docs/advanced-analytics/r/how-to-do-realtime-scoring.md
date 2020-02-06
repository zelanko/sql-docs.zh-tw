---
title: 產生各種預測
description: 在 SQL Server 機器學習中，使用 rxPredict 或 sp_rxPredict 進行即時評分，或使用 PREDICT T-SQL 對原生評分進行預測，以及在 R 和 Python 中進行預測。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7822cd56a52e47493fe175c293dbfe491a9524af
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "73727442"
---
# <a name="how-to-generate-forecasts-and-predictions-using-machine-learning-models-in-sql-server"></a>如何在 SQL Server 中使用機器學習模型產生各種預測
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

使用現有模型，來預測新資料輸入的結果是機器學習的核心工作。 本文將列舉在 SQL Server 中產生預測的方法。 在這些方法中有適用於高速預測的內部處理方法，其中的速度會以遞減執行階段相依性為依據。 較少的相依性表示預測速度更快。

使用內部處理基礎結構 (即時或原生評分) 隨附程式庫需求。 函式必須來自 Microsoft 程式庫。 CLR 或 C++ 擴充功能不支援呼叫開放原始碼或協力廠商函式的 R 或 Python 程式碼。

下表摘要說明預測的評分架構。 

| 方法           | 介面         | 程式庫需求 | 處理速度 |
|-----------------------|-------------------|----------------------|----------------------|
| Extensibility Framework | [rxPredict (R)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) \(英文\) <br/>[rx_predict (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) \(英文\) | 無。 模型可以任何 R 或 Python 函式為依據 | 數百毫秒。 <br/>在對任何新資料進行評分之前，載入執行階段環境會產生固定成本，平均為三到六百毫秒。 |
| [即時評分 CLR 擴充功能](../real-time-scoring.md) | 序列化模型上的 [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) \(部分機器翻譯\) | R：RevoScaleR、MicrosoftML <br/>Python：revoscalepy、microsoftml | 平均為數十毫秒。 |
| [原生評分 C++ 擴充功能](../sql-native-scoring.md) | 序列化模型上的 [PREDICT T-SQL 函式](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) | R：RevoScaleR <br/>Python：revoscalepy | 平均小於 20 毫秒。 | 

處理的速度而非輸出本質為區分功能。 假設您使用相同的函式和輸入，則評分的輸出不應因您使用的方法而有所不同。

模型必須使用支援的函式來建立，然後序列化為儲存至磁碟的原始位元組串流，或以二進位格式儲存於資料庫。 使用預存程序或 T-SQL，您可以載入並使用二進位模型，而不會產生 R 或 Python 語言執行階段的額外負荷，並在針對新輸入產生預測分數時加快完成的時間。

CLR 和 C++ 擴充功能的重要性就是與資料庫引擎本身的鄰近程度。 資料庫引擎的原生語言是 C++，這表示以 C++ 撰寫的擴充功能會搭配較少的相依性來執行。 相反地，CLR 擴充功能相依於 .NET Core。 

如您所預期，平台支援會受到這些執行階段環境所影響。 原生資料庫引擎擴充功能可在支援關聯式資料庫的任何位置執行：Windows、Linux、Azure。 具有 .NET Core 需求的 CLR 擴充功能目前僅限 Windows。

## <a name="scoring-overview"></a>評分概觀

「評分」  是一個兩步驟的處理序。 首先，您指定要從資料表載入且已經定型的模型。 其次，將新的輸入資料傳遞至該函式，以產生預測值 (或「分數」  )。 輸入通常是 T-SQL 查詢，會傳回表格式或單一資料列。 您可以選擇輸出代表可能性的單一資料行值，或者可能輸出數個值，例如，信賴區間、錯誤，或其他對預測有用的補數。

退一步來說，準備模型，然後產生分數的整個處理序，可透過下列方式進行摘要說明：

1. 使用支援的演算法建立模型。 支援會因您選擇的評分方法而有所不同。
2. 將模型定型。
3. 使用特殊的二進位格式來將模型序列化。
3. 將模型儲存至 SQL Server。 這通常表示會將序列化的模型儲存於 SQL Server 資料表中。
4. 呼叫函式或預存程序，會將模型和資料輸入指定為參數。

當輸入包含許多資料列時，通常會在處理評分的過程中，更快地將預測值插入至資料表。 在您從表單或使用者要求中取得輸入值，並將分數傳回給用戶端應用程式的案例中，產生單一分數更為典型。 為了在產生連續分數時改善效能，SQL Server 可能會快取模型，使其可重新載入到記憶體。

## <a name="compare-methods"></a>比較方法

為了保留核心資料庫引擎處理序的完整性，對 R 和 Python 的支援會在將語言處理與 RDBMS 處理隔離的雙重架構中啟用。 從 SQL Server 2016 開始，Microsoft 新增了擴充性架構，可讓您從 T-SQL 執行 R 指令碼。 在 SQL Server 2017 中，則新增了 Python 整合。 

擴充性架構支援您可能在 R 或 Python 中執行的任何作業，範圍從簡單的函式到將複雜的機器學習模型定型。 但是，不論作業的複雜度為何，雙重處理序架構都需要針對每個呼叫來叫用外部 R 或 Python 處理序。 當工作負載需要從資料表載入預先定型的模型，並根據 SQL Server 中現有的資料對其進行評分時，呼叫外部處理序的額外負荷會增加在特定情況下可能無法接受的延遲。 例如，詐騙偵測需要快速評分才有意義。

為了提高詐騙偵測之類案例的評分速度，SQL Server 新增內建的評分程式庫作為 C++ 和 CLR 擴充功能，以消除 R 和 Python 啟動處理序的額外負荷。

[**即時評分**](../real-time-scoring.md)是第一個適用於高效能評分的解決方案。 在 SQL Server 2017 的早期版本和 SQL Server 2016 的較新更新中引進的即時評分會依賴 CLR 程式庫，以代表 R 和 Python 在 RevoScaleR、MicrosoftML (R)、revoscalepy 和 microsoftml (Python) 中，透過 Mcrosoft 控制的函式進行處理。 CLR 程式庫會使用 **sp_rxPredict** 預存程序來叫用，以從任何支援的模型類型產生分數，而不需呼叫 R 或 Python 執行階段。

[**原生評分**](../sql-native-scoring.md)是一個 SQL Server 2017 功能，會實作為原生 C++ 程式庫，但僅適用於 RevoScaleR 和 revoscalepy 模型。 這是最快速且更安全的方法，但支援與其他方法相關的較小型功能集。

## <a name="choose-a-scoring-method"></a>選擇評分方法

平台需求通常會指定要使用的評分方法。

| 產品版本和平台 | 方法 |
|------------------------------|-------------|
| Windows 上的 SQL Server 2017、SQL Server 2017 Linux 及 Azure SQL Database | 使用 T-SQL PREDICT 的**原生評分** |
| SQL Server 2017 (僅限 Windows)、SQL Server 2016 R Services (位於 SP1 或更新版本) | 使用 sp\_rxPredict 預存程序的**即時評分** |

建議您使用 PREDICT 函式進行原生評分。 您必須啟用 SQLCLR 整合，才能使用 sp\_rxPredict。 啟用此選項之前，請先考慮對安全性的影響。

## <a name="serialization-and-storage"></a>序列化和儲存體

若要使用具有任一快速評分選項的模型，請使用已針對大小和評分效率最佳化的特殊序列化格式來儲存模型。

+ 呼叫 [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) \(英文\)，以將支援的模型寫入至**原始**格式。
+ 呼叫 [rxUnserializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) \(英文\)，以重新構成要在其他 R 程式碼中使用的模型，或檢視該模型。

**使用 SQL**

在 SQL 程式碼中，您可以使用 [sp_execute_external_script](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) \(部分機器翻譯\) 來將模型定型，並直接將定型的模型插入至資料表中 **varbinary(max)** 類型的資料行。 如需簡單的範例，請參閱[在 R 中建立預測模型](../tutorials/quickstart-r-train-score-model.md)。

**使用 R**

在 R 程式碼中，呼叫來自 RevoScaleR 套件的 [rxWriteObject](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxwriteobject) \(英文\) 函式，將模型直接寫入至資料庫。 **rxWriteObject()** 函式可以從 ODBC 資料來源 (例如 SQL Server) 取出 R 物件，或將物件寫入至 SQL Server。 此 API 會在簡單的索引鍵值存放區之後進行模型化。
  
如果您使用此函式，請務必先使用 [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) \(英文\) 來將模型序列化。 然後，將 **rxWriteObject** 中的 *serialize* 引數設定為 FALSE，以避免重複進行序列化步驟。

將模型序列化為二進位格式非常實用，但如果您要在擴充性架構中使用 R 和 Python 執行階段環境進行評分預測，則不需要進行此作業。 您可以將原始位元組格式的模型儲存至檔案，然後從該檔案中讀取到 SQL Server。 如果您要在環境之間移動或複製模型，則此選項可能很實用。

## <a name="scoring-in-related-products"></a>在相關產品中進行評分

如果您使用[獨立伺服器](r-server-standalone.md)或 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server) \(英文\)，除了預存程序和 T-SQL 函式之外，還有其他選項可快速產生預測。 獨立伺服器和 Machine Learning Server 均支援可用來進行程式碼部署的「Web 服務」  概念。 您可以將 R 或 Python 預先定型的模型組合成 Web 服務，在執行階段進行呼叫以評估新的資料輸入。 如需詳細資訊，請參閱這些文章：

+ [Machine Learning Server 中有哪些 Web 服務？](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services) \(英文\)
+ [什麼是作業化？](https://docs.microsoft.com/machine-learning-server/what-is-operationalization) \(英文\)
+ [使用 azureml-model-management-sdk 將 Python 模型部署為 Web 服務](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service) \(英文\)
+ [將 R 程式碼區塊或即時模型發佈為新的 Web 服務](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice) \(英文\)
+ [適用於 R 的 mrsdeploy 套件](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package) \(英文\)


## <a name="see-also"></a>另請參閱

+ [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) \(英文\)  
+ [rxRealTimeScoring](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxrealtimescoring) \(英文\)
+ [sp-rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) \(部分機器翻譯\)
+ [PREDICT T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)