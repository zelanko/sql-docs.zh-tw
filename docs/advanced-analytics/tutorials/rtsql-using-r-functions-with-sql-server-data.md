---
title: "R 函式中使用 SQL Server 資料 (SQL 快速入門中的 R) |Microsoft 文件"
ms.custom: 
ms.date: 07/26/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
dev_langs:
- R
- SQL
ms.assetid: e2fe5d90-eee9-4daf-9eae-21d17b3ef320
caps.latest.revision: "8"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0a536b0d569fba36c84b550bec0b60896b448e45
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2017
---
# <a name="using-r-functions-with-sql-server-data-r-in-sql-quickstart"></a>R 函式中使用 SQL Server 資料 (SQL 快速入門中的 R)

您已經熟悉基本的作業，現在可以開始使用 R。例如，許多進階統計函式若使用 T-SQL 來實作可能會很複雜，但卻只需要單行的 R 程式碼。  透過 R 服務，您可以輕鬆地在預存程序中內嵌 R 公用程式指令碼。

在這些範例中，您將會在 SQL Server 預存程序中內嵌 R 數學和公用程式函式。

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>建立預存程序來產生亂數

為了簡單起見，我們使用 R`stats`套件，如此已安裝並與 R Services 的預設載入。 該套件包含數百個用來進行一般統計工作的函式，其中 `rnorm` 函式會在指定標準差和平均值的情況下，使用常態分佈產生指定數目的亂數。

例如，這個 R 程式碼會在指定標準差為 3 的情況下，傳回平均值為 50 的 100 個數字。

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

若要從 T-SQL 呼叫此行的 R，請執行 sp_execute_external_script 並新增 R 指令碼參數中的 R 函式，如下所示：

```sql
EXEC sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'
    , @input_data_1 = N'   ;'
      WITH RESULT SETS (([Density] float NOT NULL));
```

想要更輕鬆地產生一組不同的亂數？

與 SQL Server 結合簡單： 定義從使用者取得的引數的預存程序。 然後，將那些引數做為變數傳入 R 指令碼中。

```sql
CREATE PROCEDURE MyRNorm (@param1 int, @param2 int, @param3 int)
AS
    EXEC sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynumbers, mymean, mysd));'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
    WITH RESULT SETS (([Density] float NOT NULL));
```

+ 第一行定義執行預存程序時所需要的每個 SQL 輸入參數。

+ 開頭為 `@params` 的行會定義 R 程式碼所使用的所有變數，以及對應的 SQL 資料類型。

+ 緊接的行會將 SQL 參數名稱對應至相對應的 R 變數名稱。

現在您已將 R 函式包裝於預存程序中，您將可以輕鬆地呼叫函式並傳入不同的值，如下所示︰

```sql
EXEC MyRNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="related-resources"></a>相關資源

+ 您想要安裝更多的 R 封裝，以取得更多進階的統計函數嗎？ 請參閱[安裝和管理的 R 封裝](../r/installing-and-managing-r-packages.md)。

+ 為了協助您將您的獨立 R 程式碼轉換成的格式，可以輕鬆地參數化使用 SQL Server 預存程序，Microsoft R 團隊提供新的 R 封裝， **sqlrutils**。 如需詳細資訊，請參閱[如何建立預存程序中使用 sqlrutils](../r/how-to-create-a-stored-procedure-using-sqlrutils.md)。

## <a name="use-r-utility-functions-for-troubleshooting"></a>使用 R 公用程式函式進行疑難排解

根據預設，包括 R 安裝`utils`套件，調查目前的 R 環境提供各種不同的公用程式函式。 如果您發現您的 R 程式碼在 SQL Server 和外部環境中的執行方式不一致，這會非常有用。

例如，您可以使用 R `memory.limit()` 函式來取得目前 R 環境的記憶體。 由於 `utils` 套件預設會安裝但不會載入，您必須使用 `library()` 函式先載入它。

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
        library(utils);
        mymemory <- memory.limit();
        OutputDataSet <- as.data.frame(mymemory);'
    , @input_data_1 = N' ;'
WITH RESULT SETS (([Col1] int not null));
```

許多使用者要在 R 中使用系統計時函式，例如`system.time`和`proc.time`，來擷取 R 處理序所使用的時間和分析的效能問題。

如需範例，請參閱此教學課程︰[建立資料功能](../tutorials/walkthrough-create-data-features.md)。 在此逐步解說中，R 計時函式會內嵌在方案中，以比較 R 函式與T-SQL 函式從資料建立功能的效能。

## <a name="next-lesson"></a>下一課

接下來，您將在 SQL Server 中使用 R 建置預測模型。

[建立預測模型](../tutorials/rtsql-create-a-predictive-model-r.md)
