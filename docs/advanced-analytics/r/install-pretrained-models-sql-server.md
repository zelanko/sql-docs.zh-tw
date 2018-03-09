---
title: "SQL Server 上安裝預先定型的機器學習模型 |Microsoft 文件"
ms.date: 11/16/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 5d9f60684cc749c35674233fbdaaa222953396d9
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2018
---
# <a name="install-pretrained-machine-learning-models-on-sql-server"></a>安裝預先定型的機器學習模型 SQL Server 上
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何將預先定型的模型加入至 SQL Server 執行個體在具有 R 服務或機器學習服務安裝。

Microsoft R Server 或 Server 機器學習中用於個別的 Windows 安裝程式時，使用選項來安裝預先定型的模型。 您可以使用此安裝程式取得只預先定型的模型，或您可以用它來[升級機器學習元件](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)中 SQL Server 2016 或 SQL Server 2017 的執行個體。

執行安裝程式下載預先定型的模型之後，有一些額外的步驟來設定模型以供 SQL server。 本文說明處理程序。

如需如何使用 SQL Server 資料的預先定型的模型的範例，請參閱 SQL Server 機器學習小組的這篇部落格： 

+ [使用 SQL Server 機器學習服務中的 Python 情緒分析](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/11/01/sentiment-analysis-with-python-in-sql-server-machine-learning-services/)

## <a name="benefits-of-using-pretrained-models"></a>使用 預先定型的模型的優點

為了協助的客戶需要以執行工作，例如情緒分析或映像功能，其潛在，但沒有取得大型資料集或複雜的模型定型的資源，這些預先定型的模型所建立。 使用預先定型的模型，可讓您開始文字和影像有效率地處理。

目前可用的模型是情緒分析和影像分類的深度類神經網路 (DNN) 模型。 所有預先定型的模型已定型使用 Microsoft 的[計算網路 Toolkit](https://cntk.ai/Features/Index.html)，或**CNTK**。

每個網路的設定根據下列參考實作：

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

如需有關這些模型的詳細資訊，請參閱[預先定型的機器學習模型情緒分析及映像偵測](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)

如需深入了解網路及使用 CNTK 其實作的詳細資訊，請參閱下列文章：

+ [Microsoft 研究人員演算法設定 ImageNet 挑戰里程碑](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Microsoft 計算網路工具組提供最有效率的分散式的深層學習計算效能](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="how-to-install-the-models-on-sql-server"></a>如何安裝 SQL Server 上的模型

1. 執行個別的 windows 安裝程式的機器學習服務伺服器。 如需下載位置，請參閱：

    + [安裝機器學習適用於 Windows 的伺服器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
    + [安裝 R Server 9.1 適用於 Windows](https://docs.microsoft.com/r-server/install/r-server-install-windows)

2. 選取要安裝的功能取決於您是在取得只模型，或執行其他使用安裝程式的更新。
 
    + 如果這是新安裝的機器學習伺服器，且不想進行其他變更 R 或 Python 元件，選取**只**預先定型的模型選項。 接受所有其他提示，包括授權合約。

    + 若要同時升級 R 或 Python 元件，選取您想要更新的語言 （R，或 Python，或兩者） 和選取 預先定型的模型。 選取要套用這些變更的一或多個執行個體。

    + 如果您之前安裝 Server 機器學習並更新 R 或 Python 元件使用的繫結選項，保留所有先前的選取項目**現狀**，然後選取 預先定型的模型選項。 無法取消選取任何先前選取的選項。如果您這樣做時，安裝程式會移除元件。

3. 安裝完成時，開啟 Windows 命令提示字元**以系統管理員身分**，並瀏覽至安裝程式啟動載入器資料夾，針對 SQL Server，其中也包含 Microsoft R 安裝程式。 在 SQL Server 2017 的預設執行個體，將為資料夾：
    
    `C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\SQL2017\x64\`

4. 執行 RSetup.exe，表示要安裝的元件、 版本，以及包含模型的來源檔案，使用這些範例所示的命令列引數的資料夾：

    + 若要使用模型與**R_SERVICES**:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<SQL_DB_instance_folder>\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    例如，若要允許使用預先定型的模型的最新版本的 SQL Server 2017 的預設執行個體中的 R，您會執行此陳述式：

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    具名執行個體，命令看起來會像下面這樣：

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MyInstanceName\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    + 若要使用預先定型的模型與 R 伺服器 （獨立） 或機器學習伺服器 （獨立）：

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "~\R_SERVER\library\MicrosoftML\mxLibs\x64"`

    比方說，若要啟用用於預先定型的模型的最新版本的 R、 R Server 與 SQL Server 2016 中，預設安裝中，您會執行此陳述式：

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir ‘C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\MicrosoftML\mxLibs\"`
    
    + 若要使用預先定型的模型與**PYTHON_SERVICES**:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<SQL_DB_instance_folder>\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    比方說，若要允許使用 Python，SQL Server 2017 的預設執行個體中的最新版的預先定型的模型，您會執行此陳述式：

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    具名執行個體，命令看起來會像下面這樣：

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MyInstanceName\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    + 若要使用 Python 預先定型模型使用機器學習 Server （獨立）：

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<sql_folder>\PYTHON_SERVER\site-packages\microsoftml\mxLibs"`

    例如，假設使用 SQL Server 2017 安裝程式的預設安裝的機器學習伺服器 （獨立），執行此陳述式：

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER\Lib\site-packages\microsoftml\mxLibs"`

5. 版本參數支援下列值：

    + 發行候選版本 0: **9.1.0.0**
    + 候選版 1: **9.2.0.22**
    + RTM: **9.2.0.100**
    + 累計更新 1: **9.2.0.24**

6. 如果安裝成功，下列模型應加入至您的 R\_服務或 PYTHON\_SERVICES 資料夾：

    - AlexNet\_Updated.model
    - ImageNet1K\_mean.xml
    - pretrained.model
    - ResNet\_101\_Updated.model
    - ResNet\_18\_Updated.model
    - ResNet\_50\_Updated.model


> [!NOTE]
> 
> 如果模型檔案的路徑太長，您可能會發生錯誤時從 Python 程式碼呼叫的模型檔案。 這是因為在目前的 Python 實作限制。 在服務即將發行版本中，將會修正此問題。

## <a name="examples"></a>範例

您已安裝的模型之後，您可以使用模型，從您的程式碼呼叫的方式。

### <a name="image-featurization-example"></a>映像功能，其潛在範例

映像預先定型的模型支援功能，其潛在您提供的映像。 這個特定模型已定型使用[CNTK](https://docs.microsoft.com/cognitive-toolkit/)。 

若要使用模型，您呼叫**featurizeImage**轉換。

+ [featurizeImage： 機器學習映像功能，其潛在轉換](https://docs.microsoft.com/r-server/r-reference/microsoftml/featurizeimage)

在此範例中，請參閱程式碼的第二個區塊。 載入影像時，調整大小，以及預先定型的 convolutional DNN 模型的特徵化。 DNN featurizer 輸出接著用於定型影像分類的線性模型。

影像必須調整大小以符合需求的定型的模型： 用於定型的影像時發生 224 x 224 像素。 如果您使用 AlexNet 模型，影像會調整大小以便 227 x 227 像素。

```R
 model <- rxFastLinear(
     Label ~ Features,
     data = train,
     mlTransforms = list(
         loadImage(vars = list(Features = "Path")),
         resizeImage(vars = "Features", width = 224, height = 224), 
         extractPixels(vars = "Features"),
         featurizeImage(var = "Features")
         ),
     mlTransformVars = "Path")
```

> [!NOTE]
> 不可能讀取或修改預先定型的模型，因為它們會壓縮使用原生格式，來改善效能。

### <a name="text-analysis-example"></a>文字分析範例

請參閱下列範例示範如何使用預先定型的文字如何模型文字分類：

[使用文字 Featurizer 情緒分析](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)
