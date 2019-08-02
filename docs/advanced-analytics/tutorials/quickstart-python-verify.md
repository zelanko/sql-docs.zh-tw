---
title: SQL Server 中存在驗證 Python 的快速入門
description: 驗證 SQL Server 中是否有 Python 和 Machine Learning 服務的快速入門。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 98e89cf61e5c53793108a455873382da00a8ea35
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715448"
---
# <a name="quickstart-verify-python-exists-in-sql-server"></a>快速入門：驗證 Python 存在於 SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 包含適用于常駐 SQL Server 資料之資料科學分析的 Python 語言支援。 腳本執行是透過預存程式, 使用下列其中一種方法:

+ 內建的[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)預存程式, 以輸入參數的形式傳遞 Python 腳本。
+ 將 Python 腳本包裝在您建立的[自訂預存](sqldev-in-database-r-for-sql-developers.md)程式中。

在本快速入門中, 您將確認已安裝並設定[SQL Server Machine Learning 服務](../what-is-sql-server-machine-learning.md)。

## <a name="prerequisites"></a>必要條件

此練習需要存取已安裝[SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)的 SQL Server 實例。

您的 SQL Server 實例可以位於 Azure 虛擬機器或內部部署中。 請注意, 預設會停用外部腳本功能, 因此您可能需要[啟用外部腳本](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature), 並在開始之前確認**SQL Server Launchpad 服務**正在執行。

您也需要用來執行 SQL 查詢的工具。 您可以使用任何資料庫管理或查詢工具來執行 Python 腳本, 只要它可以連接到 SQL Server 實例, 並執行 T-SQL 查詢或預存程式即可。 本快速入門使用[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="verify-python-exists"></a>確認 Python 存在

您可以確認 Machine Learning 服務 (已針對您的 SQL Server 實例和安裝的 Python 版本啟用)。 請遵循下列步驟。

1. 開啟 SQL Server Management Studio, 並連接到您的 SQL Server 實例。

2. 執行下列程式碼。 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import sys
    print(sys.version)';
    GO
    ```

3. Python `print`函式會將版本傳回至 [**訊息**] 視窗。 在下面的範例輸出中, 您可以看到此案例中的 SQL Server 已安裝 Python 版本3.5.2。

    **結果**

    ```text
    STDOUT message(s) from external script: 
    3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
    ```

如果您收到錯誤, 您可以執行各種動作, 以確保實例和 Python 可以進行通訊。

首先, 請排除任何安裝問題。 必須安裝後續設定, 才能啟用外部程式碼程式庫的使用。 請參閱[安裝 SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)。 同樣地, 請確定啟動列服務正在執行。

您也必須將 Windows 使用者群組`SQLRUserGroup`新增為實例上的登入, 以確保啟動列可以提供 Python 和 SQL Server 之間的通訊。 (相同的群組用於 R 和 Python 程式碼執行)。如需詳細資訊, 請參閱[建立 SQLRUserGroup 的登](../security/create-a-login-for-sqlrusergroup.md)入。

此外, 您可能需要啟用已停用的網路通訊協定, 或開啟防火牆, 讓 SQL Server 可以與外部用戶端通訊。 如需詳細資訊, 請參閱[疑難排解設定](../common-issues-external-script-execution.md)。

## <a name="call-revoscalepy-functions"></a>呼叫 revoscalepy 函式

若要確認**revoscalepy**可供使用, 請執行包含產生統計摘要資料之[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)的範例腳本。 下列腳本示範如何從 revoscalepy 所包含的內建範例中, 取出 xdf 資料檔案。 RxOptions 函數會提供**sampleDataDir**參數, 以傳回範例檔案的位置。

由於 rx_summary 會傳回類型`class revoscalepy.functions.RxSummary.RxSummaryResults`為的物件, 其中包含多個元素, 因此您可以使用 pandas, 以表格格式只解壓縮資料框架。

```sql
EXEC sp_execute_external_script @language = N'Python', 
@script = N'
import os
from pandas import DataFrame
from revoscalepy import rx_summary
from revoscalepy import RxXdfData
from revoscalepy import RxOptions

sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)

ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay + DayOfWeek", ds)
print(summary)
dfsummary = summary.summary_data_frame
OutputDataSet = dfsummary
'
WITH RESULT SETS  ((ColName nvarchar(25) , ColMean float, ColStdDev  float, ColMin  float,   ColMax  float, Col_ValidObs  float, Col_MissingObs int))
```

## <a name="list-python-packages"></a>列出 Python 套件

Microsoft 提供一些在您的 SQL Server 實例中預先安裝了 Machine Learning 服務的 Python 套件。 若要查看已安裝的 Python 套件清單 (包括版本), 請遵循下列步驟。

1. 在您的 SQL Server 實例上執行下列腳本。

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import pip
    for i in pip.get_installed_distributions():
        print(i)';
    GO
    ```

2. 輸出來自`pip.get_installed_distributions()`于 Python 中的, 並以`STDOUT`訊息的形式傳回。

    **結果**

    ```text
    STDOUT message(s) from external script: 
    xlwt 1.2.0
    XlsxWriter 0.9.6
    xlrd 1.0.0
    win-unicode-console 0.5
    widgetsnbextension 2.0.0
    wheel 0.29.0
    Werkzeug 0.12.1
    wcwidth 0.1.7
    unicodecsv 0.14.1
    traitlets 4.3.2
    tornado 4.4.2
    toolz 0.8.2
    testpath 0.3
    tables 3.2.2
    sympy 1.0
    statsmodels 0.8.0
    sqlparse 0.1.19
    SQLAlchemy 1.1.9
    snowballstemmer 1.2.1
    six 1.10.0
    simplegeneric 0.8.1
    seaborn 0.7.1
    scipy 0.19.0
    scikit-learn 0.18.1
    ...
    ```

## <a name="next-steps"></a>後續步驟

既然您已確認您的實例已準備好使用 Python, 請仔細查看基本的 Python 互動。

> [!div class="nextstepaction"]
> [入門SQL Server 中的 "Hello world" Python 腳本](quickstart-python-run-using-t-sql.md)
