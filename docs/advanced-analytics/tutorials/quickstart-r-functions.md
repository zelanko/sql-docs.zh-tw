---
title: 說明 R 函式-SQL Server Machine Learning 的快速入門
description: 在本快速入門，了解如何撰寫適用於進階統計運算的 R 函式。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: fa2d47729641e8efd13e9e30be7a61186a892b5c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962016"
---
# <a name="quickstart-using-r-functions"></a>快速入門：使用 R 函式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

如果您已完成先前的快速入門，您已熟悉基本作業，而且準備好進行更為複雜，例如統計函數。 在 T-SQL 中實作複雜的進階統計函式可以在 R 中使用只有一行程式碼。

在本快速入門中，您將內嵌 R 數學和公用程式函式，在 SQL Server 預存程序。

## <a name="prerequisites"></a>先決條件

先前的快速入門中，[確認 R 存在於 SQL Server](quickstart-r-verify.md)，提供資訊並連結設定本快速入門所需的 R 環境。

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>建立預存程序來產生亂數

為了簡單起見，讓我們使用 R`stats`套件會安裝並載入根據預設，當您安裝 SQL Server 中的 R 功能的支援。 該套件包含數百個用來進行一般統計工作的函式，其中 `rnorm` 函式會在指定標準差和平均值的情況下，使用常態分佈產生指定數目的亂數。

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

很簡單，結合 SQL Server 時： 定義從使用者取得的引數的預存程序。 然後，將那些引數做為變數傳入 R 指令碼中。

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

## <a name="use-r-utility-functions-for-troubleshooting"></a>使用 R 公用程式函式進行疑難排解

根據預設，R 的安裝包含`utils`套件，其提供用於調查目前 R 環境的各種不同的公用程式函式。 如果您發現您的 R 程式碼在 SQL Server 和外部環境中的執行方式不一致，這會非常有用。

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

許多使用者想要在 R 中使用系統時間函式，例如`system.time`和`proc.time`，以擷取 R 處理序所使用的時間，並分析效能問題。

如需範例，請參閱本教學課程：[建立資料特徵](../tutorials/walkthrough-create-data-features.md)。 在本逐步解說中，R 計時函式被內嵌在方案，以比較兩種方法從資料建立特徵的效能：R 函式與T-SQL 函式從資料建立功能的效能。

## <a name="next-steps"></a>後續步驟

接下來，您將在 SQL Server 中使用 R 建置預測模型。

> [!div class="nextstepaction"]
> [快速入門：建立預測模型](quickstart-r-create-predictive-model.md)
