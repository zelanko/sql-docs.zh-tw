---
title: 取得 SQL Server 機器學習的 R，並將 Python 封裝資訊 |Microsoft 文件
description: 判斷 R，並將 Python 封裝版本、 驗證安裝，並取得一份已安裝 SQL Server R 服務或機器學習服務上的封裝。
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/08/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3295bbdbb00c73c9aaa37dcb15d35121b82454bb
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2018
---
#  <a name="get-r-and-python-package-information-on-sql-server-machine-learning"></a>取得 SQL Server 機器學習的 R，並將 Python 封裝資訊
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

如果您已安裝多個 Python 環境，或使用 R 的多個工具，很容易將套件安裝到錯誤的媒體櫃或環境，則無法日後尋找它。 本文章提供查詢和指導方針適用於 determininga 封裝版本，以及列出已安裝目前的 SQL Server 環境中的封裝。

## <a name="verify-the-current-default-library"></a>確認目前的預設程式庫

如**R**在 SQL Server 中，執行下列陳述式，請確認目前的執行個體的預設程式庫：

```sql
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

如**Python**在 SQL Server 中，執行下列陳述式，請確認目前的執行個體的預設程式庫：

```sql
EXEC sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

## <a name="generate-a-package-list-using-a-stored-procedure"></a>產生使用預存程序的封裝清單

有多種方法，您可以取得目前安裝的套件的完整清單。 Sp_execute_external_script 執行中封裝清單命令的其中一個優點是保證以取得安裝執行個體文件庫中的封裝。

### <a name="r"></a>R

下列範例使用 R 函式`installed.packages()`中[!INCLUDE[tsql](..\..\includes\tsql-md.md)]預存程序取得已安裝目前的執行個體 R_SERVICES 文件庫中的封裝矩陣。 為了避免剖析 DESCRIPTION 檔案中的欄位，只會傳回名稱。

```SQL
EXECUTE sp_execute_external_script
@language=N'R'
,@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
NameOnly <- packagematrix[,1];
OutputDataSet <- as.data.frame(NameOnly);'
, @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250) ))
```

如需詳細的選擇性資訊和 R 封裝的描述欄位的預設欄位，請參閱[ https://cran.r-project.org ](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)。

### <a name="python"></a>Python

`pip`模組安裝依預設，並且可支援許多列出安裝套件時，除了標準的 Python 所支援的作業。 您可以執行`pip`Python 從命令提示字元中，但您也可以呼叫某些 pip 函式，從`sp_execute_external_script`。

```sql
execute sp_execute_external_script 
@language = N'Python', 
@script = N'
import pip
import pandas as pd
installed_packages = pip.get_installed_distributions()
installed_packages_list = sorted(["%s==%s" % (i.key, i.version)
     for i in installed_packages])
df = pd.DataFrame(installed_packages_list)
OutputDataSet = df
'
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

當執行`pip`從命令列中，還有許多其他有用的函式：`pip list`取得所有已安裝的封裝，而`pip freeze`列出所安裝的套件`pip`，並不會列出 pip 本身的封裝而定。 您也可以使用`pip freeze`產生相依性檔案。

## <a name="verify-whether-a-package-is-installed-with-an-instance"></a>確認封裝是否已安裝的執行個體

如果您已安裝封裝，並想要確定它是適用於特定的 SQL Server 執行個體，您可以執行下列預存程序呼叫來載入封裝，並傳回只有訊息。

### <a name="r"></a>R

這個範例會尋找並載入 RevoScaleR 程式庫中，如果有的話。

```sql
EXEC sp_execute_external_script  @language =N'R',
@script=N'require("RevoScaleR")'
GO
```

+ 如果找到封裝，傳回一則訊息: 「 命令成功完成。 」

+ 如果不能位於或載入封裝，您會收到含有文字錯誤: 「 有 」 呼叫 'MissingPackageName' 沒有封裝

### <a name="python"></a>Python

您可以從 Python 執行 Python 的相等檢查殼層，使用`conda`或`pip`命令。 或者，在預存程序中執行此陳述式：

```sql
exec sp_execute_external_script
       @language = N'Python'
       , @script = N'
import pip
import pkg_resources
pckg_name = "revoscalepy"
pckgs = pandas.DataFrame([(i.key) for i in pip.get_installed_distributions()], columns = ["key"])
installed_pckg = pckgs.query(''key == @pckg_name'')
print("Package", pckg_name, "is", "not" if installed_pckg.empty else "", "installed")'
```

## <a name="view-installed-packages-using-a-utility-or-ide"></a>檢視已安裝的封裝使用的公用程式或 IDE

大部分的開發工具提供物件瀏覽器或所安裝，或在目前的工作區或環境中載入的封裝清單。 本節提供簡短的一些祕訣使用熱門的 R 或 Python 工具。

### <a name="r-tools"></a>R 工具

有多個方法來取得一份使用 R 公用程式的安裝或載入封裝。 

+ 從本機的 R 公用程式，使用基底 R 函數，例如`installed.packages()`，隨附於`utils`封裝。 若要取得正確的執行個體的清單，您必須明確地指定程式庫路徑，或使用與執行個體文件庫相關聯的 R 工具。

### <a name="python-tools"></a>Python 工具

Visual Studio 的 Python 擴充功能，請很容易就能檢視安裝在目前的環境中，或其他 IDE 中所列的虛擬環境中的封裝。 您可以設定多個環境、 從清單中，選擇 環境檢視封裝或以該環境中安裝新的封裝。

+ [Python 環境](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)

Visual Studio 程式碼是可用的編輯器，支援數個可用的 Python linters Python。 雖然 VS 程式碼不會提供類似 Visual Studio 中的封裝瀏覽器，它支援設定，以及在多個環境之間切換。

+ [在 Visual Studio 程式碼中的 Python](https://code.visualstudio.com/docs/languages/python)

執行時可能需要一些額外的設定**revoscalepy**來自遠端用戶端的命令：

+ [自訂 Python 封裝和解譯器本機上安裝 Windows](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)

這篇部落格提供一些設定其他的 Python 環境，包括 PyCharm，若要使用的實用秘訣**revoscalepy**。

+ [開始使用 Python Web 服務使用機器學習伺服器](https://blogs.msdn.microsoft.com/mlserver/2017/12/13/getting-started-with-python-web-services-using-machine-learning-server/)

## <a name="use-functions-from-machine-learning-server"></a>使用從 Server 機器學習服務函數

因為使用與 SQL Server 支援執行的程式碼從遠端用戶端程式庫，您可以使用這些函數來找出哪些封裝會安裝在遠端環境中。

### <a name="revoscaler"></a>RevoScaleR

如果您正在遠端用戶端，而且不需要伺服器的存取權，您仍然可以取得使用 RevoScaleR 函數來安裝 SQL Server 的封裝清單。 您可以指定 SQL Server 做為運算環境，您需要連線到伺服器的權限。 

+ [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage)尋找遠端計算內容中的封裝路徑。

+ [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages)取得計算內容中安裝套件的相關資訊。

例如，執行下列 R 程式碼，以取得指定的 SQL Server 計算內容中可用的封裝清單。

```R
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
sqlPackages
```

下列範例會取得在本機計算內容和封裝版本的 RevoScaleR 文件庫位置。

```R
rxFindPackage(RevoScaleR, "local")
packageVersion("RevoScaleR")
```

### <a name="revoscalepy"></a>revoscalepy

此時，沒有可用類似的 RevoScaleR 函式。 在新版中尋找這些**revoscalepy**。

## <a name="get-library-location-and-version"></a>取得程式庫位置和版本

有時當您正在使用多個環境或安裝的 R 或 Python，您需要確認您正在執行的程式碼使用 Python 或 [正確] 工作區進行正確的環境如。

例如，如果您已升級的機器學習使用繫結元件，R 程式庫的路徑可能比預設值的不同資料夾中。 此外，如果您安裝 R 用戶端或獨立伺服器執行個體，您可能多個 R 程式庫在您的電腦上。

這些範例會示範如何取得的路徑和版本的 SQL Server 正在使用的文件庫。

### <a name="r"></a>R

這個預存程序會傳回執行個體文件庫的路徑和版本的 SQL Server 所使用的 RevoScaleR 封裝：

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'
  sql_r_path <- rxSqlLibPaths("local")
  print(sql_r_path)
  version_info <-packageVersion("RevoScaleR")
  print(version_info)'
```

> [!NOTE]
> [RxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths)函式可以只在目標電腦上執行。 此函式不能傳回遠端連接程式庫的路徑。

**結果**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.2.1'
```

### <a name="python"></a>Python

這個範例會傳回包含在 Python 的資料夾清單`sys.path`變數。 此清單包含目前的目錄和標準程式庫路徑。

```sql
EXEC sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

**結果**

```text
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\python35.zip
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\DLLs
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Sphinx-1.5.4-py3.5.egg
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Pythonwin
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\setuptools-27.2.0-py3.5.egg
```

如需有關變數`sys.path`以及如何它用來設定模組，解譯器搜尋路徑，請參閱[Python 文件](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)

