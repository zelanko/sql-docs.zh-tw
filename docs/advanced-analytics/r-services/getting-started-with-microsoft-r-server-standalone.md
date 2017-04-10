---
title: "開始使用 Microsoft R Server (獨立) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "r-server"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 52347d0d-ce60-4bb8-98d2-6163e87716b0
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 16
---
# 開始使用 Microsoft R Server (獨立)
  Microsoft R Server (獨立) 可協助您將熱門的開放原始碼 R 語言帶入企業中，以便啟用高效能分析方案以及與其他商務應用程式整合。  
  
## 什麼是 Microsoft R Server？  
 Microsoft R Server (獨立) 包含由 R Revolution Analytics 開發的增強 R 封裝，並支援與不同資料來源，例如 Hadoop、Teradata 等等的連接。 藉由安裝獨立伺服器，您可以建立伺服器環境來執行複雜、可調整的 R 作業。  
  
## 使用 Microsoft R 伺服器 （獨立） 的優點  
 R 是世界上功能最強大的程式設計語言，可用於統計計算、機器學習及圖形，並且受到全球蓬勃發展的使用者、開發人員及參與者社群所支援。 傳統上，在企業設定中使用 R 會出現特定的挑戰，特別是在資料量增加，或當您需要將方案部署到生產環境時。 Microsoft R Server 會解決部署與實施 R 程式碼的問題。  
  
 Microsoft R 伺服器可以安裝在任何 Windows 電腦，並且包含所有的 R 封裝和連接工具，以啟用遠端計算內容，並支援可擴充、 可並行的解決方案。  
  
 Microsoft R 伺服器 （獨立） 可支援這些案例︰  
  
-   **使用中央伺服器來實施 R 方案**  
  
     獨立伺服器可讓您的 R 效能改善，而毋須仰賴 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 可以執行複雜或需要大量資源的計算，可能會有有限資源的膝上型電腦或開發電腦上，而是在伺服器上。  
  
     您也可以集中工作，比方說，如果您要針對生產環境中，在預測模型評分，或使用單一的連絡點 R 的 R 伺服器繪製和報告中使用的預測。 
     
     我們也建議您在 SQL Server 電腦上安裝 R 伺服器 （獨立），如果您經常需要以內容以外的 SQL Server 執行 R。
  
-   **啟用功能更強大的資料探索和預測模型**  
  
     資料科學家可以使用任何用戶端工作站和任何 R 開發工具來建置 R 方案。 如果方案使用 RevoScaleR 封裝 API，可以在伺服器上執行運算，伺服器通常會有強大許多的處理能力和記憶體。 因此您的方案可以處理更大的資料集，並且利用多執行緒、多核心、多處理序的運算。  
  
## 如何取得？  
 如需安裝指示，請參閱 [Create a Standalone R Server](../../advanced-analytics/r-services/create-a-standalone-r-server.md)。 來安裝所有元件，請使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式。  
  
## 安裝其他 R 工具  
 如果您沒有慣用的 R 開發環境，有許多選項。 如需詳細資訊，請參閱 [安裝或設定 R 工具](../../advanced-analytics/r-services/setup-or-configure-r-tools.md)。 
 
 連線到 Microsoft R Server 或 SQL Server R 服務的資料科學工作站，我們建議免費 [Microsoft R Client](http://aka.ms/rclient/download) （下載）。  
  
## Microsoft R 伺服器 （獨立） 上執行 R 指令碼  
 您已設定的伺服器元件，並安裝您最喜愛的 R IDE 之後，您可以開始開發使用 RevoScaleR 封裝您的方案。 這些 API 可讓您將 R 命令傳送到遠端伺服器執行。  
  
-   [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started)︰ 瀏覽此集合的可散布提供高效能的分析函數，然後調整到 R 解決方案，即可啟動。 包含許多最受歡迎的 R 模型的封裝，例如 k-means 群集、 決策樹和決策樹和資料操作的工具可並行版本。 您也可以使用 HPC 來建構自己的平行演算法。  
    
-   [DeployR](https://msdn.microsoft.com/microsoft-r/deployr-about)︰ 這個選擇性的架構提供適用於 R 程式設計人員使用 Java、 JavaScript 或.Net 整合的協力廠商封裝輸出 R 分析的工具。  

您可以使用各種不同的格式，包括 SAS、 SPSS、 Hadoop 和文字檔案中的資料。 您可以分析資料的位置，或將資料移入本機 R 開發環境使用.xdf 檔案格式的有效。  
  
若要開始使用 R 的伺服器，請參閱 MSDN Library 中的本指南︰ [R Server-入門](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started)  
  
 如需如何使用 ScaleR 封裝資訊，請參閱 [25 函式中的 R 教學課程](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started#an-r-tutorial-in-25-functions-or-so)  
  
## 另請參閱  
 [SQL Server R 服務使用者入門](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  