---
title: "SQL Server R 服務功能及工作 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 52ad3f10-6d24-477a-aeb6-110456b2ed1c
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 13
---
# SQL Server R 服務功能及工作
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 結合資料儲存和管理、 工作流程開發，並報告和視覺效果的企業級工具的威力與彈性的開放原始碼 R 語言。 它支援四種不同的資料專業人員和案例的需求。  
  
## 資料科學家︰使用 R 和 SQL Server 來分析、建立模型及計分  
 資料科學家可以存取各種工具來進行資料分析和機器學習，範圍可從熟悉的 Excel 和開放原始碼平台，到昂貴且需要深入技術知識的統計套件。 其中， [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 會提供獨特的優點，因為它可讓資料科學家將計算推送到資料庫，以避免資料移動並符合企業安全性原則。 此外，資料科學家所建立的 R 程式碼可輕鬆部署到生產環境，並透過熟悉的企業工具和解決方案來呼叫︰以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫、BI 報表工具和儀表板為基礎的應用程式。 使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], ，資料科學家可以部署和更新分析解決方案，同時滿足企業資料管理的標準需求，包括安全性、簡化部署、管理和監視，以及存取稽核。  
  
-   **熟悉的使用者介面。**  使用您選擇的 R 開發環境來開發和測試解決方案。  
  
-   **資料庫內部處理程序。**  執行 R 程式碼，在裝載 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的電腦上執行計算。 這不需要移動資料。  
  
-   **效能和延展性。**  包含可調整的 R 封裝與 Api，因此不會再受到單一執行緒、 記憶體繫結架構的。您可以處理大型資料集和多執行緒、 多核心、 多處理序的計算。  
    
-   **程式碼可攜性。**  對執行相同的 R 程式碼 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料可以輕鬆地重複使用針對其他資料來源，例如 Hadoop。  
  
 如需相關的工作與概念的詳細資訊，請參閱 [資料探索和預測模型以 R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md)。  
  
## 應用程式和資料庫開發人員︰部署 R 解決方案  
 資料庫開發人員負責整合多項技術，以及將結果合併在一起，讓整個企業都能共用這些結果。 資料庫開發人員可與應用程式開發人員、SQL 開發人員及資料科學家合作，來設計解決方案、建議資料管理方法，以及架構和部署解決方案。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 可以為和資料科學家合作的開發人員提供許多優點︰  
  
-   **使用 R 指令碼進行互動 [!INCLUDE[tsql](../../includes/tsql-md.md)]。**  您的報表開發人員、分析人員和資料庫開發人員可以藉由呼叫系統預存程序來叫用 R 指令碼。 如果您的方案使用複雜的彙總，或是牽涉到大型資料集，您可以執行在資料庫，或使用 R 混合運算和 [!INCLUDE[tsql](../../includes/tsql-md.md)], ，取決於提供最佳效能。 當您需要重複執行大量資料的工作時 (例如，針對生產環境的資料產生預測分數)，隨時都能與  [!INCLUDE[tsql](../../includes/tsql-md.md)] 輕鬆整合。  
  
     與整合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也表示您可以從任何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]的應用程式執行 R 指令碼。 比方說，您可以輕鬆地呼叫預存程序 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 來叫用 R 指令碼，並在報表中產生預測以及繪圖的報表。  
  
-   **效能和延展性。**  已知的開放原始碼 R 語言有限制，雖然 RevoScaleR 封裝 Api 所提供 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 可以處理大型資料集，並受益於多執行緒、 多核心、 多處理序的資料庫中計算。  
  
-   **標準的開發和管理工具。**  不需要任何其他的系統管理或部署工具；所有的 R 工作都可藉由叫用預存程序來呼叫。 此外，您針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料執行的相同 R 程式碼也可針對其他資料來源 (例如 Hadoop) 使用。  
  
 如需相關的工作與概念的詳細資訊，請參閱 [另尋高就您的 R 程式碼](../../advanced-analytics/r-services/operationalizing-your-r-code.md)。  
  
## 資料庫管理員︰管理進階分析解決方案  
 資料庫管理員必須將競爭專案和優先順序整合至單一窗口︰資料庫伺服器。 他們不只應將資料存取權提供給資料科學家，還必須提供給各種報表開發人員、商務分析人員和商務資料取用者，同時維護操作和報告資料存放區的健康情況。 在企業中，DBA 是建置與部署適用於資料科學之有效基礎結構的一個重要部分。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 可以為支援資料科學角色的資料庫系統管理員提供許多優點︰  
  
-   **安全性。**  架構的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 會將資料庫保留在安全和隔離的資料庫執行個體的作業 R 工作階段執行。  
  
     您可以指定誰有權執行 R 指令碼，並確保 R 作業中使用的資料使用相同的安全性角色中所定義的管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   **可靠性。**  R 工作階段會在不同處理序中執行，以確保即使 R 工作階段發生問題，您的伺服器還是會如往常般繼續執行。  
  
-   **資源管理。**  您可以控制配置給 R 執行階段的資源數量，以避止從大量計算危及整體伺服器效能。  
  
 如需相關工作與概念的詳細資訊，請參閱 [Managing and Monitoring R Solutions](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
  
## 架構設計人員和 ETL 設計人員︰建立跨越 R 和 SQL Server 的整合式工作流程  
 資料工程師會設計和建置 ETL 解決方案。 架構設計人員設計提供競爭及補充商務需求的資料平台。 因為 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 密切整合，例如商務智慧和資料倉儲堆疊、 企業雲端及行動工具和 Hadoop 其他 Microsoft 工具，它提供的優點陣列資料工程師或系統架構設計人員想要升級進階的分析。  
  
-   **一組廣泛且熟悉的開發工具。**  開發 R 解決方案時，請使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和系統預存程序來填入資料集、執行 R 工作或取得預測。 資料科學工具中不再設計平行的工作流程；請在熟悉的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]環境中建置您的資料管線。  
  
     需要使用雲端資料？ Azure Data Factory 和 Azure SQL Database 的支援可讓您更輕鬆地轉換和管理資料，而只是工作流程中的使用雲端資料來源要在內部部署的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料。  
  
-   **撰寫和管理工作流程。**  排程工作和撰寫工作流程包含 R 指令碼，使用系統預存程序。  
  
 如需相關的工作與概念的詳細資訊，請參閱 [建立工作流程 SQL Server 中，使用 R](../../advanced-analytics/r-services/creating-workflows-that-use-r-in-sql-server.md)。  
  
## 另請參閱  
 [SQL Server R 服務使用者入門](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  