---
title: "R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "12/20/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 341e80f5-3b59-4122-bbaa-969d7904297d
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 20
---
# R Services
  Microsoft R Services 提供兩種伺服器平台，以整合受歡迎的開放原始碼 R 語言和商務應用程式：**SQL Server R Services (資料庫內)** 用來與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 **Microsoft R Server** 整合。  
  
-   **R Services (資料庫內)**  
  
     [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的目的是根據 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 平台及相關服務，啟用快速開發、部署以及實施 R 解決方案。  
  
     藉由在同一部電腦上將 R 當成資料庫執行，[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 可在資料中帶入計算。 它包含了在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 程序外執行的資料庫服務，並與 R 執行階段安全地通訊。 您可以訓練 R 模型、產生 R 繪圖、執行評分，以及在 R 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之間輕鬆移動資料。 測試和開發解決方案的資料科學家，可以從遠端的開發電腦與伺服器通訊以在伺服器上執行 R 程式碼，並藉由在預存程序中內嵌對 R 的呼叫，來將完成的解決方案部署到 SQL Server。  
  
     這個下載項目包含開放原始碼 R 語言的發佈版本以及一組高效能且可調整的 R 套件，ScaleR。 其中包含的提供者為所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術帶來更簡單、更快速的連線能力。  
  
     如需相關資訊，請參閱 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)。 如需範例案例，請參閱 [SQL Server R Services 教學課程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)。  
  
-   **Microsoft R Server**  
  
     此獨立伺服器系統支援多種平台上的分散式、可調整的 R 解決方案，且使用多種企業資料來源，包括 Linux、Hadoop 和 Teradata。  
  
     如需詳細資訊，請參閱 [Microsoft R Server (MSDN)](https://msdn.microsoft.com/microsoft-r/index)。  
  
## <a name="related-technologies"></a>相關技術  
 Microsoft 為開放原始碼 R 語言生態系統提供廣泛的支援，包括工具、提供者、增強的 R 封裝，以及整合式開發環境。  
  
-   **適用於 Visual Studio 的 R 工具**  
  
     Visual Studio 提供完整的 R 語言開發環境。 該外掛程式包括編輯器、互動式視窗、繪圖功能、偵錯工具等等。 您可以從 R 使用 .NET 語言，或從 .NET 透過開放原始碼程式庫 (如 R.NET 和 rClr) 叫用 R。  
  
     如需詳細資訊，請參閱 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/) (適用於 Visual Studio 的 R 工具)。  
  
-   **Azure Machine Learning 中的 R**  
  
     在 Azure Machine Learning Studio 中建立自己的工作區，您可以在其中存取超過 400 種已預先載入的 R 封裝。 建立並訓練模型來部署為 Web 服務，或是撰寫自訂指令碼來轉換資料。 建立您自己的 R 封裝並上傳到 Azure 以做為自訂的模組來執行，以及將解決方案發佈至 [Machine Learning Marketplace](http://datamarket.azure.com/browse/data?category=machine-learning)。  
  
     如需詳細資訊，請參閱[透過 R 擴展您的經驗](https://docs.microsoft.com/azure/machine-learning/machine-learning-extend-your-experiment-with-r)和[在 Azure Machine Learning 中撰寫自訂 R 模組](https://docs.microsoft.com/azure/machine-learning/machine-learning-custom-r-modules)。  
  
-   **資料科學虛擬機器**  
  
     您可以在 Microsoft Azure 部署預先安裝或預先設定版本的 [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)]，以便更輕鬆開始使用資料探索，並且立即在雲端建立模型，而不需在內部部署設定已完整設定的系統。  
  
     Azure Marketplace 包含數部支援資料科學的虛擬機器︰
     + **Microsoft 資料科學虛擬機器**設定使用 Microsoft R Server，以及 Python (Anaconda 發佈版本)、Jupyter 筆記本伺服器、Visual Studio Community 版、Power BI Desktop、Azure SDK 以及 SQL Server Express 版。 
     + **Microsoft R Server 2016 for Linux** 包含最新版的 R Server (9.0.1 版)。 分別提供 CentOS 7.2 版及 Ubuntu 16.04 版的 VM。 
     + **R Server 專用 SQL Server 2016 Enterprise** 虛擬機器包含支援新的新式軟體開發週期授權模型的 R Server 9.0.1 獨立安裝程式。
 

## <a name="see-also"></a>另請參閱  
[開始使用 SQL Server R 服務](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md) 

[開始使用 Microsoft R Server](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  

 [安裝 SQL Server Database Engine](../../database-engine/install-windows/install-sql-server-database-engine.md)  
  
  