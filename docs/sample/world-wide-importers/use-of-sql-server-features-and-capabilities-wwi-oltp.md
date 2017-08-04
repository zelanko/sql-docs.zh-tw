---
title: "使用 SQL Server 特性與功能 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- samples
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 06f89721-8478-4abc-8ada-e9c73b08bf51
caps.latest.revision: 2
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 90b1cd86f2fcc282922111ac9325470635bcfcad
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="use-of-sql-server-features-and-capabilities"></a>使用 SQL Server 功能和功能
WideWorldImporters 使用 SQL Server 特性與 OLTP 資料庫中的功能。

WideWorldImporters 被為了展現許多重要功能的 SQL Server，包括最新 SQL Server 2016 中引進的功能。 以下是一份 SQL Server 功能和功能，以及在 WideWorldImporters 的使用方式的描述。

|SQL Server 功能或功能|用於 WideWorldImporters|
|-----------------------------|---------------------|
|時態表|有許多的時態表，包括所有查閱樣式參考資料表與主要實體，例如 StockItems、 客戶及供應商。 使用時態表可讓以方便地追蹤這些實體的歷程記錄。|
|For JSON 的 AJAX 呼叫|應用程式經常使用 AJAX 呼叫來查詢這些資料表： 人員、 客戶、 供應商和 StockItems。 呼叫傳回 JSON 承載 （也就是所傳回的資料會格式化為 JSON 資料）。 請參閱，例如預存程序`Website.SearchForCustomers`。|
|JSON 屬性/值袋|資料表的數目會有保存擴充資料表中的關聯式資料的 JSON 資料的資料行。 例如，`Application.SystemParameters`有應用程式設定的資料行和`Application.People`具有記錄的使用者喜好設定的資料行。 使用這些資料表`nvarchar(max)`記錄 JSON 資料，以及使用內建函式的 CHECK 條件約束的資料行`ISJSON`以確保資料行的值為有效的 JSON。|
|資料列層級安全性 (RLS)|資料列層級安全性 (RLS) 用來限制存取 Customers 資料表中，根據角色成員資格。 每個銷售地區都有角色和使用者。 若要查看此動作中，使用對應的指令碼範例-script.zip，也就是組件中的[版本的範例](http://go.microsoft.com/fwlink/?LinkID=800630)。|
|即時作業分析|（完整版的資料庫）核心交易資料表`Sales.InvoiceLines`和`Sales.OrderLines`兩者都有支援有效率的方式執行分析查詢，對作業的工作負載的影響降到最低的交易式資料庫中的非叢集資料行存放區索引。 在相同資料庫中執行的交易和分析也稱為[混合式交易式/分析處理 (HTAP)](https://wikipedia.org/wiki/Hybrid_Transactional/Analytical_Processing_(HTAP))。 若要查看此動作中，使用對應的指令碼範例-script.zip，也就是組件中的[版本的範例](http://go.microsoft.com/fwlink/?LinkID=800630)。|
|PolyBase|若要查看此 PolyBase 在動作中，使用外部資料表具有公用的資料集，裝載於 Azure blob 儲存體，使用對應的指令碼範例-script.zip，也就是組件中的[版本的範例](http://go.microsoft.com/fwlink/?LinkID=800630)。|
|In-Memory OLTP|（完整版的資料庫）資料表類型是所有記憶體最佳化，以便從記憶體最佳化的資料表值參數 (Tvp 所有) 獲益。<br/><br/>兩個監視資料表，`Warehouse.VehicleTemperatures`和`Warehouse.ColdRoomTemperatures`，是記憶體最佳化。 這可讓 ColdRoomTemperatures 資料表填入最高速度比傳統以磁碟為基礎的資料表。 VehicleTemperatures 資料表保存 JSON 承載，而借用本身進行朝向 IoT 案例的擴充功能。 進一步 VehicleTemperatures 資料表本身涉及 EventHubs、 Stream Analytics 中，與 Power BI 的案例。<br/><br/>預存程序`Website.RecordColdRoomTemperatures`原生編譯以進一步改善錄製冷聊天室溫度的效能。<br/><br/>若要查看作用中記憶體內部 OLTP 的範例，請參閱工作負載-drivers.zip，這是一部分的一種載具，位置工作負載驅動程式的[版本的範例](http://go.microsoft.com/fwlink/?LinkID=800630)。|
|叢集資料行存放區索引|（完整版的資料庫）資料表`Warehouse.StockItemTransactions`使用叢集資料行存放區索引。 此資料表中的資料列數目預期成長大，而且叢集資料行存放區索引大幅降低磁碟大小的資料表，並可改善查詢效能。 修改此資料表上的只能插入-沒有任何更新/刪除中線上工作負載中的此資料表上，而且叢集資料行存放區索引也會執行插入工作負載。|
|動態資料遮罩|資料庫結構描述中的資料遮罩已套用至供應商，保留在資料表的銀行詳細資料`Purchasing.Suppliers`。 非系統管理人員不會存取此資訊。|
|永遠加密|永遠加密示範隨附於可下載 samples.zip，也就是組件的[版本的範例](http://go.microsoft.com/fwlink/?LinkID=800630)... 示範建立加密金鑰，以加密敏感性資料，以及將資料插入資料表的小型範例應用程式的資料表。|
|Stretch database|`Warehouse.ColdRoomTemperatures`資料表已實作為時態表，而且記憶體最佳化的範例資料庫的完整版本。 封存資料表是以磁碟為基礎，並可以延伸到 Azure。|
|全文檢索索引|全文檢索索引會改善搜尋人員、 客戶及 StockItems。 只有當您安裝 SQL Server 執行個體上的全文檢索索引，會套用至查詢索引。 非保存計算資料行用來建立的全文檢索索引 StockItems 資料表中的資料。<br/><br/>`CONCAT`用於如串連欄位建立的全文檢索索引的 SearchData。<br/>若要啟用的範例中的全文檢索索引使用的資料庫中執行下列陳述式：<br/><br/>    `EXECUTE [Application].[Configuration_ConfigureFullTextIndexing]`<br/><br/>程序會建立預設全文檢索目錄如果其中一個不存在，則取代這些檢視的全文檢索版本的搜尋檢視）。<br/><br/>請注意，使用 SQL Server 中的全文檢索索引需要全文檢索安裝時選取選項。 Azure SQL Database 不需要和特定組態資訊才能啟用全文檢索索引。|
|保存計算資料行編製索引|編製索引 SupplierTransactions 和 CustomerTransactions 中使用的保存計算資料行。|
|檢查條件約束|相對複雜的檢查條件約束處於`Sales.SpecialDeals`。 這可確保一且只有其中一個 DiscountAmount，DiscountPercentage，並且以設定單價。|
|Unique 條件約束|對 Warehouse.StockItemStockGroups' 多對多建構 （和唯一條件約束） 所設定的。|
|資料表資料分割|（完整版的資料庫）資料表`Sales.CustomerTransactions`和`Purchasing.SupplierTransactions`兩者都分割所使用的資料分割函數的年份`PF_TransactionDate`和分割區配置`PS_TransactionDate`。 若要改善管理性的大型資料表使用資料分割。|
|清單處理|範例資料表類型`Website.OrderIDList`提供。 它由範例程序`Website.InvoiceCustomerOrders`。 程序會使用通用資料表運算式 (Cte)、 TRY/CATCH、 JSON_MODIFY、 XACT_ABORT、 NOCOUNT、 擲回和 XACT_STATE 示範處理一份訂單，而不只單一訂單，從 database engine 應用程式的往返降到最低。|
|GZip 壓縮|`Warehouse.VehicleTemperature`的資料表保有完整的感應器資料，但超過幾個月舊資料時，會壓縮，以節省空間使用 COMPRESS 函數，它會使用 GZip 壓縮。<br/><br/>檢視`Website.VehicleTemperatures`擷取先前已壓縮的資料時，使用 DECOMPRESS 函式。|
|查詢存放區|在資料庫上啟用查詢存放區。 執行幾個查詢之後, 在 Management Studio 中開啟的資料庫，開啟查詢存放區，也就是資料庫底下的節點並開啟報表的 熱門資源取用查詢以查看查詢執行和剛剛所執行的查詢計劃。|
|STRING_SPLIT|資料行`DeliveryInstructions`資料表中`Sales.Invoices`可以用來示範 STRING_SPLIT 的逗點分隔值。|
|稽核|可以在資料庫中執行下列陳述式，為這個範例資料庫啟用 SQL Server Audit。<br/><br/>    `EXECUTE [Application].[Configuration_ApplyAuditing]`<br/><br/>透過已啟用 Azure SQL Database 稽核[Azure 入口網站](https://portal.azure.com/)。<br/><br/>包含登入的安全性作業，角色和權限登入所有的系統啟用稽核 （包括標準版的系統） 的位置。 稽核會導向至應用程式記錄檔中，因為這是用於所有系統，不需要其他權限。 警告會假設為提高安全性，就應該重新導向至安全性記錄檔或安全的資料夾中的檔案。 提供的連結，以描述所需的其他設定。<br/><br/>適用於評估/developer/企業版系統稽核所有的財務交易資料的存取權。|

