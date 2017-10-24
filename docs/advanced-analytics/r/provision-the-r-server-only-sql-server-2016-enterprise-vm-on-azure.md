---
title: "佈建虛擬機器上 Azure 機器學習 |Microsoft 文件"
ms.custom: 
ms.date: 10/16/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c8826df7-aa67-4768-baa9-bdc875c4a766
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8cc1fcfdeae8742a93916dfb08c9db1215f88721
ms.openlocfilehash: 7cb9e069fc3b537f8aab9d048a152435ad0cc6ac
ms.contentlocale: zh-tw
ms.lasthandoff: 10/17/2017

---
# <a name="provision-a-virtual-machine-for-machine-learning-on-azure"></a>佈建虛擬機器上 Azure 機器學習

在 Azure 上的虛擬機器是快速設定機器學習解決方案的完整伺服器環境的方便選項。 本文列出一些使用機器學習中包含 R Server、 機器學習伺服器或 SQL Server 的虛擬機器映像。

這份清單不是完整的但只提供機器學習伺服器或 SQL Server 機器學習服務，以便探索相關的映像的名稱。

> [!TIP]
> 我們建議您使用新版 Azure 入口網站和 Azure Marketplace。 如果瀏覽在傳統入口網站上 Azure 資源庫，便無法使用一些映像。

## <a name="how-to-provision-a-virtual-machine"></a>如何佈建虛擬機器

如果您不熟悉使用 Azure Vm，建議您看到這些文件，如需有關使用入口網站，並設定虛擬機器。

+ [虛擬機器 - 快速入門](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)
+ [開始使用 Windows 虛擬機器](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/)

## <a name="find-a-machine-learning-image"></a>找到的機器學習映像

1. 從 Azure 入口網站 (portal.azure.com)，按一下 **虛擬機器**，或按一下**新增**。

2. 找出在頁面上，依名稱篩選資源，您可以使用頂端的 [搜尋] 方塊。 

3. 在中，輸入 「 R 伺服器 」 （或 「 ML 伺服器 」）**篩選**控制項以查看相關資源的清單。 按一下**Marketplace 中的搜尋**以檢視虛擬機器。

    > [!TIP]
    > 
    > 篩選控制項的其他可能的字串為"資料科學 」 和 「 機器學習 」。
    > 
    > 使用`%`萬用字元搜尋來尋找虛擬機器的名稱中。 例如，您可以輸入`"`%julia%` or `%R %'。

4. 若要取得 R Server for Windows，請選取**R 伺服器只有 SQL Server 2016 Enterprise**。
  
    [R 伺服器](https://msdn.microsoft.com/microsoft-r/rserver-whats-new)授權 SQL Server Enterprise Edition 的功能，但版本 9.1 安裝成獨立伺服器和服務的現代的生命週期支援原則。

    > [!NOTE] 
    > 
    > 這是落在查看新的虛擬機器，其中包含 SQL Server 2017 和 9.2.1 發行的機器學習 Server 版本。
    > 之前，您可以更新使用 SQL Server 安裝中心，然後選擇 [升級] 選項安裝這部虛擬機器上的 SQL Server 版本。 如需詳細資訊，請參閱[使用安裝精靈升級 SQL Server](https://docs.microsoft.com/sql/database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup)。

5. 虛擬機器已建立並執行之後，按**連接**按鈕來開啟連接並登入新的機器。

5. 您連接之後，您可以安裝其他的 R 封裝或您慣用的開發工具。

### <a name="install-additional-r-tools"></a>安裝其他的 R 工具

根據預設，Microsoft R Server 包含所有已安裝的 R 工具，以及 R 的基本安裝，包括 RTerm 和 RGui。 也已加入 RGui 捷徑至桌面。

不過，您可能想要安裝其他的 R 工具，例如 RStudio、 R Tools for Visual Studio (RTVS) 或 Microsoft R 用戶端。 請參閱下列連結，以取得下載位置和指示︰

+ [適用於 Visual Studio 的 R 工具](https://docs.microsoft.com/visualstudio/rtvs/installation)
+ [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/install-r-client-windows)
+ [RStudio for Windows](https://www.rstudio.com/products/rstudio/download/)

安裝完成之後，請務必變更預設的 R 執行階段位置，好讓所有的 R 開發工具都能使用 Microsoft R Server 程式庫。

### <a name="configure-r-server-to-support-web-services"></a>設定為支援 web 服務的 R 伺服器

若要使用 web 服務部署，遠端執行，或為您組織中部署伺服器利用 R 伺服器需要額外的設定。 如需指示，請參閱[設定 R 伺服器來實施分析](https://docs.microsoft.com/machine-learning-server/install/operationalize-r-server-one-box-config)。

> [!NOTE]
> 如果您只想要使用 RevoScaleR 或 MicrosoftML 等套件不需要進行其他設定。

## <a name="other-virtual-machines"></a>其他虛擬機器

下列映像可從 Azure Marketplace，包括完整設定機器學習工具，但不是一定包含 SQL Server。

### <a name="data-science-virtual-machine"></a>Data Science 虛擬機器

此映像已預先設定與 Microsoft R Server，以及 Python （Anaconda 發佈）、 Jupyter 筆記本伺服器、 Visual Studio Community 版本、 Power BI Desktop、 Azure SDK 和 SQL Server Express edition。

在 Windows Server 2012 上執行的 Windows 版本，而且包含許多特別工具可用來模型化和分析，包括[CNTK](https://www.microsoft.com/cognitive-toolkit/)， [mxNet](https://mxnet.incubator.apache.org/)，並將受歡迎的 R 封裝這類**xgboost**.

Linux 版本可供 Ubuntu、 Centos 和 Centos CSP，而且包含許多常用的工具，用於資料科學和開發活動。

如需詳細資訊，請參閱[簡介至 Azure Data Science 虛擬機器的 Linux 和 Windows](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/provision-vm)。

此映像最近已更新成包含： 

+ Julia，未來的可擴充、 功能強大的資料科學語言的支援 
+ JupyterHub，這是很有用的選項，當您想要執行訓練類別，並想要所有學生共用相同的伺服器，但使用不同的筆記本和目錄。

如需有關支援的工具和機器學習架構的詳細資訊，請參閱[了解您的 Data Science 虛擬機器](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/dsvm-tools-overview)

### <a name="r-server-virtual-machines"></a>R Server 虛擬機器

除了**R 伺服器只有 SQL Server 2016 Enterprise**映像，您可以取得包含 R Server 的獨立虛擬機器。 Linux CentOS 版本 7.2、 Linux RedHat 版本 7.2，和 Ubuntu 版本 16.04 使用映像。

如需詳細資訊，請參閱[雲端中的機器學習伺服器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-in-the-cloud)

 > [!NOTE]
 > 這些虛擬機器會取代 Azure Marketplace 中先前提供的 **RRE for Windows 虛擬機器**。

### <a name="sql-server-virtual-machines"></a>SQL Server 虛擬機器

有兩個使用 SQL Server 機器學習在 Azure 中的選項：

+ 取得其中一個包含預先安裝的 SQL Server R 服務的虛擬機器映像。
+ 建立 Azure 虛擬機器並安裝 SQL Server Enterprise 或 Developer edition 使用您自己的授權金鑰。 
  
    然後，執行安裝程式以新增並啟用機器學習服務，如這裡所述： [Azure 的虛擬機器上安裝 SQL Server R Services](../r/installing-sql-server-r-services-on-an-azure-virtual-machine.md)。
+ 建立 Azure SQL Database 使用服務層可以支援機器學習並使用新的 R 服務功能目前在預覽中。 如需詳細資訊，請參閱[Azure SQL DB](../r/using-r-in-azure-sql-database.md)。

> [!NOTE]
> 目前，SQL Server 機器學習服務不支援的 Linux 虛擬機器上的 SQL Server 2017。 不過，您可以執行計分上定型的模型使用 T-SQL 的預測函數。 如需詳細資訊，請參閱[SQl Server 中的原生計分](../sql-native-scoring.md)。 

### <a name="virtual-machines-for-deep-learning"></a>深入了解虛擬機器 

之前，Microsoft 提供深入學習工具組的 Data Science 虛擬機器，您無法加入至現有 Data Science 虛擬機器。 深入了解虛擬機器，其中包含常用的深入學習工具現在已取代這個工具組：

+ GPU 深入學習架構版本像 Microsoft 認知工具組、 TensorFlow、 Keras 和 Caffe
+ 內建的 GPU 驅動程式
+ 讓影像和文字處理工具的集合
+ Enterprise 開發工具，例如 Microsoft R Server Developer Edition，Anaconda Python Jupyter 筆記本的 Python 和 R
+ Python、 R、 SQL Server，以及執行更多的開發人員工具
+ 讓影像和文字了解的端對端範例

使用 Windows 2016 或 Ubuntu Linux 平台上深入學習虛擬機器。 如需詳細資訊，請參閱[深入學習和 AI 架構](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/dsvm-deep-learning-ai-frameworks)。

> [!IMPORTANT]
> 
> 部署此虛擬機器需要有限的 Azure 區域中可用的 Azure GPU NC 系列虛擬機器映像。 如需可用性資訊，請參閱[依地區可用的產品](https://azure.microsoft.com/en-us/regions/services/)。 當您佈建虛擬機器時，請務必使用**HDD**為磁碟類型，不**SSD**。

## <a name="frequently-asked-questions"></a>常見問題集

本節中的機器學習來自 Microsoft 的虛擬機器的一些常見問題。

### <a name="can-i-install-a-virtual-machine-with-sql-server-2017"></a>可以安裝在虛擬機器與 SQL Server 2017 嗎？

Windows 型虛擬機器的 SQL Server 2017 Enterprise Edition，其中包含機器學習服務即將推出。 尋找這些部落格網站上的公告：

+ [Cortana 智慧和機器學習](https://blogs.technet.microsoft.com/machinelearning/)
+ [資料平台內幕](https://blogs.technet.microsoft.com/dataplatforminsider/)

### <a name="how-do-i-access-data-in-an-azure-storage-account"></a>如何存取 Azure 儲存體帳戶中的資料？

當您需要使用 Azure 儲存體帳戶中的資料時，有幾個選項可以存取或移動資料︰

+ 使用公用程式，例如 [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only)，將資料從儲存體帳戶複製到本機檔案系統。 

+ 將檔案新增至儲存體帳戶上的檔案共用，然後將檔案共用掛接為 VM 上的網路磁碟機。  如需詳細資訊，請參閱 [掛接 Azure 檔案](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/)。 

### <a name="how-do-i-use-data-from-azure-data-lake-storage-adls"></a>如何使用來自 Azure Data Lake 儲存體 (ADLS) 的資料？

如果您參考相同的方式就像 HDFS 檔案系統中，使用 webHDFS 的儲存體帳戶，您可以從使用 RevoScaleR，ADLS 儲存體讀取資料。  如需詳細資訊，請參閱這篇文章：[使用 R 來執行 Azure Data Lake Store 上的檔案系統作業](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/03/14/using-r-to-perform-filesystem-operations-on-azure-data-lake-store/)。



