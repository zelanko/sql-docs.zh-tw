---
title: "資料科學案例和解決方案範本 | Microsoft Docs"
ms.custom: ""
ms.date: "04/18/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 49e54fa9-9b28-44ba-b256-06dad4e8dece
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 17
---
# 資料科學案例和解決方案範本
範本是範例解決方案，其示範最佳做法，並提供可協助您快速實作解決方案的建置組塊。 每個範本的設計目的都是為了解決特定問題，並包含範例資料、R 程式碼 (Microsoft R Server) 和 SQL 預存程序。 每個範本所包含的工作，從資料準備和特徵工程，到模型定型和計分，應有盡有。 程式碼可以在 R IDE 中執行並在 SQL Server 中完成計算，或透過 SQL 用戶端工具執行，例如 SQL Server Management Studio。  
  
您可以使用這些範本來了解 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的運作方式，並透過自訂範本來建立及部署您自己的解決方案，以符合您自己的案例。  
  
如需下載和安裝指示，請參閱本主題結尾的[如何使用範本](#bkmk_HowTo)。  
  
## 詐騙偵測  
[線上詐騙偵測範本 (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/FraudDetection/Introduction.md)  
  
線上商務的一項重要工作是偵測詐騙交易，並識別經由竊取的付款方式或認證所做的交易，以減少賠償要求損失。 發現詐騙交易時，企業通常會盡快採取措施來封鎖特定帳戶，以避免進一歩損失。 在此案例中，您將了解如何使用線上購物交易資料來識別可能的詐騙。 您可以輕易地將此方法應用在其他網域中的詐騙偵測。  
  
在此範本中，您將了解如何使用線上購物交易資料來識別可能的詐騙。 詐騙偵測會當作二元分類問題來解決。 此範本中所使用的方法可輕易地應用在其他網域中的詐騙偵測。    
  
## 客戶流失  
[客戶流失偵測範本 (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/Introduction.md)  
  
分析及預測客戶流失對任何產業都很重要，不論是銀行業、電信業和零售業等等，都必須管理及防止客戶流失到競爭對手。 客戶流失分析的目標是為了識別哪些客戶可能流失，然後採取適當動作，以留下這類客戶並保持業務往來。  
  
此範本可協助您開始進行客戶流失偵測，其做法是將客戶流失問題以**二元分類**問題來表示。 它使用兩個來源 (客戶人口統計和客戶交易) 中的範例資料，將客戶分類為可能流失或不可能流失。   
  
## 預測性維護  
[預測性維護範本 (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/Introduction.md)  
  
「資料驅動」預測性維護的目標是藉由擷取過去的故障資訊，並使用該資訊來預測裝置何時或何處可能會故障，來提升維護工作的效率。 預測裝置過時的能力對於依賴分散式資料或感應器的應用程式特別重要，物聯網 (IoT) 即為一例。  
  
此範本主要在回答「運行中的電腦何時故障」的問題。 輸入資料代表飛機引擎的模擬感應器度量。 此資料是透過監視引擎的目前作業狀況來取得 (例如目前的工作週期、設定、感應器度量等等)，可用來建立三種預測模型類型：  
  
-   **迴歸模型**：預測引擎故障前的持續時間。 此範例模型預測「剩餘使用年限」(Remaining Useful Life，RUL) 度量，也稱為「故障時間」(Time to Failure，TTF)。  
  
-   **分類模型**：預測引擎是否可能會故障。  
  
    **二元分類模型**：預測引擎是否會在特定時間範圍內 (天數) 故障。  
  
    **多類別分類模型**：預測特定引擎是否會故障；如果會故障，則提供可能的故障時間範圍。 例如，在指定日期下，您可以預測任何裝置可能在該指定日期故障，還是在該指定日期過一段時間後故障。  
      
      
## 能源需求預測  
[能源需求預測範本 (SQL Server R Services)](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast_Template_with_SQL-Server-R-Services-1)  
  
此範本示範如何使用 SQL Server R Services 來預測電力需求。 此解決方案包含需求模擬器、定型模型需要的所有 R 和 T-SQL 程式碼，以及您可以用來產生及報告預測的預存程序。   
  
## <a name="bkmk_HowTo"></a>如何使用範本  
若要下載每個範本中所包含的檔案，您可以使用 GitHub 命令，或開啟連結，然後按一下 [Download Zip (下載 Zip)] 將所有檔案儲存至您的電腦。  下載後的解決方案通常會包含下列資料夾：  
  
-   **Data**︰包含每個應用程式的範例資料。  
  
-   **R**︰包含解決方案需要的所有 R 開發程式碼。 解決方案需要由 Microsoft R Server 提供，但可在任何 R IDE 中開啟及編輯的程式庫。 R 程式碼已經過最佳化，藉由將計算內容設定為 SQL Server 執行個體，以便在「資料庫內」執行計算。  
  
-   **SQLR**︰包含多個 .sql 檔案，您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 等 SQL 環境中執行這些檔案來建立預存程序，以便執行資料處理、特徵工程和模型部署等相關工作。  
  
    此資料夾也包含 PowerShell 指令碼，可加以執行來叫用所有指令碼，並建立端對端環境。  
  
    請務必編輯此指令碼，以符合您的環境。  
  
  
## 另請參閱  
[SQL Server R Services 教學課程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
[宣告 Azure ML 中的範本](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)  
[新的預測性維護範本](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)  
  
  
  
