---
title: "SQL Server 上安裝預先定型的機器學習模型 |Microsoft 文件"
ms.date: 03/14/2018
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
ms.openlocfilehash: fd02766e4020e6f522d50bbd471c5f84c66a998b
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/19/2018
---
# <a name="install-pretrained-machine-learning-models-on-sql-server"></a>安裝預先定型的機器學習模型 SQL Server 上
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何將預先定型的模型加入至 SQL Server 執行個體在具有 R 服務或機器學習服務安裝。

建立預先定型的模型包含在 MicrosoftML 協助客戶需要以執行工作，例如情緒分析或映像功能，其潛在，但沒有取得大型資料集或複雜的模型定型的資源。 機器學習 Server 小組建立並定型這些模型，以協助您開始在文字和影像有效率地處理。 如需詳細資訊，請參閱[資源](#bkmk_resources)本文一節。

如需如何使用 SQL Server 資料的預先定型的模型的範例，請參閱 SQL Server 機器學習小組的這篇部落格：

+ [使用 SQL Server 機器學習服務中的 Python 情緒分析](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/11/01/sentiment-analysis-with-python-in-sql-server-machine-learning-services/)

## <a name="install-the-pre-trained-models"></a>安裝預先定型的模型

您可以使用 預先定型的模型與下列產品：

+ SQL Server 2016 R 服務 （資料庫）
+ SQL Server 2017 機器學習服務 （資料庫）
+ Machine Learning 伺服器 (獨立式)

安裝程序稍有不同的 SQL Server 版本而定。 請參閱下列章節，以針對每個版本的指示。

> [!NOTE]
> 不可能讀取或修改預先定型的模型，因為它們會壓縮使用原生格式，來改善效能。

### <a name="obtain-files-for-an-offline-installation"></a>取得檔案的離線安裝

若要在沒有網際網路存取的伺服器上安裝預先定型的模型，您必須事先下載適當的安裝程式，並將安裝程式複製到伺服器上的本機資料夾。 

所有的 R 伺服器和機器學習伺服器安裝程式會看到這個頁面下載連結：[離線安裝](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)

### <a name="install-pretrained-models-with-sql-server-2016-r-services"></a>使用 SQL Server 2016 R 服務安裝預先定型的模型

SQL Server 2016，您可以安裝並使用預先定型的 R 模型，只有在第一次升級機器學習中處理程序呼叫的元件，**繫結**。 

您可以執行個別的 Windows 安裝程式，Microsoft R Server 的機器學習伺服器，並選取執行個體、 執行個體**繫結**。 繫結執行個體表示的執行個體相關聯的支援原則變更為允許更頻繁更新。 

1. 啟動個別的 windows 安裝程式針對[R Server](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server)或[Server 機器學習](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)。

2. 選取要升級的執行個體，然後選取 取得預先定型的模型的選項。

    如需詳細資訊，請參閱[升級 SQL Server 所使用的機器學習元件](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

    如果您先前已執行要更新的 R 元件，而且只想要將預先定型的模型繫結，保留所有先前的選取項目**現狀**，並選取預先定型的模型選項。 
    
    無法取消選取任何先前選取的選項。如果您這樣做時，安裝程式會移除元件。

3. 我們建議您接受模型位置的預設設定。

4. 接受所有其他提示，包括授權合約。

完成繫結之後，表示的 R 版本和執行個體相關聯的程式庫使用 R 伺服器或 Server 機器學習中所提供的較新版本取代。 

SQL Server 2016，您必須執行一些額外的步驟，以向 SQL Server 2016 執行個體文件庫中的模型。 重複上述步驟，每個執行個體安裝的預先定型的模型。

1. 開啟 Windows 命令提示字元**以系統管理員身分**。

2. 瀏覽至安裝程式啟動載入器資料夾，針對 SQL Server，其中也包含 Microsoft R 安裝程式。 在 SQL Server 2016 的預設執行個體，將為資料夾：
    
    `C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\SQL2017\x64\`

3. 執行`RSetup.exe`和表示要安裝的元件、 版本，以及包含模型的來源檔案，使用此語法的資料夾：

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<SQL_DB_instance_folder>\R_SERVICES\library\MicrosoftML\mxLibs\x64"`。 

    版本參數支援下列值：

    + 發行候選版本 0: **9.1.0.0**
    + 候選版 1: **9.2.0.22**
    + RTM: **9.2.0.100**
    + 累計更新 1: **9.2.0.24**
    + 累計更新 4: **9.3.0**

    > [!NOTE]
    > 列出對應的 SQL Server 版本，讓您了解的更新發佈的時間。 如果您不確定的 SQL Server 安裝的版本，請開啟 R_SERVICES 資料夾的執行個體，並且開啟 RGui (`~\R_SERVICES\bin\x64`)。 開始畫面會列出適用於 Microsoft R Open 版本和機器學習 Server 版本。 

    例如，若要使用預先定型的 R 模型的預設執行個體**R_SERVICES**，您可以執行這個命令：

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    具名執行個體，命令看起來會像下面這樣：

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL13.MyInstanceName\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

4. 如果安裝成功，下列模型應加入至您`R_SERVICES`資料夾：

    + AlexNet\_Updated.model
    + ImageNet1K\_mean.xml
    + pretrained.model
    + ResNet\_101\_Updated.model
    + ResNet\_18\_Updated.model
    + ResNet\_50\_Updated.model

### <a name="install-pretrained-models-on-sql-server-2017"></a>安裝 SQL Server 2017 預先定型的模型

如果您已安裝 SQL Server 2017，您可以取得預先定型的模型有兩種：

+ 使用繫結，來升級的 Python 和 R 元件，並同時安裝預先定型的模型
+ 安裝預先定型的模型

下面的指示說明的程序來升級機器學習服務元件，並在相同的時間取得預先定型的模型。

1. 執行 windows 安裝程式的機器學習服務伺服器。 您可以從這個頁面上的連結下載安裝程式：[安裝機器學習 Server for Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)。

2. 如果您要安裝之模型到沒有網際網路存取的伺服器，請務必也從本頁面下載的安裝程式的預先定型的模型：[離線安裝的機器學習伺服器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)。

3. 執行安裝程式。

4. 若要同時升級 R 或 Python 元件，選取您想要更新的語言 （R，或 Python，或兩者）。

    如果您之前安裝 Server 機器學習並更新 R 或 Python 元件使用的繫結選項，保留所有先前的選取項目**現狀**，然後選取 預先定型的模型選項。 無法取消選取任何先前選取的選項。如果您這樣做時，安裝程式會移除元件。

5. 接受所有其他提示，包括授權合約。

需要使用 with SQL Server 2017，不需要額外組態。

> [!NOTE]
> 
> 對於 Python 模型，您可能會發生錯誤時從 Python 程式碼呼叫的模型檔案。 這是路徑的因為限制在目前的 Python 實作，其中的模型檔案長度限制。 已修正此問題，並將可在服務即將發行版本中。

### <a name="installing-pretrained-models-with-r-server-standalone"></a>安裝 R Server （獨立） 預先定型的模型

如果您已安裝舊版的 R 伺服器 （獨立） 使用 SQL Server 2016 安裝程式，您可以新增藉由升級使用較新的 windows installer 的 R 伺服器使用預先定型的模型的能力。 

預先定型的模型先開始，變成可以做為選項與[Microsoft R Server 9.1](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/introducing-microsoft-r-server-9-1-release/)，但是已新增每個版本升級。 我們建議您取得最新版本，但此處所列的舊版[R Server 版本](https://docs.microsoft.com/machine-learning-server/install/r-server-install)

下列指示說明如何升級的 R 元件，並同時將加入預先定型的模型。

1. 啟動個別的 windows 安裝程式針對[R Server](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server)或[Server 機器學習](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)。

2. 選取您想要更新，然後選取的語言**Pre-trained 模型**選項。

    > [!TIP]
    > 如果您先前已執行安裝程式更新 R 伺服器 （獨立），而且只想要將預先定型的模型，保留所有先前的選取項目**現狀**，然後選取剛才預先**-定型模型**選項. **不這麼做**取消選取任何先前選取的選項; 如果您這樣做時，安裝程式會移除元件。

    我們建議您接受模型位置的預設設定。

3. 按一下 **[繼續]**。 

4. 接受所有其他提示，包括授權合約。

安裝完成之後，您必須執行一些額外的步驟來註冊預先定型的模型。

1. 開啟 Windows 命令提示字元**以系統管理員身分**。

2. R 伺服器 （獨立），其中也包含 Microsoft R 安裝程式，瀏覽至安裝程式啟動載入器資料夾。 

3. 執行`RSetup.exe`和表示要安裝的元件、 版本，以及包含模型的來源檔案，使用此語法的資料夾：

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "~\R_SERVER\library\MicrosoftML\mxLibs\x64"`

    版本參數支援下列值：

    + 發行候選版本 0: **9.1.0.0**
    + 候選版 1: **9.2.0.22**
    + RTM: **9.2.0.100**
    + 累計更新 1: **9.2.0.24**
    + 累計更新 4: **9.3.0**

    比方說，若要啟用預先定型的模型的最新版本的 R 中使用預設安裝的 R 伺服器 （獨立），您會執行此陳述式：

    `RSetup.exe /install /component MLM /version 9.3.0 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\MicrosoftML\mxLibs\"`

### <a name="installing-pretrained-models-with-machine-learning-server-standalone"></a>安裝預先定型的模型使用機器學習 Server （獨立）

如果您安裝使用 SQL Server 2017 安裝程式的機器學習伺服器時，您會加入執行 windows 安裝程式的預先定型的模型。 您可以選取選項以升級的 R 或 Python 的元件，並同時加入 預先定型的模型。 

安裝已完成不之後，需要任何額外的設定。

## <a name="bkmk_resources"></a> 參考資料和資源

目前可用的模型是情緒分析和影像分類的深度類神經網路 (DNN) 模型。 所有預先定型的模型已定型使用 Microsoft 的[計算網路 Toolkit](https://cntk.ai/Features/Index.html)，或**CNTK**。

每個網路的設定根據下列參考實作：

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

如需這些深層學習模型，以及如何 ere 實作與 CNTK 來定型中使用的演算法的詳細資訊，請參閱下列文章：

+ [Microsoft 研究人員演算法設定 ImageNet 挑戰里程碑](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Microsoft 計算網路工具組提供最有效率的分散式的深層學習計算效能](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

### <a name="how-to-use-pre-trained-models-for-text-analysis"></a>如何預先定型的模型用於文字分析

請參閱下列範例示範如何使用預先定型的文字如何模型文字分類：

[使用文字 Featurizer 情緒分析](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

### <a name="how-to-use-pretrained-models-for-image-detection"></a>如何使用映像偵測預先定型的模型

映像預先定型的模型支援功能，其潛在您提供的映像。 若要使用模型，您呼叫**featurizeImage**轉換。 載入影像時，調整大小，以及定型模型的特徵化。 DNN featurizer 輸出接著用於定型影像分類的線性模型。

若要使用此模型中，所有映像必須調整大小以符合需求的定型的模型。 例如，如果您使用 AlexNet 模型時，影像應該能調整 227 x 227 像素。

如需詳細資訊，請參閱[情緒分析及映像偵測預先定型的模型](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)
