---
title: 設定用於 SQL Server Machine Learning Python 用戶端工具 |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: ace5ea536c020d2713f1aa07bd1b26c41065a587
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
ms.locfileid: "31203800"
---
# <a name="set-up-python-client-tools-for-use-with-sql-server-machine-learning"></a>設定用戶端工具，搭配 SQL Server 機器學習使用 Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何設定 Python 環境以支援 SQL Server 中執行 Python 程式碼的 Windows 電腦上。 這包括下列案例：

+ 測試和開發解決方案的遠端 Python 工作站上，並送到 SQL Server 的程式碼，在 SQL Server 計算內容中執行時。 

    您通常想要安裝完整的 Python 開發環境。 
    
    本機 Python 環境應該與 SQL Server 執行個體上的 Python 環境相容，而且您必須安裝支援遠端計算內容的文件庫。

+ 您開發和測試使用專用的 Python 工具的程式碼，並再移轉到 SQL Server 來執行預存程序中的 程式碼。

    您可以使用完整的 Python IDE 進行開發，請關閉伺服器。 不過，在部署您的程式碼之前，您測試模擬 SQL Server 環境的環境中。

+ 您主要是在 SQL Server 中的預存程序中執行 Python 程式碼，您並未開發 Python 程式碼。 您會預期程式碼具有測試和偵錯之前將它包裝在預存程序。 不過，偶爾您可能需要執行 SQL Server，以判斷問題來源之外的程式碼。

    您不想要在伺服器上，安裝任何的 Python 工具，並使用只安裝與分配的預設工具。 您可能會決定設定使用執行個體文件庫中，以確認程式碼可以運作，在預存程序之外的 Python 環境。

## <a name="requirements"></a>需求

不論您用來開發您的 Python 程式碼的工具，每當您在 SQL Server 中執行 Python 程式碼或使用 SQL Server 資料時適用下列需求：

+ 若要使用 Python，2017年或更新版本的 SQL Server 是必要的。 您必須同時安裝功能，支援機器學習服務 （資料庫），並明確地啟用此功能。 如需詳細資訊，請參閱[設定 SQL Server 2017](../r/set-up-sql-server-r-services-in-database.md)。

    如果您安裝 SQL Server 2017 早期發行版本，您可能會收到錯誤，如果您嘗試此命令列公用程式從執行 Python 指令。 我們建議您[升級至最新版本](#bkmk_update)的話。 

+ 您必須確定您執行的程式碼使用的帳戶已連接到資料庫，以及執行 Python 程式碼的權限。 特殊權限`EXECUTE ANY EXTERNAL SCRIPT`無須使用 R 或 Python 指令碼的所有帳戶。 

+ 您必須確定的帳戶具有資料庫的權限，可能會要求讀取資料，或建立新物件。 

+ 如果您的程式碼需要使用 SQL Server 預設不會安裝的封裝，來排列與資料庫管理員的執行個體使用 Python 環境中安裝的封裝。 SQL Server 安全的環境，且有一些限制可以安裝封裝。 

    不建議隨安裝封裝做為您的程式碼的一部分，即使您沒有權限。 此外，請慎重考慮的安全性含意伺服器文件庫中安裝新的封裝之前。

> [!NOTE]
> 如果您想要使用 Python 與機器學習伺服器支援額外的計算內容，例如 Linux 或 Spark 叢集，請參閱下列文章：
> 
> + [如何自訂 Python 封裝和解譯器本機上安裝 Windows](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)
> + [連結的 Python 工具和 Ide Python 解譯器安裝在機器學習伺服器](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)

## <a name="default-tools-included-with-standard-install"></a>標準安裝所隨附的預設工具

預設安裝的 SQL Server 2017 使用機器學習服務 （資料庫），並將 Python 新增下列標準的 Python 工具和資源：

+ Python 範例資料
+ Anaconda 4.2 發佈 
+ Python 可執行檔 python.exe 和 pythonw.exe

根據預設，安裝為此資料夾： `~\Program Files\Microsoft SQL Server\<instance_name>\PYTHON_SERVICES`。 

## <a name="open-python-from-the-command-line"></a>從命令列開啟 Python 

若要使用 Python 執行階段與執行個體一起安裝，您可以從安裝路徑來啟動可執行 Python。 使用上的基本指示[Python 的 Windows 常見問題集](https://docs.python.org/3/faq/windows.html)。

> [!IMPORTANT]
> 一般而言，若要避免資源爭用的情況，我們建議您**不**Python 從執行個體的程式庫伺服器上執行，如果您認為可能是 SQL Server 執行個體的 Python 程式碼。 不過，執行個體文件庫中使用的工具可能會有價值，如果您嘗試偵錯 SQL Server 中執行時，才會發生的問題，並想要檢視更詳細的錯誤訊息，或請確定已安裝所有必要的封裝。

1. 瀏覽至安裝執行個體文件庫的資料夾。 例如，在預設安裝資料夾是`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`。

2. 找出 Python.exe。 

3. 以滑鼠右鍵按一下並選取**系統管理員身分執行**開啟互動式命令列視窗。

## <a name="bkmk_update"></a> 更新 Python 元件

您可以更新 Python 元件下載和安裝較新版本，使用此處所述的指令碼： [Windows 上的安裝 Python 用戶端](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter#install-on-windows)
> 
> 安裝程式下載的指令碼是[SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054&clcid=1033)。 如果您需要不同的版本，請參閱[安裝沒有網際網路存取的機器學習服務元件](http://bing.com)

## <a name="set-up-a-python-development-environment"></a>Python 開發環境設定

如果您只需從命令列指令碼，您可以取得機器學習服務，以安裝的標準的 Python 工具，或使用文字編輯器。 不過，如果您正在開發新的解決方案，或從遠端用戶端，建議使用的是功能完整的 Python IDE。 常用的選項如下：

+ [Visual Studio 2017 Community Edition](https://www.visualstudio.com/vs/features/python/)使用 Python
+ [AI 適用於 Visual Studio 工具](https://docs.microsoft.com/visualstudio/ai/installation)
+ [在 Visual Studio 程式碼中的 Python](https://code.visualstudio.com/docs/languages/python)
+ 受歡迎的協力廠商工具，例如 PyCharm、 Spyder 和 Eclipse

我們建議 Visual Studio，因為它支援的資料庫專案，以及您在機器學習服務專案。 如需設定的 Python 環境的說明，請參閱[Visual Studio 中的管理 Python 環境](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)

## <a name="install-revoscalepy"></a>安裝 revoscalepy

即使您已成功安裝的機器學習服務，您可能會發生錯誤時嘗試載入**revoscalepy** Python 命令列從函式。 這些步驟說明如何安裝更新，以便使用**revoscalepy**。

1. 下載安裝殼層指令碼，從https://aka.ms/mls93-py(或使用https://aka.ms/mls-py9.2 的。 發行）。 指令碼安裝 Anaconda 4.2.0，包含 Python 3.5.2，以及先前所列的所有封裝。

2. （以系統管理員身分），以更高權限開啟新的 PowerShell 視窗。

3. 開啟您下載安裝程式的資料夾，並執行指令碼：

```ps1
cd {{download-directory}}
.\Install-PyForMLS.ps1
```

您也可以執行`-InstallFolder`命令列引數，並指定新路徑，做為命令的一部分。 例如： 

```ps1
.\Install-PyForMLS.ps1 -InstallFolder "<installation_path>")
```

如果您收到錯誤，您可能需要暫停特定的檔案，執行原則的工作階段中，持續時間，如下所示： 

```ps1
powershell -ExecutionPolicy Bypass -File "C:\<installation_path>\Install-PyForMLS.ps1"
```

您也可以暫停工作階段期間執行原則。 使用此陳述式中，執行原則設定為`Unrestricted`持續時間的工作階段，而且不變更設定或變更寫入磁碟。

```ps1
Set-ExecutionPolicy Bypass -Scope Process
```

## <a name="verify-that-python-and-revoscalepy-are-working"></a>確認 Python 和 revoscalepy 正常

安裝所有工具和程式庫之後，您應該連接到伺服器，並確認您可以建立計算內容，或 Python 可與 SQL Server 通訊。

### <a name="verify-that-revoscalepy-works-from-the-python-command-line"></a>請確認該 revoscalepy 的運作方式與 Python 命令列

若要確認**revoscalepy**可以載入模組，Python 互動式命令提示字元執行下列範例程式碼。 程式碼會產生資料摘要使用 Python 範例資料和[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)。 

```Python
import os
from revoscalepy import rx_summary
from revoscalepy import RxXdfData
from revoscalepy import RxOptions
sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)
ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay+DayOfWeek", ds)
print(summary)
```

範例資料路徑，以便決定呼叫哪一個執行個體的 Python 列印。

### <a name="verify-that-python-can-be-called-from-sql-server"></a>驗證從 SQL Server，可以呼叫 Python

若要確認 Python 與 SQL Server 通訊，請開啟 SQL Server Management Studio。 (您可以使用另一個類似的工具，例如[SQL 作業 Studio](https://docs.microsoft.com/sql/sql-operations-studio/what-is)。)開啟新**查詢**視窗並執行預存程序的內容中的任何簡單的 Python 命令：

```SQL
EXEC sp_execute_external_script @language = N'Python', 
@script = N'print(3+4)'
```

它可能需要一段 Python 執行階段啟動第一次，但如果有任何錯誤，您知道 SQL Server Launchpad 運作正常，而且可以從 SQL Server 啟動 Python。

若要可讓您確認**revoscalepy**可在 SQL Server 執行個體庫中，執行指令碼，根據[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)，有一些有些微修改，以產生結果與 SQL Server 相容。 

```SQL
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

因為 rx_summary 傳回型別的物件`class revoscalepy.functions.RxSummary.RxSummaryResults`，其中包含多個項目，來處理 SQL Server 中的結果，您可以擷取資料框架中表格的格式。

### <a name="verify-python-execution-in-sql-server-as-remote-compute-context"></a>確認 SQL Server 中的 Python 執行做為遠端計算內容

如果您已安裝**revoscalepy**在您本機的 Python 開發環境，您也應該能夠連線到執行個體的 SQL Server 2017 其中 Python 已啟用，並執行類似的程式碼範例使用為計算的伺服器內容。 


```Python
import os
from revoscalepy import rx_summary, RxOptions, RxXdfData, RxSqlServerData, RxInSqlServer

# define connection string and compute context
sql_conn_string="Driver=SQL Server;Server=;Database=TestDB;Trusted_Connection=True"
sqlcc = RxInSqlServer(
    connection_string = sql_conn_string,
    num_tasks = 1,
    auto_cleanup = False,
    console_output = True,
    execution_timeout_seconds = 0,
    wait = True
    )
rx_set_compute_context(sqlcc)

# get sample data and path
sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)

# generate summary
ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay+DayOfWeek", ds)
print(summary)
```

在此範例中，主控台中，而不被傳回格式正確的表格式資料到 SQL Server 會傳回摘要的物件。 

此外，因為[rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context)已叫用，範例資料載入從 [samples] 資料夾的 SQL Server 電腦上，而不是從您的本機範例資料夾。
