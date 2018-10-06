---
title: 如何在 SQL Server 2019 預覽中使用 notebook |Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/05/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 989ee419406d0f69cd7bda26485d3d44cbf56550
ms.sourcegitcommit: c7d3a903eb7f410db3a0230101d24de0af17621a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2018
ms.locfileid: "48827329"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>如何在 SQL Server 2019 預覽中使用 notebook

本文說明如何啟動 SQL Server 2019 巨量資料叢集上的 notebook。 此外，它也會示範如何開始撰寫自己的 notebook，以及如何將針對叢集的作業提交。

## <a name="prerequisites"></a>先決條件

若要使用 notebook，您必須安裝下列必要條件：

- [SQL Server 2019 巨量資料叢集](deployment-guidance.md)
- [Azure Data Studio](../azure-data-studio/what-is.md)
- [SQL Server 2019 擴充功能 （預覽版）](../azure-data-studio/sql-server-2019-extension.md)。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="connect-to-the-sql-server-big-data-cluster-end-point"></a>連接到 SQL Server 的巨量資料叢集端點

您可以連接到叢集中的其他端點。 您可以連接到 Microsoft SQL Server 連接類型或 SQL Server 的巨量資料叢集端點。

在 Azure Data Studio （預覽），鍵入**F1** > **新連線**，並連接到您的 SQL Server 巨量資料叢集端點。

![image1](media/notebooks-guidance/image1.png)

## <a name="browse-hdfs"></a>瀏覽 HDFS
連接之後，您將能夠瀏覽您的 HDFS 資料夾。 當部署完成，而且您會無法啟動 WebHDFS**重新整理**，新增**新目錄**，**上傳**檔案，和**刪除**.

![image2](media/notebooks-guidance/image2.png)

這些簡單作業可讓您使用您自己的資料到 HDFS。

## <a name="launch-new-notebooks"></a>啟動新的 Notebook

有多種方式可用來啟動新的 notebook。

1. 從管理儀表板。 在進行新連線時，您會看到儀表板。 按一下新的 Notebook 工作儀表板上。

  ![image3](media/notebooks-guidance/image3.png)

1. 以滑鼠右鍵按一下 HDFS/Spark 連接和快顯功能表中有新的 Notebook

![image4](media/notebooks-guidance/image4.png)

提供 Notebook 的名稱 (範例： *Test.ipynb*)，按一下 **儲存**。

![image5](media/notebooks-guidance/image5.png)

## <a name="supported-kernels-and-attach-to-context"></a>支援的核心，並將附加至內容

在 Notebook 安裝中，我們支援 PySpark 和 Spark，Spark Magic 的核心，可讓使用者撰寫使用 Spark 的 Python 和 Scala 程式碼。 我們也允許使用者選擇 Python 針對其本機開發用途。

![image6](media/notebooks-guidance/image6.png)

當您選取其中一個這些核心時，在虛擬環境中，我們將安裝該核心，以及您可以開始撰寫程式碼，以支援的語言。

| 核心 | 描述
|---- |----
|PySpark 核心| 撰寫使用 Spark 的 Python 程式碼，計算從叢集中。
|Spark 核心|撰寫使用 Spark 的 Scala 程式碼，計算從叢集中。
|Python 核心|撰寫適用於本機開發的 Python 程式碼。

附加至選取項目提供的核心，以附加的內容。 當您連接到 SQL Server 的巨量資料叢集端點時，預設值附加至曾說: 「 選取項目會是叢集中的該端點。

![image7](media/notebooks-guidance/image7.png)

## <a name="hello-world-in-the-different-contexts"></a>不同的內容中的 hello world

### <a name="pyspark-kernel"></a>Pyspark 核心

選擇 PySpark 核心在下列程式碼中的資料格類型：

![image8](media/notebooks-guidance/image8.png)

按一下 [執行] 您應該啟動 Spark 應用程式，請參閱，您會看到下列輸出：

![image9](media/notebooks-guidance/image9.png)

輸出看起來應該類似下列映像。

![Image10](media/notebooks-guidance/image10.png)

### <a name="spark-kernel"></a>Spark 核心
加入新的程式碼儲存格，請按一下 + 程式碼在工具列中的命令。

![Image11](media/notebooks-guidance/image11.png)

資料格類型/貼上和核心的下拉式清單中，選擇 Spark 核心 

![Image12](media/notebooks-guidance/image12.png)

按一下 **執行**您應該會看到正在啟動 Spark 應用程式，而這會建立 Spark 工作階段**spark**並將定義**HelloWorld**物件。

Notebook 看起來應該類似下圖。

![Image13](media/notebooks-guidance/image13.png)

一旦您定義的物件然後在下列程式碼中的下一個 Notebook 資料格類型：

![Image14](media/notebooks-guidance/image14.png)

按一下 **執行**Notebook 中，而且您應該會看到"Hello，world ！" 在輸出中。

![Image15](media/notebooks-guidance/image15.png)

### <a name="local-python-kernel"></a>本機 python 核心
選擇本機 Python 核心中的資料格類型在 * *

![Image16](media/notebooks-guidance/image16.png)

您應該會看到下列輸出：

![Image17](media/notebooks-guidance/image17.png)

### <a name="markdown-text"></a>Markdown 文字
加入新的文字儲存格，請按一下 + 工具列中的文字命令。

![Image18](media/notebooks-guidance/image18.png)

按一下以新增您的 markdown 預覽圖示

![Image19](media/notebooks-guidance/image19.png)

按一下 [預覽] 圖示以切換為查看只 markdown

![Image20](media/notebooks-guidance/image20.png)

## <a name="manage-packages"></a>管理套件
我們針對本機 Python 開發最佳化的事情之一是要包含的安裝套件，客戶就必須針對其案例能力。 根據預設，我們包含常見的套件像 pandas、 numpy 等等，但如果您預期封裝未包含然後撰寫下列程式碼中的 Notebook 資料格

```python
import <package-name>
```

當您執行此命令時，您會取得`Module not found`時發生錯誤。 如果您的套件存在，則您不會收到錯誤。

如果您發現`Module not Found`錯誤，然後按一下**管理套件**為識別您 Virtualenv 啟動終端機中的路徑。 您現在可以安裝在本機的套件。 使用下列命令來安裝封裝：

```
./pip install <package-name>
```

安裝套件之後，您應該能夠在 Notebook 資料格，並輸入下列命令：

```python
import <package-name>
```

現在當您執行資料格時，您不應該取得`Module not found`時發生錯誤。

如果您想要解除安裝套件，請使用下列命令，從您的終端機：

```
./pip uninstall <package-name>
```

## <a name="next-steps"></a>後續步驟

若要了解如何使用現有的 notebook，請參閱[如何管理 Azure Data Studio 中的 notebook](notebooks-how-to-manage.md)。