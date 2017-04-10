---
title: "建立在 SQL Server 中使用 R 的工作流程 | Microsoft Docs"
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
ms.assetid: 34c3b1c2-97db-4cea-b287-c7f4fe4ecc1b
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# 建立在 SQL Server 中使用 R 的工作流程
  關聯式資料庫是高度最佳化的技術，提供可擴充的解決方案，交易處理、 儲存和查詢資料。 不過，傳統 R 解決方案有通常依賴從各種不同的來源，通常要進一步探索資料和模型的 CSV 格式匯入資料。 這種作法不僅沒有效率，而且也不安全。  
  
 使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 提供多項優點︰  
  
-   資料安全性。 R 的威力帶入資料庫接近的資料來源。 可避免浪費或不安全的資料移動。  
  
-   速度。 資料庫最適合以集合為基礎的操作。 此外，在資料庫中的最新創新例如記憶體中資料表和單欄式資料存放區進一步改善資料科學藉由快速閃電彙總。  
  
-   整合。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是許多其他的資料管理工作和使用企業的應用程式的作業的中心點。 已使用資料庫中的資料可確保資料的一致且最新狀態。 而不是處理 R 中的資料，您可以依賴企業資料管線，包括 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和 Azure Data Factory。 報告結果或分析很容易透過 Power BI 或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
 資料科學家和開發人員可以使用正確的 SQL 和 R 組合，來進行不同的資料處理和分析工作，因此更有效率。 本節說明如何將 R 與針對資料轉換、分析和報告的其他企業解決方案進行整合。  
  
##  <a name="bkmk_ssis"></a> 建立跨越 R 和資料庫的高效率工作流程  
 資料科學工作流程的互動性很高，並涉及許多資料的轉換，包括縮放、彙總、機率計算，以及重新命名與合併屬性。 資料科學家習慣執行大部分的工作在 R、 Python 或另一種語言。不過，在企業資料上執行這些工作流程需要與 ETL 工具和程序的緊密整合。  
  
 因為 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 可讓您使用執行複雜的作業，透過 TRANSACT-SQL 和預存程序，您可以將 R 專屬的工作整合現有的 ETL 程序，而無需最少的重新開發工作。 而非執行一連串的工作記憶體 ntensive R 中，資料準備可最佳化使用最有效率的工具，包括 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和 [!INCLUDE[tsql](../../includes/tsql-md.md)]。  
  
 例如，您可以結合使用 R [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 這類案例中︰  
  
-   使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 工作，以建立 SQL 資料庫中的必要物件  
  
-   使用條件式分支切換 R 工作的計算內容  
  
-   執行會產生自身資料的 R 工作  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來呼叫 R 指令碼儲存在變數中的文字  
  
### 範例和資源  
 [將您使用 SQL Server 2016 SSIS 和 R 服務的機器學習專案](https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/)  
  
 在此部落格文章，您將學習如何︰  
  
-   在 「 執行 SQL 」 工作中使用 R 來產生資料並儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   使用定型的 R 模型，並將它儲存在資料庫中的預存程序  
  
-   執行指令碼工作和 「 執行 SQL 」 工作所使用的模型評分  
  
##  <a name="bkmk_ssrs"></a> 建立跨越 R 和企業報告工具的視覺效果  
 雖然 R 可以建立圖表和有趣的視覺效果，但它與外部資料來源的整合度並不高，這表示您必須個別產生每個圖表或圖形。 共用也可能很困難。  
  
 使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], ，您可以執行複雜的作業中透過 R [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序，可以很容易地使用各種不同的企業報表工具，包括 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 Power BI。  
  
-   以視覺化方式檢視圖形從 R 指令碼傳回的物件   
    使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   使用 Power BI 中的表格  
  
## 範例和資源  
 [Microsoft Reporting Services (SSRS) 的 R 圖形裝置](https://rgraphicsdevice.codeplex.com/)  
  
 下列 CodePlex 專案提供的程式碼，可協助您建立自訂報表項目轉譯為映像，可用於 R 的圖形輸出 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表。  藉由使用自訂報表項目，您可以︰  
  
-   將圖表和使用 R 圖形裝置，若要建立的繪圖發佈 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 儀表板  
  
-   傳遞 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] R 繪圖的參數  
  
> [!NOTE]  
>  請注意在 Reporting Services 伺服器上，以及 Visual Studio 中，必須安裝 Reporting services 支援 R 圖形裝置的程式碼。 手動編譯和組態也會是必要項目。  
  
  