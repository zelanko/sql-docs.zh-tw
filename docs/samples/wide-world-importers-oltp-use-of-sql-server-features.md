---
title: 使用 SQL Server 特性與功能 |Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 06f89721-8478-4abc-8ada-e9c73b08bf51
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 866b32abbc7f7e754b11fd286dd0c35eeeb92165
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52400691"
---
# <a name="use-of-sql-server-features-and-capabilities"></a>使用 SQL Server 功能和功能
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
WideWorldImporters 使用 SQL Server 特性與 OLTP 資料庫中的功能。

WideWorldImporters 被設計來展示的許多重要功能的 SQL Server，包括最新 SQL Server 2016 中引進的功能。 以下是一份 SQL Server 功能和功能，以及在 WideWorldImporters 的使用方式的描述。

|SQL Server 功能或功能|用於 WideWorldImporters|
|-----------------------------|---------------------|
|時態表|有許多的時態表，包括所有的查閱樣式參考資料表和主要實體，例如 StockItems、 客戶及供應商。 使用時態表可讓以方便地追蹤這些實體的歷程記錄。|
|適用於 JSON 的 AJAX 呼叫|應用程式經常會使用 AJAX 呼叫來查詢這些資料表：人員、 客戶、 供應商和 StockItems。 呼叫會傳回 JSON 承載 （也就是會傳回的資料會格式化為 JSON 資料）。 請參閱，例如預存程序`Website.SearchForCustomers`。|
|JSON 屬性/值包|一些資料表有包含擴充資料表中的關聯式資料的 JSON 資料的資料行。 例如，`Application.SystemParameters`有應用程式設定的資料行和`Application.People`具有記錄的使用者偏好設定的資料行。 這些資料表會使用`nvarchar(max)`要記錄的 JSON 資料，以及使用內建函式的 CHECK 條件約束的資料行`ISJSON`以確保資料行值都是有效的 JSON。|
|資料列層級安全性 (RLS)|資料列層級安全性 (RLS) 用來限制存取權 [客戶] 資料表中，根據角色成員資格。 每個銷售領域有角色和使用者。 若要查看此動作，請使用對應的指令碼範例-script.zip，也就是組件中的[版本的範例](https://go.microsoft.com/fwlink/?LinkID=800630)。|
|即時作業分析|（完整版的資料庫）核心交易資料表`Sales.InvoiceLines`和`Sales.OrderLines`兩者都有支援有效率的分析查詢的執行上作業的工作負載的影響降到最低的交易式資料庫中的非叢集資料行存放區索引。 在相同的資料庫執行交易和分析也稱為[混合式交易/分析處理 (HTAP)](https://wikipedia.org/wiki/Hybrid_Transactional/Analytical_Processing_(HTAP))。 若要查看此動作，請使用對應的指令碼範例-script.zip，也就是組件中的[版本的範例](https://go.microsoft.com/fwlink/?LinkID=800630)。|
|PolyBase|若要查看此 PolyBase 外部資料表使用公用資料集，裝載於 Azure blob 儲存體，在動作中，請使用對應的指令碼範例-script.zip，也就是組件中的[版本的範例](https://go.microsoft.com/fwlink/?LinkID=800630)。|
|In-Memory OLTP|（完整版的資料庫）資料表類型是所有記憶體最佳化，以便從記憶體最佳化的資料表值參數 (Tvp) 都會獲益。<br/><br/>兩個監視資料表`Warehouse.VehicleTemperatures`和`Warehouse.ColdRoomTemperatures`，是記憶體最佳化。 這可讓 ColdRoomTemperatures 資料表填入以較高的速度，比傳統以磁碟為基礎的資料表。 VehicleTemperatures 資料表保存 JSON 承載，並朝向 IoT 案例的擴充功能可用於。 進一步 VehicleTemperatures 資料表本身涉及 EventHubs、 Stream Analytics 與 Power BI 的案例。<br/><br/>預存程序`Website.RecordColdRoomTemperatures`原生編譯以進一步改善記錄冷聊天室溫度的效能。<br/><br/>若要查看作用中記憶體內部 OLTP 的範例，請參閱工作負載-drivers.zip，也就是組件中的車輛位置的工作負載驅動程式的[版本的範例](https://go.microsoft.com/fwlink/?LinkID=800630)。|
|叢集資料行存放區索引|（完整版的資料庫）資料表`Warehouse.StockItemTransactions`使用叢集資料行存放區索引。 此資料表中的資料列數目預期變大，而且叢集資料行存放區索引大幅減少磁碟上資料表的大小，並可改善查詢效能。 此資料表上所作的修改都只能插入-沒有任何更新/刪除在線上的工作負載-這個資料表上和叢集資料行存放區索引也會執行插入的工作負載。|
|動態資料遮罩|資料庫結構描述中的資料遮罩已套用至資料表中的供應商，保留銀行詳細資料`Purchasing.Suppliers`。 非系統管理人員不會有存取此資訊。|
|永遠加密|Always Encrypted 的示範包含可下載 samples.zip，也就是組件中的[版本的範例](https://go.microsoft.com/fwlink/?LinkID=800630)... 示範建立加密金鑰，使用加密的敏感性資料，以及將資料插入資料表的小型範例應用程式的資料表。|
|Stretch Database|`Warehouse.ColdRoomTemperatures`資料表已實作為時態表，並為完整版的範例資料庫中記憶體最佳化。 封存資料表是以磁碟為基礎，並可以延展到 Azure。|
|全文檢索索引|全文檢索索引會改善搜尋的人員、 客戶和 StockItems。 只有當您安裝在您的 SQL Server 執行個體上的全文檢索索引，索引會套用至查詢。 非持續性的計算資料行用來建立的全文檢索索引 StockItems 資料表中的資料。<br/><br/>`CONCAT` 用於串連欄位以建立的全文檢索索引的 SearchData。<br/>若要啟用全文檢索索引，在此範例中使用，請在資料庫中執行下列陳述式：<br/><br/>    `EXECUTE [Application].[Configuration_ConfigureFullTextIndexing]`<br/><br/>在程序建立預設全文檢索目錄如果其中一個尚未存在，則搜尋檢視取代這些檢視的全文檢索版本）。<br/><br/>請注意，使用 SQL Server 中的全文檢索索引需要全文檢索安裝時選取選項。 Azure SQL Database 不需要和特定組態資訊才能啟用全文檢索索引。|
|索引的保存計算資料行|編製索引 SupplierTransactions 和 CustomerTransactions 中使用的保存計算資料行。|
|檢查條件約束|相對複雜的 check 條件約束是在`Sales.SpecialDeals`。 這可確保一，而且只有其中一個 DiscountAmount，DiscountPercentage，且會設定 UnitPrice。|
|Unique 條件約束|多對多建構 （和唯一條件約束） 會設定 Warehouse.StockItemStockGroups'。|
|資料表資料分割|（完整版的資料庫）資料表`Sales.CustomerTransactions`並`Purchasing.SupplierTransactions`兩者都分割所使用的資料分割函數的年度`PF_TransactionDate`和分割區配置`PS_TransactionDate`。 資料分割用來改善大型資料表管理能力。|
|清單處理|類型的範例資料表`Website.OrderIDList`提供。 它由範例程序`Website.InvoiceCustomerOrders`。 程序使用通用資料表運算式 (Cte)、 TRY/CATCH，JSON_MODIFY，XACT_ABORT、 NOCOUNT、 擲回和 XACT_STATE 來示範如何處理訂單，而不是只是單一訂單，以減少來回行程，從應用程式清單database engine。|
|GZip 壓縮|`Warehouse.VehicleTemperature`的資料表會保存完整的感應器資料，但超過幾個月舊資料時，它會壓縮成節省使用 COMPRESS 函數，它會使用 GZip 壓縮的空間。<br/><br/>檢視`Website.VehicleTemperatures`擷取先前已壓縮的資料時，會使用 DECOMPRESS 函式。|
|查詢存放區|在資料庫上啟用查詢存放區。 執行一些查詢之後, 在 Management Studio 中開啟資料庫，開啟節點的 查詢存放區，也就是資料庫底下，並開啟報表的 熱門資源取用查詢以查看查詢執行，以及您剛剛執行的查詢計畫。|
|STRING_SPLIT|資料行`DeliveryInstructions`資料表中`Sales.Invoices`可以用來示範 STRING_SPLIT 的逗號分隔的值。|
|稽核|SQL Server Audit 可以啟用這個範例資料庫，在資料庫中執行下列陳述式：<br/><br/>    `EXECUTE [Application].[Configuration_ApplyAuditing]`<br/><br/>透過已啟用 Azure SQL Database 稽核[Azure 入口網站](https://portal.azure.com/)。<br/><br/>安全性牽涉到登入，角色和權限會記錄作業時啟用稽核 （包括標準版的系統） 的所有系統上。 稽核會導向至應用程式記錄檔中，因為這是在所有的系統上使用，而不需要額外的權限。 警告會假設為提高安全性，它應該重新導向至安全性記錄檔或安全的資料夾中的檔案。 會提供連結，描述所需的其他組態。<br/><br/>適用於評估/開發人員/企業版系統稽核所有的財務交易資料的存取權。|
