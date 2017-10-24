---
title: "Microsoft 的機器學習服務 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 10/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 341e80f5-3b59-4122-bbaa-969d7904297d
caps.latest.revision: 23
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 246ea9f306c7d99b835c933c9feec695850a861b
ms.openlocfilehash: ddc9b3f17afe1f9d4c811e4a5871f48a3a08de7f
ms.contentlocale: zh-tw
ms.lasthandoff: 10/13/2017

---
# <a name="microsoft-machine-learning-services"></a>Microsoft 機器學習服務

Microsoft 機器學習服務的目標是提供可延伸性並可擴充的平台整合與使用機器學習服務的應用程式的機器學習工作和工具。 平台必須滿足需求的所有使用者參與的資料開發和分析程序中，資料科學家從架構設計人員和資料庫管理員。

主要優點包括：

+ 可擴充的分析
+ 多個平台和 「 寫入一次，部署隨處 」 解決方案的計算內容
+ 會使分析資料，就能避免資料移動和資料的風險
+ 資料科學家可以選擇他們自己的工具和語言
+ 與 Microsoft 的企業功能整合開放原始碼的最佳的功能
+ 簡化的系統管理
+ 容易部署及使用預測模型

## <a name="in-database-analytics-with-sql-server"></a>資料庫與 SQL Server 分析

在 SQL Server 2016 中，Microsoft 會啟動整合熱門的開放原始碼 R 語言與商務應用程式的兩個伺服器平台：

+ **SQL Server R Services (資料庫內)**用來與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
+ **Microsoft R Server**，針對 Windows 和 Linux 伺服器上的企業層級 R 部署

在 SQL Server 2017，名稱已變更以反映受歡迎的 Python 語言的支援。

+ **SQL Server 機器學習服務 （資料庫）**針對資料庫中的分析支援 R 和 Python。
+ **Microsoft Machine Learning 伺服器**Windows 伺服器上，與其他支援的平台晚期 2017年計劃的擴充支援 R，並將 Python 的部署。

### <a name="benefits"></a>優點

Microsoft 機器學習服務將藉由使用資料庫的同一部電腦上執行的 R 整合到資料的計算。 它包含受信任的啟動控制板服務外部執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]處理，並與 R 或 Python 執行階段安全地通訊。

使用 SQL Server 機器學習服務，您可以定型的模型、 產生繪圖、 執行計分，以及輕鬆之間移動資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Python 或 R。

資料科學家測試和開發解決方案可以從遠端的開發電腦以安全地在伺服器上，執行程式碼傳送指令碼，或他們也可以內嵌 SQL 預存程序中的機器學習程式碼至 SQL Server 部署完成的解決方案。

當您安裝 SQL Server 的機器學習服務時，您會取得的開放原始碼 R 或 Python 語言，以及可調整 R 和 Python 程式庫由 Microsoft 提供的分佈。 SQL Server 資料庫引擎也會包含增強的連線，並確保更快、 更安全的通訊，例如 R 或 Python 外部語言設計的新元件。

### <a name="where-to-get-it"></a>取得位置

若要開始，請參閱下列資源：

+ [SQL Server R 服務](sql-server-r-services.md)
+ [SQL Server Python 的服務](../python/sql-server-python-services.md)
+ [機器學習教學課程](../tutorials/machine-learning-services-tutorials.md)

> [!NOTE]
> 只有在 SQL Server 2017 提供 python 的支援。 

## <a name="machine-learning-server-standalone-and-microsoft-r-server-standalone"></a>機器學習服務伺服器 （獨立） 與 Microsoft R Server （獨立）

此獨立伺服器系統支援多種平台和使用多種企業資料來源，例如 Linux 和 HD Insight 上的分散式、 可調整的 R 解決方案。 如果您不需要整合與 SQL Server，您可以安裝 R 伺服器，以啟用快速開發、 部署與實施機器學習的解決方案。 您也可以使用 R Server 安裝程式來升級 SQL Server 執行個體相關聯的 R 元件，並取得最新版的。

如果您安裝 Microsoft Machine Learning 伺服器使用 SQL Server 2017 安裝程式，但您也會部署，並使用 Python 應用程式。

如需詳細資訊，請參閱[Microsoft Machine Learning 伺服器](https://docs.microsoft.com/r-server/index)。

## <a name="related-technologies"></a>相關的技術

機器學習生態系統，包括工具、 提供者、 增強的 R，並將 Python 封裝、 雲端開發和服務平台，以及整合式的開發環境中，Microsoft 提供廣泛的支援。

### <a name="r-tools-for-visual-studio"></a>適用於 Visual Studio 的 R 工具

Visual Studio 提供完整的 R 語言開發環境。 該外掛程式包括編輯器、互動式視窗、繪圖功能、偵錯工具等等。 您可以從 R 使用 .NET 語言，或從 .NET 透過開放原始碼程式庫 (如 R.NET 和 rClr) 叫用 R。

Visual Studio 也會有極佳的 Python 開發環境。 沒有任何簡單的方法可以享受存取 SQL 資料庫開發工具，同時它會使用機器學習語言。

如需詳細資訊，請參閱：

+ [適用於 Visual Studio 的 R 工具](https://www.visualstudio.com/vs/rtvs/)
+ [Python-Visual Studio](https://www.visualstudio.com/vs/python/)

### <a name="azure-machine-learning"></a>Azure Machine Learning

當您在 Azure Machine Learning Studio 中建立您自己工作區時，您必須存取超過 400 種已預先載入的 R 封裝。 您也可以選擇當您建立的實驗使用 R 來部署 R 使用標準 CRAN R 散發，或 Microsoft R Open。 您甚至可以建立您自己的 R 封裝並上傳到 Azure，以執行做為自訂的模組。

如需詳細資訊，請參閱下列資源：

+ [透過 R 擴展您的經驗](https://docs.microsoft.com/azure/machine-learning/machine-learning-extend-your-experiment-with-r)
+ [Azure Machine Learning 中撰寫自訂 R 模組](https://docs.microsoft.com/azure/machine-learning/machine-learning-custom-r-modules)

許多 Azure ML 中提供的演算法現在會包含在 Microsoft 機器學習服務，做為 MicrosoftML 封裝的一部分。 如需詳細資訊，請參閱[MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)。

Azure Machine Learning 為資料科學家和開發人員建立、 定型和使用 Web 服務的模型部署至另一個方便的平台。 您可以將解決方案發佈至[Machine Learning Marketplace](http://datamarket.azure.com/browse/data?category=machine-learning)。

### <a name="data-science-virtual-machines"></a>資料科學虛擬機器

您可以在 Microsoft Azure 部署預先安裝或預先設定版本的 [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] ，以便更輕鬆開始使用資料探索，並且立即在雲端建立模型，而不需在內部部署設定已完整設定的系統。

Azure Marketplace 包含數部支援資料科學的虛擬機器︰

+ **Microsoft 資料科學虛擬機器** 設定使用 Microsoft R Server，以及 Python (Anaconda 發佈版本)、Jupyter 筆記本伺服器、Visual Studio Community 版、Power BI Desktop、Azure SDK 以及 SQL Server Express 版。

+ **Microsoft R Server 2016 for Linux** 包含最新版的 R Server (9.0.1 版)。 不同 Vm 可供 CentOS 版本 7.2 和 Ubuntu 16.04 版本。

+ **R 伺服器只有 SQL Server 2016 Enterprise**虛擬機器包含 R 伺服器 9.0.1 支援新的現代化軟體生命週期授權模型的獨立安裝程式。

> [!TIP]
> 新[資料科學 VM 的 Windows Server 2016](http://aka.ms/dsvm/win2016)提供常用的深入學習架構，例如 CNTK GPU 版本。 預先安裝的工具包括 GPU NVIDIA 驅動程式、 CUDA Toolkit 8.0 和 GPU 工作負載的 NVIDIA cuDNN 程式庫。 在只是分鐘，您可以擁有完整的環境來建立可以在 CPU 或 CPU 和 GPU 執行的深入學習模型。

## <a name="next-steps"></a>後續的步驟

[機器學習服務使用者入門](getting-started-with-sql-server-r-services.md)

[機器學習 Server 入門](getting-started-with-microsoft-r-server-standalone.md)

[安裝 SQL Server database engine](../../database-engine/install-windows/install-sql-server-database-engine.md)

