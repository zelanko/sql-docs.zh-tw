---
title: 如何在 Azure Data Studio 中使用 SQL Notebook
titleSuffix: Azure Data Studio
description: 了解如何在 Azure Data Studio 中使用 SQL Notebook
ms.custom: seodec18
ms.date: 03/17/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: achatter; alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: ceaf172fc36ee92d15be326d4356061ea1674df1
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161988"
---
# <a name="how-to-use-notebooks-in-azure-data-studio"></a>如何在 Azure Data Studio 中使用 notebook

本文說明如何啟動 Azure Data Studio 中的 Notebook 體驗，以及如何開始撰寫自己的 notebook。 它也會示範如何撰寫使用不同的核心的 Notebook。


## <a name="connect-to-sql-server"></a>連接至 SQL Server

您可以連接到 Azure Data Studio 中的 Microsoft SQL Server 連接類型。
在 Azure 資料 Studio 中，您可以也按 f1 鍵，然後按一下**新的連線** 並連接到您的 SQL Server。

![image1](media/sql-notebooks/connection-info.png)

## <a name="launch-notebooks"></a>啟動 Notebook

有多種方式可用來啟動新的 notebook。

1. 移至 **[檔案] 功能表**在 Azure Data Studio，然後按一下**新的 Notebook**。

    ![image3](media/sql-notebooks/file-new-notebook.png)

3. 以滑鼠右鍵按一下**SQL Server**連線，然後啟動**新的 Notebook**。 
    ![image3](media/sql-notebooks/server-new-notebook.png)

4. 開啟命令選擇區 (**Ctrl + Shift + P**))，然後輸入在**新的 Notebook**。 新的檔案，名為`Notebook-1.ipynb`隨即開啟。

## <a name="supported-kernels-and-attach-to-context"></a>支援的核心，並將附加至內容

在 Azure Data Studio Notebook 安裝原生支援 SQL 核心。 如果您是 SQL 開發人員並且想要使用 Notebook 則此項將為您選擇的核心。 

SQL 核心也可用來連線到 PostgreSQL 伺服器執行個體。 如果您是 PostgreSQL 開發人員，而且想要連線到 PostgreSQL 伺服器然後下載[ **PostgreSQL 擴充功能**](postgres-extension.md) Azure Data Studio 擴充功能 marketplace 中。

![image7](media/sql-notebooks/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>SQL Kernel

在程式碼內的資料格的 Notebook，類似於查詢編輯器中，我們支援最新的 SQL 程式碼撰寫體驗，可讓您日常的工作更容易利用內建的功能，例如豐富的 SQL 編輯器、 IntelliSense 和內建的程式碼片段。 程式碼片段可讓您產生適當的 SQL 語法來建立資料庫、 資料表、 檢視、 預存程序等，並更新現有的資料庫物件。 使用程式碼片段來快速建立您用於開發或測試用途的資料庫副本，以及產生和執行指令碼。

按一下 **執行**執行每個資料格。

若要連接到 SQL Server 執行個體的 SQL 核心

![image7](media/sql-notebooks/intellisense-code-cell.png)

查詢結果

![image19](media/sql-notebooks/sql-cell-results.png)

若要連接到 PostgreSQL 伺服器執行個體的 SQL 核心 

![image18](media/sql-notebooks/pgsql-code-cell.png)

查詢結果

![image20](media/sql-notebooks/pgsql-cell-results.png)

### <a name="configure-python-for-notebooks"></a>設定 Python notebook

當您從 [核心] 下拉式清單選取任何除了 SQL 之外的其他核心時，這會提示您**設定適用於 Python Notebook**。 Notebook 相依性都會安裝在指定的位置，但您可以決定是否要將安裝位置。 這項安裝可能需要一些時間，直到安裝完成時，不關閉應用程式建議。 一旦安裝完成後，就可以開始撰寫程式碼，以支援的語言。

![image21](media/sql-notebooks/configure-python.png)

安裝成功後，您會發現通知工作歷程記錄，以及輸出終端機中執行的 Jupyter 後端伺服器的位置中。

![image22](media/sql-notebooks/jupyter-backend.png)

|核心|描述
|:-----|:-----
| SQL Kernel | 撰寫針對您的 SQL Server 的 SQL 程式碼。
|PySpark3 和 PySpark 核心| 撰寫使用從叢集的 Spark 計算的 Python 程式碼。
|Spark 核心|撰寫使用 Spark 的計算，從叢集的 Scala 和 R 程式碼。
|Python Kernel|撰寫適用於本機開發的 Python 程式碼。

`Attach to` 提供的核心，以附加的內容。 如果您使用的 SQL 核心，則您可以`Attach to`任何您的 SQL Server 執行個體。

如果您使用的核心 Python3`Attach to`是`localhost`。 您可以使用此核心，您的本機 Python 開發的。

當您連接到 SQL Server 2019 巨量資料叢集，預設值`Attach to`叢集中的該結束點，可讓您提交 Python、 Scala 和 R 程式碼使用 Spark 的計算叢集。

### <a name="code-cells-and-markdown-cells"></a>程式碼儲存格和 Markdown 資料格

加入新的程式碼儲存格，請按一下 **+ Code**工具列中的命令。

加入新的文字儲存格，請按一下 **+ 文字**工具列中的命令。

![image8](media/sql-notebooks/notebook-toolbar.png)

編輯模式，而現在輸入 markdown 和您的儲存格變更將會看到一次預覽

![image9](media/sql-notebooks/notebook-markdown-cell.png)

文字中的資料格外按一下，會顯示的 markdown 文字。

![image10](media/sql-notebooks/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>信任和非信任

在 Azure Data Studio 中開啟 notebook 是在預設**信任**。

如果您從其他來源開啟 Notebook 會以開啟它**非信任**模式，然後您可以讓**信任**。

### <a name="save"></a>儲存 

您可以將儲存的 Notebook **Ctrl + S**或按一下**儲存檔案**，**檔案另存新檔...** 並**儲存所有檔案**從 [檔案] 功能表命令和**檔案：儲存**在命令選擇區輸入命令。

### <a name="pyspark3pyspark-kernel"></a>Pyspark3/PySpark 核心

選擇`PySpark Kernel`在下列程式碼中的資料格類型。

按一下 **[執行]**。

Spark 應用程式已啟動，並傳回下列輸出：

![image12](media/sql-notebooks/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Spark 核心 |Scala 語言

選擇`Spark|Scala Kernel`在下列程式碼中的資料格類型。

![image13](media/sql-notebooks/spark-scala.png)

您也可以檢視 [資料格選項]，當您按一下下面的 – 的選項圖示

![image14](media/sql-notebooks/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Spark 核心 |R 語言

選擇 Spark |核心的下拉式清單中的 R。 在資料格中，輸入或貼上程式碼中。 按一下 **執行**看到下列輸出。

![image15](media/sql-notebooks/spark-r.png)

### <a name="local-python-kernel"></a>本機 Python 核心

選擇本機 Python 核心和資料格類型:-

![image16](media/sql-notebooks/local-python.png)

## <a name="manage-packages"></a>管理套件
我們針對本機 Python 開發最佳化的事情之一是要包含的安裝套件，客戶就必須針對其案例能力。 根據預設，我們包含常見的套件，例如`pandas`，`numpy`等，但如果您預期封裝未包含然後撰寫下列程式碼中的 notebook 資料格： 

```python
import <package-name>
```

當您執行此命令，`Module not found`會傳回。 如果您的套件存在，則您不會收到錯誤。

如果它傳回`Module not Found`錯誤，然後按一下**管理套件**啟動終端機。 您現在可以安裝在本機的套件。 使用下列命令來安裝封裝：

```bash
./pip install <package-name>
```

   > [!Tip]
   > 在 Mac 上，請遵循安裝套件的終端機視窗中的指示。 

安裝套件之後，您應該能夠在 Notebook 資料格，並輸入下列命令：

```python
import <package-name>
```

若要解除安裝封裝，請使用下列命令，從您的終端機：

```bash
./pip uninstall <package-name>
```

## <a name="next-steps"></a>後續步驟

若要了解如何使用現有的 notebook，請參閱[如何管理 Azure Data Studio 中的 notebook](https://docs.microsoft.com/sql/big-data-cluster/notebooks-how-to-manage?view=sqlallproducts-allversions)。