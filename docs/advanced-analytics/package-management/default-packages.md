---
title: 取得 R 和 Python 套件資訊
description: 判斷 R 和 Python 套件版本、確認安裝, 並取得 SQL Server R Services 或 Machine Learning 服務上已安裝的套件清單。
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: dec0fe7147eab6a4b6545decf99e1731d773957c
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343424"
---
#  <a name="get-r-and-python-package-information"></a>取得 R 和 Python 套件資訊
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

有時候當您使用多個環境或 R 或 Python 的安裝時, 您必須確認您執行的程式碼使用 Python 的預期環境, 或 R 的正確工作區。例如, 如果您已[升級 r 或 Python](../install/upgrade-r-and-python.md), r 程式庫的路徑可能位於與預設值不同的資料夾中。 此外, 如果您安裝 R 用戶端或獨立伺服器的實例, 您的電腦上可能會有多個 R 程式庫。

本文中的 R 和 Python 腳本範例會示範如何取得 SQL Server 所使用之封裝的路徑和版本。

## <a name="get-the-r-library-location"></a>取得 R 程式庫位置

針對任何版本的 SQL Server, 執行下列語句來確認目前實例的預設 R 封裝程式庫:

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

(選擇性) 您可以在較新版本的 RevoScaleR 中使用[rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) , SQL Server 2017 Machine Learning 服務或[R Services 升級 r 到至少 RevoScaleR 9.0.1](../install/upgrade-r-and-python.md)。 這個預存程式會傳回實例程式庫的路徑, 以及 SQL Server 所使用的 RevoScaleR 版本:

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
> [RxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths)函數只能在本機電腦上執行。 函數無法傳回遠端連線的程式庫路徑。

**結果**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.3.0'
```

## <a name="get-the-python-library-location"></a>取得 Python 程式庫位置

針對 SQL Server 2017 中的**Python** , 請執行下列語句來確認目前實例的預設程式庫。 這個範例會傳回 Python `sys.path`變數中包含的資料夾清單。 此清單包含目前的目錄和標準程式庫路徑。

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

如需變數`sys.path`的詳細資訊, 以及如何使用它來設定解譯器的模組搜尋路徑, 請參閱[Python 檔](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)

## <a name="list-all-packages"></a>列出所有套件

有多種方法可讓您取得目前已安裝之套件的完整清單。 從 sp_execute_external_script 執行封裝清單命令的其中一個優點是, 您保證會取得安裝在實例程式庫中的封裝。

### <a name="r"></a>R

下列範例會[!INCLUDE[tsql](../../includes/tsql-md.md)]在預存程式`installed.packages()`中使用 R 函數, 以取得已安裝在目前實例之 R_SERVICES 程式庫中的封裝矩陣。 此腳本會傳回描述檔案中的 [封裝名稱] 和 [版本] 欄位, 而只會傳回名稱。

```sql
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

如需 [R 封裝描述] 欄位之選擇性和預設欄位的詳細資訊, [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)請參閱。

### <a name="python"></a>Python

此`pip`模組預設會安裝, 而且除了標準 Python 支援的套件之外, 還支援許多作業來列出已安裝的封裝。 當然, 您`pip`可以從 Python 命令提示字元執行, 但是您也可以從`sp_execute_external_script`呼叫一些 pip 函數。

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

從命令列執行時, 有許多其他有用的函式: `pip list`取得已安裝的所有封裝, 而`pip freeze`列出所安裝`pip`的套件, 且不會列出 pip 本身的封裝`pip`視而定。 您也可以使用`pip freeze`來產生相依性檔案。

## <a name="find-a-single-package"></a>尋找單一套件

如果您已安裝封裝, 而且想要確定它可用於特定的 SQL Server 實例, 您可以執行下列預存程序呼叫, 以載入封裝並只傳回訊息。

### <a name="r"></a>R

這個範例會尋找並載入 RevoScaleR 程式庫 (如果有的話)。

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("RevoScaleR")'
GO
```

+ 如果找到封裝, 則會傳回訊息:「命令已順利完成。」

+ 如果找不到或無法載入封裝, 您會收到包含下列文字的錯誤: 「沒有名為 ' MissingPackageName ' 的套件」

### <a name="python"></a>Python

您可以使用`conda`或`pip`命令, 從 python shell 執行 python 的對等檢查。 或者, 在預存程式中執行此語句:

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

<a name="get-package-vers"></a>

## <a name="get-package-version"></a>取得套件版本

您可以使用 Management Studio 來取得 R 和 Python 套件版本資訊。

### <a name="r-package-version"></a>R 封裝版本

此語句會傳回 RevoScaleR 封裝版本和基底 R 版本。

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("RevoScaleR"))
print(packageDescription("base"))
'
```

### <a name="python-package-version"></a>Python 套件版本

此語句會傳回 revoscalepy 套件版本和 Python 版本。

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import revoscalepy
import sys
print(revoscalepy.__version__)
print(sys.version)
'
```

## <a name="next-steps"></a>後續步驟

+ [安裝新的 R 封裝](../r/install-additional-r-packages-on-sql-server.md)
+ [安裝新的 Python 封裝](../python/install-additional-python-packages-on-sql-server.md)
+ [教學課程、範例、解決方案](../tutorials/machine-learning-services-tutorials.md)