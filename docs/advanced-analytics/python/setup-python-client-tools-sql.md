---
title: 設定用於 Python 開發的資料科學用戶端
description: 針對使用 Python 的 SQL Server Machine Learning 服務, 設定遠端連線的 Python 本機環境 (Jupyter Notebook 或 PyCharm)。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a37f0eb62ec0483b8c73bd5cc4d6d29221e8082f
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715178"
---
# <a name="set-up-a-data-science-client-for-python-development-on-sql-server-machine-learning-services"></a>在 SQL Server Machine Learning 服務上設定用於 Python 開發的資料科學用戶端
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

從 SQL Server 2017 或更新版本開始, 當您在[Machine Learning Services (資料庫內) 安裝](../install/sql-machine-learning-services-windows-install.md)中包含 python 選項時, 即可使用 python 整合。 

若要開發及部署適用于 SQL Server 的 Python 解決方案, 請安裝 Microsoft 的[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)和其他 python 程式庫您的開發工作站。 Revoscalepy 程式庫 (也位於遠端 SQL Server 實例) 會協調兩個系統之間的計算要求。 

在本文中, 您將瞭解如何設定 Python 開發工作站, 讓您可以與針對機器學習和 Python 整合啟用的遠端 SQL Server 進行互動。 完成本文中的步驟之後, 您將會擁有與 SQL Server 上相同的 Python 程式庫。 您也會知道如何將本機 Python 會話的計算推送至 SQL Server 上的遠端 Python 會話。

![用戶端-伺服器元件](media/sqlmls-python-client-revo.png "本機和遠端 Python 會話和程式庫")

若要驗證安裝, 您可以使用本文中所述的內建 Jupyter 筆記本, 或將[程式庫連結](#install-ide)至 PyCharm 或您通常使用的其他任何 IDE。

> [!Tip]
> 如需這些練習的示範影片, 請參閱[從 Jupyter 筆記本的 SQL Server 遠端執行 R 和 Python](https://youtu.be/D5erljpJDjE)。

> [!Note]
> 用戶端程式庫安裝的另一個替代方案是使用[獨立伺服器](../install/sql-machine-learning-standalone-windows-install.md)做為豐富型用戶端, 而某些客戶會偏好更深入的案例工作。 獨立伺服器與 SQL Server 完全分離, 但因為它具有相同的 Python 程式庫, 所以您可以使用它做為 SQL Server 資料庫內分析的用戶端。 您也可以將它用於與非 SQL 相關的工作, 包括能夠從其他資料平臺匯入和模型資料。 如果您安裝獨立伺服器, 您可以在以下位置找到 Python 可執行檔: `C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`。 若要驗證您的安裝, 請[開啟 Jupyter 筆記本](#python-tools), 以在該位置使用 Python 執行命令。

## <a name="commonly-used-tools"></a>常用的工具

無論您是 SQL 的 Python 開發人員新手, 或是 Python 和資料庫內分析的 SQL 開發人員新手, 您都需要 Python 開發工具和 T-SQL 查詢編輯器 (例如[SQL Server Management Studio (SSMS))](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)來執行所有功能資料庫內分析。

針對 Python 開發, 您可以使用 Jupyter 筆記本, 這會隨附于 SQL Server 所安裝的 Anaconda 散發套件中。 本文說明如何開始 Jupyter 筆記本, 讓您可以在 SQL Server 本機和遠端執行 Python 程式碼。

SSMS 是個別的下載, 適用于在 SQL Server 上建立和執行預存程式, 包括包含 Python 程式碼的程式。 您在 Jupyter 筆記本中撰寫的任何 Python 程式碼, 幾乎都可以內嵌在預存程式中。 您可以逐步執行其他快速入門, 以瞭解[SSMS 和內嵌的 Python](../tutorials/quickstart-python-verify.md)。

## <a name="1---install-python-packages"></a>1-安裝 Python 套件

本機工作站必須具有與 SQL Server 上相同的 Python 套件版本, 包括具有 Python 3.5.2 散發的基底 Anaconda 4.2.0, 以及 Microsoft 特定套件。

安裝腳本會將三個 Microsoft 特定程式庫新增至 Python 用戶端。 腳本會安裝[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package), 用來定義資料來源物件和計算內容。 它會安裝[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)來提供機器學習演算法。 [Azureml](https://docs.microsoft.com/machine-learning-server/python-reference/azureml-model-management-sdk/azureml-model-management-sdk)套件也會一併安裝, 但它適用于與獨立 (非實例) Machine Learning Server 內容相關聯的運算化工作, 而且可能用於資料庫內分析。

1. 下載安裝腳本。

  + [https://aka.ms/mls-py](https://aka.ms/mls-py)安裝 Microsoft Python 套件的版本9.2.1。 這個版本會對應到預設的 SQL Server 實例。 

  + [https://aka.ms/mls93-py](https://aka.ms/mls93-py)會安裝 Microsoft Python 套件的9.3 版。 如果您的遠端 SQL Server 實例系結[至 Machine Learning Server 9.3](../install/upgrade-r-and-python.md), 此版本是較好的選擇。

2. 以較高的系統管理員許可權開啟 PowerShell 視窗 (以滑鼠右鍵按一下 [**以系統管理員身分執行**])。

3. 移至您下載安裝程式的資料夾, 並執行腳本。 `-InstallFolder`新增命令列引數以指定程式庫的資料夾位置。 例如: 

   ```python
   cd {{download-directory}}
   .\Install-PyForMLS.ps1 -InstallFolder "C:\path-to-python-for-mls"
   ```

如果您省略安裝資料夾, 預設值為 C:\Program Files\Microsoft\PyForMLS。

安裝需要一些時間才能完成。 您可以在 PowerShell 視窗中監視進度。 當安裝程式完成時, 您會有一組完整的套件。 

> [!Tip] 
> 我們建議適用于[windows 的 PYTHON 常見問題](https://docs.python.org/3/faq/windows.html), 以取得在 Windows 上執行 Python 程式的一般 purppose 資訊。

## <a name="2---locate-executables"></a>2-尋找可執行檔

仍然在 PowerShell 中, 列出安裝資料夾的內容, 以確認已安裝 Python、腳本和其他套件。 

1. 輸入`cd \`以移至根磁片磁碟機, 然後輸入您在上一個步驟中`-InstallFolder`指定的路徑。 如果您在安裝期間省略此參數, 預設值`cd C:\Program Files\Microsoft\PyForMLS`為。

2. 輸入`dir *.exe`以列出可執行檔。 您應該會看到**python .exe**、 **pythonw.exe**和**uninstall-anaconda**。

  ![Python 可執行檔案清單](media/powershell-python-exe.png)
   
在具有多個 Python 版本的系統上, 如果您想要載入**revoscalepy**和其他 Microsoft 封裝, 請記得使用這個特定的 python。

> [!Note] 
> 安裝腳本不會修改電腦上的 PATH 環境變數, 這表示新的 python 解譯器和您剛安裝的模組不會自動提供給您可能擁有的其他工具。 如需將 Python 解譯器和程式庫連結至工具的說明, 請參閱[安裝 IDE](#install-ide)。

<a name="python-tools"></a>

## <a name="3---open-jupyter-notebooks"></a>3-開啟 Jupyter 筆記本

Anaconda 包含 Jupyter 筆記本。 在下一個步驟中, 建立筆記本並執行一些 Python 程式碼, 其中包含您剛安裝的程式庫。

1. 在 Powershell 命令提示字元中, 仍在 C:\Program Files\Microsoft\PyForMLS 目錄中, 從 Scripts 資料夾開啟 Jupyter 筆記本:

  ```powershell
  .\Scripts\jupyter-notebook
  ```

  筆記本應該會在您的預設瀏覽器`https://localhost:8889/tree`中開啟, 網址為。

  另一個開始的方法是按兩下 [ **jupyter-notebook**]。 

2. 按一下 [**新增**], 然後按一下 [ **Python 3**]。

  ![具有新的 Python 3 選取範圍的 jupyter 筆記本](media/jupyter-notebook-new-p3.png)

3. 輸入`import revoscalepy`並執行命令, 以載入其中一個 Microsoft 特定程式庫。

4. 輸入並執行`print(revoscalepy.__version__)`以傳回版本資訊。 您應該會看到9.2.1 或9.3.0。 您可以在[伺服器上搭配 revoscalepy](../package-management/installed-package-information.md)使用其中一個版本。 

4. 輸入更複雜的語句系列。 這個範例會使用[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)透過本機資料集來產生摘要統計資料。 其他函數會取得範例資料的位置, 並建立 xdf 檔案的資料來源物件。

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

下列螢幕擷取畫面顯示輸出的輸入和部分, 為了簡潔起見, 已修剪。

  ![顯示 revoscalepy 輸入和輸出的 jupyter 筆記本](media/jupyter-notebook-local-revo.png)

## <a name="4---get-sql-permissions"></a>4-取得 SQL 許可權

若要連接到 SQL Server 的實例, 以執行腳本並上傳資料, 您必須在資料庫伺服器上有有效的登入。 您可以使用 SQL 登入或整合式 Windows 驗證。 我們通常會建議您使用 Windows 整合式驗證, 但在某些情況下, 使用 SQL 登入比較簡單, 特別是當您的腳本包含外部資料的連接字串時。

用來執行程式碼的帳戶至少必須具有讀取您所使用之資料庫的許可權, 以及執行任何外部腳本的特殊許可權。 大部分的開發人員也需要許可權來建立預存程式, 以及將資料寫入包含定型資料或計分資料的資料表。 

要求資料庫管理員在您使用 Python 的資料庫中, 為[您的帳戶設定下列許可權](../security/user-permission.md):

+ **執行任何外部腳本**, 以在伺服器上執行 Python。
+ **db_datareader**許可權, 以執行用來定型模型的查詢。
+ **db_datawriter**以寫入定型資料或評分資料。
+ **db_owner**以建立預存程式、資料表、函數等物件。 
  您也需要**db_owner**來建立範例和測試資料庫。 

如果您的程式碼需要 SQL Server 預設不會安裝的封裝, 請向資料庫管理員安排, 讓封裝與實例一起安裝。 SQL Server 是安全的環境, 而且可能會限制安裝套件的位置。 不建議您在程式碼中使用套件的臨機操作安裝, 即使您有許可權也一樣。 此外, 在伺服器程式庫中安裝新套件之前, 請務必仔細考慮安全性影響。


<a name="create-iris-remotely"></a>

## <a name="5---create-test-data"></a>5-建立測試資料

如果您有在遠端伺服器上建立資料庫的許可權, 您可以執行下列程式碼來建立鳶尾花示範資料庫, 以用於本文中的其餘步驟。

### <a name="1---create-the-irissql-database-remotely"></a>1-遠端建立 irissql 資料庫

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

### <a name="2---import-iris-sample-from-sklearn"></a>2-從 SkLearn 匯入鳶尾花範例

```python
from sklearn import datasets
import pandas as pd

# SkLearn has the Iris sample dataset built in to the package
iris = datasets.load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
```

### <a name="3---use-revoscalepy-apis-to-create-a-table-and-load-the-iris-data"></a>3-使用 Revoscalepy Api 來建立資料表並載入鳶尾花資料

```python
from revoscalepy import RxSqlServerData, rx_data_step

# Example of using RX APIs to load data into SQL table. You can also do this with pyodbc
table_ref = RxSqlServerData(connection_string=connection_string.format(new_db_name), table="iris_data")
rx_data_step(input_data = df, output_file = table_ref, overwrite = True)

print("New Table Created: Iris")
print("Sklearn Iris sample loaded into Iris table")
```

## <a name="6---test-remote-connection"></a>6-測試遠端連線

嘗試進行下一個步驟之前, 請確定您具有 SQL Server 實例的許可權, 以及[鳶尾花範例資料庫](../tutorials/demo-data-iris-in-sql.md)的連接字串。 如果資料庫不存在, 而且您有足夠的許可權, 您可以[使用這些內嵌指示來建立資料庫](#create-iris-remotely)。

以有效的值取代連接字串。 範例程式碼會`"Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"`使用, 但是您的程式碼應該指定遠端伺服器 (可能包含實例名稱), 以及對應至資料庫使用者登入的認證選項。

### <a name="define-a-function"></a>定義函式

下列程式碼會定義您將在稍後步驟中傳送給 SQL Server 的函式。 執行時, 它會使用遠端伺服器上的資料和程式庫 (revoscalepy、pandas、matplotlib) 來建立鳶尾花資料集的散佈圖。 它會將 .png 的位流傳回 Jupyter 筆記本, 以在瀏覽器中呈現。

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

### <a name="send-the-function-to-sql-server"></a>將函數傳送至 SQL Server

在此範例中, 建立遠端計算內容, 然後使用[rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec)將函數的執行傳送至 SQL Server。 **Rx_exec**函數很有用, 因為它接受計算內容做為引數。 您想要從遠端執行的任何函式都必須具有 compute 內容引數。 某些函式 (例如[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) ) 直接支援此引數。 針對不是的作業, 您可以使用**rx_exec**在遠端計算內容中傳遞您的程式碼。

在此範例中, 沒有任何原始資料必須從 SQL Server 傳輸到 Jupyter Notebook。 所有計算都是在鳶尾花資料庫內進行, 只有影像檔案會傳回給用戶端。

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

下列螢幕擷取畫面顯示輸入和散佈圖輸出。

  ![顯示散佈圖輸出的 jupyter 筆記本](media/jupyter-notebook-scatterplot.png)


<a name="install-ide"></a>

## <a name="7---start-python-from-tools"></a>7-從工具啟動 Python

因為開發人員經常使用多個 Python 版本, 所以安裝程式不會將 Python 新增至您的路徑。 若要使用安裝程式所安裝的 Python 可執行檔和程式庫, 請在也提供**revoscalepy**和**microsoftml**的路徑上, 將您的 IDE 連結至**python .exe** 。 

### <a name="command-line"></a>命令列

當您從 C:\Program Files\Microsoft\PyForMLS (或您為 Python 用戶端程式庫安裝指定的任何位置) 執行**Python**時, 您可以存取完整的 Anaconda 發佈, 加上 Microsoft Python 模組, **revoscalepy**和**microsoftml**。

1. 移至 [C:\Program Files\Microsoft\PyForMLS], 然後按兩下 [ **Python .exe**]。
2. 開啟 [互動式說明]:`help()`
3. 在 [說明] 提示字元中輸入模組的名稱`help> revoscalepy`:。 [說明] 會傳回名稱、封裝內容、版本和檔案位置。
4. 在說明 **>** 提示字元中傳回版本和套件資訊`revoscalepy`:。 按 Enter 鍵以結束 [說明]。
5. 匯入模組:`import revoscalepy`


### <a name="jupyter-notebooks"></a>Jupyter 筆記本

本文使用內建的 Jupyter 筆記本來示範**revoscalepy**的函式呼叫。 如果您不熟悉這項工具, 下列螢幕擷取畫面將說明這些片段如何彼此搭配運作, 以及為什麼所有的「都能順利執行」。 

父資料夾 C:\Program Files\Microsoft\PyForMLS 包含 Anaconda 加上 Microsoft 套件。 Jupyter 筆記本包含在 Anaconda 中的 Scripts 資料夾底下, 而且 Python 可執行檔會自動向 Jupyter 筆記本註冊。 在網站套件下找到的套件可匯入至筆記本, 包括用於資料科學和機器學習的三個 Microsoft 套件。

  ![可執行檔和程式庫](media/jupyter-notebook-python-registration.png)

如果您使用另一個 IDE, 則需要將 Python 可執行檔和函式程式庫連結至您的工具。 下列各節提供常用工具的指示。

### <a name="visual-studio"></a>Visual Studio

如果您[在 Visual Studio 中有 python](https://code.visualstudio.com/docs/languages/python), 請使用下列設定選項來建立包含 Microsoft python 套件的 python 環境。

| 設定 | value |
|-----------------------|-------|
| **前置詞路徑** | C:\Program Files\Microsoft\PyForMLS |
| **解譯器路徑** | C:\Program Files\Microsoft\PyForMLS\python.exe |
| **視窗型解譯器** | C:\Program Files\Microsoft\PyForMLS\pythonw.exe |

如需設定 Python 環境的協助, 請參閱[管理 Visual Studio 中的 python 環境](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)。

### <a name="pycharm"></a>PyCharm

在 PyCharm 中, 將解譯器設定為 Machine Learning Server 所安裝的 Python 可執行檔。

1. 在新專案的 [設定] 中, 按一下 [**新增本機**]。

2. 輸入`C:\Program Files\Microsoft\PyForMLS\`。

您現在可以匯入**revoscalepy**、 **microsoftml**或**azureml**模組。 您也可以選擇 [**工具** > ] [**Python 主控台**] 來開啟互動式視窗。

## <a name="next-steps"></a>後續步驟

現在您已有工具和 SQL Server 的連線, 您可以使用[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)透過 Python 快速入門來擴充您的技能。

> [!div class="nextstepaction"]
> [入門確認 Python 存在於 SQL Server](../tutorials/quickstart-python-verify.md)