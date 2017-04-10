---
title: "如何使用 sqlrutils 建立預存程序 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 5ba99b49-481e-4b30-967a-a429b855b1bd
caps.latest.revision: 10
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# 如何使用 sqlrutils 建立預存程序
本主題描述如何轉換 R 程式碼，以透過 T-SQL 預存程序形式加以執行的步驟。 為了獲得最佳的結果，您的程式碼可能需要稍加修改，以確保所有輸入皆可參數化。

## <a name="step-1-format-your-r-script"></a>步驟 1： 格式化您的 R 指令碼

1. 將所有的程式碼包裝成單一函式。

   這表示函式所使用的所有變數皆必須定義在函式內，或定義為輸入參數。 請參閱本主題的[範例程式碼](#samples)。

## <a name="step-2-standardize-the-inputs-and-outputs"></a>步驟 2： 標準化輸入和輸出

函式的輸入參數會成為 SQL 預存程序的輸入參數，因此應符合以下的類型需求：
- 輸入參數之間最多只能有一個資料框架。
- 資料框架內的物件與函式的其他所有輸入參數，皆必須是下列 R 資料類型：
    - POSIXct
    - numeric
    - character
    - integer
    - 邏輯
    - 未經處理的

- 如果輸入類型不是上述類型之一，就必須將其序列化並以*未經處理的*形式傳遞給函式。 在此情況下，函式也必須包含可還原序列化輸入項目的程式碼。

函式可以輸出下列其中一個項目：

- 資料框架，其中包含支援的資料類型。 資料框架中的所有物件都必須使用其中一種支援的資料類型。
- 具名清單，其中包含最多一個資料框架。 清單的所有成員都應該使用其中一種支援的資料類型。 
- NULL (如果您的函式未傳回任何結果)

## <a name="step-3-make-calls-to-the-sqlrutils-package-to-generate-the-stored-procedure"></a>步驟 3： 呼叫 sqlrutils 套件以產生預存程序

清理好 R 程式碼並可透過單一函式形式進行呼叫之後，您即可開始使用 **sqlrutils** 中的函式，將您的程式碼轉換為預存程序。

根據參數的資料類型，您將使用不同的函式來擷取資料並建立參數物件。

1. 如果您的函式接受輸入參數，請為每個參數，建立下列其中一個物件： 
    - 如果輸入參數為資料框架，請使用 `setInputData`。
    - 針對其他所有輸入參數，請使用 `setInputParameter`。

2. 如果您的函式會輸出清單，請建立一個物件以處理來自這份清單的所需資料，如下所示： 
    - 如果清單中的變數為資料框架，請使用 `setOutputData`。
    - 針對清單的其他所有成員，請使用 `setOutputParameter`。
    - 如果您的函式會直接輸出資料框架，而不需先將其包裝到清單中，您即可略過這個步驟。 
    - 如果您的函式會傳回 NULL，請略過此步驟。

3. 準備好所有輸入和輸出參數時，請呼叫 `StoredProcedure` 建構函式以產生含有 R 函式的預存程序。
4. 若要立即使用資料庫來註冊預存程序，請使用 `registerStoredProcedure`。

## <a name="step-4-execute-the-stored-procedure"></a>步驟 4： 執行預存程序

1. 如果您想要從 R 程式碼 (而不是從 SQL Server) 執行預存程序，但預存程序需要輸入項目，則您必須設定這些輸入參數，然後才能執行此函式： 
    - 呼叫 `getInputParameters` 以取得輸入參數物件的清單。
    - 針對每個輸入參數，定義 `$query` 或設定 `$value`。 

2. 使用 `executeStoredProcedure` 以從 R 開發環境執行預存程序，同時傳遞您所設定的輸入參數物件清單。

## <a name="a-name-samplesaexamples-prepare-your-code"></a><a name = "samples"></a>範例：準備您的程式碼 

在此範例中，R 程式碼會讀取資料庫、執行部分資料轉換作業，並將資料儲存到另一個資料庫。 這個簡單的範例僅用來說明您可以如何重新排列 R 程式碼，以提供更簡潔的預存程序轉換介面。

**格式化之前**


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
請注意，若您使用 ODBC 連接，而不是叫用 *RxSqlServerData* 函式的話，則必須使用 *rxOpen* 開啟連接，才能在資料庫上執行作業。



**格式化之後**

在重新格式化的版本中，第一行會定義函式名稱。

所有來自原始 R 方案的程式碼都會變成該函式的一部分。 

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
雖然您不需要明確地在程式碼中開啟 ODBC 連接，但使用 **sqlrutils** 時仍需要 ODBC 連接。 


## <a name="see-also"></a>另請參閱

[使用 sqlrutils 產生預存程序](../../advanced-analytics/r-services/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)

