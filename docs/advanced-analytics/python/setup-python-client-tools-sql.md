---
title: 設定用於 SQL Server Machine Learning Python 用戶端 |Microsoft Docs
description: 設定遠端連線到 SQL Server Machine Learning 服務與 Python 本機 Python 環境。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/25/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 326676d1be684b90784351de316590ebdb1ff29f
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2018
ms.locfileid: "50051150"
---
# <a name="set-up-a-python-client-for-use-with-sql-server-machine-learning"></a>設定用於 SQL Server Machine Learning Python 用戶端
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Python 整合可啟動 SQL Server 2017 或更新版本，當您在 Machine Learning 服務 （資料庫） 安裝中包含 Python 選項。 如需詳細資訊，請參閱 <<c0> [ 安裝 SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)。

在這篇文章，了解如何設定用戶端開發工作站，以便您可以連接到遠端 SQL Server 進行機器學習服務和 Python 整合。 在結束時，您將會有相同的 Python 程式庫，為 SQL Server 上再加上能力將計算推送從 SQL Server 的遠端工作階段的本機工作階段。

> [!Tip]
> 如需影片示範，請參閱 <<c0> [ 執行的 R 和遠端 SQL Server 從 Jupyter Notebook 中的 Python](https://blogs.msdn.microsoft.com/mlserver/2018/07/10/run-r-and-python-remotely-in-sql-server-from-jupyter-notebooks-or-any-ide/)。

> [!Note]
> 只要用戶端程式庫安裝的替代方式使用獨立伺服器。 使用獨立豐富用戶端與伺服器是某些客戶偏好的更多的端對端案例工作的選項。 如果您有[獨立伺服器](../install/sql-machine-learning-standalone-windows-install.md)提供 SQL Server 安裝程式中，您必須是 SQL Server 資料庫引擎執行個體完全分離的 Python 伺服器。 Standalon 伺服器包含 Anaconda，再加上的 Microsoft 特定程式庫的開放原始碼基底散發。 您可以找到此位置的 Python 可執行檔： `C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`。 在豐富型用戶端安裝的驗證，以開啟[Jupyter notebook](#python-tools)伺服器上使用 Python.exe 來執行命令。

## <a name="1---install-python-packages"></a>1-安裝 Python 套件

本機工作站必須有相同的 Python 套件版本的 SQL Server 上，包括基底散發，以及 Microsoft 特定的套件[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)並[microsftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)。 [Azureml 模型管理](https://docs.microsoft.com/machine-learning-server/python-reference/azureml-model-management-sdk/azureml-model-management-sdk)也安裝套件，但它適用於運算化的獨立 （非執行個體） 的 Machine Learning Server 內容相關聯的工作。 對於 SQL Server 執行個體上的資料庫內分析，操作化是透過預存程序。

1. 下載安裝指令碼，若要使用 Python 3.5.2 安裝 Anaconda 4.2.0 和三個先前列出的 Microsoft 套件。

  + [https://aka.ms/mls-py](https://aka.ms/mls-py) 如果不是 SQL Server 2017 繫結 （常見的情況）。 如果您不確定，請選擇此指令碼。

  + [https://aka.ms/mls93-py](https://aka.ms/mls93-py) 如果遠端 SQL Server 執行個體[繫結至 Machine Learning Server 9.3](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

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

仍在 PowerShell 中，瀏覽至安裝資料夾以確認 Python.exe、 指令碼，以及其他封裝的位置。 

1. 請輸入`cd \`移至根磁碟機，然後輸入您針對指定的路徑`-InstallFolder`上一個步驟。 如果您省略此參數在安裝期間，預設值是`cd C:\Program Files\Microsoft\PyForMLS`。

2. 輸入`dir *.exe`列出可執行檔。 您應該會看到**python.exe**， **pythonw.exe**，並**解除安裝 anaconda.exe**。

  ![Python 可執行檔的清單](media/powershell-python-exe.png)
   
在系統上有多個版本的 Python，請記得如果您想要載入，請使用此特定 Python.exe **revoscalepy**和其他 Microsoft 套件。

> [!Note] 
> 安裝指令碼不會修改您在電腦上，這表示新的 python 解譯器和您剛才安裝的模組不會自動提供給您可能需要其他工具的 PATH 環境變數。 在將 Python 解譯器和程式庫連結至工具的協助，請參閱[安裝 IDE](#install-ide)。

<a name="python-tool"></a>

## <a name="3---open-jupyter-notebooks"></a>3-開啟 Jupyter Notebook

Anaconda 包含 Jupyter Notebook。 下一個步驟中，建立 notebook，並執行一些 Python 程式碼，其中包含您剛才安裝的程式庫。

1. 在 Powershell 提示字元中，瀏覽到指令碼資料夾，以開啟 Jupyter Notebook:

   ```powershell
   .\Scripts\jupyter-notebook
   ```

  應該會在預設瀏覽器中開啟 notebook `http://localhost:8889/tree`。

2. 按一下 **的新**，然後按一下**Python 3**。

  ![jupyter notebook 使用新的 Python 3 選取項目](media/jupyter-notebook-new-p3.png)

3. 輸入`import revoscalepy`並執行的 Microsoft 特定程式庫載入其中一個命令。

4. 輸入一系列更複雜的陳述式。 這個範例會產生摘要統計資料使用[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)透過本機的資料集。 其他函式會取得範例資料的位置，並建立本機的.xdf 檔案資料來源物件。

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

下列螢幕擷取畫面顯示的輸入和輸出中，為了簡潔起見已修剪的一部分。

  ![顯示 revoscalepy 輸入和輸出的 jupyter notebook](media/jupyter-notebook-local-revo.png)

## <a name="4---get-sql-permissions"></a>4-取得 SQL 權限

若要連接到執行指令碼，並上傳資料的 SQL Server 的執行個體，您必須具有有效的登入資料庫伺服器上。 您可以使用 SQL 登入或整合式 Windows 驗證。 我們通常建議使用 Windows 整合式的驗證，但使用 SQL 登入是某些情況下，更容易，尤其是您的指令碼包含到外部資料的連接字串。

最小值，用來執行程式碼的帳戶必須具有您正在使用，再加上特殊權限執行的任何外部指令碼，從資料庫讀取的權限。 大部分的開發人員也需要若要建立預存程序，並將資料寫入資料表，其中包含定型資料的權限，或評分的資料。 

詢問資料庫管理員，以便您用來使用 Python 的資料庫中設定下列權限的帳戶：

+ **EXECUTE ANY EXTERNAL SCRIPT**伺服器上執行 Python。
+ **db_datareader**權限才能執行用來定型模型的查詢。
+ **db_datawriter**撰寫定型資料或評分的資料。
+ **db_owner**為了建立物件，例如預存程序，資料表，函式。 
  您也需要**db_owner**建立範例和測試資料庫。 

如果您的程式碼需要使用 SQL Server 預設不會安裝的封裝，來排列資料庫系統管理員，以具有安裝與執行個體的套件。 SQL Server 是安全的環境，並限制可安裝套件的位置。 不建議為您的程式碼的一部分臨機操作安裝封裝，即使您有權限。 此外，請務必仔細考慮安全性隱含意義 server 文件庫中安裝新套件之前。

## <a name="5---test-remote-connection"></a>5-測試遠端連線

在之前嘗試下一個步驟中，請確定您具有權限的連接字串和 SQL Server 執行個體[Iris 範例資料庫](../tutorials/demo-data-iris-in-sql.md)。 如果資料庫不存在，而且您有足夠的權限，您可以[建立資料庫，使用這些內嵌指示](#create-iris-remotely)。

以有效的值取代連接字串。 範例程式碼使用`"Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"`，但您的程式碼應該可能指定在遠端伺服器，以執行個體名稱。

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

## <a name="6---link-ide-to-pythonexe"></a>6-連結至 python.exe 的 IDE

如果您只需偵錯指令碼，從命令列時，您可以取得的標準的 Python 工具。 不過，如果您正在開發新的解決方案，您可能需要功能完整的 Python IDE。 受歡迎的選項如下：

+ [Visual Studio 2017 Community Edition](https://www.visualstudio.com/vs/features/python/)與 Python
+ [適用於 Visual Studio 的 AI 工具](https://docs.microsoft.com/visualstudio/ai/installation)
+ [Visual Studio Code 中的 Python](https://code.visualstudio.com/docs/languages/python)
+ PyCharm、 Spyder 和 Eclipse 等熱門協力廠商工具

我們建議 Visual Studio，因為它可支援資料庫專案，以及機器學習專案。 設定 Python 環境的協助，請參閱[Visual Studio 中的管理 Python 環境](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)。

因為開發人員經常會使用多個版本的 Python，安裝程式不會不將 Python 新增至您的路徑。 若要使用的 Python 可執行檔和安裝程式安裝的程式庫，連結至您的 IDE **Python.exe**也會提供路徑**revoscalepy**並**microsoftml**。 

在 Visual Studio 中 Python 專案，您的自訂環境會指定下列值，假設是預設安裝。

| 組態設定 | value |
|-----------------------|-------|
| **前置詞路徑** | C:\Program Files\Microsoft\PyForMLS |
| **Cesta k interpretu** | C:\Program Files\Microsoft\PyForMLS\python.exe |
| **Interpret v okně** | C:\Program Files\Microsoft\PyForMLS\pythonw.exe |

<a name="create-iris-remotely"></a>

## <a name="optional-create-the-iris-database-remotely"></a>選擇性： 建立鳶尾花資料庫從遠端

如果您在遠端伺服器上建立資料庫的權限，您可以執行下列的程式碼，以建立鳶尾花示範資料庫用於這篇文章中的範例。

### <a name="1---create-the-irissql-database"></a>1-建立 irissql 資料庫

```Python
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

```Python
from sklearn import datasets
import pandas as pd

# SkLearn has the Iris sample dataset built in to the package
iris = datasets.load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
```

### <a name="3---use-recoscalepy-apis-to-create-a-table-and-load-the-iris-data"></a>3-使用 RecoscalePy Api 來建立資料表，並將鳶尾花資料

```Python
from revoscalepy import RxSqlServerData, rx_data_step

# Example of using RX APIs to load data into SQL table. You can also do this with pyodbc
table_ref = RxSqlServerData(connection_string=connection_string.format(new_db_name), table="iris_data")
rx_data_step(input_data = df, output_file = table_ref, overwrite = True)

print("New Table Created: Iris")
print("Sklearn Iris sample loaded into Iris table")
```

<a name="install-ide"></a>

## <a name="next-steps"></a>後續步驟

既然您有工具和工作連接到 SQL Server，逐步教學課程，以更進一步了解 revoscalepy 函式，以及切換計算內容。

> [!div class="nextstepaction"]
> [建立模型，使用 revoscalepy 和遠端計算內容](../tutorials/use-python-revoscalepy-to-create-model.md)