---
title: "資料科學逐步解說的必要條件 (SQL Server R 服務) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 0b0582b8-8843-4787-94a8-2e28bdc04fb2
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# 資料科學逐步解說的必要條件 (SQL Server R 服務)
要進行逐步解說之前，建議您先選擇可連線到相同網路上 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦的 R 工作站 您也可以在同時具有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 R 開發環境的電腦上執行逐步解說。 
  
  
## <a name="install-sql-server-2016-r-services-in-database"></a>安裝 SQL Server 2016 R 服務 (資料庫內)  
您必須能夠存取已安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 執行個體。 如需如何設定 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]的詳細資訊，請參閱 [Set up  SQL Server R Services (In-Database](https://msdn.microsoft.com/library/mt696069.aspx)(設定 SQL Server R 服務 (資料庫內))。  
  
  
> [!IMPORTANT]  
> 請務必使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或更新版本。 舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援 R 整合。不過，您可以使用 SQL 資料庫做為 ODBC 資料來源。  
  
## <a name="install-an-r-development-environment"></a>安裝 R 開發環境  
若要在您的電腦上完成此逐步解說，您必須具備 R 開發環境，或任何可以執行 R 命令的其他命令列工具。    
  
- **適用於 Visual Studio 的 R 工具** 是免費的外掛程式，可提供 Intellisense、偵錯及 Microsoft R Server 和 SQL Server R 服務支援等功能。 若要下載，請參閱 [適用於 Visual Studio 的 R 工具](https://www.visualstudio.com/features/rtvs-vs.aspx)。  
    
- **Microsoft R Client** 是輕量級開發工具，可支援在 R 中使用 ScaleR 封裝進行開發。 若要取得它，請參閱[開始使用 Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-get-started)。
  
- **RStudio** 是其中一個比較常見的 R 開發環境。 如需詳細資訊，請參閱 [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/)。  
  
    但是，使用一般安裝的 RStudio 或其他環境時，並無法完成此教學課程；您也必須安裝 R 封裝和適用於 Microsoft R Open 的連線程式庫。 如需詳細資訊，請參閱 [Set Up a Data Science Client](https://msdn.microsoft.com/library/mt696067.aspx)(設定資料科學用戶端)。  

- 當您安裝 [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)] 時，系統預設會安裝 R 工具 (R.exe、RTerm.exe、RScripts.exe)。 如果您不想安裝 IDE，即可使用這些工具。  
  
  
## <a name="get-permissions-to-connect-to-sql-server"></a>取得連線至 SQL Server 的權限  
在本逐步解說中，您將連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，以執行指令碼並上傳資料。 若要這樣做，您必須具備資料庫伺服器的有效登入。  您可以使用 SQL 登入或整合式 Windows 驗證。 請資料庫管理員在伺服器上為您建立帳戶，並提供下列權限，讓您可以在資料庫上使用 R：  
  
-   建立資料庫、資料表、函數和預存程序    
-   將資料插入資料表  
  
  
## <a name="start-the-walkthrough"></a>開始逐步解說  
[第 1 課︰準備資料 &#40;資料科學端對端逐步解說&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
