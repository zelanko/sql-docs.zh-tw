---
title: "使用 DQS 預設知識庫 | Microsoft Docs"
ms.custom: ""
ms.date: "07/31/2012"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b36af13b-9fcc-4168-bb92-214d600b1c93
caps.latest.revision: 13
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 13
---
# 使用 DQS 預設知識庫
  本主題將說明預設知識庫 **DQS 資料**, ，在安裝 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS)。 這是包含下列定義域之預先建立的預設知識庫：  
  
-   **國家/地區**︰ 包含傳統的完整 （國家/地區所指定的官方名稱） 和簡短名稱 （清單、 地圖等所使用的一般名稱）、 兩個字母的縮寫、 三個字母縮寫以及針對每個位置的三位數代碼。  前置值設定為完整的國家/地區名稱。  
  
-   **國家/地區 （前置三個字母）**︰ 包含傳統的完整 （國家/地區所指定的官方名稱） 和簡短名稱 （清單、 對應等等使用的一般名稱）、 兩個字母的縮寫、 三個字母縮寫以及針對每個位置的三位數代碼。  前置值設定為三個字母的縣市縮寫。  
  
-   **國家/地區 （前置兩個字母）**︰ 包含傳統的完整 （國家/地區所指定的官方名稱） 和簡短名稱 （清單、 地圖等所使用的一般名稱）、 兩個字母的縮寫、 三個字母縮寫以及針對每個位置的三位數代碼。  前置值設定為兩個字母的國家/地區縮寫。  
  
-   **美國-郡**︰ 包含美國各郡的清單。  
  
-   **美國-姓氏**︰ 包含清單的最後一個名稱 （含） 發生 100 次或多次人口普查 2000年中。  
  
-   **美國-地點**︰ 包含 50 州、 學區 of Columbia 和擷取自 Census 2010 波多黎各的地點清單。  
  
-   **美國-州**︰ 包含傳統的完整 （官方） 名稱和美國各州的兩個字母縮寫。 前置值設定為傳統的州名稱。  
  
-   **美國-狀態 （2 個字母標題）**︰ 包含傳統的完整 （官方） 名稱和美國各州的兩個字母縮寫。 前置值設定為兩個字母的州名縮寫。  
  
## 使用預設知識庫  
 您可以透過下列方式使用預設的 DQS 知識庫 DQS 資料：  
  
-   使用預設知識庫快速啟動並執行清理資料品質專案，而不需要先在 DQS 中建立新的知識庫。  
  
-   在預設知識庫上執行定義域管理、知識探索或比對原則活動。 若要這樣做，請按一下 [ **開啟知識庫** 中 [資料品質用戶端首頁畫面](../data-quality-services/data-quality-client-home-screen.md), ，請選取 **DQS 資料** 知識庫 **開啟知識庫** 螢幕，然後再選取所需的活動 **選取活動** 區域。 按 **[下一步]** 繼續進行。  
  
-   使用預設知識庫建立新的知識庫。 若要從現有的知識庫建立知識庫，請參閱 [建立知識庫](../data-quality-services/create-a-knowledge-base.md)。  
  
-   將它用於 [Integration Services 中的 DQS 清理元件](http://go.microsoft.com/fwlink/?LinkId=238830) 和 [Master Data Services 增益集適用於 Excel](../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)。  
  
## 另請參閱  
 [DQS Knowledge Bases and Domains](../data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  