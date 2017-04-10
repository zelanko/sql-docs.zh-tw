---
title: "資料科學深入探討︰使用 RevoScaleR 套件 | Microsoft Docs"
ms.custom: ""
ms.date: "09/27/2016"
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
ms.assetid: c2efb3f2-cad5-4188-b889-15d68b742ef5
caps.latest.revision: 18
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 17
---
# 資料科學深入探討︰使用 RevoScaleR 套件
本教學課程介紹 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中提供的增強型 R 套件。 您將了解如何使用可調整規模的企業架構，在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中執行 R 套件。   透過使用這些可調整 R 函數，資料科學家可以使用這項新服務，建置在本機或伺服器內容中執行的自訂 R 解決方案，以便支援高效能的巨量資料分析。  
  
在本教學課程中，您將了解如何在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 R 工作站之間移動資料、分析和繪製資料，以及建立和部署模型。  
    
## 概觀 
 
為了說明 ScaleR 套件的彈性和處理能力，在本教學課程中，您將會頻繁地移動資料以及交換計算內容。

+ 資料最初是從 CSV 檔案或 XDF 檔案取得。 您將使用 RevoScaleR 套件中的函數，將資料匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。    
+ 模型定型和計分將會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 計算內容中執行。 
    您將使用 **rx** 函數建立新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表，以儲存您的計分結果。    
+ 您將在伺服器和本機計算內容中建立繪圖。  
+ 為了定型模型，您將使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中已儲存的資料。 所有計算都會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上執行。    
+ 您將擷取資料子集，並將它儲存為 XDF 檔案，以便在本機工作站上重複用於分析。    
+ 計分程序期間所使用的新資料是透過 ODBC 連線從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫擷取。 所有計算都會在本機工作站上執行。 
+ 最後，您將使用伺服器計算內容，根據自訂 R 函數來執行模擬。

### 立即開始使用  

本教學課程需要大約一小時才能完成 (不包括設定時間)。  

-   [第 1 課：使用 R 處理 SQL Server 資料](../../advanced-analytics/r-services/lesson-1-work-with-sql-server-data-using-r-data-science-deep-dive.md)  
  
-   [第 2 課︰建立及執行 R 指令碼](../../advanced-analytics/r-services/lesson-2-create-and-run-r-scripts-data-science-deep-dive.md)  
  
-   [第 3 課︰使用 R 轉換資料](../../advanced-analytics/r-services/lesson-3-transform-data-using-r-data-science-deep-dive.md)  
  
-   [第 4 課︰分析本機計算內容中的資料](../../advanced-analytics/r-services/lesson-4-analyze-data-in-local-compute-context-data-science-deep-dive.md)  
  
-   [第 5 課︰建立簡單的模擬](../../advanced-analytics/r-services/lesson-5-create-a-simple-simulation-data-science-deep-dive.md)  

      
### 目標對象  
  
本教學課程適用於或已對 R 和資料科學工作 (包括瀏覽、統計分析和模型調整) 有點熟悉的資料科學家或人員。  不過，會提供所有程式碼，讓您可以輕鬆地執行程式碼並依照指示進行，也會假設您擁有必要的伺服器和用戶端環境。  
  
您也應該熟悉 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法，而且知道如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或其他資料庫工具 (例如 Visual Studio) 來存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。  
  
> [!TIP]  
> 在每堂課之間儲存 R 工作區，以輕鬆地從先前離開的地方繼續進行。  
  
### 必要條件  
  
-   **支援 R 的資料庫伺服器**  
  
    安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，並啟用 SQL Server R 服務 (資料庫內)。 此程序描述於 [SQL Server 2016 線上叢書](http://msdn.microsoft.com/library/mt696069(SQL.130).aspx)。  
  
-   **資料庫權限**  
  
    若要執行用來定型模型的查詢，您必須具有資料儲存所在資料庫的 **db_datareader** 權限。  
  
  
-   **資料科學工作站**  
  
    您必須安裝 RevoScaleR 套件。 若要這樣做，最簡單的方法是安裝 Microsoft R Server (獨立式) 或 Microsoft R Client。 如需詳細資訊，請參閱 [Set Up a Data Science Client](http://msdn.microsoft.co/library/mt696067(SQL.130).aspx) (設定資料科學用戶端)。
      
    > [!NOTE] 
    > 不支援 Revolution R Enterprise 或 Revolution R Open 的其他版本。 
    > 
    > 因為只有 ScaleR 函數才能使用遠端計算內容，所以 R 的開放原始碼散發 (例如 R 3.2.2) 不適用於本教學課程。 
  
-   **其他 R 套件**  
  
    在本教學課程中，您必須安裝下列套件︰**dplyr**、**ggplot2**、**ggthemes**、**reshape2** 和 **e1071**。 相關指示會隨本教學課程一起提供。  
  
    您也必須在執行定型的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上安裝所有套件。 請務必在 SQL Server 所使用的 R 套件程式庫中安裝套件。 **請不要將套件安裝至使用者程式庫。** 如果您沒有在此資料夾中安裝套件的權限，請要求資料庫管理員加入套件。   
  
如需詳細資訊，請參閱[資料科學逐步解說的必要條件 &#40;SQL Server R 服務&#41;](../../advanced-analytics/r-services/prerequisites-for-data-science-walkthroughs-sql-server-r-services.md)。  
  
## 適用於分散式 R 解決方案的資料策略
    
一般而言，在本機開發環境中開始撰寫並執行 R 指令碼之前，請務必花點時間規劃您的資料使用量，並決定要在何處執行每個解決方案部分，以獲得最佳效能。  

在本教學課程中，您將體驗 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中所含且用於分析資料、建立模型及建立繪圖的高效能函數。 我們一般會將這些函數參照為 ScaleR 或 Microsoft R，區分它們與衍生自其他開放原始碼 R 套件的函數。 如需 Microsoft R 與開放原始碼 R 之差異的詳細資訊，請參閱這個[快速入門指南](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started#microsoft-r-products)。 

使用 ScaleR 函數的主要優點在於，它們支援使用本機或伺服器「資料來源」，以及本機或遠端「計算內容」。  因此，當您完成本教學課程時，請考慮您可能需要用於您自己解決方案的資料策略。
  
-   **您要執行的分析類型為何？** 這僅供您使用，或者您想要與其他人共用模型、結果或圖表？
 
    在本教學課程中，您將了解如何在開發環境與伺服器之間之間來回移動結果，以促進共用和分析。 
  
-   **是否需要 R 套件支援遠端執行？** [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 所提供之 ScaleR 套件中的所有函數都可以在遠端計算內容中執行，並可以使用平行執行。 相反地，協力廠商套件中的函數可能需要其他資源才能進行單一執行緒執行。 
    
    在本教學課程中，您將了解如何切換本機與遠端計算內容，以在需要時利用伺服器資源。 您也將了解如何將標準 R 函數包裝至 *rxExec*，以支援遠端執行任意 R 函數。
    
  
-   **您的資料在哪裡，它的特點為何？**  如果您的資料位於本機，則必須決定是否將所有新的資料上傳至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，或在本機定型，並且只將模型儲存至資料庫。 不過，當您部署至生產環境時，可能需要從企業資料定型，並使用 ETL 程序來清除和載入資料。  
  
-   對資料計分時也會有類似的問題。 您要建立資料管線對工作站上的資料計分，還是要使用企業資料來源？ 您應該將資料清理和準備當作 ETL 程序的一部分執行，還是要執行一次性實驗？  

    在本教學課程中，您將了解如何有效且安全地在本機 R 環境與 SQL Server 之間移動資料。 
  
-   **您應該使用哪種計算內容？** 您可能想要根據取樣的資料在本機定型模型，然後切換成使用伺服器資料來進行測試和生產。

    在本教學課程中，您將了解如何使用 R 在 SQL Server 與 R 之間移動資料。您也將了解如何使用 XDF 檔案來處理資料，以及如何使用 ScaleR 函數來處理區塊中的資料。  
  
 
  
## 下一個步驟  
[第 1 課：使用 R 處理 SQL Server 資料 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/lesson-1-work-with-sql-server-data-using-r-data-science-deep-dive.md)  
  
  
  
