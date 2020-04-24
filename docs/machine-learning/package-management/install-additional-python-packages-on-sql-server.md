---
title: 使用 sqlmlutils 安裝 Python 套件
description: 了解如何使用 Python pip，在 SQL Server 機器學習服務服務的執行個體上安裝新的 Python 套件。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/30/2020
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4e72ded2e2f2a51805403132c662bff3d70c97ce
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487108"
---
# <a name="install-python-packages-with-sqlmlutils"></a>使用 sqlmlutils 安裝 Python 套件

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明如何使用 [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) 套件中的函式，將新的 Python 套件安裝到 SQL Server 機器學習服務的執行個體上。 您安裝的套件可用於使用 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) T-SQL 陳述式在資料庫中執行的 Python 指令碼。

如需套件位置和安裝路徑的詳細資訊，請參閱[取得 Python 套件資訊](../package-management/python-package-information.md)。

> [!NOTE]
> 不建議使用標準 Python `pip install` 命令在 SQL Server 2019 上新增 Python 套件。 請依照此文章所述改為使用 **sqlmlutils**。

## <a name="prerequisites"></a>Prerequisites

+ 您必須使用 Python 語言選項安裝 [SQL Server 機器學習服務](../install/sql-machine-learning-services-windows-install.md)。

+ 在用來連線到 SQL Server 的用戶端電腦上安裝 [python](https://www.python.org/)。 您也可能想要有 Python 開發環境，例如加裝 [Python 延伸模組](https://marketplace.visualstudio.com/items?itemName=ms-python.python)的 [Visual Studio Code](https://code.visualstudio.com/download)。 

+ 在用來連線到 SQL Server 的用戶端電腦上安裝 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) 或 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) (SSMS)。 您可以使用其他資料庫管理或查詢工具，但此文章假設使用 Azure Data Studio 或 SSMS。

### <a name="other-considerations"></a>其他考量

+ 套件必須與您擁有的 Python 版本相容。 如需每個 SQL Server 版本所隨附 Python 版本的詳細資訊，請參閱[什麼是 SQL Server 機器學習服務 (Python 與 R) 中的 Python 與 R 版本](../sql-server-machine-learning-services.md#versions)

+ Python 套件程式庫位於 SQL Server 執行個體的 Program Files 資料夾中，而且根據預設，在此資料夾中安裝需要系統管理員權限。 如需詳細資訊，請參閱[套件程式庫位置](../package-management/python-package-information.md#default-python-library-location)。

+ 套件安裝是按每個執行個體進行。 如果您有多個機器學習服務的執行個體，則必須將套件新增至每一個執行個體。

+ 新增套件之前，請考慮套件是否適合用於 SQL Server 環境。

  + 我們建議您在資料庫中使用 Python，以進行與資料庫引擎 (例如機器學習服務) 緊密整合的工作，而不是單純查詢資料庫的工作。

  + 如果您新增的套件為伺服器帶來過多的計算壓力，效能將會受到影響。

  + 在已強化的 SQL Server 環境中，您可以避免下列情況：
    + 需要網路存取的套件
    + 需要提升檔案系統存取權的套件
    + 用於網頁程式開發或其他工作，但無法透過在 SQL Server 內部執行而獲益的套件

## <a name="install-sqlmlutils-on-the-client-computer"></a>在用戶端電腦上安裝 sqlmlutils

若要使用 **sqlmlutils**，您必須先將其安裝在用來連接到 SQL Server 的用戶端電腦上。 請確定您已安裝 `pip`，並請參閱 [pip 安裝](https://pip.pypa.io/en/stable/installing/)以了解詳細資訊。

1. 從 https://github.com/Microsoft/sqlmlutils/tree/master/Python/dist 將最新的 **sqlmlutils** ZIP 檔案下載到用戶端電腦。 請勿解壓縮檔案。

1. 開啟 [命令提示字元]  並執行下列命令，以安裝 **sqlmlutils** 套件。 以您所下載 **sqlmlutils** ZIP 檔案的完整路徑取代，此範例假設下載的檔案是 `c:\temp\sqlmlutils-1.0.0.zip`。

   ```console
   pip install "pymssql<3.0"
   pip install --upgrade --upgrade-strategy only-if-needed c:\temp\sqlmlutils-1.0.0.zip
   ```

## <a name="add-a-python-package-on-sql-server"></a>在 SQL Server 上新增 Python 套件

在下列範例中，您會將 [text-tools](https://pypi.org/project/text-tools/) 套件新增至 SQL Server。

### <a name="add-the-package-online"></a>線上新增套件

如果您用來連線到 SQL Server 的用戶端電腦可以存取網際網路，則可以使用 **sqlmlutils** 透過網際網路尋找 **text-tools** 套件和任何相依性，然後從遠端將套件安裝到 SQL Server 執行個體。

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

1. 在用戶端電腦上，開啟 **Python** 或 Python 環境。

1. 使用下列命令來安裝 **text-tools** 套件。 替代自有的 SQL Server 資料庫連線資訊 (如果使用 Windows 驗證，則不需要 `uid` 和 `pwd` 參數)。

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

1. 在用戶端電腦上，開啟 **Python** 或 Python 環境。

1. 使用下列命令來安裝 **text-tools** 套件。 替換為您自己的 SQL Server 資料庫連線資訊。

::: moniker-end

   ```python
   import sqlmlutils
   connection = sqlmlutils.ConnectionInfo(server="server", database="database", uid="username", pwd="password")
   sqlmlutils.SQLPackageManager(connection).install("text-tools")
   ```

### <a name="add-the-package-offline"></a>離線新增套件

如果您用來連接到 SQL Server 的用戶端電腦沒有網際網路連線，您可以在能存取網際網路的電腦上使用 **pip**，將套件和任何相依套件下載到本機資料夾。 然後，將資料夾複製到用戶端電腦，讓您可以離線安裝套件。

#### <a name="on-a-computer-with-internet-access"></a>在有網際網路存取的電腦上

1. 開啟 [命令提示字元]  並執行下列命令，以建立包含 **text-tools** 套件的本機資料夾。 這個範例會建立 `c:\temp\text-tools` 資料夾。

   ```console
   pip download text-tools -d c:\temp\text-tools
   ```

1. 將 `text-tools` 資料夾複製到用戶端電腦。 下列範例假設您已將其複製到 `c:\temp\packages\text-tools`。

#### <a name="on-the-client-computer"></a>在用戶端電腦上

使用 **sqlmlutils**，安裝您在 **pip** 建立的本機資料夾中找到的每個套件 (WHL 檔案)。 安裝套件的順序並不重要。

在此範例中，**text-tools** 沒有相依性，因此 `text-tools` 資料夾中只有一個檔案可供您安裝。 相反地，**scikit-plot** 之類的套件有11 個相依性，因此您會在資料夾中找到 12 個檔案 (**scikit-plot** 套件和 11 個相依套件)，而且您將會安裝每個檔案。

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

請執行下列 Python 指令碼。 替代實際檔案路徑和套件名稱，以及自有的 SQL Server 資料庫連線資訊 (如果使用 Windows 驗證，則不需要 `uid` 和 `pwd` 參數)。 針對資料夾中的每個套件檔案重複 `sqlmlutils.SQLPackageManager` 陳述式。

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

請執行下列 Python 指令碼。 替代實際檔案路徑和套件名稱，以及自有的 SQL Server 資料庫連線資訊。 針對資料夾中的每個套件檔案重複 `sqlmlutils.SQLPackageManager` 陳述式。

::: moniker-end

```python
import sqlmlutils
connection = sqlmlutils.ConnectionInfo(server="yourserver", database="yourdatabase", uid="username", pwd="password"))
sqlmlutils.SQLPackageManager(connection).install("text_tools-1.0.0-py3-none-any.whl")
```

## <a name="use-the-package-in-sql-server"></a>在 SQL Server 中使用套件

您現在可以在 SQL Server 的 Python 指令碼中使用套件。 例如：

```python
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
from text_tools.finders import find_best_string
corpus = "Lorem Ipsum text"
query = "Ipsum"
first_match = find_best_string(query, corpus)
print(first_match)
  '
```

## <a name="remove-the-package-from-sql-server"></a>從 SQL Server 移除套件

如果您想要移除 **text-tools** 套件，請利用您稍早定義的相同連線變數，在用戶端電腦上使用下列 Python 命令。

```python
sqlmlutils.SQLPackageManager(connection).uninstall("text-tools")
```

## <a name="see-also"></a>另請參閱

+ 若要檢視 SQL Server 機器學習服務中所安裝 Python 套件的相關資訊，請參閱[取得 Python 套件資訊](../package-management/python-package-information.md)。

+ 如需在 SQL Server 機器學習服務中安裝 R 套件的相關資訊，請參閱[在 SQL Server 上安裝新的 R 套件](install-additional-r-packages-on-sql-server.md)。
