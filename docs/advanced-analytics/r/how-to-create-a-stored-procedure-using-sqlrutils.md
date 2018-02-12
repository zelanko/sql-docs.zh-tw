---
title: "如何使用 sqlrutils 來建立預存程序 | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 5ba99b49-481e-4b30-967a-a429b855b1bd
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: ad0cf99c59bcd3295acf0e1c29b14c8523f6f925
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2018
---
# <a name="create-a-stored-procedure-using-sqlrutils"></a>建立預存程序使用的 sqlrutils
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本主題描述如何轉換 R 程式碼，以透過 T-SQL 預存程序形式加以執行的步驟。 為了獲得最佳的結果，您的程式碼可能需要稍加修改，以確保所有輸入皆可參數化。

## <a name="bkmk_rewrite"></a>步驟 1： 請重寫 R 指令碼

為獲得最佳結果，您應該重新撰寫您的 R 程式碼封裝作為單一函式。

函數所使用的所有變數應該定義在函數中，或應定義為輸入參數。 請參閱本主題的 [範例程式碼](#samples) 。

此外，因為將會變成 R 函數的輸入的參數的輸入的參數的 SQL 預存程序，您必須確定您的輸入和輸出符合下列類型的需求：

### <a name="inputs"></a>輸入

輸入參數之間最多只能有一個資料框架。

資料框架內的物件與函式的其他所有輸入參數，皆必須是下列 R 資料類型：
- POSIXct
- numeric
- character
- integer
- 邏輯
- 未經處理的

如果輸入類型不是上述類型之一，就必須將其序列化並以 *未經處理的*形式傳遞給函式。 在此情況下，函式也必須包含可還原序列化輸入項目的程式碼。

### <a name="outputs"></a>輸出

函式可以輸出下列其中一個項目：

- 資料框架，其中包含支援的資料類型。 資料框架中的所有物件都必須使用其中一種支援的資料類型。
- 具名清單，其中包含最多一個資料框架。 清單的所有成員都應該使用其中一種支援的資料類型。
- NULL (如果您的函式未傳回任何結果)

## <a name="step-2-generate-required-objects"></a>步驟 2： 產生所需的物件

R 程式碼已被清除，而且可以當做單一函式呼叫之後，您將使用中的函式**sqlrutils**準備輸入和輸出的形式，可傳遞至建構函式合格後實際建置的套件預存程序。

**sqlrutils**提供定義輸入的資料結構描述和類型，以及定義輸出資料結構描述和類型的函式。 它也可以將 R 物件轉換為需的輸出類型的函式。 您可能會使多個函式呼叫來建立必要的物件，視您的程式碼使用的資料類型而定。

### <a name="inputs"></a>輸入

如果您的函式不接受輸入，針對每個輸入中，呼叫下列函數：

- `setInputData`如果輸入是資料框架
- `setInputParameter`對於所有其他輸入類型

當您進行每個呼叫的函式時，R 建立物件時，您稍後將會傳遞做為引數`StoredProcedure`，以建立完整的預存程序。

### <a name="outputs"></a>輸出

**sqlrutils**提供多個函式，例如 SQL Server 所需 data.frame 還列出轉換 R 物件。
如果您的函式會直接輸出資料框架，而不需先將其包裝到清單中，您即可略過這個步驟。
您也可以略過轉換此步驟中如果您的函式會傳回 NULL。

當轉換清單，或從清單中，取得特定的項目選擇這些函式：

- `setOutputData`如果要從清單中取得的變數資料框架
- `setOutputParameter`所有其他成員的清單

當您進行每個呼叫的函式時，R 建立物件時，您稍後將會傳遞做為引數`StoredProcedure`，以建立完整的預存程序。

## <a name="step-3-generate-the-stored-procedure"></a>步驟 3： 產生預存程序

準備好所有輸入和輸出參數時，呼叫以`StoredProcedure`建構函式。

**使用方式**

`StoredProcedure (func, spName, ..., filePath = NULL ,dbName = NULL, connectionString = NULL, batchSeparator = "GO")`

為了說明，假設您想要建立名為預存程序**sp_rsample**使用這些參數：

- 使用現有的函式**foosql**。 函式根據現有的程式碼中的 R 函數**foo**，但如果要在重寫要符合的需求中所述的函式[本節](#bkmk_rewrite)，和名為更新的功能與**foosql**。
- 使用資料框架**queryinput**做為輸入
- 會產生做為輸出資料框架使用 R 的變數名稱、 **sqloutput**
- 您想要建立 T-SQL 程式碼中的檔案為`C:\Temp`資料夾，以便稍後使用 SQL Server Management Studio 執行

```R
StoredProcedure (foosql, sp_rsample, queryinput, sqloutput, filePath = "C:\\Temp")
```

> [!NOTE]
> 由於您要將檔案寫入檔案系統，您可以省略引數，定義的資料庫連接。

函式的輸出，則可以在 SQL Server 2016 （需要 R 服務） 或 SQL Server 2017 （需要使用 R 的機器學習服務） 的執行個體執行的 T-SQL 預存程序。 

如需其他範例，請參閱封裝的說明，請藉由呼叫`help(StoredProcedure)`從 R 環境。

## <a name="step-4-register-and-run-the-stored-procedure"></a>步驟 4： 註冊並執行預存程序

有兩種方式，您可以執行預存程序：

- 使用 T-SQL、 從任何支援的 SQL Server 2016 或 SQL Server 2017 的執行個體連接的用戶端
- 從 R 環境

這兩種方法需要預存程序登錄中您想要使用預存程序的資料庫。

### <a name="register-the-stored-procedure"></a>暫存預存程序

您可以註冊預存程序中使用 R，或者您可以執行 CREATE PROCEDURE 陳述式在 T-SQL 中。

- 使用 T-SQL。  如果您是使用 T-SQL 更方便，開啟 SQl Server Management Studio （或其他任何可以執行 SQL DDL 命令的用戶端） 執行 CREATE PROCEDURE 陳述式，使用程式碼項目來準備`StoredProcedure`函式。
- 使用。雖然您仍在您的 R 環境中，您可以使用`registerStoredProcedure`函式在**sqlrutils**預存程序註冊資料庫。

  例如，您無法註冊預存程序**sp_rsample**中的執行個體和資料庫中定義*sqlConnStr*，藉此 R 呼叫：

  ```R
  registerStoredProcedure(sp_rsample, sqlConnStr)
  ```


> [!IMPORTANT]
> 不論您是使用 R 或 SQL，您必須執行的陳述式，使用已建立新的資料庫物件的權限的帳戶。

### <a name="run-using-sql"></a>使用 SQL 執行

建立預存程序之後，開啟 使用任何用戶端可支援 T-SQL、 SQL 資料庫的連接，並將預存程序所需之任何參數的值傳遞。

### <a name="run-using-r"></a>執行使用 R

如果您想要執行 R 程式碼，而是從 SQL Server 預存程序，則需要一些額外的準備工作。 例如，如果預存程序需要輸入的值，您必須先設定這些輸入的參數，才能函式可以執行，然後將這些物件傳遞給您的 R 程式碼中的預存程序。

呼叫已備妥的 SQL 預存程序的整體程序如下所示：

1. 呼叫 `getInputParameters` 以取得輸入參數物件的清單。
2. 針對每個輸入參數，定義 `$query` 或設定 `$value` 。
3. 使用 `executeStoredProcedure` 以從 R 開發環境執行預存程序，同時傳遞您所設定的輸入參數物件清單。

## <a name = "samples"></a>範例

這個範例會示範之前和之後的 R 指令碼，從 SQL Server 資料庫取得資料、 執行部分轉換在資料上，並將它儲存到不同的資料庫版本。

這則簡易範例僅用於示範如何讓您更輕鬆地轉換成預存程序的 R 程式碼可能會重新排列。

### <a name="before-code-preparation"></a>在準備程式碼之前


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
> 當您使用 ODBC 連接而不是叫用*RxSqlServerData*函式，您必須開啟連接使用*rxOpen*才能執行資料庫上的作業。


### <a name="after-code-preparation"></a>程式碼的準備之後

在更新版本中的第一行會定義函式名稱。 從原始的 R 解決方案的所有其他程式碼會變成該函式的一部分。

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

[使用 sqlrutils 產生預存程序](../../advanced-analytics/r-services/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)


