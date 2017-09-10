---
title: "在 Azure 上佈建 R Server 專用的 SQL Server 2016 Enterprise VM | Microsoft Docs"
ms.custom: 
ms.date: 06/05/2017
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
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a3bfca0753984f09220d8ca4e4f6933c949daf2b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="advanced-analytics-virtual-machines-on-azure"></a>進階的分析 Azure 上的虛擬機器

在 Azure 上的虛擬機器是快速設定機器學習解決方案的完整伺服器環境的方便選項。 本主題列出一些包含 R Server、 SQL Server 與 machine learning 中或其他資料科學工具，從 Microsoft 的虛擬機器映像。

> [!TIP]
> 我們建議您使用新版 Azure 入口網站和 Azure Marketplace。 如果瀏覽在傳統入口網站上 Azure 資源庫，便無法使用一些映像。

Azure Marketplace 包含支援資料科學的多部虛擬機器。 這份清單不是完整的但只提供，包括 Microsoft R Server 或 SQL Server 的機器學習服務，以便探索映像的名稱。

## <a name="how-to-provision-a-vm"></a>如何佈建 VM

如果您不熟悉使用 Azure Vm，建議您看到這些文件，如需有關使用入口網站，並設定虛擬機器。

+ [虛擬機器 - 快速入門](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)
+ [開始使用 Windows 虛擬機器](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-hero-tutorial/)

### <a name="find-an-image"></a>尋找映像

1. 從 Azure 儀表板中，按一下 [ **Marketplace**。

    - 按一下**智慧及分析**或**資料庫**，然後在中輸入"R"**篩選**控制項以查看 R Server 虛擬機器的清單。
    - 其他可能字串**篩選**控制是*資料科學*和*機器學習*
    - 在搜尋中使用 %萬用字元，來尋找包含目標字串，例如 VM 名稱*R*或*Julia*。

2. 若要取得 R Server for Windows，請選取**R 伺服器只有 SQL Server 2016 Enterprise**。
  
    [R 伺服器](https://msdn.microsoft.com/microsoft-r/rserver-whats-new)授權為 SQL Server Enterprise Edition 的功能，但版本 9.1。 會安裝成獨立伺服器和服務的現代的生命週期支援原則。

3. VM 已建立並在執行之後，按一下 [連接] 按鈕以開啟連線並登入新電腦。

4. 您連接之後，您可能需要安裝其他的 R 工具或開發工具。

### <a name="install-additional-r-tools"></a>安裝其他的 R 工具

根據預設，Microsoft R Server 包含所有已安裝的 R 工具，以及 R 的基本安裝，包括 RTerm 和 RGui。 如果您想要立即開始使用 R，在桌面上已經新增 RGui 的捷徑。

不過，您可能想要安裝其他的 R 工具，例如 RStudio、 Visual Studio (RTVS) 或 Microsoft R 用戶端的 R 工具。 請參閱下列連結，以取得下載位置和指示︰
+ [適用於 Visual Studio 的 R 工具](https://docs.microsoft.com/visualstudio/rtvs/installation)
+ [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/install-r-client-windows)
+ [RStudio for Windows](https://www.rstudio.com/products/rstudio/download/)

安裝完成之後，請務必變更預設的 R 執行階段位置，好讓所有的 R 開發工具都能使用 Microsoft R Server 程式庫。

### <a name="configure-server-for-web-services"></a>設定 web 服務的伺服器

如果虛擬機器包含 R Server，則需要其他的設定來使用 Web 服務部署、遠端執行或利用 R Server 做為組織中的部署伺服器。 如需指示，請參閱[設定 R Server 以進行運作化 (英文)](https://msdn.microsoft.com/microsoft-r/operationalize/configuration-initial)。

> [!NOTE]
> 如果您只想要使用 RevoScaleR 或 MicrosoftML 等套件不需要進行其他設定。

## <a name="r-server-images"></a>R 伺服器映像

### <a name="microsoft-data-science-virtual-machine"></a>Microsoft Data Science 虛擬機器

來自設定與 Microsoft R Server，以及 Python （Anaconda 發佈）、 Jupyter 筆記本伺服器、 Visual Studio Community 版本、 Power BI Desktop、 Azure SDK 和 SQL Server Express edition。

在 Windows Server 2012 上執行的 Windows 版本，並包含許多特別工具可用來模型化和分析，包括 CNTK 和 mxnet、 受歡迎的 R 封裝，例如 xgboost，與 Vowpal Wabbit。

### <a name="linux-data-science-virtual-machine"></a>Linux Data Science 虛擬機器

也包含用於資料科學和開發活動，包括 Microsoft R Open、 Microsoft R Server Developer Edition、 Anaconda Python 和 Jupyter 筆記本 Python、 R 和 Julia 的常用工具。

這個 VM 映像最近已更新以包含 JupyterHub，可讓多個使用者，使用不同的驗證方法，包括本機作業系統帳戶驗證與 Github 帳戶驗證透過開放原始碼軟體。 如果您想要執行訓練類別，並想要所有學生共用相同的伺服器，但使用不同的筆記及目錄，JupyterHub 是特別有用的選項。

Ubuntu、 Centos 和 Centos CSP 提供映像。

### <a name="r-server-only-sql-server-2016-enterprise"></a>R 伺服器只有 SQL Server 2016 Enterprise

此虛擬機器包含的獨立安裝程式[R 伺服器 9.1。](https://msdn.microsoft.com/microsoft-r/rserver-whats-new) 支援新的現代化軟體生命週期授權模型。

 R 伺服器也會提供 Linux CentOS 版本 7.2、 Linux RedHat 版本 7.2，和 Ubuntu 版本 16.04 映像。

 > [!NOTE]
 > 這些虛擬機器會取代 Azure Marketplace 中先前提供的 **RRE for Windows 虛擬機器**。

## <a name="sql-server-images"></a>SQL Server 映像

若要使用 R 服務 （資料庫） 或機器學習服務，您就必須安裝其中一個 SQL Server Enterprise 或 Developer edition 虛擬機器，並新增機器學習服務，如這裡所述：[上安裝 SQL Server R ServicesAzure 虛擬機器](../../advanced-analytics/r-services/installing-sql-server-r-services-on-an-azure-virtual-machine.md)。

> [!NOTE]
> 目前，機器學習服務不支援的 Linux 虛擬機器上的 SQL Server 2017，或在 Azure SQL Database。 您必須使用 SQL Server 2016 SP1 或 SQL Server 2017 for Windows。

Data Science 虛擬機器也會包含已啟用 R 服務功能的 SQL Server 2016。


## <a name="other-vms"></a>其他 Vm

### <a name="deep-learning-toolkit-for-the-data-science-virtual-machine"></a>深層的 Data Science 虛擬機器學習工具組

此虛擬機器包含相同的機器學習工具用於資料科學虛擬機器，但使用 mxnet、 CNTK、 TensorFlow 和 Keras GPU 版本。 此映像只用於 Azure 的 GPU N 數列執行個體。 

深入學習工具組也提供一組深入了解使用 GPU，包括 CIFAR 10 資料庫上的影像辨識和 MNIST 資料庫上的字元辨識範例解決方案的範例。 美國中南部、 美國東部、 西歐、 和東南亞中目前使用 GPU 的執行個體。

> [!IMPORTANT]
> GPU 執行個體目前僅適用於美國中南部。


## <a name="frequently-asked-questions"></a>常見問題集

### <a name="can-i-install-a-virtual-machine-with-sql-server-2017"></a>可以安裝在虛擬機器與 SQL Server 2017 嗎？

映像可包含的 SQL Server 2017 CTP 2.0 Linux 環境中，但這些環境目前不支援機器學習服務。 

Windows 型虛擬機器的 SQL Server 2017 Enterprise Edition，其中包含機器學習服務後，即可使用的公開版本。 

或者，您可以使用 SQL Server 2016 映像，並升級您的 R 執行個體，如下所述：[升級執行個體使用 SqlBindR](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。 

或者，建立虛擬機器並下載 CTP 2.0 preview 的[SQL Server 2017](https://www.microsoft.com/sql-server/sql-server-2017)。

### <a name="how-do-i-access-data-in-an-azure-storage-account"></a>如何存取 Azure 儲存體帳戶中的資料？

當您需要使用 Azure 儲存體帳戶中的資料時，有幾個選項可以存取或移動資料︰

+ 使用公用程式，例如 [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only)，將資料從儲存體帳戶複製到本機檔案系統。 

+ 將檔案新增至儲存體帳戶上的檔案共用，然後將檔案共用掛接為 VM 上的網路磁碟機。  如需詳細資訊，請參閱 [掛接 Azure 檔案](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/)。 

### <a name="how-do-i-use-data-from-azure-data-lake-storage-adls"></a>如何使用來自 Azure Data Lake 儲存體 (ADLS) 的資料？

如果您參考相同的方式就像 HDFS 檔案系統中，使用 [webHDFS 的儲存體帳戶，您可以從使用 RevoScaleR，ADLS 儲存體讀取資料。  如需詳細資訊，請參閱這篇文章：[使用 R 來執行 Azure Data Lake Store 上的檔案系統作業](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/03/14/using-r-to-perform-filesystem-operations-on-azure-data-lake-store/)。

## <a name="see-also"></a>另請參閱

[SQL Server R 服務](https://msdn.microsoft.com/library/mt604845.aspx)


