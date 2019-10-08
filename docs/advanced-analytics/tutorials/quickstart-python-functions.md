---
title: 撰寫 advanced Python 函式
titleSuffix: SQL Server Machine Learning Services
description: 在本快速入門中，瞭解如何使用 SQL Server Machine Learning 服務撰寫 Python 函式，以進行 advanced 統計計算。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e369e83c99543cc31287932a25949c2ddec98e89
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007718"
---
# <a name="quickstart-write-advanced-python-functions-with-sql-server-machine-learning-services"></a>快速入門：使用 SQL Server Machine Learning 服務撰寫先進的 Python 功能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本快速入門說明如何使用 SQL Server Machine Learning 服務，在 SQL 預存程式中內嵌 Python 數學和公用程式函數。 在 T-sql 中執行複雜的先進統計函數，只需要一行程式碼就能在 Python 中完成。

## <a name="prerequisites"></a>必要條件

- 本快速入門需要使用已安裝 Python 語言的[SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)，來存取 SQL Server 的實例。

  您的 SQL Server 實例可以位於 Azure 虛擬機器或內部部署中。 請注意，預設會停用外部腳本功能，因此您可能需要[啟用外部腳本](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)，並在開始之前確認**SQL Server Launchpad 服務**正在執行。

- 您也需要工具來執行包含 Python 腳本的 SQL 查詢。 您可以使用任何資料庫管理或查詢工具來執行這些腳本，只要它可以連接到 SQL Server 實例，並執行 T-SQL 查詢或預存程式即可。 本快速入門使用[SQL Server Management Studio （SSMS）](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>建立預存程序來產生亂數

為了簡單起見，讓我們使用 Python `numpy` 封裝，此套件預設會安裝並載入至已安裝 Python 的 SQL Server Machine Learning Services 中。 該套件包含數百個用來進行一般統計工作的函式，其中 `random.normal` 函式會在指定標準差和平均值的情況下，使用常態分佈產生指定數目的亂數。

例如，下列 Python 程式碼會在指定標準差3的情況下，傳回100的平均50數位。

```Python
numpy.random.normal(size=100, loc=50, scale=3)
```

若要從 T-sql 呼叫這行 Python，請在 `sp_execute_external_script` 的 Python 腳本參數中新增 Python 函式。 輸出預期會有資料框架，因此請使用 `pandas` 來進行轉換。

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import numpy
import pandas
OutputDataSet = pandas.DataFrame(numpy.random.normal(size=100, loc=50, scale=3));
'
    , @input_data_1 = N'   ;'
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

想要更輕鬆地產生一組不同的亂數？

這在與 SQL Server 結合時很容易。 您可以定義一個預存程式來取得使用者的引數，然後將這些引數當做變數傳遞至 Python 腳本。

```sql
CREATE PROCEDURE MyPyNorm (
      @param1 INT
    , @param2 INT
    , @param3 INT
    )
AS
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import numpy
import pandas
OutputDataSet = pandas.DataFrame(numpy.random.normal(size=mynumbers, loc=mymean, scale=mysd));
'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

- 第一行定義執行預存程序時所需要的每個 SQL 輸入參數。

- 開頭為 `@params` 的行會定義 Python 程式碼所使用的所有變數，以及對應的 SQL 資料類型。

- 緊接在後面的幾行，會將 SQL 參數名稱對應至對應的 Python 變數名稱。

現在您已將 Python 函式包裝在預存程式中，您可以輕鬆地呼叫函式並傳入不同的值，如下所示：

```sql
EXECUTE MyPyNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-python-utility-functions-for-troubleshooting"></a>使用 Python 公用程式功能進行疑難排解

Python 套件提供各種公用程式函式來調查目前的 Python 環境。 如果您的 Python 程式碼在 SQL Server 和外部環境中執行的方式不一致，這些函式會很有用。

例如，您可以使用 `time` 封裝中的系統計時函數來測量 Python 進程所使用的時間量，並分析效能問題。

```sql
EXECUTE sp_execute_external_script
      @language = N'Python'
    , @script = N'
import time
start_time = time.time()

# Run Python processes

elapsed_time = time.time() - start_time
'
    , @input_data_1 = N' ;';
```

## <a name="next-steps"></a>後續步驟

若要在 SQL Server 中使用 Python 建立機器學習模型，請遵循此快速入門：

> [!div class="nextstepaction"]
> [快速入門：使用 SQL Server Machine Learning Services @ no__t-0，在 Python 中建立和評分預測模型

如需 SQL Server Machine Learning 服務的詳細資訊，請參閱：

- [什麼是 SQL Server Machine Learning 服務（Python 和 R）？](../what-is-sql-server-machine-learning.md)
