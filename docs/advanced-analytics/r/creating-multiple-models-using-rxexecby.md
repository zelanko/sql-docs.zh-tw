---
title: 使用 rxExecBy 建立多個模型
description: 使用 RevoScaleR 程式庫中的 rxExecBy 函式，透過 SQL Server 中儲存的機器資料來建置多個迷你模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: dbba63ae69997c9c5dbdccf49ec590b3f4eba652
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727490"
---
# <a name="creating-multiple-models-using-rxexecby"></a>使用 rxExecBy 建立多個模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

RevoScaleR 中的 **rxExecBy** 函式支援多個相關模型的平行處理。 資料科學家可以快速建立許多相關的模型，而不是根據多個類似實體的資料來定型一個大型模型，每一個都使用單一實體特有的資料。 

例如，假設您正在監視裝置失敗，擷取許多不同類型設備的資料。 藉由使用 rxExecBy，您可以提供單一大型資料集作為輸入、指定要對其進行分層的資料行 (例如裝置類型)，然後為個別裝置建立多個模型。

這個使用案例被稱為 ["pleasingly parallel"](https://en.wikipedia.org/wiki/Embarrassingly_parallel) \(英文\)，因為它將一個大的複雜問題分解成元件部分以進行並行處理。

這種方法的一般應用包括對個別家庭智慧電錶進行預測、建立個別生產線的收益預測，或者針對個別銀行分支量身打造貸款核准模型。

## <a name="how-rxexec-works"></a>rxExec 的運作方式

RevoScaleR 中的 rxExecBy 函式是針對大量小型資料集的高容量平行處理所設計。

1. 您會在 R 程式碼中呼叫 rxExecBy 函式，並傳遞未排序資料的資料集。
2. 指定資料應分組和排序的分割。
3. 定義應該套用到每個資料分割的轉換或模型化函式
4. 當函式執行時，如果您的環境支援資料查詢，則會以平行方式處理它。 此外，模型化或轉換工作會分散在個別的核心中，並以平行方式執行。 這些作業支援的計算內容包括 RxSpark 和 RxInSQLServer。
5. 會傳回多個結果。

## <a name="rxexecby-syntax-and-examples"></a>rxExecBy 語法和範例

**rxExecBy** 接受四個輸入，其中一個輸入是資料集或資料來源物件，可在指定的**索引鍵**資料行上進行分割。 函式會傳回每個分割的輸出。 輸出的形式取決於當做引數傳遞的函式。 例如，如果您傳遞 rxLinMod 之類的模型化函式，您可以針對資料集的每個分割傳回個別的定型模型。

### <a name="supported-functions"></a>支援的函數

模型化：`rxLinMod`、`rxLogit`、`rxGlm`、`rxDtree`

評分：`rxPredict`、

轉換或分析：`rxCovCor`

## <a name="example"></a>範例

下列範例示範如何使用航空公司資料集來建立多個模型，這會在 [DayOfWeek] 資料行上進行分割。 使用者定義函式 `delayFunc`，會藉由呼叫 rxExecBy 套用至每個分割。 函式會針對星期一、星期二等建立不同的模型。

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

如果您收到錯誤 `varsToPartition is invalid`，請檢查索引鍵資料行或其他資料行的名稱是否輸入正確。 R 語言為區分大小寫。

此特定範例未針對 SQL Server 進行最佳化，而在許多情況下，您可以使用 SQL 將資料分組，以達到更佳的效能。 不過，使用 rxExecBy，您可以從 R 建立並行作業。

下列範例說明 R 中的程序，使用 SQL Server 作為計算內容：

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


