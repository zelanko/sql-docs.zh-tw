---
title: 建立使用 rxExecBy-SQL Server Machine Learning 服務的多個模型
description: 使用 RevoScaleR 程式庫從 rxExecBy 函式，來建置多個小型的模型儲存在 SQL Server 的機器資料。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 246f786243a95598f899034b3e0c67481d4082e5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641836"
---
# <a name="creating-multiple-models-using-rxexecby"></a>使用 rxExecBy 建立多個模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**RxExecBy** RevoScaleR 中的函式支援平行處理多個相關模型。 而不是定型一個大型模型根據多個類似的實體的資料、 資料科學家可以快速建立許多相關的模型，每個都使用單一實體的特定資料。 

例如，假設您正在監視裝置故障，擷取資料的許多不同類型的設備。 藉由使用 rxExecBy，您可以提供單一的大型資料集做為輸入，指定的分層資料集，例如裝置類型的資料行，然後建立 個別裝置的多個模型。

這個使用案例已被稱為[「 pleasingly 平行 」](https://en.wikipedia.org/wiki/Embarrassingly_parallel)因為大型的複雜的問題分成並行處理的元件組件。

這種方法的一般應用程式包含個別的家庭智慧型電表預測、 建立個別的產品線的營收預測或建立個別的銀行分支量身訂做的貸款核准的模型。

## <a name="how-rxexec-works"></a>RxExec 的運作方式

RevoScaleR 中的 rxExecBy 函式被設計用於大量平行處理大量的小型資料集。

1. 您呼叫 rxExecBy 函式做為 R 程式碼的一部分，並傳遞的資料集的未排序的資料。
2. 指定資料分割的資料應該分組和排序。
3. 定義轉換或模型應該套用至每個資料分割的函式
4. 函式執行時，資料查詢會以平行方式處理，如果您的環境支援它。 此外，模型或轉換工作會分散到個別的核心，並以平行方式執行。 支援的計算內容的三個作業會包括 RxSpark 和 RxInSQLServer。
5. 會傳回多個結果。

## <a name="rxexecby-syntax-and-examples"></a>rxExecBy 語法和範例

**rxExecBy**會採用四個輸入，其中一個輸入正在進行資料分割的資料集或資料來源物件上指定**金鑰**資料行。 函數會傳回每個資料分割的輸出。 輸出的格式取決於傳遞做為引數的函式。 比方說，如果您傳遞例如 rxLinMod 的模型化函式時，您可能會傳回不同的定型的模型，每個資料分割的資料集。

### <a name="supported-functions"></a>支援的函數

模型化： `rxLinMod`， `rxLogit`， `rxGlm`， `rxDtree`

評分： `rxPredict`，

轉換或分析： `rxCovCor`

## <a name="example"></a>範例

下列範例示範如何建立使用航班資料集，在 [DayOfWeek] 資料行上進行分割的多個模型。 使用者定義函式， `delayFunc`，根據呼叫 rxExecBy 會套用至每個分割區。 函式建立不同的模型為星期一、 星期二，依此類推。

```sql
EXEC sp_execute_external_script
@language = N'R'
, @script = N'
delayFunc <- function(key, data, params) { 
    df <- rxImport(inData = airlineData) 
    rxLinMod(ArrDelay ~ CRSDepTime, data = df) 
} 
OutputDataSet <- rxExecBy(airlineData, c("DayOfWeek"), delayFunc)
'
, @input_data_1 = N'select ArrDelay, DayOfWeek, CRSDepTime from AirlineDemoSmall]'
, @input_data_1_name = N'airlineData'

```

如果您收到錯誤， `varsToPartition is invalid`，檢查是否已正確輸入索引鍵資料行或資料行的名稱。 R 語言會區分大小寫。

此特定範例不適合 SQL Server，您可以在許多情況下達到更佳的效能使用 SQL 來分組資料。 不過，使用 rxExecBy，您可以建立平行作業從。

下列範例說明在 R 中，使用 SQL Server 作為計算內容的程序：

```R
sqlServerConnString <- "SERVER=hostname;DATABASE=TestDB;UID=DBUser;PWD=Password;"
inTable <- paste("airlinedemosmall")
sqlServerDataDS <- RxSqlServerData(table = inTable, connectionString = sqlServerConnString)

# user function
".Count" <- function(keys, data, params)
{
  myDF <- rxImport(inData = data)
  return (nrow(myDF))
}

# Set SQL Server compute context with level of parallelism = 2
sqlServerCC <- RxInSqlServer(connectionString = sqlServerConnString, numTasks = 4)
rxSetComputeContext(sqlServerCC)

# Execute rxExecBy in SQL Server compute context
sqlServerCCResults <- rxExecBy(inData = sqlServerDataDS, keys = c("DayOfWeek"), func = .Count)
```


