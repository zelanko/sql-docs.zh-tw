---
title: 在 Azure Data Studio 中使用 SQL Server 的 Jupyter Notebook
description: 了解如何開始在 Azure Data Studio 中使用 Notebook。
author: yualan
ms.author: alayu
ms.reviewer: achatter, maghan, mikeray
ms.topic: conceptual
ms.prod: sql
ms.technology: azure-data-studio
ms.custom: seo-lt-2019
ms.date: 03/30/2020
ms.openlocfilehash: 480b5df927adddd38b8f9f2ea13fa25c3f653606
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "82178617"
---
# <a name="notebooks-with-sql-server-in-azure-data-studio"></a>SQL Server 在 Azure Data Studio 中的 Notebook

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Jupyter Notebook 是開放原始碼的 Web 應用程式，可讓您建立及共用含有即時程式碼、方程式、視覺效果和敘述文字的文件。 使用方式包含資料清理和轉換、數字模擬、統計模型、資料視覺效果和機器學習。

此文章說明如何在最新版本的 [**Azure Data Studio**](../azure-data-studio/download.md) 中啟動 Notebook 體驗，以及如何開始撰寫您自己的筆記本。 它也會說明如何使用不同的核心來撰寫筆記本。

觀看這段簡短的 5 分鐘影片，以取得 Azure Data Studio 中的筆記本簡介：

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introduction-to-Azure-Data-Studio-Notebooks/player?WT.mc_id=dataexposed-c9-niner]

## <a name="connect-to-sql-server"></a>連接至 SQL Server

您可以連線到 Azure Data Studio 中的 Microsoft SQL Server 連線類型。
在 Azure Data Studio 中，您也可以按 F1 鍵，然後選取 [新增連線]    並連線到 SQL Server。

![連線資訊](media/notebooks-guidance/connection-info.png)

## <a name="launch-notebooks"></a>啟動筆記本

有多種方式可以啟動新的筆記本。

- 移至 Azure Data Studio 中的 [檔案]  功能表，然後選取 [新增筆記本]  。

    ![新增筆記本](media/notebooks-guidance/file-new-notebook.png)

- 以滑鼠右鍵選取 **SQL Server** 連線，然後啟動 [新增筆記本]  。

    ![新增筆記本](media/notebooks-guidance/server-new-notebook.png)

- 開啟命令選擇區 (**Ctrl+Shift+P**) 然後輸入**新增筆記本**。 系統會隨即開啟名為 `Notebook-1.ipynb` 的新檔案。

## <a name="supported-kernels-and-attach-to-context"></a>支援的核心及附加至內容

Azure Data Studio 中的筆記本安裝能原生支援 SQL 核心。 如果您是 SQL 開發人員，且想要使用筆記本，SQL 核心即是您應選擇的核心。

SQL 核心也可用於連線 PostgreSQL 伺服器執行個體。 如果您是 PostgreSQL 開發人員，且想要將筆記本連線到 PostgreSQL 伺服器，請在 Azure Data Studio 延伸模組市集中下載 [**PostgreSQL 延伸模組**](../azure-data-studio/postgres-extension.md)，然後啟動 [新增筆記本]  以開啟筆記本執行個體來連線到 PostgreSQL 伺服器。

![PostgreSQL 連線](media/notebooks-guidance/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>SQL 核心

在 Notebook 中的程式碼儲存格中 (類似於我們的查詢編輯器)，我們支援新式 SQL 程式碼撰寫體驗，透過豐富的 SQL 編輯器、IntelliSense 和內建的程式碼片段，讓您可以更輕鬆地完成日常工作。 程式碼片段可供產生適當的 SQL 語法，以建立資料庫、資料表、檢視、預存程序，以及更新現有資料庫物件。 使用程式碼片段來快速建立資料庫的複本以供進行開發或測試，以及產生和執行指令碼。

選取 [執行]  來執行每個儲存格。

要連線至 SQL Server 執行個體的 SQL 核心

![SQL 核心](media/notebooks-guidance/intellisense-code-cell.png)

查詢結果

![查詢結果](media/notebooks-guidance/sql-cell-results.png)

要連線至 PostgreSQL 伺服器執行個體的 SQL 核心

![PostgreSQL 連線](media/notebooks-guidance/pgsql-code-cell.png)

查詢結果

![查詢結果](media/notebooks-guidance/pgsql-cell-results.png)

如果想將文字儲存格新增到附加至 SQL 核心的現有 Notebook，請選取工具列中的 [+文字]  命令。

![筆記本工具列](media/notebooks-guidance/notebook-toolbar.png)

資料格會變更為編輯模式；現在當您鍵入 Markdown 時，即可同時查看預覽

![Markdown 儲存格](media/notebooks-guidance/notebook-markdown-cell.png)

選取文字儲存格以外的地方會顯示 Markdown 文字。

![Markdown 文字](media/notebooks-guidance/notebook-markdown-preview.png)

### <a name="configure-python-for-notebooks"></a>設定適用於 Notebooks 的 Python

當從核心下拉式清單中選取 SQL 以外的任何其他核心時，系統會提示您**設定適用於 Notebooks 的 Python**。 筆記本相依性會被安裝在指定的位置，但是您可以決定是否要設定安裝位置。 此安裝可能需要一些時間，且在安裝完成之前，建議您不要關閉應用程式。 安裝完成之後，您就可以開始以支援的語言撰寫程式碼。

![設定 Python](media/notebooks-guidance/configure-python.png)

安裝成功後，[工作歷程記錄] 中會顯示通知，並會顯示 [輸出終端機] 中 Jupyter 後端伺服器執行所在的位置。

![Jupyter 後端](media/notebooks-guidance/jupyter-backend.png)

|核心|描述
|:-----|:-----
| SQL 核心 | 撰寫以您的關聯式資料庫為目標的 SQL 程式碼。
|PySpark3 和 PySpark 核心| 使用來自叢集的 Spark 計算來撰寫 Python 程式碼。
|Spark 核心|使用來自叢集的 Spark 計算來撰寫 Scala 和 R 程式碼。
|Python 核心|撰寫 Python 程式碼以進行本機開發。

`Attach to` 能提供要附加之核心的內容。 如果您正在使用 SQL 核心，則可以 `Attach to` 任何 SQL Server 執行個體。

如果您正在使用 Python3 核心，則 `Attach to` 將會是 `localhost`。 您可以使用此核心來進行本機 Python 開發。

當連線到 SQL Server 2019 巨量資料叢集時，預設的 `Attach to` 將會是叢集的端點，可供使用叢集的 Spark 計算來提交 Python、Scala 和 R 程式碼。

### <a name="code-cells-and-markdown-cells"></a>程式碼儲存格和 Markdown 儲存格

選取工具列中的 [+程式碼]  命令來新增新程式碼儲存格。

選取工具列中的 [+文字]  命令來新增新文字儲存格。

![筆記本工具列](media/notebooks-guidance/notebook-toolbar.png)

資料格會變更為編輯模式；現在當您鍵入 Markdown 時，即可同時查看預覽

![Markdown 儲存格](media/notebooks-guidance/notebook-markdown-cell.png)

選取文字儲存格以外的地方會顯示 Markdown 文字。

![Markdown 文字](media/notebooks-guidance/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>信任的和不信任的

在 Azure Data Studio 中開啟的 Notebooks 預設為**受信任**。

如果從某個其他來源開啟筆記本，該筆記本會以**不受信任**模式開啟，然後您就可以將其設為**受信任**。

### <a name="run-cells"></a>執行儲存格

如果想要執行筆記本中的所有儲存格，請選取工具列中的 [Run Cells] \(執行儲存格\)  按鈕。

### <a name="clear-results"></a>清除結果

如果想要將筆記本中所有已執行儲存格的結果清除，則可選取工具列中的 [清除結果]  按鈕。

### <a name="save"></a>儲存

若要儲存筆記本，執行下列其中一個動作。

- 選取 Ctrl+S
- 選取 [檔案]   > [儲存] 
- 選取 [檔案]   > [另存新檔] 
- 選取 [檔案]   > [全部儲存] 
- 在命令選擇區中，輸入 **File:Save**

### <a name="pyspark3pyspark-kernel"></a>Pyspark3/PySpark 核心

選擇 `PySpark Kernel`，然後在儲存格中輸入下列程式碼。

選取 [執行]  。

Spark 應用程式已啟動，並傳回下列輸出：

![Spark 應用程式](media/notebooks-guidance/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Spark 核心 | Scala 語言

選擇 `Spark|Scala Kernel`，然後在儲存格中輸入下列程式碼。

![Spark Scala](media/notebooks-guidance/spark-scala.png)

當選取下方的選項圖示時，也可以檢視「儲存格選項」–

![儲存格選項](media/notebooks-guidance/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Spark 核心 | R 語言

在核心的下拉式清單中選擇 [Spark | R]。 在儲存格中，輸入或貼上程式碼。 選取 [執行]  以查看下列輸出。

![Spark R](media/notebooks-guidance/spark-r.png)

### <a name="local-python-kernel"></a>本機 Python 核心

選擇本機 Python 核心，然後在儲存格中輸入 -

![本機 Python](media/notebooks-guidance/local-python.png)

## <a name="manage-packages"></a>管理套件

我們針對本機 Python 開發最佳化的其中一個項目，就是提供安裝客戶案例所需之套件的能力。 根據預設，我們會包含像 `pandas`、`numpy` 等常見的套件，但如果您預期不會包含套件，請在筆記本資料格中撰寫下列程式碼：

```python
import <package-name>
```

當您執行此命令時，系統會傳回 `Module not found`。 如果套件已存在，則不會發生錯誤。

如果其傳回 `Module not Found` 錯誤，請選取 [管理套件]  以啟動終端機。 您現在可以在本機安裝套件。 使用下列命令來安裝套件：

```bash
./pip install <package-name>
```

   > [!Tip]
   > 在 Mac 上，請遵循 [終端機] 視窗中的指示來安裝套件。

安裝套件之後，您應該能夠進入 [筆記本] 儲存格，並輸入下列命令：

```python
import <package-name>
```

若要將套件解除安裝，請從終端機使用下列命令：

```bash
./pip uninstall <package-name>
```

## <a name="next-steps"></a>後續步驟

- [如何管理 Azure Data Studio 中的筆記本](notebooks-manage-sql-server.md)。
- [建立並執行 SQL Server 筆記本](notebooks-tutorial-sql-kernel.md)。
- [使用 Azure Data Studio 筆記本部署 SQL Server 巨量資料叢集](../big-data-cluster/notebooks-deploy.md)。
- [使用 Azure Data Studio 筆記本管理 SQL Server 巨量資料叢集](../big-data-cluster/notebooks-manage-bdc.md)。
- [執行使用 Spark 的範例筆記本](../big-data-cluster/notebooks-tutorial-spark.md)。
- [使用 SQL Server 機器學習服務在 Azure Data Studio 筆記本中執行 Python 和 R 指令碼](../machine-learning/install/sql-machine-learning-azure-data-studio.md)。
