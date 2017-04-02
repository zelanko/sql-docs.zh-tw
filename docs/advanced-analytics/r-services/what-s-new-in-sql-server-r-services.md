---
title: "SQL Server R 服務的新功能 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6aff043a-8b37-4f3f-9827-10a671e1ad1c
caps.latest.revision: 36
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 35
---
# SQL Server R 服務的新功能
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 和 SQL Server vNext 的功能，支援企業級資料科學。  R 是對進階分析人員而言最受歡迎的程式設計語言，其會提供一組非常豐富的封裝以及一個活躍且快速成長的開發人員社群。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 可協助您在企業中使用非常熱門的開放原始碼 R 語言。 
  
 > [!TIP] 已經有 SQL Server 2016 R Services 嗎？
 > 您現在可以在 2016 執行個體上安裝最新版本的 Microsoft R Server，以發揮 R 元件更常更新的優勢。 如需詳細資訊，請參閱 [Microsoft R Server 9.0.1 (英文)](https://msdn.microsoft.com/microsoft-r/rserver-whats-new)。  

## <a name="whats-new-in-sql-server-vnext"></a>SQL Server vNext 的新功能
  
+ 推出 **MicrosoftML** 套件

   MicrosoftML 是 Microsoft R Server 和 Microsoft 資料科學小組提供的新 R 機器學習服務套件。 在 R 模型中只需要幾行程式碼，MicrosoftML 即可在處理大型主體文字資料和高維度類別資料時提高速度、效能和等級。 此外，Microsoft R Server 客戶可以存取五個隨附於 Azure Machine Learning 的快速、高精確觀摩者。 
   
   如需詳細資訊，請參閱[在 SQL Server R Services 中使用 MicrosoftML 套件](../../advanced-analytics/r-services/using-the-microsoftml-package-with-sql-server-r-services.md)。
   
+ 方便資料科學家管理套件

  您不再需要依賴資料庫管理員為您在 SQL Server 上安裝需要的 R 套件。 **RevoScaleR** 的新套件安裝和解除安裝函數讓您輕鬆從用戶端電腦安裝與更新 R Services 套件。 
  
  資料庫管理員的新角色包含在 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]，管理執行個體層級和資料庫層級與套件相關聯的權限。 
  
  如需詳細資訊，請參閱 [SQL Server R Services 的 R 套件管理](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)。 
     
+ **RevoScaleR** 的新函數處理讀取和寫入 R 模型物件

  RevoScaleR 現在包含新的序列化函數和更精簡的模型儲存格式，以便快速載入及讀取模型。 
  
  如需詳細資訊，請參閱[從 SQL Server 使用 ODBC 儲存和載入 R 物件](../../advanced-analytics/r-services/save-and-load-r-objects-from-sql-server-using-odbc.md)。 

+ 便利 SQL 整合的 **sqlrutils** 套件

  此 R 套件可協助您產生 R 程式碼的 SQL 預存程序呼叫。 然後產生的 SQL 預存程序可以用在 SQL Server R Services。 提供範例協助您將 R 程式碼合併到 SQL 預存程序中可參數化的函數中。
  
  如需詳細資訊，請參閱[使用 sqlrutils 產生 R 程式碼的預存程序](../../advanced-analytics/r-services/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)。 
  

+ 便利 SSAS 連線的 **olapR** 套件

   這個新套件為 R 和 SQL Server Analysis Services 提供連線的新維度，讓使用 R 分析 OLAP 資料更容易。您可以執行現有的 MDX 查詢以及取回 R 資料框架，或在 R 程式碼中定義 Cube 座標軸與交叉分析篩選器來建置簡單的 MDX 陳述式。 
   
   如需詳細資訊，請參閱[在 R 中使用 OLAP Cube 的資料](../../advanced-analytics/r-services/using-data-from-olap-cubes-in-r.md)。
   

  
## <a name="features-in-sql-server-2016-r-services-and-sql-server-vnext"></a>SQL Server 2016 R Services 和 SQL Server vNext 的功能  
  
- 使用 R 進行快速且可並行機器學習服務的 **RevoScaleR** 套件。

-   同時支援 SQL 登入和整合式 Windows 驗證。  
    
-   包括最佳化 SQL 附屬程序的顯著效能改進，連接 R 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，支援可使用大量資料的資料分頁，以及可快速處理數十億資料列的串流。 
  
-   使用 SQL Server 資源集區來管理 R 程序所使用的記憶體。 如需詳細資訊，請參閱 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。  
  

### <a name="tools-and-setup"></a>工具和安裝

-   輕鬆安裝所有元件。 SQL Server 安裝精靈可以安裝 **SQL Server R Services (資料庫內)** 或 **Microsoft R Server (獨立式)**。   當您執行安裝精靈時，如果要安裝 SQL Server 執行個體請選擇 R Services，如果要設定資料科學工作站請選擇 R Server (獨立式)。   如需安裝選項的詳細資訊，請參閱[安裝 SQL Server R Services &#40;資料庫內&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md) 或[建立獨立的 R Server](../../advanced-analytics/r-services/create-a-standalone-r-server.md)。  

-   如果 SQL Server 中不需要使用資料，請考慮 [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)]，它可在各種平台上執行，並為熱門的開放原始碼 R 語言提供企業規模和效能。 [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)]. 如需詳細資訊，請參閱 MSDN 上的 [R Server &#40;獨立式&#41;](../../advanced-analytics/r-services/r-server-standalone.md) 或 [R Server 簡介](https://msdn.microsoft.com/microsoft-r/rserver)。

- 若要升級 SQL Server 2016 執行個體以使用 Microsoft R Server 9.0.1，請使用 [SqlBindR.exe 公用程式](https://msdn.microsoft.com/library/mt791781.aspx)。  

- [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-install) 是免費的 R 環境，包括建置在 R Services 或 R Server 上執行的 R 解決方案所需要的所有工具和程式庫。  

-   R Tools for Visual Studio 是有豐富 R 支援的免費 Visual Studio 外掛程式，包括標準的 R 互動式和變數視窗、R 函數的 Intellisense、偵錯和 R Markdown，並可匯出至 Word 和 HTML。  如需詳細資訊，請參閱 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/) (適用於 Visual Studio 的 R 工具)。  

## <a name="learn-more"></a>深入了解
  
-  相關資源可供想要了解 SQL Server 整合的資料科學家，以及想要使用 T-SQL 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 熟悉環境來建立 R 解決方案的 SQL 開發人員。 
   + [SQL Server R Services 教學課程](https://msdn.microsoft.com/library/mt591993.aspx)
   + [Free ebook: Data Science with SQL Server 2016](https://mva.microsoft.com/ebooks/) (免費電子書︰使用 SQL Server 2016 的資料科學)
 
+ 如果您需要現成的解決方案，Microsoft 資料科學小組所提供的[機器學習服務範本 (英文)](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/) 會示範常見分析工作的實務解決方案，包括預測性維護以及避免客戶流失。
 

  
## <a name="see-also"></a>另請參閱  
[SQL Server vNext 的新功能](../../sql-server/what-s-new-in-sql-server-vnext.md)
  