---
title: 在 Azure 資料 Studio 中執行 notebook
titleSuffix: SQL Server 2019 big data clusters
description: 這篇文章說明如何在 Azure Data Studio conneected 連往 SQL Server 2019 巨量資料叢集執行的 Jupyter Notebook。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: af1393b38b297e451903d5a39942a3e878c88ee6
ms.sourcegitcommit: edf7372cb674179f03a330de5e674824a8b4118f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53246607"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>如何在 SQL Server 2019 預覽中使用 notebook

本文說明如何在巨量資料叢集上啟動 Jupyter Notebook 以及如何開始撰寫自己的 Notebook。 它也會示範如何將針對叢集的作業提交。

## <a name="prerequisites"></a>先決條件

若要使用 notebook，您必須安裝下列必要條件：

- [SQL Server 2019 巨量資料叢集](deployment-guidance.md)
- [SQL Server 2019 巨量資料工具](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
   - **kubectl**

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="connect-to-the-hadoop-gateway-knox-end-point"></a>連接到 Hadoop 閘道 Knox 結束點

您可以連接到叢集中的不同結束點。 您可以連接到 Microsoft SQL Server 連接類型或 HDFS/Spark 閘道結束點。
在 Azure 資料 Studio （預覽），請按 f1 鍵，，然後按一下**新的連線** 就可以連接到您的 HDFS/Spark 閘道結束點。

![image1](media/notebooks-guidance/image1.png)

## <a name="browse-hdfs"></a>瀏覽 HDFS

連接之後，您將能夠瀏覽您的 HDFS 資料夾。 當部署完成，而且您會無法啟動 WebHDFS**重新整理**，新增**新目錄**，**上傳**檔案，和**刪除**.

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

  提供您的 Notebook 的名稱，例如`Test.ipynb`。 按一下 [儲存] 。

![image6](media/notebooks-guidance/image6.png)

## <a name="supported-kernels-and-attach-to-context"></a>支援的核心，並將附加至內容

Notebook 安裝支援 PySpark 和 Spark，Spark Magic 的核心，可讓您撰寫使用 Spark 的 Python 和 Scala 程式碼。 （選擇性） 您可以選擇 Python 進行本機開發。

![image7](media/notebooks-guidance/image7.png)

當您選取其中一個這些核心時，在虛擬環境中，我們將安裝該核心，以及您可以開始撰寫程式碼，以支援的語言。

|核心|描述
|:-----|:-----
|PySpark 核心|撰寫使用從叢集的 Spark 計算的 Python 程式碼。
|Spark 核心|撰寫使用 Spark 的計算，從叢集的 Scala 程式碼。
|Python 核心|撰寫適用於本機開發的 Python 程式碼。

`Attach to`提供核心以附加的內容。 當您連接到 HDFS/Spark 閘道 (Knox) 結束點上的預設`Attach to`叢集中的該結束點。

![image8](media/notebooks-guidance/image8.png)

## <a name="hello-world-in-different-contexts"></a>不同的內容中的 hello world

### <a name="pyspark-kernel"></a>Pyspark 核心

選擇 PySpark 核心在下列程式碼中的資料格類型：

![image9](media/notebooks-guidance/image9.png)

按一下 [執行] 您應該啟動 Spark 應用程式，請參閱，您會看到下列輸出：

![Image10](media/notebooks-guidance/image10.png)

輸出看起來應該類似下列映像。

![Image11](media/notebooks-guidance/image11.png)

### <a name="spark-kernel"></a>Spark 核心
加入新的程式碼儲存格，請按一下 **+ Code**工具列中的命令。

![Image12](media/notebooks-guidance/image12.png)

您也可以檢視 [資料格選項]，當您按一下下方的 [選項] 圖示

![Image13](media/notebooks-guidance/image13.png)

以下是針對每個資料格集的選項

![Image14](media/notebooks-guidance/image14.png)-

現在，請選擇 Spark 核心，在下拉式清單中的核心和資料格輸入/貼上:-

![Image15](media/notebooks-guidance/image15.png)

按一下 **執行**和您應該會看到正在啟動 Spark 應用程式，這會建立做為 Spark 工作階段**spark**並將定義**HelloWorld**物件。

Notebook 看起來應該類似下圖。

![Image16](media/notebooks-guidance/image16.png)

一旦您定義的物件，然後在下一步 的 Notebook 資料格中，輸入下列程式碼：

![Image17](media/notebooks-guidance/image17.png)

按一下 **執行**Notebook 中，而且您應該會看到"Hello，world ！" 在輸出中。

![Image18](media/notebooks-guidance/image18.png)

### <a name="local-python-kernel"></a>本機 python 核心
選擇本機 Python 核心和資料格類型:-

![Image19](media/notebooks-guidance/image19.png)

您應該會看到下列輸出：

![Image20](media/notebooks-guidance/image20.png)

### <a name="markdown-text"></a>Markdown 文字
加入新的文字儲存格，請按一下 **+ 文字**工具列中的命令。

![Image21](media/notebooks-guidance/image21.png)

按一下以新增您的 markdown 預覽圖示

![Image22](media/notebooks-guidance/image22.png)

按一下 [預覽] 圖示以切換為查看只 markdown

![Image23](media/notebooks-guidance/image23.png)

## <a name="manage-packages"></a>管理套件
我們針對本機 Python 開發最佳化的事情之一是要包含的安裝套件，客戶就必須針對其案例能力。 根據預設，我們包含常見的套件像 pandas、 numpy 等等，但如果您預期封裝未包含然後撰寫下列程式碼中的 Notebook 資料格： 

```python
import <package-name>
```

當您執行此命令時，您會取得`Module not found`時發生錯誤。 如果您的套件存在，則您不會收到錯誤。

如果您發現`Module not Found`錯誤，然後按一下**管理套件**為識別您 Virtualenv 啟動終端機中的路徑。 您現在可以安裝在本機的套件。 使用下列命令來安裝封裝：

```bash
./pip install <package-name>
```

安裝套件之後，您應該能夠在 Notebook 資料格，並輸入下列命令：

```python
import <package-name>
```

現在當您執行資料格時，您不應該取得`Module not found`時發生錯誤。

若要解除安裝封裝，請使用下列命令，從您的終端機：

```bash
./pip uninstall <package-name>
```

## <a name="next-steps"></a>後續步驟

若要了解如何使用現有的 notebook，請參閱[如何管理 Azure Data Studio 中的 notebook](notebooks-how-to-manage.md)。