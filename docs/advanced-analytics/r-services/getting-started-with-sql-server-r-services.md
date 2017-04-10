---
title: "SQL Server R 服務使用者入門 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "12/07/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: 5b28a663-effe-41f6-9bda-eda95f0c6943
caps.latest.revision: 34
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 32
---
# SQL Server R 服務使用者入門
 建立進階分析解決方案的一般工作流程，是從資料瀏覽和預測模型開始，而資料科學家則是開發證明對手邊工作有效的 R 指令碼和模型。 指令碼和模型就緒後，即可部署至生產環境，與現有或新的應用程式相整合。   
  
SQL Server R Services 旨在幫助您完成這些資料科學工作。 您可以繼續使用您最愛的 R 或 SQL 工具，不需要額外硬體的數百萬筆記錄的量表分析、大幅提升效能，以及避免不必要的資料移動。 現在您可以將 R 程式碼放到生產環境，而不必用另一種語言重新撰寫。 這樣在使用 SQL 實作困難的統計計算中使用 R，也更為容易。 與此同時，您可以使用記憶體內部資料庫引擎和資料行存放區索引等功能，運用強大的 SQL Server 達到最高效能。  
  
下列章節會提供一些完整的一般分析工作流程，以及如何使用 SQL Server R Services 進行流程。  

> [!TIP] 請參閱本教學課程以快速開始。 您會了解滑雪板租賃業如何使用機器學習服務預測未來的租賃業務，以及如何進行人力調配以因應需求。
> 
> [Build an intelligent app with SQL Server and R](https://www.microsoft.com/sql-server/developer-get-started/r) (使用 SQL Server 和 R 建立智慧型應用程式)


  
-   **開發**  
  
     資料科學家通常會使用 R 來探索資料，並使用他們選擇的 R IDE 從其工作站建立預測模型。 資料科學家會反覆測試與微調，直到達成良好的預測模型為止。 
     
     [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 用戶端元件為資料科學家提供了所有進行實驗與開發所需的工具。 這些工具包括 R 執行階段 (大幅提升標準 R 作業效能的 Intel 核心數學程式庫)，以及一組支援在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中執行 R 程式碼的增強型 R 套件。  
  
     資料科學家可以連線至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，一如往常將資料帶入用戶端進行本機分析。 但更好的解決方案是使用 **ScaleR** API，將計算推送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦，避免高成本且不安全的資料移動。  
  
     若要開發 R 解決方案，資料科學家可以使用任何支援 R 的 Windows IDE，包括 [R Tools for Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx) 或 RStudio。  
 
    ![rsql_keyscenario2](../../advanced-analytics/r-services/media/rsql-keyscenario2.PNG) 
 
     如需詳細資訊，請參閱 [Data Exploration and Predictive Modeling with R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md)。  

  
-   **最佳化**  
  
     利用 R 分析大型資料集時，資料科學家通常會遇到效能與調整大小的問題，這是因為通用執行階段實作是單一執行緒，而且可能只可容納能放入本機電腦可用記憶體的資料集。 若要取得更佳效能以及處理更多資料，資料科學家可以使用隨附於 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的 **ScaleR** API。 **RevoScaleR** 套件包含某些最熱門的 R 函數實作，這些函數經過重新設計可提供平行處理與延展的功能。 此套件包含能進一步提升效能與延展性的函數，方法是將計算推送至通常記憶體較大且運算能力更佳的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦。  
  
     如需詳細資訊，請參閱 [Data Exploration and Predictive Modeling with R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md)。  
  
-   **部署**  
  
     在 R 指令碼或模型可供生產環境使用之後，資料庫開發人員即可在預存程序中內嵌程式碼或模型，並從應用程式叫用儲存的程式碼。 從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 儲存及執行 R 程式碼有許多優點︰您可以使用方便的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 介面和所有發生在資料庫中的計算，避免不必要的資料移動。 您可以在生產環境中使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] ，從預測模型產生分數，或傳回 R 所產生的繪圖，並將其呈現在像是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]這類應用程式中。  
  
     若要進一步最佳化內嵌在系統預存程序中的 R 程式碼，建議您使用 [ScaleR](https://msdn.microsoft.com/microsoft-r/rserver/rserver-scaler-getting-started) 套件 API，其可在較大型的資料集上操作。 這些封裝支援在多執行緒、多核心、多處理序計算的資料庫內執行。  
  
     當您需要將 R 程式碼部署到生產環境時， [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 能提供最佳的 R 和 SQL 環境。 您可以使用 R 進行在 SQL 難以運作的統計計算，使用像是記憶體內資料庫引擎與資料行存放區索引之類的功能，運用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的能力達到最佳效能。  
  
    ![rsql_keyscenario1](../../advanced-analytics/r-services/media/rsql-keyscenario1.PNG)  
  
     如需詳細資訊，請參閱[運用您的 R 程式碼](../../advanced-analytics/r-services/operationalizing-your-r-code.md)。  
 
 > [!TIP]在本書中深入了解如何整合 SQL Server 與資料科學，您可從 Microsoft Virtual Academy 免費下載使用︰[Data Science with Microsoft SQL Server 2016](https://mva.microsoft.com/ebooks/) (資料科學與 Microsoft SQL Server 2016)。

-   **管理與監視**  
  
     [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 使用全新的擴充性架構，保持您資料庫引擎的安全，並隔離 R 工作階段。 您也可以控制可以執行 R 指令碼的使用者，同時可以指定 R 程式碼可以存取的資料庫。 您可以控制配置給 R 執行階段的資源數量，以避止從大量計算危及整體伺服器效能。  
  
     在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中執行 R 工作時，也可以控制和稽核分析師所使用的資料，或是排程工作以及撰寫包含 R 指令碼的工作流程，就和其他預存程序一樣。  
  
     如需相關資訊，請參閱 [Managing and Monitoring R Solutions](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
  
  
-   **整合**  
  
     您不再需要花費 IT 預算才可取得企業級工具來處理某些外部 R 執行階段環境。 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的熟悉環境，以使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]來開發整合式工作流程和產生報表的解決方案。  
  
     如需詳細資訊，請參閱[建立在 SQL Server 中使用 R 的工作流程](../../advanced-analytics/r-services/creating-workflows-that-use-r-in-sql-server.md)。  
  
  
## <a name="how-do-i-get-it"></a>如何取得？  
   
  
+   **安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或更新版本並啟用 R Services (資料庫內)**)  
  
    [設定 SQL Server R Services &#40;資料庫內&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。  
  
  
-   **設定用戶端工作站**  
  
     [設定資料科學用戶端](../../advanced-analytics/r-services/set-up-a-data-science-client.md)  
   
> [!TIP]   
>   
> 需要為 R 作業建立伺服器，但不需要 SQL Server？ 請嘗試 [Microsoft R Server](https://msdn.microsoft.com/library/mt674874.aspx)。  
  
## <a name="how-to-run-r-code-using-sql-server-r-services"></a>如何使用 SQL Server R 服務執行 R 程式碼  
 完成安裝之後，您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上執行 R 程式碼，方法是在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序上內嵌 R，或者撰寫臨機操作 R 指令碼來與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料搭配使用。  
  
-   了解如何從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式呼叫 R，並在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中傳回結果。  
  
     [在 Transact-SQL 中使用 R 程式碼](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md)  
  
-   了解建立進階分析解決方案，並使用 SQL Server R Services 來部署它的完整流程。  
  
     [資料科學端對端逐步解說](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)  
  
-   了解如何使用 RevoScaleR 套件處理可延展及高效能的分析，以及如何將 R 計算推送至 SQL Server 電腦。  
  
     [資料科學深入探討︰使用 RevoScaleR 套件](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
-   在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序中內嵌工作 R 指令碼，以便讓您可呼叫模型來進行預測、重新定型模型，或從應用程式取得預測。  
  
     [適用於 SQL 開發人員的資料庫內進階分析](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
  
-   在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 堆疊中使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和相關的商業智慧工具，來自動化機器學習程序。 資料準備和報告可使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]來自動化；使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 或 Power View 來顯示 R 繪圖以及其他報表。  
  
+ 更多範例，包括解決方案範本和 R 程式碼範例。  
   [SQL Server R Services 教學課程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [開始使用 Microsoft R Server &#40;獨立&#41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  