---
title: "建立多個模型使用 rxExecBy |Microsoft 文件"
ms.custom: 
ms.date: 04/18/2017
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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 38e675f5f7bdcd5c11ab946d9e73d0c6af2ea770
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="creating-multiple-models-using-rxexecby"></a>建立多個模型使用 rxExecBy

SQL Server 2017 CTP 2.0 包含新的函式， **rxExecBy**，支援多個相關模型的平行處理。 而不是定型一個極大的模型根據類似的多個實體的資料，資料科學家可以非常快速地建立多個相關的模型，每個都使用單一實體的特定資料。

例如，假設您監視裝置失敗，並擷取資料的許多不同類型的設備。 藉由使用 rxExecBy，您可以提供單一大型資料集做為輸入指定醫療資料集，例如裝置類型的資料行，然後建立多個模型模型以供個別裝置。

此程序已被稱為"pleasingly parallel"的處理，因為它會採用有點麻煩，資料科學家或最繁瑣，並使其成為快速、 簡單作業的工作。

這種方法的一般應用程式包括預測為個別的家庭智慧公尺、 建立營收預測不同產品線，或建立為個別的銀行分支貸款核准的模型。

## <a name="how-rxexec-works"></a>RxExec 的運作方式

RevoScaleR 的 rxExecBy 函式可供進行大量平行處理大量的小型資料集。

1. 您 rxExecBy 函式呼叫 R 程式碼的一部分，並將傳遞的資料集的未排序的資料。
2. 指定資料分割的資料應該分組和排序。
3. 定義轉換或模型應該套用至每個資料分割的函式
4. 此函式執行時，如果您的環境可支援處理查詢的資料以平行方式。 此外，「 模型 」 或 「 轉換 」 工作會分散到個別的核心，而且以平行方式執行。 支援的計算內容的三個作業可包括 RxSpark 和 RxInSQLServer。
5. 會傳回多個結果。

## <a name="rxexecby-syntax-and-examples"></a>rxExecBy 語法和範例

**rxExecBy**採用四個輸入，其中一個輸入正在進行資料分割的資料集或資料來源物件上指定**金鑰**資料行。 函數會傳回每個資料分割的輸出。 輸出的形式取決於所收到做為引數函式、、 比方說，如果您要傳入模型函式，例如 rxLinMod，您可能會傳回個別定型的模型，每個資料分割的資料集。

### <a name="supported-functions"></a>支援的函數

模型化： `rxLinMod`， `rxLogit`， `rxGlm`，`rxDtree`

計分： `rxPredict`，

轉換或分析：`rxCovCor`

## <a name="example"></a>範例

下列範例會示範如何建立使用 Airline 資料集，[DayOfWeek] 資料行分割的多個模型。 使用者定義函數， `delayFunc`，根據呼叫 rxExecBy 會套用至每個資料分割。 函式會建立不同的模型為星期一、 星期二，依此類推。

```SQL
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

請注意，此範例不會針對 SQL Server 最佳化，而且您可以在許多情況下會使用 SQL 來分組資料，以達到更佳的效能。 不過，使用 rxExecBy，您可以建立平行工作從。

下列範例將說明 R，當成計算內容中使用 SQL Server 中的程序：

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



