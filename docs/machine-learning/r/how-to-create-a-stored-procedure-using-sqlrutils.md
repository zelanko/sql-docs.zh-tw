---
title: 使用 sqlrutils 套件從配套的 R 程式碼建立函式
description: 在 SQL Server 中使用 sqlrutils R 套件，將 R 語言程式碼組合成可作為引數傳遞至預存程序的單一函式。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/31/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0ba94a55144278abd54ebbc2cf038463c3c5f0cb
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288279"
---
# <a name="create-a-stored-procedure-using-sqlrutils"></a>使用 sqlrutils 建立預存程序
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

本文描述如何轉換 R 程式碼，以透過 T-SQL 預存程序形式加以執行的步驟。 為了獲得最佳的結果，您的程式碼可能需要稍加修改，以確保所有輸入皆可參數化。

## <a name="step-1-rewrite-r-script"></a><a name="bkmk_rewrite"></a>步驟 1. 重寫 R 指令碼

為了獲得最佳結果，您應該重寫 R 程式碼，將它封裝為單一函式。

函式所使用的所有變數皆應該定義在函式內，或定義為輸入參數。 請參閱本文的 [範例程式碼](#samples)。

此外，由於 R 函式的輸入參數會成為 SQL 預存程序的輸入參數，因此您必須確定您的輸入和輸出符合下列類型需求：

### <a name="inputs"></a>輸入

輸入參數之間最多只能有一個資料框架。

資料框架內的物件與函式的其他所有輸入參數，皆必須是下列 R 資料類型：
- POSIXct
- NUMERIC
- character
- integer
- 邏輯
- raw

如果輸入類型不是上述類型之一，就必須將其序列化並以 *未經處理的*形式傳遞給函式。 在此情況下，函式也必須包含可還原序列化輸入項目的程式碼。

### <a name="outputs"></a>輸出

函式可以輸出下列其中一個項目：

- 資料框架，其中包含支援的資料類型。 資料框架中的所有物件都必須使用其中一種支援的資料類型。
- 具名清單，其中包含最多一個資料框架。 清單的所有成員都應該使用其中一種支援的資料類型。
- NULL (如果您的函式未傳回任何結果)

## <a name="step-2-generate-required-objects"></a>步驟 2： 產生必要的物件

在您的 R 程式碼已清除，而且可以作為單一函式來呼叫之後，您將使用 **sqlrutils** 套件中的函式，以可傳遞至實際建置預存程序的建構函式形式，來準備輸入和輸出。

**sqlrutils** 提供可定義輸入資料結構描述和類型，以及定義輸出資料結構描述和類型的函式。 它也包含可將 R 物件轉換成所需輸出類型的函式。 根據您的程式碼所使用的資料類型而定，您可能會進行多個函式呼叫來建立必要的物件。

### <a name="inputs"></a>輸入

如果您的函式接受輸入，則針對每個輸入，呼叫下列函式：

- 如果輸入是資料框架，則為 `setInputData`
- `setInputParameter` 適用於所有其他輸入類型

當您進行每個函式呼叫時，會建立一個 R 物件，稍後您會將它作為引數傳遞給 `StoredProcedure`，以建立完整的預存程序。

### <a name="outputs"></a>輸出

**sqlrutils** 提供多個函式，可將 R 物件 (例如清單) 轉換成 SQL Server 所需的 data.frame。
如果您的函式會直接輸出資料框架，而不需先將其包裝到清單中，您即可略過這個步驟。
如果您的函數傳回 NULL，您也可以略過轉換此步驟。

轉換清單或從清單中取得特定項目時，請從下列函式中選擇：

- 如果清單中的變數為資料框架，則為 `setOutputData`
- `setOutputParameter` 適用於清單的其他所有成員

當您進行每個函式呼叫時，會建立一個 R 物件，稍後您會將它作為引數傳遞給 `StoredProcedure`，以建立完整的預存程序。

## <a name="step-3-generate-the-stored-procedure"></a>步驟 3： 產生預存程序

當所有輸入和輸出參數都準備就緒時，請呼叫 `StoredProcedure` 建構函式。

**使用量**

`StoredProcedure (func, spName, ..., filePath = NULL ,dbName = NULL, connectionString = NULL, batchSeparator = "GO")`

為了說明，假設您想要使用這些參數來建立名為 **sp_rsample** 的預存程序：

- 使用現有的函式 **foosql**。 函式是以 R 函式 **foo** 中的現有程式碼為基礎，但是您重寫了函式以符合[本節](#bkmk_rewrite)中所述的需求，並將更新的函式命名為 **foosql**。
- 使用資料框架 **queryinput** 作為輸入
- 使用 R 變數名稱 (**sqloutput**) 以輸出形式產生資料框架
- 您想要建立 T-SQL 程式碼作為 `C:\Temp` 資料夾中的檔案，以便您可以在稍後使用 SQL Server Management Studio 執行它

```R
StoredProcedure (foosql, sp_rsample, queryinput, sqloutput, filePath = "C:\\Temp")
```

> [!NOTE]
> 由於您是將檔案寫入檔案系統，因此可以省略定義資料庫連線的引數。

函式的輸出是 T-SQL 預存程序，可以在 SQL Server 2016 (需要 R 服務) 或 SQL Server 2017 (需要機器學習服務搭配 R) 的執行個體上執行。 

如需其他範例，請參閱套件說明，方法是從 R 環境呼叫 `help(StoredProcedure)`。

## <a name="step-4-register-and-run-the-stored-procedure"></a>步驟 4： 註冊並執行預存程序

有兩種方式可讓您執行預存程序：

- 從支援 SQL Server 2016 或 SQL Server 2017 執行個體連線的任何用戶端使用 T-SQL
- 從 R 環境

這兩種方法都需要在您要使用預存程序的資料庫中註冊預存程序。

### <a name="register-the-stored-procedure"></a>註冊預存程序

您可以使用 R 來註冊預存程序，也可以在 T-SQL 中執行 CREATE PROCEDURE 陳述式。

- 使用 T-SQL。  如果您更熟悉 T-SQL，請開啟 SQL Server Management Studio (或任何其他可執行 SQL DDL 命令的用戶端)，然後使用 `StoredProcedure` 函式準備的程式碼來執行 CREATE PROCEDURE 陳述式。
- 使用 R。在您仍在 R 環境中時，可以使用 `registerStoredProcedure`sqlrutils**中的** 函式向資料庫註冊預存程序。

  例如，您可以藉由進行此 R 呼叫，在 **sqlConnStr** 中定義的執行個體和資料庫中註冊預存程序 *sp_rsample*：

  ```R
  registerStoredProcedure(sp_rsample, sqlConnStr)
  ```


> [!IMPORTANT]
> 無論您使用的是 R 或 SQL，都必須使用有權限建立新資料庫物件的帳戶來執行陳述式。

### <a name="run-using-sql"></a>使用 SQL 執行

建立預存程序之後，請使用支援 T-SQL 的任何用戶端開啟 SQL 資料庫的連線，並傳遞預存程序所需之任何參數的值。

### <a name="run-using-r"></a>使用 R 執行

如果您想要從 R 程式碼執行預存程序，而不是從 SQL Server，則需要一些額外的準備工作。 例如，如果預存程序需要輸入值，則必須在執行函式之前設定那些輸入參數，然後將那些物件傳遞到 R 程式碼中的預存程序。

呼叫已備妥之 SQL 預存程序的整體程序如下：

1. 呼叫 `getInputParameters` 以取得輸入參數物件的清單。
2. 針對每個輸入參數，定義 `$query` 或設定 `$value` 。
3. 使用 `executeStoredProcedure` 以從 R 開發環境執行預存程序，同時傳遞您所設定的輸入參數物件清單。

## <a name="example"></a><a name = "samples"></a>範例

此範例會顯示 R 指令碼的前後版本，該指令碼從 SQL Server 資料庫取得資料、對資料執行一些轉換，然後將其保存到不同的資料庫中。

這個簡單的範例僅用來說明您可以如何重新排列 R 程式碼，使它更容易轉換為預存程序。

### <a name="before-code-preparation"></a>程式碼準備之前


```R
sqlConnFrom <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=AirlineSrc;Trusted_Connection=Yes;"
  
sqlConnTo <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=AirlineTest;Trusted_Connection=Yes;"
  
sqlQueryAirline <- "SELECT TOP 10000 ArrDelay, CRSDepTime, DayOfWeek FROM [AirlineDemoSmall]"
  
dsSqlFrom <- RxSqlServerData(sqlQuery = sqlQueryAirline, connectionString = sqlConnFrom)
  
dsSqlTo <- RxSqlServerData(table = "cleanData", connectionString = sqlConnTo)
  
xFunc <- function(data) {
    data$CRSDepHour <- as.integer(trunc(data$CRSDepTime))
    return(data)
    }
  
xVars <- c("CRSDepTime")
  
sqlCompute <- RxInSqlServer(numTasks = 4, connectionString = sqlConnTo)
  
rxOpen(dsSqlFrom)
rxOpen(dsSqlTo)
  
if (rxSqlServerTableExists("cleanData", connectionString = sqlConnTo))   {
    rxSqlServerDropTable("cleanData")}
  
rxDataStep(inData = dsSqlFrom, 
     outFile = dsSqlTo,
     transformFunc = xFunc,
     transformVars = xVars,
     overwrite = TRUE)
```

> [!NOTE]
> 
> 當您使用 ODBC 連線，而不是叫用 *RxSqlServerData* 函式的話，則必須使用 *rxOpen* 開啟連接，才能在資料庫上執行作業。


### <a name="after-code-preparation"></a>程式碼準備之後

在更新的版本中，第一行會定義函式名稱。 所有來自原始 R 方案的其他程式碼都會變成該函式的一部分。

```R
myetl1function <- function() { 
   sqlConnFrom <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=Airline01;Trusted_Connection=Yes;"
   sqlConnTo <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer02;Database=Airline02;Trusted_Connection=Yes;"
    
   sqlQueryAirline <- "SELECT TOP 10000 ArrDelay, CRSDepTime, DayOfWeek FROM [AirlineDemoSmall]"

   dsSqlFrom <- RxSqlServerData(sqlQuery = sqlQueryAirline, connectionString = sqlConnFrom)
  
   dsSqlTo <- RxSqlServerData(table = "cleanData", connectionString = sqlConnTo)
  
   xFunc <- function(data) {
     data$CRSDepHour <- as.integer(trunc(data$CRSDepTime))
     return(data)}
  
   xVars <- c("CRSDepTime")
  
   sqlCompute <- RxInSqlServer(numTasks = 4, connectionString = sqlConnTo)
  
   if (rxSqlServerTableExists("cleanData", connectionString = sqlConnTo)) {rxSqlServerDropTable("cleanData")}
  
   rxDataStep(inData = dsSqlFrom, 
        outFile = dsSqlTo,
        transformFunc = xFunc,
        transformVars = xVars,
        overwrite = TRUE)
   return(NULL)
}
```

> [!NOTE]
> 
> 雖然您不需要明確地在程式碼中開啟 ODBC 連接，但使用 **sqlrutils**時仍需要 ODBC 連接。

## <a name="see-also"></a>另請參閱

[sqlrutils (SQL)](ref-r-sqlrutils.md)


