---
title: 設定適用於 Python 開發-SQL Server Machine Learning 資料科學用戶端
description: 設定遠端連線到 SQL Server Machine Learning 服務與 Python 的 Python 的本機環境 （Jupyter Notebook 或 PyCharm）。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/09/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: c0ca592d98f9bb69586c537006fd14d4230b661b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642817"
---
# <a name="set-up-a-data-science-client-for-python-development-on-sql-server-machine-learning-services"></a>設定適用於 SQL Server 機器學習服務上的 Python 開發的資料科學用戶端
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Python 整合功能時包括中的 [Python] 選項啟動 SQL Server 2017 或更新版本[Machine Learning 服務 （資料庫） 安裝](../install/sql-machine-learning-services-windows-install.md)。 

若要開發及部署 Python 解決方案，適用於 SQL Server，安裝 Microsoft [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)和其他的 Python 程式庫開發工作站。 Revoscalepy 程式庫，這也是遠端的 SQL Server 執行個體上，可協調計算這兩個系統之間的要求。 

在這篇文章，了解如何設定 Python 開發工作站，以便您可以與遠端的 SQL Server machine learning 和 Python 整合啟用互動。 完成這篇文章中的步驟之後，您必須使用相同的 SQL Server 上的 Python 程式庫。 您也會知道如何將 SQL Server 上推送至遠端的 Python 工作階段的計算從本機 Python 工作階段。

![用戶端-伺服器元件](media/sqlmls-python-client-revo.png "本機和遠端的 Python 工作階段和程式庫")

若要驗證安裝，您可以使用內建的 Jupyter Notebook 在本文中所述或是[連結程式庫](#install-ide)PyCharm 或您通常會使用任何其他 IDE。

> [!Tip]
> 如需這些練習的影片示範，請參閱 <<c0> [ 執行的 R 和 Python，在從 Jupyter Notebook 的 SQL Server 中遠端](https://youtu.be/D5erljpJDjE)。

> [!Note]
> 用戶端程式庫安裝的替代方案使用[獨立伺服器](../install/sql-machine-learning-standalone-windows-install.md)做為豐富的用戶端，有些客戶偏好的更深入的案例中工作。 在獨立伺服器完全分開的 SQL Server，但因為它有相同的 Python 程式庫，您可以使用它做為用戶端的 SQL Server 資料庫內分析。 您也可以使用它針對非 SQL 相關的工作，包括匯入，並從其他資料平台的資料模型的能力。 如果您安裝獨立伺服器，您可以找到此位置的 Python 可執行檔： `C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`。 若要驗證您的安裝，[開啟 Jupyter notebook](#python-tools)使用 Python.exe，在該位置來執行命令。

## <a name="commonly-used-tools"></a>常用的工具

不論您是剛接觸 SQL、 Python 開發人員或 SQL 開發人員熟悉 Python 和資料庫內分析，您將需要 Python 開發工具和 T-SQL 查詢編輯器這類[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)執行所有的資料庫內分析功能。

適用於 Python 開發，您可以使用出現在 SQL Server 安裝的 Anaconda 散發套件配套的 Jupyter Notebook。 這篇文章說明如何啟動 Jupyter Notebook，以便您可以在 SQL Server 上執行 Python 程式碼在本機或遠端。

SSMS 屬於不同下載，用於建立和執行預存程序，在 SQL Server，包括包含 Python 程式碼。 幾乎任何您在 Jupyter Notebook 中撰寫的 Python 程式碼可以內嵌在預存程序中。 您可以逐步執行其他的快速入門，以了解[SSMS 和內嵌的 Python](../tutorials/quickstart-python-verify.md)。

## <a name="1---install-python-packages"></a>1-安裝 Python 套件

本機工作站必須有相同的 Python 套件版本的 SQL Server 上，包括基底的 Anaconda 4.2.0 Python 3.5.2 分佈，與 Microsoft 特定的套件。

安裝指令碼會將 Python 用戶端中的三個 Microsoft 特定程式庫。 指令碼會安裝[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)，用來定義資料來源物件和計算內容。 它會安裝[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)提供機器學習服務演算法。 [Azureml](https://docs.microsoft.com/machine-learning-server/python-reference/azureml-model-management-sdk/azureml-model-management-sdk)也安裝套件，但它適用於運算化的獨立 （非執行個體） 的 Machine Learning Server 內容相關聯的工作，並可能會對資料庫內分析，則用途有限。

1. 下載安裝指令碼。

  + [https://aka.ms/mls-py](https://aka.ms/mls-py) 會安裝 Microsoft Python 套件的版本 9.2.1。 這個版本會對應至預設 SQL Server 2017 執行個體。 

  + [https://aka.ms/mls93-py](https://aka.ms/mls93-py) 會安裝 9.3 版的 Microsoft Python 套件。 此版本是較好的選擇，如果您的遠端 SQL Server 2017 執行個體[繫結至 Machine Learning Server 9.3](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

2. 開啟提升權限的系統管理員權限的 PowerShell 視窗 (以滑鼠右鍵按一下**系統管理員身分執行**)。

3. 請移至您下載安裝程式的資料夾，並執行指令碼。 新增`-InstallFolder`命令列引數，來指定程式庫的資料夾位置。 例如： 

   ```python
   cd {{download-directory}}
   .\Install-PyForMLS.ps1 -InstallFolder "C:\path-to-python-for-mls"
   ```

如果您省略安裝資料夾，預設為 C:\Program Files\Microsoft\PyForMLS。

安裝需要一些時間才能完成。 您可以監視進度，在 PowerShell 視窗中。 安裝程式完成時，您會有一組完整的封裝。 

> [!Tip] 
> 我們建議[Python for Windows 常見問題集](https://docs.python.org/3/faq/windows.html)如需在 Windows 上執行 Python 程式的一般 purppose 資訊。

## <a name="2---locate-executables"></a>2-找出可執行檔

仍在 PowerShell 中，列出要確認已安裝 Python.exe、 指令碼和其他套件的安裝資料夾的內容。 

1. 請輸入`cd \`移至根磁碟機，然後輸入您針對指定的路徑`-InstallFolder`上一個步驟。 如果您省略此參數在安裝期間，預設值是`cd C:\Program Files\Microsoft\PyForMLS`。

2. 輸入`dir *.exe`列出可執行檔。 您應該會看到**python.exe**， **pythonw.exe**，並**解除安裝 anaconda.exe**。

  ![Python 可執行檔的清單](media/powershell-python-exe.png)
   
在系統上有多個版本的 Python，請記得如果您想要載入，請使用此特定 Python.exe **revoscalepy**和其他 Microsoft 套件。

> [!Note] 
> 安裝指令碼不會修改您在電腦上，這表示新的 python 解譯器和您剛才安裝的模組不會自動提供給您可能需要其他工具的 PATH 環境變數。 在將 Python 解譯器和程式庫連結至工具的協助，請參閱[安裝 IDE](#install-ide)。

<a name="python-tools"></a>

## <a name="3---open-jupyter-notebooks"></a>3-開啟 Jupyter Notebook

Anaconda 包含 Jupyter Notebook。 下一個步驟中，建立 notebook，並執行一些 Python 程式碼，其中包含您剛才安裝的程式庫。

1. 在 Powershell 提示字元中，仍在 C:\Program Files\Microsoft\PyForMLS 目錄中，開啟 Jupyter Notebook 從指令碼 資料夾：

  ```powershell
  .\Scripts\jupyter-notebook
  ```

  應該會在預設瀏覽器中開啟 notebook `https://localhost:8889/tree`。

  若要啟動的另一種方式是按兩下**jupyter notebook.exe**。 

2. 按一下 **的新**，然後按一下**Python 3**。

  ![jupyter notebook 使用新的 Python 3 選取項目](media/jupyter-notebook-new-p3.png)

3. 輸入`import revoscalepy`並執行的 Microsoft 特定程式庫載入其中一個命令。

4. 輸入並執行`print(revoscalepy.__version__)`来傳回的版本資訊。 您應該會看到 9.2.1 或 9.3.0。 您可以使用任一版本與[伺服器上的 revoscalepy](../r/determine-which-packages-are-installed-on-sql-server.md#get-package-vers)。 

4. 輸入一系列更複雜的陳述式。 這個範例會產生摘要統計資料使用[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)透過本機的資料集。 其他函式會取得範例資料的位置，並建立本機的.xdf 檔案資料來源物件。

  ```python
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

下列螢幕擷取畫面顯示的輸入和輸出中，為了簡潔起見已修剪的一部分。

  ![顯示 revoscalepy 輸入和輸出的 jupyter notebook](media/jupyter-notebook-local-revo.png)

## <a name="4---get-sql-permissions"></a>4-取得 SQL 權限

若要連接到執行指令碼，並上傳資料的 SQL Server 的執行個體，您必須具有有效的登入資料庫伺服器上。 您可以使用 SQL 登入或整合式 Windows 驗證。 我們通常建議使用 Windows 整合式的驗證，但使用 SQL 登入是某些情況下，更容易，尤其是您的指令碼包含到外部資料的連接字串。

最小值，用來執行程式碼的帳戶必須具有您正在使用，再加上特殊權限執行的任何外部指令碼，從資料庫讀取的權限。 大部分的開發人員也需要若要建立預存程序，並將資料寫入資料表，其中包含定型資料的權限，或評分的資料。 

請詢問資料庫管理員，以便[設定您的帳戶的下列權限](../security/user-permission.md)，在資料庫中，您可以使用 Python:

+ **EXECUTE ANY EXTERNAL SCRIPT**伺服器上執行 Python。
+ **db_datareader**權限才能執行用來定型模型的查詢。
+ **db_datawriter**撰寫定型資料或評分的資料。
+ **db_owner**為了建立物件，例如預存程序，資料表，函式。 
  您也需要**db_owner**建立範例和測試資料庫。 

如果您的程式碼需要使用 SQL Server 預設不會安裝的封裝，來排列資料庫系統管理員，以具有安裝與執行個體的套件。 SQL Server 是安全的環境，並限制可安裝套件的位置。 不建議為您的程式碼的一部分臨機操作安裝封裝，即使您有權限。 此外，請務必仔細考慮安全性隱含意義 server 文件庫中安裝新套件之前。


<a name="create-iris-remotely"></a>

## <a name="5---create-test-data"></a>5-建立測試資料

如果您在遠端伺服器上建立資料庫的權限，您可以執行下列程式碼來建立這篇文章中的剩餘步驟使用鳶尾花示範資料庫。

### <a name="1---create-the-irissql-database-remotely"></a>1-從遠端建立 irissql 資料庫

```python
import pyodbc

# creating a new db to load Iris sample in
new_db_name = "irissql"
connection_string = "Driver=SQL Server;Server=localhost;Database={0};Trusted_Connection=Yes;" 
                        # you can also swap Trusted_Connection for UID={your username};PWD={your password}
cnxn = pyodbc.connect(connection_string.format("master"), autocommit=True)
cnxn.cursor().execute("IF EXISTS(SELECT * FROM sys.databases WHERE [name] = '{0}') DROP DATABASE {0}".format(new_db_name))
cnxn.cursor().execute("CREATE DATABASE " + new_db_name)
cnxn.close()

print("Database created")
```

### <a name="2---import-iris-sample-from-sklearn"></a>2-從匯入 Iris 範例 SkLearn

```python
from sklearn import datasets
import pandas as pd

# SkLearn has the Iris sample dataset built in to the package
iris = datasets.load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
```

### <a name="3---use-revoscalepy-apis-to-create-a-table-and-load-the-iris-data"></a>3-使用 Revoscalepy Api 來建立資料表，並將鳶尾花資料

```python
from revoscalepy import RxSqlServerData, rx_data_step

# Example of using RX APIs to load data into SQL table. You can also do this with pyodbc
table_ref = RxSqlServerData(connection_string=connection_string.format(new_db_name), table="iris_data")
rx_data_step(input_data = df, output_file = table_ref, overwrite = True)

print("New Table Created: Iris")
print("Sklearn Iris sample loaded into Iris table")
```

## <a name="6---test-remote-connection"></a>6-測試遠端連線

在之前嘗試下一個步驟中，請確定您具有權限的連接字串和 SQL Server 執行個體[Iris 範例資料庫](../tutorials/demo-data-iris-in-sql.md)。 如果資料庫不存在，而且您有足夠的權限，您可以[建立資料庫，使用這些內嵌指示](#create-iris-remotely)。

以有效的值取代連接字串。 範例程式碼使用`"Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"`，但您的程式碼應該可能指定在遠端伺服器，執行個體名稱，與對應至資料庫使用者登入的認證選項。

### <a name="define-a-function"></a>定義函式

下列程式碼定義的函式，您將在稍後步驟中傳送到 SQL Server。 在執行時，它會使用資料和程式庫 （revoscalepy，pandas，matplotlib） 在遠端伺服器上建立散佈圖的鳶尾花資料集。 它會傳回.png 位元組資料的流來呈現瀏覽器中的 Jupyter Notebook。

```python
def send_this_func_to_sql():
    from revoscalepy import RxSqlServerData, rx_import
    from pandas.tools.plotting import scatter_matrix
    import matplotlib.pyplot as plt
    import io
    
    # remember the scope of the variables in this func are within our SQL Server Python Runtime
    connection_string = "Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"
    
    # specify a query and load into pandas dataframe df
    sql_query = RxSqlServerData(connection_string=connection_string, sql_query = "select * from iris_data")
    df = rx_import(sql_query)
    
    scatter_matrix(df)
    
    # return bytestream of image created by scatter_matrix
    buf = io.BytesIO()
    plt.savefig(buf, format="png")
    buf.seek(0)
    
    return buf.getvalue()
```

### <a name="send-the-function-to-sql-server"></a>將 SQL Server 中的函式

在此範例中，建立遠端計算內容和傳送執行函式與 SQL server [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec)。 **Rx_exec**函式很有用，因為它可接受做為引數的計算內容。 任何您想要從遠端執行的函式必須有計算內容引數。 某些函式，例如[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)直接支援這個引數。 對於不的作業，您可以使用**rx_exec**遠端計算內容中提供您的程式碼。

在此範例中，任何未經處理的資料不必須從 SQL Server 傳送至 Jupyter Notebook。 鳶尾花資料庫內發生的所有計算，並僅映像檔傳回至用戶端。

```python
from IPython import display
import matplotlib.pyplot as plt 
from revoscalepy import RxInSqlServer, rx_exec

# create a remote compute context with connection to SQL Server
sql_compute_context = RxInSqlServer(connection_string=connection_string.format(new_db_name))

# use rx_exec to send the function execution to SQL Server
image = rx_exec(send_this_func_to_sql, compute_context=sql_compute_context)[0]

# only an image was returned to my jupyter client. All data remained secure and was manipulated in my db.
display.Image(data=image)
```

下列螢幕擷取畫面顯示輸入和散佈圖的輸出。

  ![顯示散佈圖輸出的 jupyter notebook](media/jupyter-notebook-scatterplot.png)


<a name="install-ide"></a>

## <a name="7---start-python-from-tools"></a>7-從工具中啟動 Python

因為開發人員經常會使用多個版本的 Python，安裝程式不會不將 Python 新增至您的路徑。 若要使用的 Python 可執行檔和安裝程式安裝的程式庫，連結至您的 IDE **Python.exe**也會提供路徑**revoscalepy**並**microsoftml**。 

### <a name="command-line"></a>命令列

當您執行**Python.exe**從 C:\Program Files\Microsoft\PyForMLS （或指定的 Python 用戶端程式庫安裝的任何位置），您可以存取完整的 Anaconda 散發套件，再加上 Microsoft Python模組**revoscalepy**並**microsoftml**。

1. 請移至 C:\Program Files\Microsoft\PyForMLS，然後按兩下**Python.exe**。
2. 開啟互動式說明： `help()`
3. 在說明提示時輸入模組名稱： `help> revoscalepy`。 說明傳回名稱、 封裝內容、 版本和檔案位置。
4. 傳回在版本和套件資訊**協助 >** 提示字元： `revoscalepy`。 幾次按下 Enter 以結束說明。
5. 匯入模組： `import revoscalepy`


### <a name="jupyter-notebooks"></a>Jupyter Notebook

本文章示範函式呼叫中使用內建的 Jupyter Notebook **revoscalepy**。 如果您不熟悉這項工具，以下的螢幕擷取畫面會說明如何拼湊在一起，以及所有 「 沒 」 的原因。 

父資料夾 C:\Program Files\Microsoft\PyForMLS 包含 Anaconda，加上 Microsoft 套件。 Jupyter Notebook 在指令碼 資料夾中，包含 Anaconda，在和 Python 可執行檔會自動註冊，搭配 Jupyter Notebook。 站台-套件下找到的封裝可以匯入 notebook，其中包括用於資料科學與機器學習服務的三個 Microsoft 套件。

  ![可執行檔和程式庫](media/jupyter-notebook-python-registration.png)

如果您使用其他 IDE，您必須將 Python 可執行檔和函式程式庫連結至您的工具。 下列各節提供常用的工具的指示。

### <a name="visual-studio"></a>Visual Studio

如果您有[Visual Studio 中的 Python](https://code.visualstudio.com/docs/languages/python)，使用下列的組態選項來建立包含 Microsoft Python 套件的 Python 環境。

| 組態設定 | value |
|-----------------------|-------|
| **前置詞路徑** | C:\Program Files\Microsoft\PyForMLS |
| **Cesta k interpretu** | C:\Program Files\Microsoft\PyForMLS\python.exe |
| **Interpret v okně** | C:\Program Files\Microsoft\PyForMLS\pythonw.exe |

設定 Python 環境的協助，請參閱[Visual Studio 中的管理 Python 環境](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)。

### <a name="pycharm"></a>PyCharm

在 PyCharm 設定安裝 Machine Learning 伺服器可執行的 python 解譯器。

1. 在新的專案中，在設定中，按一下**新增本機**。

2. 輸入`C:\Program Files\Microsoft\PyForMLS\`。

您現在可以匯入**revoscalepy**， **microsoftml**，或**azureml**模組。 您也可以選擇**工具** > **Python 主控台**開啟互動式視窗。

## <a name="next-steps"></a>後續步驟

既然您有工具和工作連接到 SQL Server，展開您的技能，透過 Python 快速入門使用執行[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

> [!div class="nextstepaction"]
> [快速入門：請確認有 SQL Server 中的 Python](../tutorials/quickstart-python-verify.md)