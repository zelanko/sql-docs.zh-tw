---
title: WideWorldImporters OLTP 資料庫目錄-SQL |Microsoft Docs
description: 瞭解 WideWorldImporters 範例資料庫目錄的架構、資料表、預存程式和設計考慮。
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d4502a64a3822741c1928fcf6faee69d80d893d5
ms.sourcegitcommit: 59c09dbe29882cbed539229a9bc1de381a5a4471
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/11/2020
ms.locfileid: "79112400"
---
# <a name="wideworldimporters-database-catalog"></a>WideWorldImporters 資料庫目錄
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
WideWorldImporters 資料庫包含銷售和購買的所有交易資訊和每日資料，以及車輛和冷室的感應器資料。

## <a name="schemas"></a>結構描述

WideWorldImporters 會使用架構來進行不同的用途，例如儲存資料、定義使用者可以存取資料的方式，以及為數據倉儲開發和整合提供物件。

### <a name="data-schemas"></a>資料結構描述

這些架構包含資料。 所有其他架構都需要許多資料表，並位於應用程式架構中。

|結構描述|描述|
|-----------------------------|---------------------|
|Application|整個應用程式的使用者、連絡人和參數。 這也包含具有多個架構所使用之資料的參考資料表|
|購買|供應商的庫存商品購買和供應商的詳細資料。|  
|Sales|零售客戶的存貨專案銷售，以及客戶和銷售人員的詳細資料。 |  
|Warehouse|存貨專案庫存和交易。|  

### <a name="secure-access-schemas"></a>安全存取架構

這些架構會用於不允許直接存取資料表的外部應用程式。 其中包含外部應用程式所使用的視圖和預存程式。

|結構描述|描述|
|-----------------------------|---------------------|
|網站|從公司網站對資料庫的所有存取都是透過此架構。|
|報表|從 Reporting Services 報表對資料庫的所有存取都是透過此架構。|
|PowerBI|透過企業閘道從 Power BI 儀表板對資料庫的所有存取都是透過此架構。|

請注意，在初始版本的範例資料庫中，不會使用報表和 PowerBI 架構。 不過，建議您建立在此資料庫之上的所有 Reporting Services 和 Power BI 範例，以使用這些架構。

### <a name="development-schemas"></a>開發架構

特殊用途的架構

|結構描述|描述|
|-----------------------------|---------------------|
|整合|資料倉儲整合所需的物件和程式（亦即，將資料移轉至 WideWorldImportersDW 資料庫）。|
|序列|保留應用程式中所有資料表所使用的序列。|

## <a name="tables"></a>資料表

資料庫中的所有資料表都在資料架構中。

### <a name="application-schema"></a>應用程式架構

參數和人員（使用者和連絡人）的詳細資料，以及一般參考資料表（通用於多個其他架構）。

|Table|描述|
|-----------------------------|---------------------|
|SystemParameters|包含全系統可設定的參數。|
|人員|包含使用者名稱、連絡人資訊、使用應用程式的所有人員，以及供 Wide World 匯入者處理客戶組織的人員。 這包括員工、客戶、供應商和其他任何連絡人。 對於已獲得許可權可以使用系統或網站的人員，此資訊包括登入詳細資料。|
|城市|系統中儲存了許多位址，適用于人員、客戶組織的交貨位址、供應商的取貨位址等等。每次儲存位址時，就會參考此資料表中的城市。 每個城市也有一個空間位置。|
|StateProvinces|城市屬於州或省。 此表格包含這些資訊的詳細資料，包括描述每個州或省之界限的空間資料。|
|國家/地區|州或省是國家/地區的一部分。 此表格包含這些資訊的詳細資料，包括描述每個國家/地區界限的空間資料。|
|DeliveryMethods|遞送貨物專案的選項（例如卡車/van、文章、取貨、貨運等等）|
|PaymentMethods|進行付款的選擇（例如現金、支票、EFT 等等）|
|TransactionTypes|客戶、供應商或庫存交易的類型（例如發票、點數注意事項等）|

### <a name="purchasing-schema"></a>購買架構

供應商和庫存商品購買的詳細資料。

|Table|描述|
|-----------------------------|---------------------|
|Suppliers|供應商的主要實體資料表（組織）|
|SupplierCategories|供應商的類別（例如，novelties、玩具、服裝、包裝等等）|
|SupplierTransactions|與供應商相關的所有財務交易（發票、付款）|
|Purchaseorders.xaml|供應商採購訂單的詳細資料|
|PurchaseOrderLines|供應商採購訂單的詳細資料行|

 
### <a name="sales-schema"></a>銷售架構

客戶、銷售人員和庫存商品銷售的詳細資料。

|Table|描述|
|-----------------------------|---------------------|
|客戶|客戶的主要實體資料表（組織或個人）|
|CustomerCategories|客戶的類別（ie novelty 商店、超市等）|
|BuyingGroups|客戶組織可以是擁有更多購買能力的群組之一部分|
|CustomerTransactions|與客戶相關的所有財務交易（發票、付款）|
|SpecialDeals|特殊定價。 這可能包括固定價格、折扣（美元）或折扣百分比。|
|訂單|客戶訂單的詳細資料|
|OrderLines|客戶訂單的詳細資料行|
|發票|客戶發票的詳細資料|
|InvoiceLines|客戶發票的詳細資料行|

### <a name="warehouse-schema"></a>倉儲架構

存貨專案、其股票和交易的詳細資料。

|Table|描述|
|-----------------------------|---------------------|
|StockItems|庫存專案的主要實體資料表|
|StockItemHoldings|存貨專案的非時態性資料行。 這些是經常更新的資料行。|
|StockGroups|用於分類存貨專案的群組（例如，novelties、玩具、edible novelties 等等）|
|StockItemStockGroups|哪些存貨專案是哪些股票群組（多對多）|
|色彩|內建專案可以（選擇性）擁有色彩|
|Packagetypes>|可以封裝存貨專案的方式（例如，box、貨箱、托貨、公斤等等）。|
|StockItemTransactions|涵蓋所有股票專案所有移動的交易（收據、銷售、勾銷）|
|VehicleTemperatures|經常記錄的車輛溫度冷卻器|
|ColdRoomTemperatures|經常記錄的冷室冷卻器溫度|


## <a name="design-considerations"></a>設計考量

資料庫設計是主觀的，而且沒有適當或不正確的方式來設計資料庫。 此資料庫中的架構和資料表會顯示如何設計您自己的資料庫的想法。

### <a name="schema-design"></a>架構設計

WideWorldImporters 會使用少數的架構，讓您輕鬆瞭解資料庫系統並示範資料庫原則。  

如果可能的話，資料庫共置的資料表通常會一起查詢到相同的架構，以將聯結複雜度降到最低。

資料庫架構已根據另一個資料庫 WWI_Preparation 中一系列的中繼資料資料表來產生程式碼。 這讓 WideWorldImporters 的設計一致性、命名一致性和完整性變得非常高。 如需如何產生架構的詳細資訊，請參閱原始程式碼： [wide world-匯入工具/wwi-資料庫-腳本](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

### <a name="table-design"></a>資料表設計

- 所有資料表都有單一資料行主鍵，以方便聯結。
- 所有架構、資料表、資料行、索引和 check 條件約束都有描述擴充屬性，可用來識別物件或資料行的用途。 記憶體優化資料表是的例外狀況，因為它們目前不支援擴充屬性。
- 除非有另一個具有相同左側元件的非叢集索引，否則會自動為所有外鍵編制索引。
- 資料表中的自動編號是以序列為基礎。 在連結的伺服器和類似的環境中，這些順序比較容易使用，而不是識別資料行。 記憶體優化資料表會使用識別欄位，因為它們在 SQL Server 2016 中不支援。
- 下列資料表會使用單一序列（TransactionID）： CustomerTransactions、SupplierTransactions 和 StockItemTransactions。 這會示範一組資料表如何具有單一序列。
- 有些資料行具有適當的預設值。

### <a name="security-schemas"></a>安全性架構

基於安全性，WideWorldImporters 不允許外部應用程式直接存取資料結構描述。 若要隔離存取，WideWorldImporters 會使用不包含資料的安全性存取架構，但包含 views 和預存程式。 外部應用程式會使用安全性架構來抓取可以查看的資料。  如此一來，使用者只能在安全存取架構中執行 views 和預存程式

例如，此範例包含 Power BI 儀表板。 外部應用程式會以具有 PowerBI 架構唯讀許可權的使用者身分，從 Power BI 閘道存取這些 Power BI 儀表板。  針對 [唯讀] 許可權，使用者只需要 PowerBI 架構的 [選取] 和 [執行] 許可權。 WWI 的資料庫管理員會視需要指派這些許可權。

## <a name="stored-procedures"></a>預存程序

預存程式會組織成架構。 大部分的架構都是用於設定或範例用途。

`Website`架構包含 Web 前端可使用的預存程式。

`Reports`和`PowerBI`架構適用于 reporting services 和 PowerBI 用途。 建議使用這些架構的任何延伸模組，以供報告之用。

### <a name="website-schema"></a>網站架構

這些是用戶端應用程式（例如 Web 前端）所使用的程式。

|程序|目的|
|-----------------------------|---------------------|
|ActivateWebsiteLogon|允許個人（從`Application.People`）存取網站。|
|ChangePassword|變更使用者的密碼（適用于未使用外部驗證機制的使用者）。|
|InsertCustomerOrders|允許插入一或多個客戶訂單（包括訂單行）。|
|InvoiceCustomerOrders|取得要開票並處理發票的訂單清單。|
|RecordColdRoomTemperatures|採用感應器資料清單做為資料表值參數（TVP），並將資料套用至`Warehouse.ColdRoomTemperatures`時態表。|
|RecordVehicleTemperature|採用 JSON 陣列，並使用它來更新`Warehouse.VehicleTemperatures`。|
|SearchForCustomers|依名稱或部分名稱（公司名稱或人員名稱）來搜尋客戶。|
|SearchForPeople|依名稱或部分名稱搜尋人員。|
|SearchForStockItems|依名稱或部分名稱或行銷批註，搜尋股票專案。|
|SearchForStockItemsByTags|依標記搜尋存貨專案。|
|SearchForSuppliers|依名稱或部分名稱（公司名稱或人員名稱）來搜尋供應商。|

### <a name="integration-schema"></a>整合架構

ETL 進程會使用此架構中的預存程式。 他們會針對[ETL 套件](wide-world-importers-perform-etl.md)所需的時間範圍，取得不同資料表所需的資料。

### <a name="dataloadsimulation-schema"></a>DataLoadSimulation 架構

模擬插入銷售和購買的工作負載。 主要的預存程式`PopulateDataToCurrentDate`是，用來將範例資料插入到目前的日期為止。

|程序|目的|
|-----------------------------|---------------------|
|Configuration_ApplyDataLoadSimulationProcedures|重新建立資料負載模擬所需的程式。 這是將資料帶入目前日期的必要工作。|
|Configuration_RemoveDataLoadSimulationProcedures|這會在資料模擬完成後再次移除這些程式。|
|DeactivateTemporalTablesBeforeDataLoad|移除所有時態表的時態性性質，並在適當的情況下套用觸發程式，如此一來，就可以將變更視為比 sys 時態表所允許的更早日期來進行。|
|PopulateDataToCurrentDate|用來將資料帶入目前的日期。 從初始備份還原資料庫之後，應該在任何其他設定選項之前執行。|
|ReactivateTemporalTablesAfterDataLoad|重新建立時態表，包括檢查資料的一致性。 （移除相關聯的觸發程式）。|


### <a name="application-schema"></a>應用程式架構

這些程式是用來設定範例。 它們可用來將 enterprise edition 功能套用至範例的 standard edition 版本，也可以加入審核和全文檢索索引。

|程序|目的|
|-----------------------------|---------------------|
|AddRoleMemberIfNonexistant|如果成員尚未存在於角色中，則將成員新增至角色|
|Configuration_ApplyAuditing|加入審核。 適用于 standard edition 資料庫的伺服器審核;已針對 enterprise edition 新增額外的資料庫審核。|
|Configuration_ApplyColumnstoreIndexing|將資料行存放`Sales.OrderLines`區`Sales.InvoiceLines`索引編制套用至和，並適當地重新編制。|
|Configuration_ApplyFullTextIndexing|將全文檢索索引`Application.People`套用`Sales.Customers`至`Purchasing.Suppliers`、、 `Warehouse.StockItems`和。 `Website.SearchForStockItemsByTags`以`Website.SearchForPeople`使用`Website.SearchForSuppliers`全文`Website.SearchForCustomers`檢索`Website.SearchForStockItems`索引的取代程式來取代、、、和。|
|Configuration_ApplyPartitioning|將資料表資料分割`Sales.CustomerTransactions`套用`Purchasing.SupplierTransactions`至和，並重新排列要符合的索引。|
|Configuration_ApplyRowLevelSecurity|套用資料列層級安全性，依據銷售領域的相關角色來篩選客戶。|
|Configuration_ConfigureForEnterpriseEdition|套用資料行存放區索引、全文檢索、記憶體內部、polybase 和資料分割。|
|Configuration_EnableInMemory|新增記憶體優化檔案群組（在 Azure 中無法運作時）、將`Warehouse.ColdRoomTemperatures`取代`Warehouse.VehicleTemperatures`為記憶體中的對等專案，並遷移資料、重新`Website.OrderIDList`建立`Website.OrderList`、 `Website.OrderLineList`、 `Website.SensorDataList` 、具有記憶體優化對應的資料表類型、卸載並重新建立`Website.InvoiceCustomerOrders`使用`Website.InsertCustomerOrders`這些資料表`Website.RecordColdRoomTemperatures`類型的程式。|
|Configuration_RemoveAuditing|移除審核設定。|
|Configuration_RemoveRowLevelSecurity|移除資料列層級安全性設定（關聯資料表的變更需要此設定）。|
|CreateRoleIfNonExistant|建立資料庫角色（如果尚未存在的話）。|


### <a name="sequences-schema"></a>順序架構

在資料庫中設定順序的程式。

|程序|目的|
|-----------------------------|---------------------|
|ReseedAllSequences|針對所有序列呼叫程式 ReseedSequenceBeyondTableValue。|
|ReseedSequenceBeyondTableValue|用來將下一個序列值重新置放到任何使用相同序列之資料表中的值之後。 （像是適用于序列但跨可能多個資料表）之識別欄位的 DBCC CHECKIDENT。|
