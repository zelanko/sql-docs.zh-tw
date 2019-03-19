---
title: 在 Azure 資料 Studio 中執行 notebook
titleSuffix: SQL Server 2019 big data clusters
description: 這篇文章說明如何在 Azure Data Studio conneected 連往 SQL Server 2019 巨量資料叢集執行的 Jupyter Notebook。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/12/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 44ba203fcd7445add8fce00dd64913f85bcf4cc1
ms.sourcegitcommit: 11ab8a241a6d884b113b3cf475b2b9ed61ff00e3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161655"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>如何在 SQL Server 2019 預覽中使用 notebook

本文說明如何在巨量資料叢集上啟動 Jupyter Notebook 以及如何開始撰寫自己的 notebook。 它也會示範如何將針對叢集的作業提交。

## <a name="prerequisites"></a>先決條件

若要使用 notebook，您必須安裝下列必要條件：

- [SQL Server 2019 巨量資料叢集](deployment-guidance.md)
- [SQL Server 2019 巨量資料工具](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
   - **kubectl**

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="connect-to-the-sql-server-big-data-cluster-end-point"></a>連接到 SQL Server 巨量資料叢集端點

您可以連接到叢集中的不同結束點。 您可以連接到 Microsoft SQL Server 連接類型或 SQL Server 的巨量資料叢集結束點。
在 Azure Data Studio，請按 f1 鍵，然後按一下**新的連線** 就可以連接到 SQL Server 巨量資料叢集結束點。

![image1](media/notebooks-guidance/image1.png)

## <a name="browse-hdfs"></a>瀏覽 HDFS

連接之後，您將能夠瀏覽您的 HDFS 資料夾。 部署完成時，會啟動 SQL Server 啟動 WebHDFS。 使用 WebHDFS，您可以**重新整理**，新增**新目錄**，**上載**檔案，以及**刪除**。

![image2](media/notebooks-guidance/image2.png)

這些簡單作業可讓您使用您自己的資料到 HDFS。

## <a name="launch-new-notebooks"></a>啟動新的 Notebook

>[!NOTE]
>如果您有多個部署環境中執行的 Python 處理序，先刪除`.scaleoutdata`安裝目錄下的資料夾。 這應該會觸發`Reinstall Notebook dependencies`在 Azure 資料 Studio 中的工作。 需要幾分鐘的時間安裝的所有相依性。

如果有安裝 notebook 相依性的問題，請按 Ctrl + Shift + P 或 Macintosh Cmd + Shift + P，然後輸入`Reinstall Notebook dependencies`命令選擇區中。

![image3](media/notebooks-guidance/image3.png)

有多種方式可用來啟動新的 notebook。

1. 從**管理儀表板**。 新的連接後，您會看到儀表板。 按一下 **新的 Notebook**儀表板的工作。
  
    ![image4](media/notebooks-guidance/image4.png)

1. 以滑鼠右鍵按一下 HDFS/Spark 連接，然後按一下 **新的 Notebook**操作功能表中。

    ![image5](media/notebooks-guidance/image5.png)

    新的檔案，名為`Notebook-0.ipynb`隨即開啟。

    ![image6](media/notebooks-guidance/image6.png)

當您從這個命令棧板開啟筆記本時，筆記本會開啟為`Untitled-0.ipynb`。

## <a name="supported-kernels-and-attach-to-context"></a>支援的核心，並將附加至內容

Notebook 安裝支援 PySpark 和 Spark，Spark Magic 的核心，可讓您撰寫使用 Spark 的 Python 和 Scala 程式碼。 （選擇性） 您可以選擇 Python 進行本機開發。

![image7](media/notebooks-guidance/image7.png)

當您選取其中一個這些核心時，安裝在虛擬環境中設定該核心，您可以開始撰寫程式碼，以支援的語言。

|核心|描述
|:-----|:-----
|PySpark3 和 PySpark 核心| 撰寫使用從叢集的 Spark 計算的 Python 程式碼。
|Spark 核心|撰寫使用 Spark 的計算，從叢集的 Scala 和 R 程式碼。
|Python Kernel|撰寫適用於本機開發的 Python 程式碼。

`Attach to` 提供的核心，以附加的內容。 當您連接到 SQL Server 巨量資料叢集結束點，預設值`Attach to`叢集中的該結束點。

當您未連接到 SQL Server 的巨量資料叢集結束點時，預設的核心是 Python 並`Attach to`是`localhost`。

## <a name="hello-world-in-different-contexts"></a>不同的內容中的 hello world

### <a name="pyspark3pyspark-kernel"></a>Pyspark3/PySpark 核心

選擇 PySpark 核心在下列程式碼中的資料格類型。

按一下 **[執行]**。

Spark 應用程式已啟動，並傳回下列輸出：

![image8](media/notebooks-guidance/image8.png)

### <a name="spark-kernel--scala-language"></a>Spark 核心 |Scala 語言

選擇 Spark |Scala 核心在下列程式碼中的資料格類型。

![image9](media/notebooks-guidance/image9.png)

加入新的程式碼儲存格，請按一下 **+ Code**工具列中的命令。

現在，請選擇 Spark |Scala 資料格類型/貼上 – 和核心的下拉式清單中

![image10](media/notebooks-guidance/image10.png)

您也可以檢視 [資料格選項]，當您按一下下面的 – 的選項圖示

![image11](media/notebooks-guidance/image11.png)

### <a name="spark-kernel--r-language"></a>Spark 核心 |R 語言

選擇 Spark |核心的下拉式清單中的 R。 在資料格中，輸入或貼上程式碼中。 按一下 **執行**看到下列輸出。

![image13](media/notebooks-guidance/image13.png)

### <a name="local-python-kernel"></a>本機 Python 核心

選擇本機 Python 核心和資料格類型:-

![image14](media/notebooks-guidance/image14.png)

### <a name="markdown-text"></a>Markdown 文字

加入新的文字儲存格，請按一下 **+ 文字**工具列中的命令。

![image15](media/notebooks-guidance/image15.png)

在 編輯檢視變更的文字資料格內按兩下 

![image16](media/notebooks-guidance/image16.png)

儲存格變更編輯模式

![image17](media/notebooks-guidance/image17.png)

現在型別 markdown，您會看到一次預覽

![image18](media/notebooks-guidance/image18.png)

按一下 **[執行]**。 啟動 Spark 應用程式會建立做為 Spark 工作階段**spark** ，並定義**HelloWorld**物件。

Notebook 看起來應該類似下圖。

文字中的資料格外按一下會變更為 [預覽] 模式，並隱藏 markdown。

![image19](media/notebooks-guidance/image19.png)


## <a name="manage-packages"></a>管理套件
我們針對本機 Python 開發最佳化的事情之一是要包含的安裝套件，客戶就必須針對其案例能力。 根據預設，我們包含常見的套件，例如`pandas`，`numpy`等，但如果您預期封裝未包含然後撰寫下列程式碼中的 notebook 資料格： 

```python
import <package-name>
```

當您執行此命令，`Module not found`會傳回。 如果您的套件存在，則您不會收到錯誤。

如果它傳回`Module not Found`錯誤，然後按一下**管理套件**為識別您 Virtualenv 啟動終端機中的路徑。 您現在可以安裝在本機的套件。 使用下列命令來安裝封裝：

```bash
./pip install <package-name>
```

安裝套件之後，您應該能夠在 Notebook 資料格，並輸入下列命令：

```python
import <package-name>
```

若要解除安裝封裝，請使用下列命令，從您的終端機：

```bash
./pip uninstall <package-name>
```

## <a name="next-steps"></a>後續步驟

若要了解如何使用現有的 notebook，請參閱[如何管理 Azure Data Studio 中的 notebook](notebooks-how-to-manage.md)。