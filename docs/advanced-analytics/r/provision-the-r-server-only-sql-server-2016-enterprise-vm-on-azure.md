---
title: "佈建虛擬機器上 Azure 機器學習 |Microsoft 文件"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c8826df7-aa67-4768-baa9-bdc875c4a766
caps.latest.revision: "12"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 6777a47d9f2078b662990c2597f84cc41222de63
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="provision-a-virtual-machine-for-machine-learning-on-azure"></a>佈建虛擬機器上 Azure 機器學習

在 Azure 上的虛擬機器是快速設定機器學習解決方案的完整伺服器環境的方便選項。

本文列出包含與機器學習服務，以及一些相關的 Vm 的 SQL Server 虛擬機器映像。

本文也會提供有關修改，或升級現有的虛擬機器中 SQL Server 執行個體的常見問題解答。

+ [目前的虛擬機器的清單](#bkmk_list)

## <a name="provision-a-virtual-machine-with-sql-server-and-machine-learning"></a>佈建 SQL server 虛擬機器和機器學習

如果您不熟悉使用 Azure Vm，建議您看到這些文件，如需有關使用入口網站，並設定虛擬機器。

+ [虛擬機器 - 快速入門](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)
+ [開始使用與 Windows 虛擬機器](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/)

請務必使用新版 Azure 入口網站或 Azure Marketplace。 如果瀏覽在傳統入口網站上 Azure 資源庫，便無法使用一些映像。

**建立虛擬機器**

1. 開啟 Azure 入口網站： [portal.azure.com](https:portal.azure.com)。

2. 按一下**虛擬機器**，或按一下**新增**。

3. 按一下 **[加入]**。

4. 在頁面頂端的 [搜尋] 方塊中輸入 「 機器學習伺服器 」 或 「 SQL Server > 以查看相關的虛擬機器的清單。

5. 檢閱需求，然後按一下 **建立**若要開始使用。

6. 虛擬機器已建立並執行之後，按**連接**按鈕來開啟連接並登入新的機器。

5. 您連接之後，您可以安裝其他的 R 或 Python 封裝，或設定慣用的開發工具。

### <a name="connect-to-the-virtual-machine"></a>連接至虛擬機器

用戶端連接至虛擬機器上執行的 SQL Server 的方式需視用戶端和網路設定的位置而有所不同。

如需詳細資訊，請參閱[連接到 Azure 上的 SQL Server 虛擬機器](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-connect)。

## <a name="frequently-asked-questions"></a>常見問題集

本節中的機器學習來自 Microsoft 的虛擬機器的一些常見問題。

### <a name="can-i-install-a-virtual-machine-with-sql-server-2017"></a>可以安裝在虛擬機器與 SQL Server 2017 嗎？

使用開始 2017 年 11 月適用於 SQL Server 2017 Enterprise Edition，其中包含機器學習服務 Windows 型虛擬機器。 

新的資料科學虛擬機器的相關公告，請觀看這些部落格網站：

+ [Cortana 智慧和機器學習服務](https://blogs.technet.microsoft.com/machinelearning/)
+ [資料平台內幕](https://blogs.technet.microsoft.com/dataplatforminsider/)

### <a name="adding-sql-server-to-an-existing-virtual-machine"></a>將 SQL 伺服器加入至現有的虛擬機器

除了建立虛擬機器使用的映像已經包含 SQL Server 機器學習服務，您可以在現有的虛擬機器上安裝 SQL Server，啟用機器學習功能。 我們建議 Enterprise 或 Developer 版本中，以避免資源條件約束。 安裝也需要您使用您自己的授權金鑰。

當您執行安裝程式時，請務必選取的機器學習功能以及至少一個語言 （R 或 Python）。 若要啟用機器學習服務與 SQL Server 通訊，並讓網路上的虛擬機器需要一些額外的步驟。

如需詳細資訊，請參閱[Azure 的虛擬機器上安裝 SQL Server R Services](../r/installing-sql-server-r-services-on-an-azure-virtual-machine.md)。

### <a name="using-machine-learning-in-azure-sql-database"></a>使用 Azure SQL database 中的機器學習服務

中的開始在 2017年，Azure SQL Database 支援使用 R 來定型模型，並將它們用於預測。 

R 服務中-資料庫可做為預覽功能，並有一些限制，因此相較於內部部署版本的 SQL Server。 如需詳細資訊，請參閱[Azure SQL DB](../r/using-r-in-azure-sql-database.md)。

### <a name="can-i-upgrade-the-sql-server-version-on-a-virtual-machine"></a>可以升級虛擬機器上的 SQL Server 版本嗎？

雖然 SQL Server 2016 映像支援 R，如果您想要使用 Python，您可以升級至 SQL Server 2017，也會升級其他機器學習服務元件。

若要更新已安裝的 SQL Server 的版本，開啟 SQL Server 安裝中心上虛擬機器，然後選取**升級**選項。 Virtual machine 根據您所建立，授權可能需要。

如需詳細資訊，請參閱[使用安裝精靈升級 SQL Server](https://docs.microsoft.com/sql/database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup)。

### <a name="can-i-upgrade-just-the-machine-learning-components"></a>可以升級機器學習服務元件嗎？

RevoScaleR、 MicrosoftML 或 revoscalepy 發行新的升級，您可以升級機器學習使用這道程序所使用的 SQL server 元件_繫結_。 這不會變更您的 SQL Server 版本，但未變更的執行個體的支援原則。

如需詳細資訊，請參閱[升級 SQL Server 上的機器學習元件使用 SqlBindR](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

### <a name="how-do-i-access-data-in-an-azure-storage-account"></a>如何存取 Azure 儲存體帳戶中的資料？

當您需要使用 Azure 儲存體帳戶中的資料時，有幾個選項可以存取或移動資料︰

+ 使用公用程式，例如 [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only)，將資料從儲存體帳戶複製到本機檔案系統。 

+ 將檔案新增至儲存體帳戶上的檔案共用，然後將檔案共用掛接為 VM 上的網路磁碟機。 如需詳細資訊，請參閱 [掛接 Azure 檔案](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/)。 

### <a name="how-do-i-use-data-from-azure-data-lake-storage-adls"></a>如何使用來自 Azure Data Lake 儲存體 (ADLS) 的資料？

您可以從 ADLS 使用 RevoScaleR，使用 webHDFS 參考相同的方式就像 HDFS 檔案系統的儲存體帳戶的儲存體讀取資料。 如需詳細資訊，請參閱這篇文章：[使用 R 來執行 Azure Data Lake Store 上的檔案系統作業](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/03/14/using-r-to-perform-filesystem-operations-on-azure-data-lake-store/)。

### <a name="i-cant-find-the-rre-virtual-machine"></a>我找不到 RRE 虛擬機器

「 RRE 的 Windows 虛擬機器 」 先前中所提供之 Azure Marketplace 中已取代 「 機器學習 Server for Windows 」 映像。

還有適用於 Linux CentOS 版本 7.2、 Linux RedHat 版本 7.2 和 Ubuntu 版本 16.04 機器學習伺服器映像。

如需詳細資訊，請參閱[雲端中的機器學習伺服器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-in-the-cloud)

### <a name="configuring-machine-learning-server-or-r-server-to-support-web-services"></a>設定機器學習伺服器或 R 伺服器以支援 web 服務

如果您使用虛擬機器包含 Server 機器學習，額外的設定可能需要使用 web 服務部署，遠端執行，或虛擬機器做為您組織中部署伺服器。

如需指示，請參閱[設定機器學習伺服器來實施分析](https://docs.microsoft.com/machine-learning-server/operationalize/configure-machine-learning-server-one-box)。

如果您只想要使用 RevoScaleR 或 MicrosoftML 等套件不需要進行其他設定。

## <a name="bkmk_list"></a>虛擬機器的清單

目前，下列虛擬機器可供 SQL server 的機器學習：

|[屬性]| 註解|
|----|----|----|
| **SQL Server 2016**| ***  |
|SQL Server 2016 SP1 Enterprise on Windows|整合式的進階分析的 R 服務。|
|BYOL SQL Server 2016 SP1 Enterprise on Windows Server |整合式的進階分析的 R 服務。 |
|Windows Server 2016 上可用的授權： SQL Server 2016 SP1 Developer |整合式的進階分析的 R 服務。 |
| Data Science 虛擬機器 Windows 2012|包含常用的工具，用於資料科學，包括 Microsoft R Server Developer Edition、 SQL Server 2016 Developer edition、 Anaconda Python 發佈、 Julia Pro developer edition 和 Jupyter 筆記本如。| 
| Data Science 虛擬機器 Windows 2016|包含 SQL Server 2016 Developer Edition 支援資料庫內部 R 分析。|
|**SQL Server 2017**| ***   |
|SQL Server 2017 企業的 Windows Server 2016| 機器學習服務，具有 Python 和 R 語言支援。|
|BYOL SQL Server 2017 企業的 Windows Server 2016|機器學習服務，具有 Python 和 R 語言支援。|
| 在 Windows 伺服器上可用的 SQL Server 授權： SQL Server 2017 Developer|機器學習服務，具有 Python 和 R 語言支援。|
| **其他**| *** |
| 機器學習伺服器只有 SQL Server 2017 Enterprise|類似於 SQL Server 2016 Enterprise 映像，但包含 Server 機器學習的獨立版本，並有核心 ScaleR 和實施功能適用於 Windows 的環境最佳化。|
| 機器學習 Server for Windows|獨立伺服器的版本機器學習，含有實施最佳化 Windows 環境的功能。|
|Data Science 虛擬機器 |Linux 版本包括 R Server。 包含 SQL Server 2017 的 Linux 虛擬機器無法執行 SQL Server 中的 R 或 Python 程式碼。 不過，您可以執行計分上定型的模型使用 T-SQL 的預測函數。 如需詳細資訊，請參閱[SQl Server 中的原生計分](../sql-native-scoring.md)。|
