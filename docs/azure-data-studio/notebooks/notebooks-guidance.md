---
title: 在 Azure Data Studio 中使用 Jupyter Notebook
description: 了解如何開始在 Azure Data Studio 中使用 Jupyter Notebook。
ms.topic: how-to
ms.prod: azure-data-studio
ms.technology: azure-data-studio
author: yualan
ms.author: alayu
ms.reviewer: achatter, maghan, mikeray
ms.custom: seo-lt-2019
ms.date: 07/01/2020
ms.openlocfilehash: c9f9e95fd6cd437d74f350afa9cc4ca1399cac16
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364005"
---
# <a name="use-jupyter-notebooks-in-azure-data-studio"></a>在 Azure Data Studio 中使用 Jupyter Notebook

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

Jupyter Notebook 是開放原始碼的 Web 應用程式，可讓您建立及共用含有即時程式碼、方程式、視覺效果和敘述文字的文件。 使用方式包含資料清理和轉換、數字模擬、統計模型、資料視覺效果和機器學習。

本文描述如何在最新版本的 [**Azure Data Studio**](../download-azure-data-studio.md) 中建立新筆記本，以及如何開始使用不同的核心來撰寫自己的筆記本。

觀看這段簡短的 5 分鐘影片，以取得 Azure Data Studio 中的筆記本簡介：

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introduction-to-Azure-Data-Studio-Notebooks/player?WT.mc_id=dataexposed-c9-niner]

## <a name="create-a-notebook"></a>建立 Notebook

有多種方式可建立新的筆記本。 在每個案例中，會開啟名為 `Notebook-1.ipynb` 的新檔案。

- 移至 Azure Data Studio 中的 [檔案] 功能表，然後選取 [新增筆記本]。

  ![新增檔案筆記本](media/notebooks-guidance/file-new-notebook.png)

- 以滑鼠右鍵按一下 [SQL Server] 連線，然後選取 [新增筆記本]。

  ![新增伺服器筆記本](media/notebooks-guidance/server-new-notebook.png)

- 開啟命令選擇區 (**Ctrl+Shift+P**)，鍵入「新增筆記本」，然後選取 [新增筆記本] 命令。

  ![新增命令選擇區筆記本](media/notebooks-guidance/command-palette-new-notebook.png)

## <a name="connect-to-a-kernel"></a>連線到核心

Azure Data Studio 筆記本支援數種不同的核心，包括 SQL Server、Python、PySpark 及其他核心。 每個核心在筆記本的程式碼資料格中支援不同語言。 例如，當連線到 SQL Server 核心時，您可在筆記本程式碼資料格中輸入並執行 T-SQL 陳述式。

[附加至] 提供核心的內容。 例如，如果正在使用 SQL 核心，則可附加至任何 SQL Server 執行個體。
如果正在使用 Python3 核心，則會附加至 **localhost**，且可使用此核心來進行本機 Python 開發。

SQL 核心也可用於連線到 PostgreSQL 伺服器執行個體。 如果您是 PostgreSQL 開發人員，且想要將筆記本連線到 PostgreSQL 伺服器，請在 Azure Data Studio 延伸模組市集中下載 [**PostgreSQL 延伸模組**](../extensions/postgres-extension.md)，然後連線到 PostgreSQL 伺服器。

如果已連線到 SQL Server 2019 巨量資料叢集，則預設的 [附加至] 將會是叢集的端點。 您可使用叢集的 Spark 計算來提交 Python、Scala 和 R 程式碼。

| 核心                      | 描述                                                  |
|:----------------------------|:-------------------------------------------------------------|
| SQL 核心                  | 撰寫以您的關聯式資料庫為目標的 SQL 程式碼。         |
| PySpark3 和 PySpark 核心 | 使用來自叢集的 Spark 計算來撰寫 Python 程式碼。      |
| Spark 核心                | 使用來自叢集的 Spark 計算來撰寫 Scala 和 R 程式碼。 |
| Python 核心               | 撰寫 Python 程式碼以進行本機開發。                     |

如需特定核心的詳細資訊，請參閱：

- [建立並執行 SQL Server 筆記本](./notebooks-sql-kernel.md)
- [建立及執行 Python 筆記本](./notebooks-python-kernel.md)
- [Azure Data Studio 中的 Kqlmagic 延伸模組](./notebooks-kqlmagic.md) - 這會擴充 Python 核心的功能

## <a name="add-a-code-cell"></a>新增程式碼資料格

程式碼資料格可供在筆記本中以互動方式執行程式碼。

按一下工具列中的 [+資料格] 命令，然後選取 [程式碼資料格] 來新增新的程式碼資料格。 新的程式碼資料格會新增在目前選取的資料格後面。

在所選核心的資料格中輸入程式碼。 例如，如果正在使用 SQL 核心，則可在程式碼資料格中輸入 T-SQL 命令。

使用 SQL 核心輸入程式碼類似於 SQL 查詢編輯器。 程式碼資料格支援新式 SQL 程式碼撰寫體驗，並提供豐富的 SQL 編輯器、IntelliSense 和內建的程式碼片段等內建功能。 程式碼片段可供產生適當的 SQL 語法，以建立資料庫、資料表、檢視、預存程序，以及更新現有資料庫物件。 使用程式碼片段來快速建立資料庫的複本以供進行開發或測試，以及產生和執行指令碼。

![SQL 核心](media/notebooks-guidance/intellisense-code-cell.png)

## <a name="add-a-text-cell"></a>新增文字資料格

文字資料格可供在程式碼資料格之間新增 Markdown 文字區塊，以記錄程式碼。

按一下工具列中的 [+資料格] 命令，然後選取 [文字資料格] 來新增新的文字資料格。

資料格會以編輯模式啟動，可在其中鍵入 Markdown 文字。 當鍵入時，即會顯示下列預覽。

![Markdown 儲存格](media/notebooks-guidance/notebook-markdown-cell.png)

選取文字資料格以外的地方會顯示 Markdown 文字。

![Markdown 文字](media/notebooks-guidance/notebook-markdown-preview.png)

如果再按一次文字資料格，則會變更為編輯模式。

## <a name="run-a-cell"></a>執行儲存格

若要執行單一資料格，請按一下資料格左邊的 [執行資料格] (圓形黑色箭號)，或選取資料格，然後按 F5 鍵。 您可按一下工具列中的 [全部執行] 來執行筆記本中所有資料格 - 資料格會一次執行一個，如果資料格中發生錯誤，則會停止執行。

資料格的結果會顯示在資料格下方。 您可選取工具列中的 [清除結果] 按鈕，以清除筆記本中所有已執行資料格的結果。

## <a name="save-a-notebook"></a>儲存筆記本

若要儲存筆記本，請執行下列其中一項動作。

- 鍵入 Ctrl+S
- 從 [檔案] 功能表選取 [儲存]
- 從 [檔案] 功能表選取 [另存新檔...]
- 從 [檔案] 功能表選取 [全部儲存] - 這會儲存所有開啟的筆記本
- 在命令選擇區中，輸入 **File:Save**

筆記本會儲存為 `.ipynb` 檔案。

## <a name="trusted-and-non-trusted"></a>信任的和不信任的

在 Azure Data Studio 中開啟的筆記本預設為 [受信任]。

如果從某個其他來源開啟筆記本，該筆記本會以 [不受信任] 模式開啟，然後即可將其設為 [受信任]。

## <a name="examples"></a>範例

下列範例示範如何使用不同核心來執行簡單的 "Hello World" 命令。 選取核心，在資料格中輸入範例程式碼，然後按一下 [執行資料格]。

### <a name="pyspark"></a>Pyspark

![Spark 應用程式](media/notebooks-guidance/pyspark.png)

### <a name="spark--scala-language"></a>Spark | Scala 語言

![Spark Scala](media/notebooks-guidance/spark-scala.png)

### <a name="spark--r-language"></a>Spark | R 語言

![Spark R](media/notebooks-guidance/spark-r.png)

### <a name="python-3"></a>Python 3

![本機 Python](media/notebooks-guidance/local-python.png)

## <a name="next-steps"></a>後續步驟

- [建立並執行 SQL Server 筆記本](./notebooks-sql-kernel.md)。
- [建立及執行 Python 筆記本](./notebooks-python-kernel.md)
- [使用 SQL Server 機器學習服務在 Azure Data Studio 筆記本中執行 Python 和 R 指令碼](../../machine-learning/install/sql-machine-learning-azure-data-studio.md)。
- [使用 Azure Data Studio 筆記本部署 SQL Server 巨量資料叢集](../../big-data-cluster/notebooks-deploy.md)。
- [使用 Azure Data Studio 筆記本管理 SQL Server 巨量資料叢集](../../big-data-cluster/notebooks-manage-bdc.md)。
- [執行使用 Spark 的範例筆記本](../../big-data-cluster/notebooks-tutorial-spark.md)。