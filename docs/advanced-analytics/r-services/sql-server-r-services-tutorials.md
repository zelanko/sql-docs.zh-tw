---
title: "SQL Server R 服務教學課程 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/17/2017"
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
ms.assetid: 5ccc75f6-6703-47d9-b879-9a740569b45e
caps.latest.revision: 31
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 27
---
# SQL Server R 服務教學課程
使用這些教學課程來深入了解 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 和它支援的資料科學案例，包括︰

+ 在 R 中開發模型，以及將其部署到 SQL Server
+ 運用 R 程式碼程序，將資料科學家所開發的 R 方案部署至伺服器或其他生產環境。
+ 在 R 與 SQL Server 之間移動資料
+ 如何使用遠端和本機計算內容
  

## <a name="a-namebkmkend-to-endadeveloping-an-end-to-end-advanced-analytics-solution"></a><a name="bkmk_end-to-end"></a>開發端對端進階分析方案  

[資料科學端對端逐步解說](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md) 

完整體驗資料科學程序，從資料擷取、分析一直到評分。 了解如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的資料，以及透過將模型儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來運作模型。  
您會使用 PowerShell 來將紐約市計程車資料集匯入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，並使用 R 瀏覽資料。 

您接著將建置預測模型，並將 R 模型部署到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，以便在 bath 和單一預測模式中進行評分。 

  
本教學課程適合對於 R 以及開發人員工具 (例如 PowerShell 和 SQL Server Management Studio) 有一定熟悉度的人。 您應該能夠存取 R 開發環境並熟悉 R 命令的使用。 
  
## <a name="a-namebkmkdatascienceadata-science-deep-dive"></a><a name="bkmk_dataScience"></a>資料科學深入探討  

[RevoScaleR 和 SQL Server 使用者入門](http://go.microsoft.com/fwlink/?LinkID=691640&clcid=0x809)  

對於已熟悉 R 語言的資料科學家或開發人員，以及想要了解 Microsoft R 中的 Revolution Analytics 加強 R 封裝和函數的人員，這個逐步解說是一個好的起點。 

您將了解如何使用 ScaleR 封裝中的函數、在 R 與 SQL 之間移動資料，以及切換計算內容以符合特定工作。 您將建立某些模型和繪圖，並在您的開發環境和 SQL Server 之間移動它們。  
  
本教學課程適合已經使用 R，而且想要深入了解 RevoScaleR 和 SQL Server 如何改善 R 體驗的人。

## <a name="in-database-advanced-analytics-for-the-sql-developer"></a>適用於 SQL 開發人員的資料庫內進階分析  
  
[適用於 SQL 開發人員的資料庫內進階分析 &#40;教學課程&#41;](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)

使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 來建立和部署完整進階分析方案。 此範例著重於如何整合開放原始碼 R 語言與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫引擎。 您將了解如何將 R 程式碼包裝在預存程序中、將 R 模型儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，以及對 R 模型進行參數化呼叫來進行預測。 
  
本教學課程適合 SQL 開發人員、應用程式開發人員或將支援 R 方案，且想要了解如何將 R 模型部署到 SQL Server 的 SQL DBA。  不需要 R 環境。已提供所有 R 程式碼，只要使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和熟悉的商務智慧與 SQL 開發工具，您便可以建置完整的方案。   

## <a name="use-r-services-in-an-application"></a>在應用程式中使用 R Services

[Build an intelligent app with SQL Server and R](https://www.microsoft.com/sql-server/developer-get-started/r) (使用 SQL Server 和 R 建立智慧型應用程式)

在本教學課程中，您會了解雪橇租賃業如何使用機器學習服務預測未來的租賃業務，這可以幫助商務計劃和人員滿足未來的需求。


## <a name="using-r-code-in-t-sql"></a>在 T-SQL 中使用 R 程式碼  

[在 Transact-SQL 中使用 R 程式碼 &#40;SQL Server R 服務&#41;](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md)  

這是一系列簡短的獨立範例，示範在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中使用 R 的基本語法。 

您將了解如何從 SQL 呼叫 R 執行階段、了解 R 和 SQL 之間資料類型中的主要差異、將 R 函數包裝於 SQL 程式碼中，以及執行預存程序來將 R 輸出儲存至 SQL 資料表。
  
本教學課程適用於不熟悉 R 服務，而且想要學習如何使用 T-SQL 呼叫 R 之基本概念的人。 不需要有 R 的經驗。不過，您需了解如何使用 SQL Server Management Studio，或其他任何可連接到資料庫並執行簡單 T-SQL 查詢的工具。

  
## <a name="a-namebkmkprerequisitesaprerequisites"></a><a name="bkmk_Prerequisites"></a>必要條件
  
若要執行這些任何教學課程，您必須下載並安裝 **R 服務 (資料庫內)**，如下所示︰[設定 SQL Server R 服務](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)

執行 SQL Server 安裝程式之後，別忘了下列額外步驟︰
+ 執行 *sp_configure* 來啟用 R 服務
+ 重新啟動伺服器
+ 確定呼叫 R 執行階段的服務具有必要權限
+ 確定您將用於 R 程式碼的 SQL 登入或 Windows 使用者帳戶具有必要的權限，可以連接到伺服器和資料庫

如果您遇到問題，請參閱這篇文章中的一些常見問題︰[升級與安裝 SQL Server R 服務](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md)

如果您還沒有慣用的 R 開發環境，可以安裝下列其中一項工具來開始：

+ [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-get-started)
+ [適用於 Visual Studio 的 R 工具](https://www.visualstudio.com/vs/rtvs/)

請注意，標準的 R 程式庫不足以使用這些教學課程。R 開發環境和執行 R 的 SQL Server 電腦都必須具有來自 Microsoft 的 ScaleR 套件。 如需 Microsoft R 內涵的詳細資訊，請參閱這篇文章︰[Microsoft R 產品](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started#compare-prods)。

## <a name="additional-resources"></a>其他資源

當您完成這些教學課程時，請使用下列連結以檢視更多進階案例和範例。
  
### <a name="end-to-end-solution-templates-for-key-machine-learning-tasks"></a>主要機器學習工作的端對端方案範本  

[Machine Learning Templates with SQL Server 2016 R Services](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/) (SQL Server 2016 R 服務的機器學習範本)。  

Microsoft Machine Learning 小組已提供一組可自訂範本，協助您快速開始這些機器學習工作的重要機器學習方案︰  
* 詐騙偵測  
* 自訂變換預測  
* 預測性維護  
  
提供所有 T-SQL 和 R 程式碼，以及如何使用 SQL Server 預存程序來定型和部署評分模型的指示。 

### <a name="sample-data-and-sample-scripts"></a>範例資料和範例指令碼  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的產品範例可以從 Microsoft 下載中心取得。 若只要取得 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的範例，請選取 ZIP 檔案，然後開啟 [進階分析] 資料夾。  有些指示適用於較早的版本，但是有根據班佛定律的保險詐騙偵測示範，以及對於極小資料集 (光圈資料集) 上之預測模型的簡單逐步解說，可能有助於示範。
  
[SQL Server 2016 產品範例](https://www.microsoft.com/en-us/download/details.aspx?id=49502)  
### <a name="learn-more-about-r"></a>深入了解 R  
若要深入了解 R 的一般資訊，請參閱這裡列出的其中一個絕佳資源： [R Language Resources](http://revolutionanalytics.com/r-language-resources)(R 語言資源)。  
  
如需 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中所提供 R 套件的其他資訊，請參閱  [Revolution Analytics 網站](http://go.microsoft.com/fwlink/?LinkId=691541)。  
  
這個部落格文章概述如何使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 所提供之 R 套件和函數來連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的程序，以及包括範例程式碼︰ [Using R inside SQL Server](http://blog.revolutionanalytics.com/2015/10/previewing-using-revolution-r-enterprise-inside-sql-server.html)(在 SQL Server 內使用 R)。  
  
## <a name="see-also"></a>另請參閱  
[開始使用 SQL Server R 服務](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
[SQL Server R 服務功能及工作](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)  
  
