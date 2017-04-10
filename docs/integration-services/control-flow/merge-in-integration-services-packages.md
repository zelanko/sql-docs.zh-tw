---
title: "MERGE in Integration Services Packages | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MERGE 陳述式 [SQL Server]"
ms.assetid: 7e44a5c2-e6d6-4fe2-a079-4f95ccdb147b
caps.latest.revision: 22
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# MERGE in Integration Services Packages
  目前版本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]之「執行 SQL」工作中的 SQL 陳述式可能會包含 MERGE 陳述式。 這個 MERGE 陳述式可讓您在單一陳述式中完成多項 INSERT、UPDATE 及 DELETE 作業。  
  
 若要在封裝中使用 MERGE 陳述式，請遵循下列步驟進行：  
  
-   建立資料流程工作，以便將來源資料載入、轉換並儲存至暫存或臨時資料表。  
  
-   建立包含 MERGE 陳述式的執行 SQL 工作。  
  
-   將資料流程工作連接至執行 SQL 工作，然後使用臨時資料表中的資料當做 MERGE 陳述式的輸入。  
  
    > [!NOTE]  
    >  一般而言，雖然 MERGE 陳述式在此狀況下需要臨時資料表，但是 MERGE 陳述式的效能通常會超過查閱轉換所執行之逐列查閱的效能。 此外，當大型查閱資料表要測試可供查閱轉換用於快取其參考資料表的記憶體時，MERGE 也很有用。  
  
 如需支援使用 MERGE 陳述式的範例目的地元件，請參閱 CodePlex 社群範例： [MERGE Destination](http://go.microsoft.com/fwlink/?LinkId=141215)。  
  
## 使用 MERGE  
 一般而言，當您想要在資料表之間套用包含插入、更新和刪除的變更時，就可以使用 MERGE 陳述式。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]之前，這項程序需要查閱轉換和多項 OLE DB 命令轉換。 查閱轉換會執行逐列查閱，以便判斷每個資料列是新的或已變更。 然後，OLE DB 命令轉換會執行必要的 INSERT、UPDATE 及 DELETE 作業。 從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]開始，單一 MERGE 陳述式即可取代查閱轉換及對應的 OLE DB 命令轉換。  
  
### MERGE 搭配累加式載入  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 新增的異動資料擷取功能可讓您更輕易地針對資料倉儲可靠地執行累加式載入。 除了使用參數化 OLE DB 命令轉換來執行插入和更新作業以外，您也可以使用 MERGE 陳述式來結合這兩種作業。  
  
 如需詳細資訊，請參閱[將變更套用到目的地](../../integration-services/change-data-capture/apply-the-changes-to-the-destination.md)。  
  
#### 在其他狀況中的 MERGE  
 在下列狀況中，您可以在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝外部或內部使用 MERGE 陳述式。 不過，您通常需要使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，從多個異質來源載入這項資料，然後結合並清除資料。 因此，為了方便和簡化維護作業，您可能會考慮在封裝中使用 MERGE 陳述式。  
  
##### 追蹤購買習慣  
 資料倉儲中的 FactBuyingHabits 資料表會追蹤某位客戶上次購買給定產品的日期。 此資料表包含 ProductID、CustomerID 及 PurchaseDate 資料行。 交易式資料庫每週都會產生一份 PurchaseRecords 資料表，其中包含當週的購買記錄。 我們的目標是要使用單一 MERGE 陳述式，將 PurchaseRecords 資料表中的資訊合併至 FactBuyingHabits 資料表中。 若為不存在的產品-客戶配對，MERGE 陳述式會插入新的資料列。 若為存在的產品-客戶配對，MERGE 陳述式就會更新最近的購買日期。  
  
###### 追蹤價格記錄  
 DimBook 資料表代表書店存貨的書籍清單並識別每本書的價格記錄。 此資料表具有下列資料行：ISBN、ProductID、Price、Shelf 和 IsCurrent。 此資料表也針對書籍的每個價格具有一個資料列。 其中一個資料列包含目前的價格。 為了指出哪一個資料列包含目前的價格，該資料列之 IsCurrent 資料行的值會設定為 1。  
  
 資料庫每週都會產生一份 WeeklyChanges 資料表，其中包含該週的價格變更以及當週加入的新書。 透過使用單一 MERGE 陳述式，您就可以將 WeeklyChanges 資料表中的變更套用至 DimBook 資料表。 MERGE 陳述式會針對新加入的書籍插入新的資料列，然後針對價格已經變更之現有書籍的資料列，將 IsCurrent 資料行更新為 0。 此外，MERGE 陳述式也會針對價格已經變更的書籍插入新的資料列，然後針對這些新的資料列，將 IsCurrent 資料行的值設定為 1。  
  
### 合併內含新資料的資料表與舊資料表  
 資料庫會使用「開放式結構描述」來設定物件屬性的模型。也就是說，資料表包含每個屬性的名稱-值配對。 Properties 資料表包含三個資料行：EntityID、PropertyID 和 Value。 NewProperties 資料表 (更新的資料表版本) 必須與 Properties 資料表同步處理。 若要同步處理這兩份資料表，您可以使用單一 MERGE 陳述式來執行下列作業：  
  
-   從 Properties 資料表中刪除屬性 (如果它們不存在 NewProperties 資料表中的話)。  
  
-   使用在 NewProperties 資料表中找到的新值來更新 Properties 資料表中的屬性值。  
  
-   針對位於 NewProperties 資料表但在 Properties 資料表中找不到的屬性，插入新的屬性。  
  
 這種方法在複寫狀況類似的狀況中很有用，因為其目標都是要在兩部同步處理的伺服器上保留兩份資料表中的資料。  
  
### 追蹤存貨  
 Inventory 資料庫具有一份 ProductsInventory 資料表，其中包含 ProductID 和 StockOnHand 資料行。 含有 ProductID、CustomerID 和 Quantity 資料行的 Shipments 資料表會追蹤客戶的產品出貨。 ProductInventory 資料表必須根據 Shipments 資料表中的資訊每日更新。 單一 MERGE 陳述式可以根據出貨減少 ProductInventory 資料表中的存貨。 如果某項產品的存貨已經減少至 0，該 MERGE 陳述式也可以從 ProductInventory 資料表中刪除該項產品的資料列。  
  
  