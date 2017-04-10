---
title: "SQL Server R 服務 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: 38
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 36
---
# SQL Server R 服務
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 提供的平台可供開發及部署展現全新深入解析的智慧型應用程式。 您可以使用功能豐富又強大的 R 語言以及社群提供的許多套件，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來建立模型及產生預測。 因為 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 整合了 R 語言與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，所以您可以保留與資料密切相關的分析，並免去和移動資料相關聯的成本與安全性風險。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援開放原始碼 R 語言與一組完整的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 工具和技術，提供更優異的效能、安全性、可靠性及管理能力。 您可以使用方便且熟悉的工具，部署 R 解決方案，而且生產應用程式可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]呼叫 R 執行階段並擷取預測和視覺效果。 您也會得到 [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) 程式庫，以提升 R 解決方案的規模與效能。  
  
透過 SQL Server 安裝程式，伺服器及用戶端元件都可以安裝。  
  
+   **R 服務 (資料庫內)︰** 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式期間會安裝這項功能，以啟用在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦上安全地執行 R 指令碼。  
  
     當您選取此項功能時，延伸模組會安裝在資料庫引擎內，以支援執行 R 指令碼，並會建立新的服務 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]，以管理 R 執行階段與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之間的通訊。  
  
+   **Microsoft R Server (獨立)：**開放原始碼 R 的散發，結合了支援平行處理及其他效能改進的專屬套件。 R Services (資料庫內) 及 Microsoft R Server (獨立) 都包括基礎 R 執行階段與套件，還有能夠加強連線能力及效能的 **ScaleR** 程式庫。 
  
+    [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/index#mrc) 可以當作獨立的免費安裝程式使用。  您可以使用 Microsoft R Client 開發解決方案，將其部署到執行於 SQL Server 的 R Services，或部署到執行於 Windows、Teradata 或 Hadoop 的 Microsoft R Server。 
     

  > [!NOTE] 如果您需要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中執行 R 程式碼，請務必安裝 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，如[此處](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)所述。
  >  
  > Microsoft R Server \(獨立\) 這個個別選項，專為在未執行 SQL Server 的 Windows 電腦上使用 ScaleR 程式庫而設計。 
>   
>  不過，如果您有 Enterprise Edition，建議您在用於 R 開發的膝上型電腦或另一部電腦上安裝 Microsoft R Server \(獨立\)，以建立可以輕鬆部署到執行 R Services \(資料庫內\) 之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 R 解決方案。
  
## <a name="additional-resources"></a>其他資源  
  
 [開始使用 SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)   
 描述搭配 SQL Server 使用 R 的常見案例。  
  
[設定 SQL Server R Services (資料庫內)](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
在 SQL Server 安裝過程中安裝 R 及相關資料庫元件。  
  
[SQL Server R Services 教學課程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
了解如何使用 R 程式碼建立 SQL Server 資料來源，以及如何使用遠端計算內容。 其他以 SQL 開發人員為對象的教學課程會示範如何在 SQL Server 中定型及部署 R 模型。  
  
## <a name="see-also"></a>另請參閱  
  
 [開始使用 Microsoft R Server &#40;獨立&#41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
 
 [設定獨立 R Server](../../advanced-analytics/r-services/create-a-standalone-r-server.md) 
  