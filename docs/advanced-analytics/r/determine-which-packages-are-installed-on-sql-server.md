---
title: 取得 SQL Server 機器學習的 R，並將 Python 封裝資訊 |Microsoft 文件
description: 判斷 R，並將 Python 封裝版本、 驗證安裝，並取得一份已安裝 SQL Server R 服務或機器學習服務上的封裝。
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 85ea4658ca8b60fc24d7e4f7849de1655eab6082
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707886"
---
#  <a name="get-r-and-python-package-information"></a>取得 R，並將 Python 封裝資訊
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

有時當您正在使用多個環境或安裝的 R 或 Python，您需要確認您正在執行的程式碼使用 Python 或 [正確] 工作區的預期的環境進行。例如，如果您已升級的機器學習元件透過[繫結](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)，R 程式庫的路徑可能是預設值不同的資料夾中。 此外，如果您安裝 R 用戶端或獨立伺服器執行個體，您可能多個 R 程式庫在您的電腦上。

本文中的 R，並將 Python 指令碼範例會示範如何取得的路徑和版本的 SQL Server 所使用的套件。

## <a name="get-the-r-library-location"></a>取得的 R 程式庫位置

任何版本的 SQL Server 中，執行下列陳述式來確認[預設 R 封裝程式庫](installing-and-managing-r-packages.md)目前執行個體：

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

或者，您可以使用[rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths)在較新版本的 SQL Server 2017 機器學習服務中的 RevoScaleR 或[R 服務升級後 R 要在最低 RevoScaleR 9.0.1](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。 這個預存程序會傳回執行個體的程式庫的路徑與 RevoScaleR SQL Server 所使用的版本：

```sql
EXECUTE sp_execute_external_script
  @language =N'R',
  @script=N'
  sql_r_path <- rxSqlLibPaths("local")
  print(sql_r_path)
  version_info <-packageVersion("RevoScaleR")
  print(version_info)'
```

> [!NOTE]
> [RxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths)函式可以只在本機電腦上執行。 此函式不能傳回遠端連接程式庫的路徑。

**結果**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.3.0'
```

## <a name="get-the-python-library-location"></a>取得的 Python 程式庫位置

如**Python**中 SQL Server 2017，執行下列陳述式，請確認目前的執行個體的預設程式庫。 這個範例會傳回包含在 Python 的資料夾清單`sys.path`變數。 此清單包含目前的目錄和標準程式庫路徑。

```sql
EXECUTE sp_execute_external_script
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

## <a name="list-all-packages"></a>列出所有的封裝

有多種方法，您可以取得目前安裝的套件的完整清單。 Sp_execute_external_script 執行中封裝清單命令的其中一個優點是保證以取得安裝執行個體文件庫中的封裝。

### <a name="r"></a>R

下列範例使用 R 函式`installed.packages()`中[!INCLUDE[tsql](..\..\includes\tsql-md.md)]預存程序取得已安裝目前的執行個體 R_SERVICES 文件庫中的封裝矩陣。 此指令碼會傳回封裝的名稱和版本欄位 DESCRIPTION 檔案中，只傳回名稱。

```SQL
EXECUTE sp_execute_external_script
  @language=N'R',
  @script = N'str(OutputDataSet);
  packagematrix <- installed.packages();
  Name <- packagematrix[,1];
  Version <- packagematrix[,3];
  OutputDataSet <- data.frame(Name, Version);',
  @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

如需詳細的選擇性資訊和 R 封裝的描述欄位的預設欄位，請參閱[ https://cran.r-project.org ](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)。

### <a name="python"></a>Python

`pip`模組安裝依預設，並且可支援許多列出安裝套件時，除了標準的 Python 所支援的作業。 您可以執行`pip`Python 從命令提示字元中，但您也可以呼叫某些 pip 函式，從`sp_execute_external_script`。

```sql
EXECUTE sp_execute_external_script 
  @language = N'Python', 
  @script = N'
  import pip
  import pandas as pd
  installed_packages = pip.get_installed_distributions()
  installed_packages_list = sorted(["%s==%s" % (i.key, i.version)
     for i in installed_packages])
  df = pd.DataFrame(installed_packages_list)
  OutputDataSet = df'
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

當執行`pip`從命令列中，還有許多其他有用的函式：`pip list`取得所有已安裝的封裝，而`pip freeze`列出所安裝的套件`pip`，並不會列出 pip 本身的封裝而定。 您也可以使用`pip freeze`產生相依性檔案。

## <a name="find-a-single-package"></a>尋找單一封裝

如果您已安裝封裝，並想要確定它是適用於特定的 SQL Server 執行個體，您可以執行下列預存程序呼叫來載入封裝，並傳回只有訊息。

### <a name="r"></a>R

這個範例會尋找並載入 RevoScaleR 程式庫中，如果有的話。

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("RevoScaleR")'
GO
```

+ 如果找到封裝，傳回一則訊息: 「 命令成功完成。 」

+ 如果不能位於或載入封裝，您會收到含有文字錯誤: 「 有 」 呼叫 'MissingPackageName' 沒有封裝

### <a name="python"></a>Python

您可以從 Python 執行 Python 的相等檢查殼層，使用`conda`或`pip`命令。 或者，在預存程序中執行此陳述式：

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
  import pip
  import pkg_resources
  pckg_name = "revoscalepy"
  pckgs = pandas.DataFrame([(i.key) for i in pip.get_installed_distributions()], columns = ["key"])
  installed_pckg = pckgs.query(''key == @pckg_name'')
  print("Package", pckg_name, "is", "not" if installed_pckg.empty else "", "installed")'
```

## <a name="get-package-information-in-r-and-python-tools"></a>取得封裝資訊在 R 和 Python 工具

所有的前述指示假設您使用 SQL Server 工具，例如 Management Studio (SSMS)。 如果您想使用 R，並將 Python tools，下列指示說明如何從 R 或 Python 的命令列取得程式庫和套件的資訊。

### <a name="r-commands"></a>R 命令

R 的執行個體程式庫是 files\microsoft SQL Server\MSSQL14。MSSQLSERVER\R_SERVICES\library。

啟動標準的 R 工具，以確保執行個體文件庫中的封裝會使用這些位置中：

+ \MSSQL14。MSSQLSERVER\R_SERVICES\bin\R.exe R 命令提示字元
+ \MSSQL14。MSSQLSERVER\R_SERVICES\bin\x64\Rgui.exe 到 R 主控台應用程式

您可以使用標準 R 命令或 RevoScaleR 命令，以取得封裝資訊。 RevoScaleR 封裝會自動載入。 

傳回的 RevoScaleR 封裝資訊：

    > print(Revo.version)

傳回所有已安裝的封裝清單：

    > installed.packages()

傳回版本的:

    > packageDescription("base")

### <a name="python-commands"></a>Python 命令

Python 支援 SQL Server 2017 只有。 Python 的執行個體程式庫是 files\microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\。

從這個位置，以確保執行個體文件庫中的封裝會開啟 [Python 命令] 視窗：

+ \MSSQL14。MSSQLSERVER\PYTHON_SERVICES\Python.exe

開啟 互動式說明：

    > help()

模組名稱在提示中輸入說明以取得封裝的內容、 版本和檔案位置：

    help> revoscalepy

<a name="pip-conda"></a>

### <a name="python-package-managers-pip-and-conda"></a>Python 封裝管理員 （Pip 和 Conda）

Anaconda 包括用來管理封裝的 Python 工具。 預設執行個體、 Pip、 Conda 和其他工具可以找到在 \Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\Scripts。

SQL Server 安裝程式不會新增 Pip 或 Conda 至系統路徑，並在實際執行 SQL Server 的執行個體，讓非必要的可執行檔路徑不是最佳作法。 不過，開發和測試環境中，您可以系統 PATH 環境變數，在命令上執行 Pip 和 Conda，從任何位置加入指令碼 資料夾。

1. 移至 C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\Scripts

1. 以滑鼠右鍵按一下**conda.exe** > **系統管理員身分執行**，並輸入`conda list`傳回目前環境中安裝的封裝清單。

1. 同樣地，以滑鼠右鍵按一下**pip.exe** > **系統管理員身分執行**，並輸入`pip list`傳回相同的資訊。 


## <a name="next-steps"></a>後續的步驟

+ [安裝新的 R 封裝](install-additional-r-packages-on-sql-server.md)
+ [安裝新的 Python 封裝](../python/install-additional-python-packages-on-sql-server.md)
+ [教學課程、範例、解決方案](../tutorials/machine-learning-services-tutorials.md)