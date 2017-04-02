---
title: "使用 R 的資料探索和預測模型 | Microsoft Docs"
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
ms.assetid: bf6de7e2-f394-4b8a-a4b7-0b8dadf25426
caps.latest.revision: 20
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 19
---
# 使用 R 的資料探索和預測模型
  資料科學家通常使用 R 來探索資料和建置預測模型。 流程通常會在嘗試與失敗間反覆，直到達成良好的預測模型為止。 身為資深的資料科學家，您可能會連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，然後使用 RODBC 封裝將資料擷取到本機工作站，再使用標準 R 封裝建置預測模型。  
  
 不過，此方法有其缺點。 資料移動可能會很緩慢、效率不佳或不安全，而 R 本身也有其效能和規模限制。 當您必須移動及分析大量資料，或電腦的可用記憶體容納不下您使用的資料集時，這些缺點變得更加明顯。  
  
 您可以使用新的可擴充封裝克服這些挑戰，並隨附於 R 函數 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。 **RevoScaleR** 封裝包含某些熱門 R 函數的實作，這些函數經過重新設計，而得以提供平行處理原則與規模。 RevoScaleR 封裝也支援變更 *「執行內容」*(execution context)。 這表示對於整個解決方案或一個函數，您都可以指定使用裝載 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的電腦資源來執行計算，而不使用您的本機工作站。 這樣做有多項優點：您可以避免不必要的資料移動，也可以運用伺服器電腦上更多的計算資源。  
  
 本節提供適用於資料科學家的指導，說明如何使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] ，以及如何執行開發與測試 R 解決方案的相關工作。  
  
##  <a name="bkmk_RDevTools"></a> R 開發工具  
 Microsoft R 用戶端可讓資料科學家完整的環境來開發和測試預測模型。 R 的用戶端包括︰  
  
-  **[!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]:** R 執行階段和一組封裝，例如 Intel 數學核心程式庫，大幅提升效能的標準 R 作業的散佈。  
  
-   **RevoScaleR:** R 封裝，可讓您發送計算執行個體的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]。 它也包含一組常見的 R 函式已經重新設計，以提供較佳的效能和延展性。 您可以依據 **rx** 前置詞識別這些改良的函數。 它也包含增強的資料提供者的各種不同的來源;這些函式前面會加上 **Rx**。  
  
-   **免費的開發工具的選擇︰** 您可以使用任何支援 R，例如 Windows 架構的程式碼編輯器 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 或 RStudio。 下載 [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)] 也包含常用的命令列工具，例如 RGui.exe。  
  
##  <a name="bkmk_packages"></a> R 環境和封裝  
 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中支援的 R 環境包含由多個封裝支援及延伸的執行階段、開放原始碼語言和圖形化引擎。 該語言允許使用封裝實作的各種延伸模組。  
  
 您可以在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 使用其他 R 封裝的多個來源：  
  
  
-   公用儲存機制中的一般用途的 R 封裝。 您可以從公用儲存機制取得最熱門的開放原始碼 R 封裝，像是 CRAN 的主機便擁有超過 6000 個可供資料科學家使用的封裝。  
  
     其他封裝可以用來支援特殊領域中的預測性分析，像是財經、基因體學等。  
  
     Windows 平台，R 封裝為 zip 檔案提供和可以下載並安裝在 GPL 授權下。  
  
     如需有關如何安裝搭配使用的協力廠商封裝資訊 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], ，請參閱 [SQL Server 上安裝其他的 R 封裝](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)  
  
-   其他套件和程式庫所提供 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。   
  
      **RevoScaleR** 封裝包括高效能巨量資料分析、 支援一般的資料科學工作，最佳化學習貝氏機率分類、 線性迴歸、 時間序列模型，與類神經網路和進階的數學程式庫函式的改良版本。  
  
     **RevoPemaR** 封裝可讓您使用 R 開發自己的平行外部記憶體演算法。  
  
     如需有關這些封裝和使用方式的詳細資訊，請參閱 [資料探索和預測模型化 & #40。教學課程︰ SQL Server R Services & #41;](../../advanced-analytics/r-services/sql-server-r-services.md)。  
  
## 使用資料來源和計算內容  
 當使用 RevoScaleR 封裝連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ，有一些重要的新函式可使用 R 程式碼中︰  
  
-   [RxSqlServerData](RxSqlServerData.md) 是 RevoScaleR 套件以支援提升的資料的連線中的函式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
     您可以在 R 程式碼中使用此函數來定義 *「資料來源」*(data source)。 資料來源物件會指定資料所在的伺服器和資料表，並管理從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]讀取資料及寫入其中的工作。  
  
-    [RxInSqlServer](rxInSqlServer.md) 函式可用來指定 *運算內容*。  換句話說，表示應執行的 R 程式碼的位置︰ 在本機工作站上，或電腦上裝載 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
     當您設定的計算內容時，它會影響只支援遠端執行內容，這表示 R 作業 RevoScaleR 封裝所提供與相關函數的計算。 一般而言，R 解決方案，根據標準 CRAN 封裝無法執行在遠端的計算內容中，雖然能夠執行的 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 如果 t-sql 啟動電腦。 不過，您可以使用 `rxExec` 函式，呼叫個別的 R 函式，並從遠端在執行它們 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。  
  
 如需如何建立及使用資料來源和執行內容的範例，請參閱這些教學課程︰
 
 + [資料科學深入探討](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
 +  [RevoScaleR SQL Server 使用者入門](https://msdn.microsoft.com/microsoft-r/rserver/rserver-scaler-sql-server-getting-started)。  
  
## 將您的 R 程式碼部署到生產環境  
 資料科學的其中一個重點是將您的分析提供給他人，或使用預測模型改進商務結果或程序。 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中，當您的 R 指令碼或模型就緒時，就能輕鬆移到生產環境。  
  
 如需有關如何將您的程式碼中執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ，請參閱 [另尋高就您的 R 程式碼](../../advanced-analytics/r-services/operationalizing-your-r-code.md)。  
  
 通常，部署程序一開始會清理您的指令碼，以排除生產環境不需要的程式碼。 當您移動更接近計算的資料，您可能會發現更有效率地移動、 彙總，或呈現優於 r 中的所有資料的方式  
  
 我們建議，請洽詢資料庫開發人員增進效能的相關資料科學家，尤其是這個解決方案會執行資料清理或功能工程，可能會在 SQL 中更有效率。 ETL 程序的變更可能需要以確保，在建置或評分模型的工作流程不會失敗，並輸入的資料位於正確的格式。  
  
##  <a name="bkmk_SQLInR"></a> 本節內容  

[ScaleR 函式和 CRAN R 函數的比較](Summary%20of%20rx%20Functions.md)

[使用 SQL Server 的 scaleR 函式](../../advanced-analytics/r-services/scaler-functions-for-working-with-sql-server-data.md)
   
## 另請參閱  

 
 [SQL Server R 服務功能及工作](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)   
 
 [運用您的 R 程式碼](../../advanced-analytics/r-services/operationalizing-your-r-code.md)  
  
  