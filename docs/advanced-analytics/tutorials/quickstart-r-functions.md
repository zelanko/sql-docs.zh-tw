---
title: 快速入門：撰寫 R 函式
titleSuffix: SQL Server Machine Learning Services
description: 在本快速入門中，您將了解如何使用 SQL Server 機器學習服務撰寫 R 函數，以進行進階統計計算。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e725282aaacde748b43a37a317037b5471efd009
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73726890"
---
# <a name="quickstart-write-advanced-r-functions-with-sql-server-machine-learning-services"></a>快速入門：使用 SQL Server 機器學習服務撰寫進階 R 函數
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本快速入門說明如何使用 SQL Server 機器學習服務，在 SQL 預存程序中內嵌 R 數學和公用程式函數。 在 T-SQL 中難以執行的進階統計函數，只需要單一程式碼就可以在 R 中完成。

## <a name="prerequisites"></a>Prerequisites

- 本快速入門需使用已安裝 R 語言的 [SQL Server 機器學習服務](../install/sql-machine-learning-services-windows-install.md)來存取 SQL Server 的執行個體。

  您的 SQL Server 執行個體可以位於 Azure 虛擬機器或內部部署中。 請注意，外部指令碼功能預設為停用，因此可能需要[啟用外部指令碼](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)，並在開始之前確認 **SQL Server Launchpad 服務**正在執行。

- 您也需要工具來執行包含 R 指令碼的 SQL 查詢。 您可以使用任何資料庫管理或查詢工具來執行這些指令碼，只要該工具可以連線到 SQL Server 執行個體，並執行 T-SQL 查詢或預存程序即可。 本快速入門使用 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>建立預存程序來產生亂數

為了方便作業，讓我們使用 R `stats` 套件；此套件會預設安裝及載入到已安裝 R 的 SQL Server 機器學習服務。 該套件包含數百個用來進行一般統計工作的函式，其中 `rnorm` 函式會在指定標準差和平均值的情況下，使用常態分佈產生指定數目的亂數。

例如，下列 R 程式碼會在指定標準差為 3 的情況下，傳回平均值為 50 的 100 個數字。

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

若要從 T-SQL 呼叫此行的 R，請在 `sp_execute_external_script` 的 R 指令碼參數中新增 R 函數，如下所示：

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'
    , @input_data_1 = N'   ;'
      WITH RESULT SETS (([Density] float NOT NULL));
```

想要更輕鬆地產生一組不同的亂數？

與 SQL Server 合併時很容易做到。 您可以定義一個預存程序來取得使用者的引數，然後將這些引數當做變數傳遞至 R 指令碼。

```sql
CREATE PROCEDURE MyRNorm (
    @param1 INT
    , @param2 INT
    , @param3 INT
    )
AS
EXECUTE sp_execute_external_script @language = N'R'
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
EXECUTE MyRNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-r-utility-functions-for-troubleshooting"></a>使用 R 公用程式函式進行疑難排解

預設安裝的 **utils** 套件可提供用來調查目前 R 環境的各種公用程式函數。 如果您發現您的 R 程式碼在 SQL Server 和外部環境中的執行方式不一致，這些函數會非常有用。

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
> 許多使用者喜歡使用 R 中的系統時間函數 (例如 `system.time` 和 `proc.time`) 來擷取 R 處理序所使用的時間，並分析效能問題。 如需範例，請參閱[建立資料特徵](../tutorials/walkthrough-create-data-features.md)教學課程，其中 R 時間函數會內嵌在解決方案中。

## <a name="next-steps"></a>後續步驟

若要在 SQL Server 中使用 R 建立機器學習模型，請依照此快速入門進行：

> [!div class="nextstepaction"]
> [使用 SQL Server 機器學習服務在 R 中建立預測模型並計算其分數](quickstart-r-train-score-model.md)

如需 SQL Server 機器學習服務的詳細資訊，請參閱：

- [什麼是 SQL Server 機器學習服務 (Python 和 R)？](../what-is-sql-server-machine-learning.md)
