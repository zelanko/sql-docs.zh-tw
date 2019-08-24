---
title: 取得 Python 套件資訊
description: 瞭解如何在 SQL Server Machine Learning 服務上取得已安裝 Python 套件的相關資訊, 包括版本和安裝位置。
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/22/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1aa12da4a138ea8f292fa8b64db00456d3c35fe3
ms.sourcegitcommit: 01c8df19cdf0670c02c645ac7d8cc9720c5db084
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000442"
---
# <a name="get-python-package-information"></a>取得 Python 套件資訊

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明如何在 SQL Server Machine Learning 服務上取得已安裝之 Python 套件的相關資訊, 包括版本和安裝位置。 範例 Python 腳本會示範如何列出封裝資訊, 例如安裝路徑和版本。

## <a name="default-python-library-location"></a>預設 Python 程式庫位置

當您使用 SQL Server 安裝機器學習服務時, 系統會針對您安裝的每個語言, 在實例層級建立單一套件程式庫。 在 Windows 上, 實例程式庫是向 SQL Server 註冊的安全資料夾。

在 SQL Server 上執行的所有腳本或程式碼, 都必須從實例程式庫載入函數。 SQL Server 無法存取已安裝到其他程式庫的套件。 這也適用于遠端用戶端: 在伺服器計算內容中執行的任何 Python 程式碼, 都只能使用安裝在實例程式庫中的套件。
若要保護伺服器資產, 預設實例庫只能由電腦系統管理員修改。

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
適用于 Python 的二進位檔的預設路徑是:

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`
::: moniker-end

::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
適用于 Python 的二進位檔的預設路徑是:

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\PYTHON_SERVICES`
::: moniker-end

這會採用預設的 SQL 實例 MSSQLSERVER。 如果 SQL Server 安裝為使用者定義的命名實例, 就會改用指定的名稱。

執行下列語句, 以確認目前實例的預設程式庫。 這個範例會傳回 Python `sys.path`變數中包含的資料夾清單。 此清單包含目前目錄和標準程式庫路徑。

```sql
EXECUTE sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

如需變數`sys.path`的詳細資訊, 以及其如何用來設定模組的解譯器搜尋路徑, 請參閱[模組搜尋路徑](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)。

## <a name="default-python-packages"></a>預設 Python 套件

當您在安裝期間選取 Python 功能時, 會使用 SQL Server Machine Learning 服務來安裝下列 Python 套件。

| Packages | Version |  描述 |
| ---------|---------|--------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2 | 用於遠端計算內容、串流、平行執行 rx 函數以進行資料匯入和轉換、模型化、視覺化和分析。 |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2 | 在 Python 中新增機器學習演算法。 |

### <a name="component-upgrades"></a>元件升級

根據預設, Python 套件會透過 service pack 和累計更新進行重新整理。 核心 Python 元件的其他套件和完整版本升級只能透過產品升級, 或將 Python 支援系結至 Microsoft Machine Learning Server。

如需詳細資訊, 請參閱[在 SQL Server 中升級 R 和 Python 元件](../install/upgrade-r-and-python.md)。

## <a name="default-open-source-python-packages"></a>預設開放原始碼 Python 套件

當您在安裝期間選取 [Python 語言] 選項時, 會安裝 Anaconda 4.2 散發 (透過 Python 3.5)。 除了 Python 程式碼程式庫, 標準安裝還包含範例資料、單元測試和範例腳本。

> [!IMPORTANT]
> 您絕對不應該手動覆寫 web 上的更新版本 SQL Server 安裝程式所安裝的 Python 版本。 Microsoft Python 套件是以特定版本的 Anaconda 為基礎。 修改您的安裝可能不穩定。

## <a name="list-all-installed-python-packages"></a>列出所有已安裝的 Python 套件

下列範例腳本會顯示已安裝的套件及其版本的清單。

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

如果您已安裝 Python 套件, 而且想要確定它可用於特定的 SQL Server 實例, 您可以執行預存程式來載入封裝並傳回訊息。

例如, 下列程式`scikit-learn`代碼會尋找封裝。
如果找到封裝, 則程式碼會傳回「套件 scikit-learn-瞭解已安裝」訊息。

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import pkg_resources
pckg_name = "scikit-learn"
pckgs = pandas.DataFrame([(i.key) for i in pkg_resources.working_set], columns = ["key"])
installed_pckg = pckgs.query(''key == @pckg_name'')
print("Package", pckg_name, "is", "not" if installed_pckg.empty else "", "installed")
  '
```

<a name="get-package-vers"></a>

下列範例會傳回 revoscalepy 封裝和 Python 的版本。

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

+ [安裝新的 Python 封裝](../python/install-additional-python-packages-on-sql-server.md)
+ [取得 R 封裝資訊](r-package-information.md)
+ [安裝新的 R 封裝](../r/install-additional-r-packages-on-sql-server.md)
+ [R 和 Python 教學課程](../tutorials/machine-learning-services-tutorials.md)
