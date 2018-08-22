---
title: 設定適用於搭配 SQL Server Machine Learning Python 用戶端工具 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/21/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6f6823870060992586756dffa93aac6937d27d65
ms.sourcegitcommit: 9528843359cc43b9c66afac363f542ae343266e9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/22/2018
ms.locfileid: "40401298"
---
# <a name="set-up-python-client-tools-for-use-with-sql-server-machine-learning"></a>設定 Python 與 SQL Server Machine Learning 搭配使用的用戶端工具
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

使用從 SQL Server 2017 或更新版本中，當您將新增到 Machine Learning 服務 （資料庫） 的 Python 支援 Python 整合。 如需詳細資訊，請參閱 <<c0> [ 安裝 SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)。

在本文中，了解如何設定開發工作站，以便您可以連線到啟用適用於 Python 的遠端 SQL Server。

### <a name="evaluation-and-independent-development"></a>評估和獨立的開發
 
如果您有 developer 版和計劃要在本機處理 Python 指令碼想要移至 SQL Server，您可以跳到[安裝 IDE](#install-ide)指向本機 SQL Server 所使用的 Python 程式庫中的工具。

> [!Tip]
> 如需示範和影片逐步解說，請參閱[執行的 R 和遠端 SQL Server 從 Jupyter Notebook 或任何 IDE 中的 Python](https://blogs.msdn.microsoft.com/mlserver/2018/07/10/run-r-and-python-remotely-in-sql-server-from-jupyter-notebooks-or-any-ide/)或這[YouTube 影片](https://youtu.be/D5erljpJDjE)。

## <a name="1---install-python-packages"></a>1-安裝 Python 套件

本機工作站必須有相同的 Python 套件版本的 SQL Server 上： revoscalepy 和 microsftml。 其他的 Python 套件可供使用，但比較常搭配獨立 （非執行個體） 的 Machine Learning 伺服器內容中的其他案例。 

1. 下載安裝殼層指令碼，從[ https://aka.ms/mls93-py ](https://aka.ms/mls93-py) (或使用[ https://aka.ms/mls-py ](https://aka.ms/mls-py) 9.2 的。 發行版本）。 指令碼安裝 Anaconda 4.2.0，其中包含 Python 3.5.2，以及先前所列的所有封裝。

  透過提供 Python 元件[SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054&clcid=1033)。 如果您需要不同的版本，請參閱[CAB 下載](../install/sql-ml-cab-downloads.md)

2. 開啟提升權限的系統管理員權限的 PowerShell 視窗 (以滑鼠右鍵按一下**系統管理員身分執行**)。

3. 請移至您下載安裝程式的資料夾，並執行指令碼。 新增`-InstallFolder`命令列引數，來指定程式庫的資料夾位置。 例如： 

   ```python
   cd {{download-directory}}
   .\Install-PyForMLS.ps1 -InstallFolder "C:\path-to-python-for-mls")
   ```

   安裝需要一些時間才能完成。 您可以監視進度，在 PowerShell 視窗中。 安裝程式完成時，您會有一組完整的封裝。 例如，如果您指定`C:\mspythonlibs`作為資料夾名稱，您會發現在封裝`C:\mspythonlibs\Lib\site-packages`。 否則，預設資料夾是`C:\Program Files\Microsoft\PyForMLS1`。

安裝指令碼不會修改您的電腦上的 PATH 環境變數，因此新的 python 解譯器和您剛才安裝的模組不會自動提供給您的工具。 在將 Python 解譯器和程式庫連結至工具的協助，請參閱[5-安裝 IDE](#install-ide)。

<a name="python-tool"></a>
 
## <a name="2---open-a-python-prompt"></a>2-開啟 Python 提示字元

在 Microsoft 中的 Python 整合包括內建的工具和產品專屬程式庫，例如 revoscalepy 和 microsoftml 除了資料。 安裝程式完成時，才會在用戶端和伺服器執行個體上，您可以使用下列項目：

+ Python 範例資料
+ Anaconda 4.2 散發套件 
+ Python 可執行檔 python.exe 和 pythonw.exe

> [!Tip] 
> 我們建議[Python for Windows 常見問題集](https://docs.python.org/3/faq/windows.html)如需在 Windows 上執行 Python 程式的一般 purppose 資訊。

### <a name="on-client-workstations"></a>用戶端工作站上

若要使用安裝指令碼安裝的 Python 可執行檔：

1. 移至`C:\Program Files\Microsoft\PyForMLS\python.exe`或您選擇的安裝路徑的任何位置。

2. 以滑鼠右鍵按一下**Python.exe** ，然後選取**系統管理員身分執行**開啟互動式命令列視窗。

### <a name="on-sql-server"></a>SQL Server 上

SQL Server 安裝程式會將標準的 Python 工具和資源加入至伺服器執行個體。 如果您正在使用 developer edition，而且想要檢查的 Python 版本，或執行臨機操作的命令：

1. 移至`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`。

2. 以滑鼠右鍵按一下**Python.exe** ，然後選取**系統管理員身分執行**開啟互動式命令列視窗。

> [!Note]
> 一般而言，若要避免資源爭用，我們建議您**沒有**Python 從執行個體的程式庫伺服器上執行，如果您認為可能的 SQL Server 執行個體正在執行 Python 程式碼。 不過，執行個體文件庫中使用的工具可能很重要，如果您嘗試偵錯 SQL Server 中執行時，才會發生的問題，並想要檢視更詳細的錯誤訊息，或請確定已安裝所有必要的套件。

## <a name="3---permissions"></a>3-權限

若要連接到執行指令碼，並上傳資料的 SQL Server 的執行個體，您必須具有有效的登入資料庫伺服器上。 您可以使用 SQL 登入或整合式 Windows 驗證。 我們通常建議使用 Windows 整合式的驗證，但使用 SQL 登入是在某些情況下更簡單。

最小值，用來執行程式碼的帳戶必須具有您正在使用，再加上特殊權限執行的任何外部指令碼，從資料庫讀取的權限。 大部分的開發人員也需要在包含您的指令碼的預存程序的形式中建立新物件的權限和資料寫入其中包含定型資料的資料表或評分的資料。 

詢問資料庫管理員，以便您用來使用 Python 的資料庫中設定下列權限的帳戶：

+ **EXECUTE ANY EXTERNAL SCRIPT**伺服器上執行 Python。
+ **db_datareader**權限才能執行用來定型模型的查詢。
+ **db_datawriter**撰寫定型資料或評分的資料。
+ **db_owner**為了建立物件，例如預存程序，資料表，函式。 
  您也需要**db_owner**建立範例和測試資料庫。 

如果您的程式碼需要使用 SQL Server 預設不會安裝的封裝，來排列資料庫系統管理員，以具有安裝與執行個體的套件。 SQL Server 是安全的環境，並限制可安裝套件的位置。 不建議為您的程式碼的一部分臨機操作安裝封裝，即使您有權限。 此外，請務必仔細考慮安全性隱含意義 server 文件庫中安裝新套件之前。

## <a name="4---test-connections"></a>4-測試連接

安裝所有工具和程式庫之後，您應該連接到伺服器，並確認您可以建立計算內容，或 Python 可以與 SQL Server 通訊。

### <a name="verify-that-revoscalepy-works-from-the-python-command-line"></a>請確認該 revoscalepy 的運作方式與 Python 命令列

若要確認**revoscalepy**可以載入模組，從 Python 互動式命令提示字元執行下列的範例程式碼。 程式碼會產生資料摘要使用 Python 的範例資料並[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)。 

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

範例資料路徑會列印，如此您就可以判斷哪一個執行個體的 Python 呼叫。

### <a name="verify-that-python-can-be-called-from-a-local-sql-server"></a>驗證可以呼叫 Python，從本機的 SQL Server

在本機開發環境中，確認 Python 會與本機通訊[外部指令碼處理所設定的 SQL Server 執行個體](../install/sql-machine-learning-services-windows-install.md)。 使用 SQL Server Management Studio 來開啟新**查詢**視窗並執行預存程序的內容中的任何簡單的 Python 命令：

```SQL
EXEC sp_execute_external_script @language = N'Python', 
@script = N'print(3+4)'
```

可能需要一段時間，第一次，啟動 Python 執行階段，但如果沒有任何錯誤，您知道 SQL Server Launchpad 正常運作，而且可以從 SQL Server 啟動 Python。

若要確認**revoscalepy**可在 SQL Server 執行個體庫中，執行指令碼，根據[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)，但有一些些微的修改，以產生與 SQL Server 相容的結果。 

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

因為 rx_summary 傳回型別的物件`class revoscalepy.functions.RxSummary.RxSummaryResults`，其中包含多個項目，來處理 SQL Server 中的結果，您可以擷取資料框架以表格格式。

### <a name="verify-python-execution-in-sql-server-as-remote-compute-context"></a>確認 SQL Server 中的 Python 執行作為遠端計算內容

如果您已安裝**revoscalepy**在本機 Python 開發環境中，您應該能夠連線到已啟用，Python，SQL Server 2017 的遠端執行個體，並執行使用與伺服器的類似程式碼範例計算內容。 

若要執行此指令碼，請指定有效的伺服器名稱和現有的資料庫。 這個指令碼不會使用資料庫，但連接字串需要它。

```Python
import os
from revoscalepy import rx_summary, RxOptions, RxXdfData, RxSqlServerData, RxInSqlServer

# define connection string and compute context
sql_conn_string="Driver=SQL Server;Server=<server-name>;Database=TestDB;Trusted_Connection=True"
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

此外，因為[rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context)已叫用範例資料載入從 SQL Server 電腦上的 [samples] 資料夾，而不是從您的本機的範例資料夾。


<a name="install-ide"></a>

## <a name="5---install-an-ide"></a>5-安裝 IDE

如果您只需偵錯指令碼，從命令列時，您可以取得的標準的 Python 工具。 不過，如果您正在開發新的解決方案，或從遠端用戶端運作，我們會建議使用功能完整的 Python IDE。 受歡迎的選項如下：

+ [Visual Studio 2017 Community Edition](https://www.visualstudio.com/vs/features/python/)與 Python
+ [適用於 Visual Studio 的 AI 工具](https://docs.microsoft.com/visualstudio/ai/installation)
+ [Visual Studio Code 中的 Python](https://code.visualstudio.com/docs/languages/python)
+ PyCharm、 Spyder 和 Eclipse 等熱門協力廠商工具

我們建議 Visual Studio，因為它可支援資料庫專案，以及機器學習專案。 設定 Python 環境的協助，請參閱[Visual Studio 中的管理 Python 環境](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)。

因為開發人員經常會使用多個版本的 Python，安裝程式不會不將 Python 新增至您的路徑。 若要使用的 Python 可執行檔和安裝程式安裝的程式庫，連結至您的 IDE **Python.exe**也提供 revoscalepy 和 microsoftml 的路徑。 比方說，在 Visual Studio 中 Python 專案，您的自訂環境會指定`C:\Program Files\Microsoft\PyForMLS`，`C:\Program Files\Microsoft\PyForMLS\python.exe`並`C:\Program Files\Microsoft\PyForMLS\pythonw.exe`如**前置詞路徑**， **cesta k interpretu**，以及**Interpret v okně**分別。

如需其他指引，請參閱[連結的 Python 工具和 Ide](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)。 發行項是針對 Microsoft Machine Learning Server 撰寫的因此 Python 路徑不同，但它會顯示您如何從各種工具連結至 Python 程式庫。

## <a name="next-steps"></a>後續步驟

既然您有工具和工作連接到 SQL Server，逐步教學課程，以更進一步了解 revoscalepy 函式，以及切換計算內容。

> [!div class="nextstepaction"]
> [建立模型，使用 revoscalepy 和遠端計算內容](../tutorials/use-python-revoscalepy-to-create-model.md)