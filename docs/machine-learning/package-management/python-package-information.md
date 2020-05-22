---
title: 取得 Python 套件資訊
description: 了解如何取得 SQL Server 機器學習服務上已安裝之 Python 套件的相關資訊，包括版本與安裝位置。
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/01/2020
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fb08940a9a6c9c15d8c633f5b3c439514bc43646
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83605990"
---
# <a name="get-python-package-information"></a>取得 Python 套件資訊

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明如何取得 SQL Server 機器學習服務上已安裝之 Python 套件的相關資訊，包括版本與安裝位置。 範例 Python 指令碼會示範如何列出套件資訊，例如安裝路徑與版本。

## <a name="default-python-library-location"></a>預設 Python 程式庫位置

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
搭配 SQL Server 安裝機器學習時，會針對您安裝的每個語言在執行個體層次建立單一套件程式庫。 執行個體程式庫是一個向 SQL Server 註冊的受保護資料夾。
::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"
搭配 SQL Server 安裝機器學習時，會針對您安裝的每個語言在執行個體層次建立單一套件程式庫。
::: moniker-end

所有在 SQL Server 上資料庫內執行的指令碼或程式碼都必須從執行個體程式庫載入函式。 SQL Server 無法存取安裝至其他程式庫的套件。 這也適用於遠端用戶端：任何在伺服器計算內容中執行的 Python 程式碼都只能使用安裝在執行個體程式庫中的套件。
為了保護伺服器資產，只有電腦系統管理員才能修改預設執行個體程式庫。

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Python 的二進位檔預設路徑是：

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

這會假設預設 SQL 執行個體 MSSQLSERVER。 如果將 SQL Server 安裝成使用者定義的具名執行個體，則會改用指定的名稱。
::: moniker-end

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
Python 的二進位檔預設路徑是：

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\PYTHON_SERVICES`

這會假設預設 SQL 執行個體 MSSQLSERVER。 如果將 SQL Server 安裝成使用者定義的具名執行個體，則會改用指定的名稱。
::: moniker-end

執行下列 SQL 命令來啟用外部指令碼：

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH override;
```

請執行下列陳述式來確認目前執行個體的預設程式庫。 此範例會傳回 Python `sys.path` 變數中所包含的資料夾清單。 此清單包含目前目錄與標準程式庫路徑。

```sql
EXECUTE sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

如需有關 `sys.path` 變數及如何使用它來為模組設定解譯器搜尋路徑的詳細資訊，請參閱[模組搜尋路徑](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)。

## <a name="default-microsoft-python-packages"></a>預設 Microsoft Python 套件

以下是您在安裝期間選取 Python 功能時，與 SQL Server 機器學習服務一起安裝的 Microsoft Python 套件。

| Packages | 版本 |  描述 |
| ---------|---------|--------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.4.7 | 用於遠端計算內容、串流、平行執行 rx 函式以進行資料匯入與轉換、模型化、視覺化，以及分析。 |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.4.7 | 在 Python 中新增機器學習演算法。 |

如需包括哪個 Python 版本的相關資訊，請參閱 [Python 和 R 版本](../sql-server-machine-learning-services.md#versions)。

### <a name="component-upgrades"></a>元件升級

預設會透過 Service Pack 和累積更新重新整理 Python 套件。 額外套件及核心 Python 元件的完整版本升級只有透過產品升級或將 Python 支援繫結至 Microsoft Machine Learning Server，才可能實現。

如需詳細資訊，請參閱[升級 SQL Server 中的 R 和 Python 元件](../install/upgrade-r-and-python.md)。

## <a name="default-open-source-python-packages"></a>預設的開放原始碼 Python 套件

當您在安裝期間選取 Python 語言選項時，會安裝 Anaconda 4.2 散發套件 (透過 Python 3.5)。 除了 Python 程式碼程式庫之外，標準安裝還包含範例資料、單元測試及範例指令碼。

> [!IMPORTANT]
> 您一律不應手動以 Web 上較新的版本覆寫 SQL Server 安裝程式所安裝的 Python 版本。 Microsoft Python 套件以特定 Anaconda 版本為基礎。 修改安裝可能使其變得不穩定。

## <a name="list-all-installed-python-packages"></a>列出所有已安裝的 Python 套件

下列範例指令碼會顯示一個清單，列出安裝在 SQL Server 執行個體中的所有 Python 套件。

```sql
EXECUTE sp_execute_external_script 
  @language = N'Python', 
  @script = N'
import pkg_resources
import pandas as pd
installed_packages = pkg_resources.working_set
installed_packages_list = sorted(["%s==%s" % (i.key, i.version) for i in installed_packages])
df = pd.DataFrame(installed_packages_list)
OutputDataSet = df
'
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

## <a name="find-a-single-python-package"></a>尋找單一 Python 套件

如果您已安裝 Python 套件並想確定該套件可用於特定 SQL Server 執行個體，則可以執行預存程序來尋找套件並傳回訊息。

例如，下列程式碼會尋找 `scikit-learn` 套件。
如果找到該套件，程式碼會列印套件版本。

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import pkg_resources
pkg_name = "pandas"
try:
    version = pkg_resources.get_distribution(pkg_name).version
    print("Package " + pkg_name + " is version " + version)
except:
    print("Package " + pkg_name + " not found")
'
```

結果：

```text
STDOUT message(s) from external script: Package pandas is version 0.23.4
```

下列範例會列印套件 `pandas` 的版本。

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import pkg_resources
pkg_name = "pandas"
print(pkg_name + " package is version " + pkg_resources.get_distribution(pkg_name).version)
'
```

下列範例會傳回 Python 的版本。

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import sys
print(sys.version)
'
```

## <a name="next-steps"></a>後續步驟

::: moniker range="<=sql-server-2017||=sqlallproducts-allversions"
+ [使用 Python 工具來安裝套件](install-python-packages-standard-tools.md)
::: moniker-end
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
+ [使用 sqlmlutils 安裝新的 Python 套件](install-additional-r-packages-on-sql-server.md)
::: moniker-end