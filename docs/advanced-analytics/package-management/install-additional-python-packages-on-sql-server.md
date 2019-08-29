---
title: 使用 pip 安裝 Python 套件
description: 瞭解如何使用 Python pip 在 SQL Server Machine Learning 服務的實例上安裝新的 Python 套件。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/22/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: dc5addca9c9bbf01408cea89f85676813b97506c
ms.sourcegitcommit: 52d3902e7b34b14d70362e5bad1526a3ca614147
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2019
ms.locfileid: "70109752"
---
# <a name="install-python-packages-with-sqlmlutils"></a>使用 sqlmlutils 安裝 Python 套件

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明如何使用[**sqlmlutils**](https://github.com/Microsoft/sqlmlutils)封裝中的函式, 將新的 Python 封裝安裝至 SQL Server Machine Learning 服務的實例。 您安裝的套件可用於使用 T-sql [sp-執行-external](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) ----sql 語句在資料庫中執行的 Python 腳本。

如需套件位置和安裝路徑的詳細資訊, 請參閱[取得 Python 套件資訊](../package-management/python-package-information.md)。

> [!NOTE]
> 不建議將`pip install`標準 python 命令新增至 SQL Server 上的 python 套件。 相反地, 請使用**sqlmlutils** , 如本文中所述。

## <a name="prerequisites"></a>必要條件

+ 您必須使用 Python 語言選項安裝[SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)。

+ 在您用來連接到 SQL Server 的用戶端電腦上安裝[python](https://www.python.org/) 。 您也可能想要 Python 開發環境, 例如具有[Python 擴充](https://marketplace.visualstudio.com/items?itemName=ms-python.python)功能的[Visual Studio Code](https://code.visualstudio.com/download) 。 

+ 在您用來連線到 SQL Server 的用戶端電腦上安裝[Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is)或[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) (SSMS)。 您可以使用其他資料庫管理或查詢工具, 但本文假設 Azure Data Studio 或 SSMS。

### <a name="other-considerations"></a>其他考慮

+ 套件必須符合 Python 3.5 規範, 並可在 Windows 上執行。

+ Python 套件程式庫位於 SQL Server 實例的 Program Files 資料夾中, 而且根據預設, 在此資料夾中安裝需要系統管理員許可權。 如需詳細資訊, 請參閱[套件程式庫位置](../package-management/python-package-information.md#default-python-library-location)。

+ 套件安裝是每個實例。 如果您有多個 Machine Learning 服務實例, 則必須將封裝新增至每一個。

+ 新增封裝之前, 請考慮套件是否適合用於 SQL Server 環境。

  + 我們建議您在資料庫中使用 Python, 以進行與資料庫引擎緊密整合 (例如機器學習服務) 的工作, 而不是單純查詢資料庫的工作。

  + 如果您新增的封裝在伺服器上放置過多的計算壓力, 效能將會受到影響。

  + 在強化的 SQL Server 環境中, 您可能會想要避免下列情況:
    + 需要網路存取的套件
    + 需要提升檔案系統存取權的封裝
    + 在 SQL Server 內執行時, 用於 網頁程式開發或其他工作的套件不會有任何好處

## <a name="install-sqlmlutils-on-the-client-computer"></a>在用戶端電腦上安裝 sqlmlutils

若要使用**sqlmlutils**, 您必須先將它安裝在用來連接到 SQL Server 的用戶端電腦上。

1. 從 https://github.com/Microsoft/sqlmlutils/tree/master/Python/dist 將最新的**sqlmlutils** zip 檔案下載到用戶端電腦。 不要解壓縮檔案。

1. 開啟**命令提示**字元, 然後執行下列命令來安裝**sqlmlutils**套件。 以您下載的**sqlmlutils** zip 檔案的完整路徑取代-此範例假設下載的檔案是`c:\temp\sqlmlutils_0.6.0.zip`。

   ```console
   pip install --upgrade --upgrade-strategy only-if-needed c:\temp\sqlmlutils_0.6.0.zip
   ```

## <a name="add-a-python-package-on-sql-server"></a>在 SQL Server 上新增 Python 套件

在下列範例中, 您會將[文字工具](https://pypi.org/project/text-tools/)封裝加入 SQL Server。

### <a name="add-the-package-online"></a>線上新增封裝

如果您用來連線到 SQL Server 的用戶端電腦可以存取網際網路, 您可以使用**sqlmlutils**來尋找**文字工具**套件, 以及透過網際網路的任何相依性, 然後從遠端將封裝安裝到 SQL Server 實例。

1. 在用戶端電腦上, 開啟 [ **python** ] 或 [python 環境]。

1. 使用下列命令來安裝**文字工具**套件。 以您自己的 SQL Server 資料庫連接資訊取代。

   ```python
   import sqlmlutils
   connection = sqlmlutils.ConnectionInfo(server="yourserver", database="yourdatabase", uid="yoursqluser", pwd="yoursqlpassword")
   sqlmlutils.SQLPackageManager(connection).install("text-tools")
   ```

### <a name="add-the-package-offline"></a>離線新增封裝

如果您用來連接到 SQL Server 的用戶端電腦沒有網際網路連線, 您可以在具有網際網路存取的電腦上使用**pip** , 將套件和任何相依套件下載到本機資料夾。 然後將資料夾複製到用戶端電腦, 讓您可以離線安裝套件。

#### <a name="on-a-computer-with-internet-access"></a>在有網際網路存取的電腦上

1. 開啟**命令提示**字元並執行下列命令, 以建立包含**文字工具**套件的本機資料夾。 這個範例會建立資料夾`c:\temp\text-tools`。

   ```console
   pip download text-tools -d c:\temp\text-tools
   ```

1. `text-tools`將資料夾複製到用戶端電腦。 下列範例假設您已將它複製`c:\temp\packages\text-tools`到。

#### <a name="on-the-client-computer"></a>在用戶端電腦上

使用**sqlmlutils**來安裝您在**pip**建立的本機資料夾中找到的每個套件 (.whl 檔案)。 您安裝套件的順序並不重要。

在此範例中,**文字工具**沒有相依性, 因此您可以安裝`text-tools`資料夾中只有一個檔案。 相反地, 套件 (例如**scikit-learn** ) 有11個相依性, 因此您可以在資料夾中找到12個檔案 ( **scikit-learn 圖**套件和11個相依套件), 然後安裝每個檔案。

執行下列 Python 腳本。 以您自己的 SQL Server 資料庫連接資訊, 以及封裝的實際檔案路徑和名稱取代。 針對資料夾中的每個封裝檔案重複語句。`sqlmlutils.SQLPackageManager`

```python
import sqlmlutils
connection = sqlmlutils.ConnectionInfo(server="yourserver", database="yourdatabase", uid="yoursqluser", pwd="yoursqlpassword")
sqlmlutils.SQLPackageManager(connection).install("c:/temp/packages/text-tools/text_tools-1.0.0-py3-none-any.whl")
```

## <a name="use-the-package-in-sql-server"></a>在 SQL Server 中使用套件

您現在可以在 SQL Server 的 Python 腳本中使用套件。 例如:

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

## <a name="remove-the-package-from-sql-server"></a>從 SQL Server 移除封裝

如果您想要移除**文字工具**套件, 請使用您稍早定義的相同連接變數, 在用戶端電腦上使用下列 Python 命令。

```python
sqlmlutils.SQLPackageManager(connection).uninstall("text-tools")
```

## <a name="see-also"></a>另請參閱

+ 若要查看安裝在 SQL Server Machine Learning 服務中之 Python 套件的相關資訊, 請參閱[取得 python 套件資訊](../package-management/python-package-information.md)。

+ 如需有關在 SQL Server Machine Learning 服務中安裝 R 套件的詳細資訊, 請參閱[在 SQL Server 上安裝新的 r 套件](../r/install-additional-r-packages-on-sql-server.md)。
