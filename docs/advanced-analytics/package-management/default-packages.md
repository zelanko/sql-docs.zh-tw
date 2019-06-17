---
title: 取得 R 和 Python 套件的資訊-SQL Server Machine Learning 服務
description: 判斷 R 和 Python 套件版本、 確認安裝，並取得一份 SQL Server R Services 或 Machine Learning 服務上已安裝的套件。
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: c2cf95e2d86836cd22aaa9dc67942f9d83c97e8c
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/14/2019
ms.locfileid: "67141407"
---
#  <a name="get-r-and-python-package-information"></a>取得 R 和 Python 套件資訊
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

有時當您正在使用多個環境或安裝的 R 或 Python，您需要確認您正在執行的程式碼使用適用於 Python 或正確的工作區的預期的環境進行。例如，如果您有[升級 R 或 Python](../install/upgrade-r-and-python.md)，R 程式庫的路徑可能會在與預設值不同的資料夾。 此外，如果您安裝 R Client 或獨立伺服器執行個體，您可能必須多個 R 程式庫在您的電腦上。

這篇文章中的 R 和 Python 指令碼範例會示範如何取得的路徑和版本的 SQL Server 所使用的套件。

## <a name="get-the-r-library-location"></a>取得 R 程式庫位置

如需 SQL Server 任何版本，執行下列陳述式，以確認目前的執行個體的預設 R 套件程式庫：

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

或者，您可以使用[rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths)較新版本的 SQL Server 2017 Machine Learning 服務中的 RevoScaleR 中或[R Services 至少升級到的 R RevoScaleR 9.0.1](../install/upgrade-r-and-python.md)。 執行個體的程式庫路徑，以及 SQL Server 所使用的 RevoScaleR 的版本，則會傳回此預存程序：

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
> [RxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths)可以只在本機電腦上執行函式。 此函數無法傳回遠端連線程式庫的路徑。

**結果**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.3.0'
```

## <a name="get-the-python-library-location"></a>取得 Python 程式庫位置

針對**Python**在 SQL Server 2017 中，執行下列陳述式，以確認目前的執行個體的預設程式庫。 這個範例會傳回包含在 Python 中的資料夾清單`sys.path`變數。 此清單包含目前的目錄，以及標準程式庫路徑。

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

如需有關變數`sys.path`以及如何它用來設定模組的解譯器搜尋路徑，請參閱[Python 文件](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)

## <a name="list-all-packages"></a>列出所有封裝

有多種方式，您可以取得目前安裝的套件的完整清單。 從 sp_execute_external_script 中執行套件清單命令的其中一個優點是，您一定會取得執行個體文件庫中安裝的套件。

### <a name="r"></a>R

下列範例使用 R 函式`installed.packages()`在[!INCLUDE[tsql](../../includes/tsql-md.md)]預存程序，若要取得的已安裝在目前的執行個體的 R_SERVICES 程式庫中的封裝矩陣。 此指令碼會傳回封裝名稱 和 版本 欄位，DESCRIPTION 檔案中，只傳回名稱。

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

如需詳細的選擇性資訊和 R 套件的描述欄位的預設欄位，請參閱[ https://cran.r-project.org ](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)。

### <a name="python"></a>Python

`pip`模組安裝預設的情況下，並且可支援列出安裝套件，除了標準的 Python 支援的許多作業。 您可以執行`pip`的 python 命令提示字元中，當然，但您也可以呼叫某些 pip 函式，從`sp_execute_external_script`。

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

執行時`pip`從命令列中，有許多其他有用的功能：`pip list`取得已安裝的所有封裝，而`pip freeze`列出所安裝的套件`pip`，並不會列出 pip 本身的套件而定。 您也可以使用`pip freeze`產生相依性檔案。

## <a name="find-a-single-package"></a>找到單一套件

如果您安裝的套件，並想要確定它可供特定的 SQL Server 執行個體，您可以執行下列預存程序呼叫來載入封裝，並傳回只有訊息。

### <a name="r"></a>R

此範例會尋找並載入 RevoScaleR 程式庫中，如果有的話。

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("RevoScaleR")'
GO
```

+ 如果找到封裝，則會傳回一則訊息：「 命令已順利完成 」。

+ 如果無法找到或載入封裝，您會取得包含文字的錯誤: 「 沒有任何套件，稱為 'MissingPackageName' 」

### <a name="python"></a>Python

適用於 Python 的相等檢查可以執行來自 Python 殼層，使用`conda`或`pip`命令。 或者，在預存程序中執行此陳述式：

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

## <a name="get-package-version"></a>取得封裝版本

您可以取得 R 和 Python 套件使用 Management Studio 的版本資訊。

### <a name="r-package-version"></a>R 套件版本

這個陳述式會傳回 RevoScaleR 套件版本與基底的 R 版本。

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("RevoScaleR"))
print(packageDescription("base"))
'
```

### <a name="python-package-version"></a>Python 套件版本

此陳述式會傳回 revoscalepy 套件版本和 Python 的版本。

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