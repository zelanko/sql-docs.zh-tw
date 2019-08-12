---
title: 如何在 Azure Data Studio 中使用 SQL Notebooks
titleSuffix: Azure Data Studio
description: 了解如何在 Azure Data Studio 中使用 SQL Notebooks
ms.custom: seodec18
ms.date: 06/28/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: achatter; alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 9af2e04a3973eddfcd714c7968c35e544302aba9
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959268"
---
# <a name="how-to-use-notebooks-in-azure-data-studio"></a>如何在 Azure Data Studio 中使用筆記本

此文章說明如何在 Azure Data Studio 中啟動 Notebook 體驗，以及如何開始撰寫您自己的筆記本。 它也會說明如何使用不同的核心來撰寫筆記本。


## <a name="connect-to-sql-server"></a>連接至 SQL Server

您可以連線到 Azure Data Studio 中的 Microsoft SQL Server 連線類型。
在 Azure Data Studio 中，您也可以按 F1 鍵，然後按一下[新增連線]    並連線到您的 SQL Server。

![image1](media/sql-notebooks/connection-info.png)

## <a name="launch-notebooks"></a>啟動 Notebooks

有多種方式可以啟動新的筆記本。

1. 移至 Azure Data Studio 中的 [檔案]  功能表，然後按一下 [新增筆記本]  。

    ![image3](media/sql-notebooks/file-new-notebook.png)

3. 以滑鼠右鍵按一下 **SQL Server** 連線，然後啟動 [新增筆記本]  。 
    ![image3](media/sql-notebooks/server-new-notebook.png)

4. 開啟命令選擇區 (**Ctrl+Shift+P**) 然後輸入 [新增筆記本]  。 隨即開啟名為 `Notebook-1.ipynb` 的新檔案。

## <a name="supported-kernels-and-attach-to-context"></a>支援的核心並附加至內容

Azure Data Studio 中的 Notebook 安裝原生支援 SQL 核心。 如果您是 SQL 開發人員，而且想要使用 Notebooks，則這會是您選擇的核心。 

SQL 核心也可用於連線 PostgreSQL 伺服器執行個體。 如果您是PostgreSQL開發人員並且想要連線到 PostgreSQL 伺服器，請在 Azure Data Stud 延伸模組市集中下載 [**PostgreSQL 延伸模組**](postgres-extension.md)。

![image7](media/sql-notebooks/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>SQL 核心

在 Notebook 中的程式碼儲存格中 (類似於我們的查詢編輯器)，我們支援新式 SQL 程式碼撰寫體驗，透過豐富的 SQL 編輯器、IntelliSense 和內建的程式碼片段，讓您可以更輕鬆地完成日常工作。 程式碼片段可讓您產生適當的 SQL 語法，以建立資料庫、資料表、檢視、預存程式等，以及更新現有的資料庫物件。 使用程式碼片段來快速建立資料庫的複本以供開發或測試，以及產生和執行腳本。

按一下 [執行]  來執行每個儲存格。

要連線至 SQL Server 執行個體的 SQL 核心

![image7](media/sql-notebooks/intellisense-code-cell.png)

查詢結果

![image19](media/sql-notebooks/sql-cell-results.png)

要連線至 PostgreSQL 伺服器執行個體的 SQL 核心 

![image18](media/sql-notebooks/pgsql-code-cell.png)

查詢結果

![image20](media/sql-notebooks/pgsql-cell-results.png)

### <a name="configure-python-for-notebooks"></a>設定適用於 Notebooks 的 Python

當您從 [核心] 下拉式清單中選取 [SQL] 以外的任何其他核心時，會提示您**設定適用於 Notebooks 的 Python**。 Notebook 相依性會安裝在指定的位置，但是您可以決定是否要設定安裝位置。 此安裝可能需要一些時間，而且在安裝完成之前，建議您不要關閉應用程式。 安裝完成之後，您就可以開始以支援的語言撰寫程式碼。

![image21](media/sql-notebooks/configure-python.png)

安裝成功後，您將在 [工作歷程記錄] 中找到通知以及在 [輸出終端機] 中執行 Jupyter 後端伺服器的位置。

![image22](media/sql-notebooks/jupyter-backend.png)

|核心|Description
|:-----|:-----
| SQL 核心 | 撰寫以關係資料庫為目標的 SQL 程式碼。
|PySpark3 和 PySpark 核心| 使用來自叢集的 Spark 計算來撰寫 Python 程式碼。
|Spark 核心|使用來自叢集的 Spark 計算來撰寫 Scala 和 R 程式碼。
|Python 核心|撰寫 Python 程式碼以進行本機開發。

`Attach to` 提供核心要附加的內容。 如果您使用的是 SQL 核心，則可以 `Attach to` 任何 SQL Server 執行個體。

如果您使用 Python3 核心，則 `Attach to` 為 `localhost`。 您可以使用此核心來進行本機 Python 開發。

當您連線到 SQL Server 2019 巨量資料叢集時，預設值 `Attach to` 是叢集的端點，並可讓您使用叢集的 Spark 計算來提交 Python、Scala 和 R 程式碼。

### <a name="code-cells-and-markdown-cells"></a>程式碼儲存格和 Markdown 儲存格

按一下工具列中的 [+程式碼]  命令，以加入新的程式碼資料格。

按一下工具列中的 [+文字]  命令，以加入新的文字儲存格。

![image8](media/sql-notebooks/notebook-toolbar.png)

儲存格會變更為編輯模式，現在輸入 Markdown，您會同時看到預覽

![image9](media/sql-notebooks/notebook-markdown-cell.png)

按一下文字儲存格以外的地方，將會顯示 Markdown 的文字。

![image10](media/sql-notebooks/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>受信任與不受信任

在 Azure Data Studio 中開啟的 Notebooks 預設是 [受信任]  。

如果您從某個其他來源開啟 Notebook，它會以 [不受信任]  模式開啟，然後您就可以將它設為 [受信任]  。

### <a name="save"></a>儲存 

您可以透過 **Ctrl+S** 儲存筆記本，或按一下 [檔案] 功能表中的 [儲存檔案]  、[另存新檔]  和 [儲存所有檔案]  命令，以及在命令選擇區中輸入 [File:  Save] 命令。

### <a name="pyspark3pyspark-kernel"></a>Pyspark3/PySpark 核心

選擇 `PySpark Kernel`，然後在儲存格中輸入下列程式碼。

按一下 **[執行]** 。

Spark 應用程式已啟動，並傳回下列輸出：

![image12](media/sql-notebooks/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Spark 核心 | Scala 語言

選擇 `Spark|Scala Kernel`，然後在儲存格中輸入下列程式碼。

![image13](media/sql-notebooks/spark-scala.png)

當您按一下下方的選項圖示時，也可以查看「儲存格選項」–

![image14](media/sql-notebooks/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Spark 核心 | R 語言

在核心的下拉式清單中選擇 Spark | R。 在儲存格中，輸入或貼上程式碼。 按一下 [執行]  以查看下列輸出。

![image15](media/sql-notebooks/spark-r.png)

### <a name="local-python-kernel"></a>本機 Python 核心

選擇本機 Python 核心，然後在儲存格中輸入 -

![image16](media/sql-notebooks/local-python.png)

## <a name="manage-packages"></a>管理套件
我們針對本機 Python 開發最佳化的其中一件事，就是包含安裝客戶在其情節中所需之套件的能力。 根據預設，我們會包含像 `pandas`、`numpy` 等常見的套件，但如果您預期不會包含套件，請在 [筆記本] 儲存格中撰寫下列程式碼： 

```python
import <package-name>
```

當您執行此命令時，會傳回 `Module not found`。 如果您的套件已存在，則不會收到錯誤。

如果它傳回 `Module not Found` 錯誤，請按一下 [管理套件]  以啟動精靈體驗。 

![image17](media/sql-notebooks/manage-packages.png)

在此精靈中，您將能夠看到**已安裝**的套件。 您可以搜尋清單和每個套件相關聯的版本。 如果您需要**解除安裝**其中任一套件，您可以按一下其中一個套件，然後按一下 [解除安裝選取的套件]  選項。

您也可以按一下 [新增套件]  來**搜尋**特定套件、選擇相關版本，然後按一下 [安裝]  。 根據預設，我們會選取搜尋套件的最新版本。 

安裝套件之後，您應該能夠進入 [筆記本] 儲存格，並輸入下列命令：

```python
import <package-name>
```

如果您需要**解除安裝**這些套件中的任何一項，您可以按一下一或多個套件，然後按一下 [解除安裝選取的套件]  選項。

## <a name="next-steps"></a>後續步驟

若要了解如何使用現有的筆記本，請參閱[如何管理 Azure Data Studio 中的筆記本](https://docs.microsoft.com/sql/big-data-cluster/notebooks-how-to-manage?view=sqlallproducts-allversions) \(部分機器翻譯\)。