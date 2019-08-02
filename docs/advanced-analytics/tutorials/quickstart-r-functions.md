---
title: 顯示 R 函數的快速入門-SQL Server Machine Learning
description: 在本快速入門中, 您將瞭解如何撰寫 R 函數來進行 advanced 統計計算。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0f81b4f755441a5129892ed321d74bb8c6427ee4
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714838"
---
# <a name="quickstart-using-r-functions"></a>快速入門：使用 R 函式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

如果您已完成先前的快速入門, 您就會熟悉基本作業, 並準備好進行更複雜的工作, 例如統計函數。 在 T-sql 中執行複雜的高階統計函數, 只需要一行程式碼, 就可以在 R 中完成。

在本快速入門中, 您將在 SQL Server 預存程式中內嵌 R 數學和公用程式函數。

## <a name="prerequisites"></a>先決條件

先前的快速入門[中, 驗證 R 存在於 SQL Server 中](quickstart-r-verify.md), 提供設定本快速入門所需之 R 環境的相關資訊和連結。

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>建立預存程序來產生亂數

為了簡單起見, 讓我們使用 r `stats`封裝, 當您在 SQL Server 中安裝 R 功能支援時, 預設會安裝並載入該套件。 該套件包含數百個用來進行一般統計工作的函式，其中 `rnorm` 函式會在指定標準差和平均值的情況下，使用常態分佈產生指定數目的亂數。

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

這在結合 SQL Server 時很簡單: 定義可從使用者取得引數的預存程式。 然後，將那些引數做為變數傳入 R 指令碼中。

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

根據預設, R 的安裝會包含`utils`封裝, 它會提供各種公用程式函式來調查目前的 R 環境。 如果您發現您的 R 程式碼在 SQL Server 和外部環境中的執行方式不一致，這會非常有用。

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

許多使用者想要使用 r 中的系統計時函數 (例如`system.time`和`proc.time`) 來捕捉 r 進程所使用的時間, 並分析效能問題。

如需範例, 請參閱此教學課程:[建立資料特徵](../tutorials/walkthrough-create-data-features.md)。 在此逐步解說中, R 計時函式內嵌于方案中, 以比較兩個方法從資料建立特徵的效能:R 函數與T-SQL 函式從資料建立功能的效能。

## <a name="next-steps"></a>後續步驟

接下來，您將在 SQL Server 中使用 R 建置預測模型。

> [!div class="nextstepaction"]
> [入門建立預測模型](quickstart-r-create-predictive-model.md)
