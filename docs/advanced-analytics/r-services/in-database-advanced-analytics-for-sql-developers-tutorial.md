---
title: "適用於 SQL 開發人員的資料庫內進階分析 (教學課程) | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
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
  - "TSQL"
ms.assetid: c18cb249-2146-41b7-8821-3a20c5d7a690
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# 適用於 SQL 開發人員的資料庫內進階分析 (教學課程)
本逐步解說的目標是為 SQL 程式設計人員提供使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 建立進階分析解決方案的實際操作經驗。 在本逐步解說中，您將了解如何藉由將 R 程式碼包裝在預存程序中，以將 R 納入應用程式或 BI 解決方案。  
  
## 概觀  
建立端對端解決方案的程序通常包含取得和清除資料、資料瀏覽和特徵工程、模型定型和微調，以及最後在生產環境中部署模型。 最好使用專為 R 建置的開發環境 (例如 RStudio 或 [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)])，來執行實際 R 程式碼的開發和測試工作。 不過，建立解決方案之後，您可以在熟悉的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 環境中，使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 輕鬆地將它部署至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
因此，在本逐步解說中，我們假設您已經取得解決方案需要的所有 R 程式碼，因此您將專注於建立及部署已撰寫 R 程式碼的進階分析解決方案。  
  
-   [步驟 1︰下載範例資料](../../advanced-analytics/r-services/step-1-download-the-sample-data-in-database-advanced-analytics-tutorial.md)。    將範例資料集和範例 SQL 指令碼檔下載至本機電腦。  
  
-   [步驟 2︰使用 PowerShell 將資料匯入 SQL Server](../../advanced-analytics/r-services/step-2-import-data-to-sql-server-using-powershell.md)。  執行 PowerShell 指令碼，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體上建立資料庫和資料表，並將範例資料載入資料表。  
  
-   [步驟 3：瀏覽及視覺化資料](../../advanced-analytics/r-services/step-3-explore-and-visualize-the-data-in-database-advanced-analytics-tutorial.md)。   從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序呼叫 R 套件和函數，以執行基本資料瀏覽和視覺效果。  
  
-   [步驟 4︰使用 T-SQL 建立資料特徵](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md)。  使用自訂 SQL 函數，建立新的資料特徵。  
  
-   [步驟 5︰使用 T-SQL 定型及儲存模型](../../advanced-analytics/r-services/step-5-train-and-save-a-model-using-t-sql.md)。  使用預存程序，建立並儲存機器學習服務模型。  
  
-   [步驟 6︰操作模型](../../advanced-analytics/r-services/step-6-operationalize-the-model-in-database-advanced-analytics-tutorial.md)。  將模型儲存至資料庫之後，使用預存程序從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 呼叫要預測的模型。  
  
> [!NOTE]  
> 建議您不要使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 撰寫或測試 R 程式碼。 如果您嵌入預存程序中的 R 程式碼有任何問題，從預存程序傳回的資訊通常不足以了解錯誤的原因。   
>   
> 建議您使用 RStudio 或 [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)] 之類的工具來進行偵錯。 本教學課程中提供的 R 指令碼已使用傳統 R 工具進行部署及偵錯。  
>   
> 如果您有興趣了解如何開發可在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中執行的 R 指令碼，請參閱下列教學課程︰[資料科學端對端逐步解說](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)  
  
### 狀況  
本逐步解說使用已知的紐約市計程車資料集。 此公用資料集包含 20GB 的 CSV 壓縮檔 (~48GB 未壓縮)，詳細列出 2013 年超過 1730 萬筆個別的計程車車程，以及每趟車程已付的車資。 為了簡化本逐步解說並加速進行，我們建立了代表性資料取樣︰資料的 1% (1,703,957 個資料列和 23 個資料行)。 在本逐步解說中，您將使用此資料建立二元分類模型，以根據當日時間、距離和上車位置，來預測特定車程是否有可能獲得小費。  
  
  
### 需求  
本逐步解說適用於已熟悉基本資料庫作業的使用者，這些作業包括建立資料庫和資料表、將資料匯入資料表，以及建立 SQL 查詢等等。 其提供所有 R 程式碼，因此不需要 R 開發環境。 有經驗的 SQL 程式設計人員應該能夠在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]，或執行所提供的 PowerShell 指令碼，來完成本逐步解說。  
  
不過，開始本逐步解說之前，您必須完成下列準備工作：  
  
-   連接到已啟用 SQL Server R Services 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體 (需要 CTP 3 或更新版本)。 如需詳細資訊，請參閱安裝指示︰[Set up SQL Server R Services (In-Database)](https://msdn.microsoft.com/library/mt696069.aspx) (設定 SQL Server R Services (資料庫內))  
  
 -   您用於本逐步解說的登入必須具有權限，可以建立資料庫和其他物件、上傳資料、選取資料，以及執行預存程序。  
  
## 下一個步驟  
[步驟 1︰下載範例資料](../../advanced-analytics/r-services/step-1-download-the-sample-data-in-database-advanced-analytics-tutorial.md)  
  
## 另請參閱  
[SQL Server R Services 教學課程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
[SQL Server R 服務](../../advanced-analytics/r-services/sql-server-r-services.md)  
  
  
  
