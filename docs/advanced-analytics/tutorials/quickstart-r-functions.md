---
title: 撰寫 advanced R 函數
titleSuffix: SQL Server Machine Learning Services
description: 在本快速入門中，您將瞭解如何使用 SQL Server Machine Learning 服務，撰寫 R 函數來進行高階統計計算。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cebd4ea6a356af6802a0e26f778667b2acc4b80c
ms.sourcegitcommit: 1661c3e1bb38ed12f8485c3860fc2d2b97dd2c9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/20/2019
ms.locfileid: "71149904"
---
# <a name="quickstart-write-advanced-r-functions-with-sql-server-machine-learning-services"></a>快速入門：使用 SQL Server Machine Learning 服務撰寫 advanced R 函數
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本快速入門說明如何使用 SQL Server Machine Learning 服務，在 SQL 預存程式中內嵌 R 數學和公用程式函數。 在 T-sql 中執行複雜的高階統計函數，只需要一行程式碼，就可以在 R 中完成。

## <a name="prerequisites"></a>必要條件

- 本快速入門需要使用已安裝 R 語言的[SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)，來存取 SQL Server 的實例。

  您的 SQL Server 實例可以位於 Azure 虛擬機器或內部部署中。 請注意，預設會停用外部腳本功能，因此您可能需要[啟用外部腳本](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)，並在開始之前確認**SQL Server Launchpad 服務**正在執行。

- 您也需要工具來執行包含 R 腳本的 SQL 查詢。 您可以使用任何資料庫管理或查詢工具來執行這些腳本，只要它可以連接到 SQL Server 實例，並執行 T-SQL 查詢或預存程式即可。 本快速入門使用[SQL Server Management Studio （SSMS）](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>建立預存程序來產生亂數

為了簡單起見，讓我們使用 r `stats`封裝，預設會在安裝 r 的 SQL Server Machine Learning 服務中安裝並載入。 該套件包含數百個用來進行一般統計工作的函式，其中 `rnorm` 函式會在指定標準差和平均值的情況下，使用常態分佈產生指定數目的亂數。

例如，下列 R 程式碼會在指定標準差3的情況下，傳回平均值為50的100數位。

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

若要從 t-sql 呼叫這行 r，請在的 r 腳本參數`sp_execute_external_script`中新增 r 函數，如下所示：

```sql
EXEC sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'
    , @input_data_1 = N'   ;'
      WITH RESULT SETS (([Density] float NOT NULL));
```

想要更輕鬆地產生一組不同的亂數？

這在與 SQL Server 結合時很容易。 您可以定義一個預存程式來取得使用者的引數，然後將這些引數當做變數傳遞至 R 腳本。

```sql
CREATE PROCEDURE MyRNorm (
    @param1 INT
    , @param2 INT
    , @param3 INT
    )
AS
EXEC sp_execute_external_script @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynumbers, mymean, mysd));'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

- 第一行定義執行預存程序時所需要的每個 SQL 輸入參數。

- 開頭為 `@params` 的行會定義 R 程式碼所使用的所有變數，以及對應的 SQL 資料類型。

- 緊接的行會將 SQL 參數名稱對應至相對應的 R 變數名稱。

現在您已將 R 函式包裝於預存程序中，您將可以輕鬆地呼叫函式並傳入不同的值，如下所示︰

```sql
EXEC MyRNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-r-utility-functions-for-troubleshooting"></a>使用 R 公用程式函式進行疑難排解

預設安裝的**utils**封裝提供各種公用程式函式來調查目前的 R 環境。 如果您的 R 程式碼在 SQL Server 和外部環境中執行的方式不一致，這些函式會很有用。

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

> [!TIP]
> 許多使用者想要使用 r 中的系統計時函數（例如`system.time`和`proc.time`）來捕捉 r 進程所使用的時間，並分析效能問題。

如需範例，請參閱此教學課程：[建立資料特徵](../tutorials/walkthrough-create-data-features.md)。 在此逐步解說中，R 計時函式會內嵌在解決方案中，以比較 R 函數的效能與用來從資料建立特徵的 t-sql 函數。

## <a name="next-steps"></a>後續步驟

如需 SQL Server Machine Learning 服務的詳細資訊，請參閱：

- [什麼是 SQL Server Machine Learning 服務（Python 和 R）？](../what-is-sql-server-machine-learning.md)
