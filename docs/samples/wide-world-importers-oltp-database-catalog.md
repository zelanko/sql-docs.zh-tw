---
title: WideWorldImporters OLTP 資料庫目錄 SQL |Microsoft 文件
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
robots: noindex,nofollow
ms.openlocfilehash: 408621e5690f8b402e5743259b43eb93f2ef518a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="wideworldimporters-database-catalog"></a>WideWorldImporters 資料庫目錄
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
WideWorldImporters 資料庫包含所有的交易資訊和銷售和購買商品每日的資料，以及車輛和冷聊天室的感應器資料。

## <a name="schemas"></a>結構描述

WideWorldImporters 使用不同的用途，例如，儲存資料、 定義使用者如何存取資料，以及提供資料倉儲開發和整合物件的結構描述。

### <a name="data-schemas"></a>資料結構描述

這些結構描述包含的資料。 所需的所有其他結構描述和位於應用程式的結構描述中的資料表數目。

|結構描述|Description|
|-----------------------------|---------------------|
|應用程式|整個應用程式的使用者、 連絡人和參數。 這也包含可由多個結構描述的資料與參考資料表|
|Purchasing|內建項目購買的供應商以及供應商詳細資料。|  
|Sales|內建項目銷售零售客戶與客戶和銷售人員相關的詳細資料。 |  
|Warehouse|內建項目清查和交易。|  

### <a name="secure-access-schemas"></a>安全存取結構描述

這些結構描述用於外部應用程式，不允許直接存取資料的資料表。 它們包含檢視與外部應用程式所使用的預存程序。

|結構描述|Description|
|-----------------------------|---------------------|
|網站|從公司網站資料庫的所有存取都是透過此結構描述。|
|報表|從 Reporting Services 報表資料庫的所有存取都是透過此結構描述。|
|PowerBI|所有資料庫的存取權透過企業閘道，Power BI 儀表板都是透過此結構描述。|

請注意，報表和 power Bi 的範例資料庫的初始版本中不會使用結構描述。 不過，建置於這個資料庫的所有 Reporting Services 和 Power BI 範例鼓勵使用這些結構描述。

### <a name="development-schemas"></a>開發結構描述

特殊用途的結構描述

|結構描述|Description|
|-----------------------------|---------------------|
|整合|物件和資料倉儲整合所需的程序 （也就是將資料移轉至 WideWorldImportersDW 資料庫）。|
|序列|保存應用程式中的所有資料表所使用的序列。|

## <a name="tables"></a>資料表

在資料庫中的所有資料表都都在資料結構描述。

### <a name="application-schema"></a>應用程式結構描述

參數和人員 （使用者和連絡人） 以及通用 （通用於多個其他結構描述） 的參考資料表的詳細資料。

|Table|Description|
|-----------------------------|---------------------|
|SystemParameters|包含全系統的可設定參數。|
|人員|包含使用者名稱，使用應用程式中，所有與 Wide World Importers 處理在客戶組織的人員的連絡資訊。 這包括員工、 客戶、 供應商，以及任何其他連絡人。 針對被授與使用的系統或網站的權限的人員，資訊會包含登入詳細資料。|
|城市|有多個地址，儲存在系統中，對人員來說，客戶組織送貨地址，收取等供應商的位址。每當儲存地址，但沒有參考此資料表中的城市。 此外，還有每個城市的空間位置。|
|StateProvinces|會部分州或省的城市。 這個資料表有這些包括描述界限的空間資料的詳細資料，每個州或省。|
|國家 （地區)|州或省是國家 （地區） 的一部分。 這個資料表有這些包括描述每個國家/地區的界限的空間資料的詳細資料。|
|DeliveryMethods|適用於傳遞庫存項目 （例如卡車/van、 post、 收取，新細明體等） 的選項|
|PaymentMethods|適用於進行付款選項 (例如，現金、 核取，EFT，等。)|
|TransactionTypes|類型的客戶、 供應商或股票交易 （例如，發票信用額度附註、 等）|

### <a name="purchasing-schema"></a>購買結構描述

和內建項目購買的供應商的詳細資料。

|Table|Description|
|-----------------------------|---------------------|
|Suppliers|供應商 （組織） 的主要實體資料表|
|SupplierCategories|供應商 （例如 novelties、 玩具、 衣服封裝等） 的類別|
|SupplierTransactions|所有的財務交易供應商相關 （發票、 付款）。|
|PurchaseOrders|供應商採購訂單的詳細資料|
|PurchaseOrderLines|詳細資料行，從供應商採購訂單|

 
### <a name="sales-schema"></a>銷售的結構描述

客戶、 銷售人員，以及內建項目銷售額詳細資料。

|Table|Description|
|-----------------------------|---------------------|
|客戶|（「 組織 」 或 「 個人 」） 客戶的主要實體資料表|
|CustomerCategories|客戶 （ie 新式存放區、 超級市場等） 的類別|
|BuyingGroups|客戶組織可以是下購買能力的群組的一部分|
|CustomerTransactions|所有的財務交易客戶相關 （發票、 付款）。|
|SpecialDeals|特殊定價。 這可以包含固定的價格，折扣美元或折扣百分比。|
|Orders|客戶訂單的詳細資料|
|訂單產品線|從客戶訂單的詳細資料行|
|發票|客戶發票的詳細資料|
|InvoiceLines|從客戶發票詳細資料行|

### <a name="warehouse-schema"></a>倉儲結構描述

內建的項目、 其控股和交易的詳細資料。

|Table|Description|
|-----------------------------|---------------------|
|StockItems|內建項目的的主要實體資料表|
|StockItemHoldings|內建項目非暫時資料行。 這些是經常更新的資料行。|
|StockGroups|分類 （例如 novelties、 玩具、 edible novelties 等） 的內建項目群組|
|StockItemStockGroups|中的內建群組 （多對多） 所的內建的項目|
|色彩|內建項目可以 （選擇性） 具有色彩|
|PackageTypes|可封裝方式內建項目 （例如方塊 european carton、 棧板、 公斤、 等等。|
|StockItemTransactions|涵蓋所有的移動的所有內建項目 （回條、 銷售、 write-off） 的交易|
|VehicleTemperatures|定期記錄的溫度的車輛 chillers|
|ColdRoomTemperatures|定期記錄的原始空間 chillers 溫度|


## <a name="design-considerations"></a>設計考量

資料庫設計屬主觀看法，就不正確或錯誤來設計資料庫。 結構描述與此資料庫中的資料表會顯示您如何設計您自己的資料庫的想法。

### <a name="schema-design"></a>結構描述設計

WideWorldImporters 會使用少量的結構描述，讓您很容易了解資料庫系統，並示範資料庫原則。  

可能的情況下，資料庫會 collocates 通常到相同的結構描述，以減少複雜度聯結在一起查詢的資料表。

資料庫結構描述已經過程式碼產生的一系列的另一個資料庫 WWI_Preparation 中的中繼資料資料表為基礎。 這可讓 WideWorldImporters 非常高的設計一致性、 命名的一致性和完整性。 如需方式會產生結構描述的詳細資訊，請參閱原始程式碼：[寬-world-匯入工具/生平-資料庫-指令碼](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

### <a name="table-design"></a>資料表設計

- 所有資料表都有單一資料行主索引鍵聯結為了簡單起見。
- 所有結構描述、 資料表、 資料行、 索引和檢查條件約束具有擴充屬性可以用來識別物件或資料行的用途的描述。 記憶體最佳化資料表是這個例外狀況，因為它們目前不支援擴充的屬性。
- 除非具有相同的左側元件另一個非叢集的索引，否則，所有外部索引鍵會自動索引。
- 自動編號資料表中，根據序列。 這些順序會更輕鬆地使用適用於所有連結的伺服器和以上的身分識別資料行相似的環境。 記憶體最佳化資料表使用 IDENTITY 資料行，因為它們不支援 SQL Server 2016 中。
- 單一序列 (TransactionID) 用於這些資料表： CustomerTransactions、 SupplierTransactions 和 StockItemTransactions。 這會顯示一組資料表可以有單一序列的方式。
- 某些資料行擁有適當的預設值。

### <a name="security-schemas"></a>安全性結構描述

為了安全性，WideWorldImporters 不允許直接存取資料的結構描述的外部應用程式。 若要隔離存取，WideWorldImporters 會使用安全性存取結構描述不保留資料，但包含檢視和預存程序。 外部應用程式會使用安全性結構描述擷取可檢視的資料。  如此一來，使用者只可執行的檢視和預存程序中的安全存取結構描述

例如，此範例包含 Power BI 儀表板。 外部應用程式為 PowerBI 結構描述具有唯讀權限的使用者從 Power BI 閘道存取這些 Power BI 儀表板。  唯讀權限，使用者只需要 PowerBI 結構描述上的 SELECT 和 EXECUTE 權限。 視需要在生平資料庫管理員會指派這些權限。

## <a name="stored-procedures"></a>預存程序

預存程序會組織在結構描述中。 大部分的結構描述可用來設定或範例用途。

`Website`結構描述包含可由 Web 前端的預存程序。

`Reports`和`PowerBI`結構描述適用於 reporting services 和 power Bi 的用途。 我們鼓勵範例的任何延伸模組供報告用途使用這些結構描述。

### <a name="website-schema"></a>網站結構描述

這些是用戶端應用程式，例如 Web 前端的程序。

|程序|目的|
|-----------------------------|---------------------|
|ActivateWebsiteLogon|可讓個人 (從`Application.People`) 存取網站。|
|ChangePassword|變更使用者的密碼 （適用於不使用外部驗證機制的使用者）。|
|InsertCustomerOrders|允許插入 （包括訂單行） 的一或多個客戶訂單。|
|InvoiceCustomerOrders|根據要開發票的訂單的清單，並處理發票。|
|RecordColdRoomTemperatures|根據感應器資料清單，做為資料表值參數 (TVP)，並套用至資料`Warehouse.ColdRoomTemperatures`時態表。|
|RecordVehicleTemperature|採用 JSON 陣列，並使用它來更新`Warehouse.VehicleTemperatures`。|
|SearchForCustomers|搜尋客戶的名稱或部分名稱 （公司名稱或使用者名稱）。|
|SearchForPeople|人員的名稱或部分名稱的搜尋。|
|SearchForStockItems|依名稱或部分名稱或行銷註解的內建項目搜尋。|
|SearchForStockItemsByTags|搜尋所標記的內建項目。|
|SearchForSuppliers|依名稱或部分名稱 （公司名稱或使用者名稱） 的供應商的搜尋。|

### <a name="integration-schema"></a>整合的結構描述

ETL 程序會使用此結構描述中的預存程序。 取得所需的時間範圍的各種資料表所需的資料[ETL 封裝](wide-world-importers-perform-etl.md)。

### <a name="dataloadsimulation-schema"></a>DataLoadSimulation 結構描述

模擬的工作負載，將插入的銷售與購買項目。 主要的預存程序`PopulateDataToCurrentDate`，用來插入到目前日期為止的範例資料。

|程序|目的|
|-----------------------------|---------------------|
|Configuration_ApplyDataLoadSimulationProcedures|重新建立程序需要資料負載模擬。 這被必要帶到目前日期為止的資料。|
|Configuration_RemoveDataLoadSimulationProcedures|這會移除程序一次資料模擬完成之後。|
|DeactiveTemporalTablesBeforeDataLoad|移除所有時態表的時態本質和情況適用時，會套用觸發程序使其可以進行變更，就好像這些交易正在套用在非 sys 時態資料表允許較早的日期。|
|PopulateDataToCurrentDate|用來帶到目前日期為止的資料。 應在執行之前從初始備份還原資料庫之後的任何其他設定選項。|
|ReactivateTemporalTablesAfterDataLoad|重新建立時態表，包括資料的一致性檢查。 （會移除相關聯的觸發程序）。|


### <a name="application-schema"></a>應用程式結構描述

這些程序可用來設定範例。 它們會使用適用於企業版功能的範例，並將稽核新增的標準版版本和全文檢索索引。

|程序|目的|
|-----------------------------|---------------------|
|AddRoleMemberIfNonexistant|如果成員沒有角色中的角色加入成員|
|Configuration_ApplyAuditing|將稽核。 伺服器稽核被套用標準版資料庫;其他的資料庫稽核會新增適用於 enterprise edition。|
|Configuration_ApplyColumnstoreIndexing|適用於資料行存放區索引以`Sales.OrderLines`和`Sales.InvoiceLines`並適當地 reindexes。|
|Configuration_ApplyFullTextIndexing|套用至全文檢索索引`Application.People`， `Sales.Customers`， `Purchasing.Suppliers`，和`Warehouse.StockItems`。 取代`Website.SearchForPeople`， `Website.SearchForSuppliers`， `Website.SearchForCustomers`， `Website.SearchForStockItems`，`Website.SearchForStockItemsByTags`搭配使用全文檢索索引的取代程序。|
|Configuration_ApplyPartitioning|適用於資料表資料分割到`Sales.CustomerTransactions and `Purchasing.SupplierTransactions'，並重新整理的索引，以符合。|
|Configuration_ApplyRowLevelSecurity|套用至篩選客戶的資料列層級安全性，方式是銷售領域相關的角色。|
|Configuration_ConfigureForEnterpriseEdition|適用於資料行存放區索引、 全文檢索、 記憶體、 polybase，和資料分割。|
|Configuration_EnableInMemory|將記憶體最佳化檔案群組 （不使用在 Azure 中） 時，會取代`Warehouse.ColdRoomTemperatures`，`Warehouse.VehicleTemperatures`記憶體中的對等用法，並將資料移轉，就會重新建立`Website.OrderIDList`， `Website.OrderList`， `Website.OrderLineList`，`Website.SensorDataList`資料表類型，記憶體最佳化的對等用法，會卸除並重新建立程序`Website.InvoiceCustomerOrders`， `Website.InsertCustomerOrders`，和`Website.RecordColdRoomTemperatures`使用這些資料表類型。|
|Configuration_RemoveAuditing|移除稽核設定。|
|Configuration_RemoveRowLevelSecurity|移除資料列層級安全性 （這所需的設定變更相關聯的資料表）。|
|CreateRoleIfNonExistant|如果不存在，請建立資料庫角色。|


### <a name="sequences-schema"></a>順序結構描述

程序來設定資料庫中的順序。

|程序|目的|
|-----------------------------|---------------------|
|ReseedAllSequences|所有序列都呼叫程序 ReseedSequenceBeyondTableValue。|
|ReseedSequenceBeyondTableValue|用來在任何資料表，可使用相同的順序重新定位下一個順序值超過值。 （例如在 DBCC CHECKIDENT 針對識別資料行對等項目序列 (sequence)，但可能多個資料表)。|
