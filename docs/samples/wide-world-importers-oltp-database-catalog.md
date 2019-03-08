---
title: WideWorldImporters OLTP 資料庫目錄-SQL |Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e26299f221facfc6828369e1c75225f206937eb4
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579578"
---
# <a name="wideworldimporters-database-catalog"></a>WideWorldImporters 資料庫目錄
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
WideWorldImporters 資料庫包含所有的交易資訊和銷售和採購，每日資料，以及與冷聊天室的感應器資料。

## <a name="schemas"></a>結構描述

WideWorldImporters 用於不同的用途，例如儲存資料、 定義使用者如何存取資料，以及提供資料倉儲開發和整合物件的結構描述。

### <a name="data-schemas"></a>資料結構描述

這些結構描述包含的資料。 一些資料表所需的所有其他的結構描述，而位於應用程式結構描述中。

|結構描述|描述|
|-----------------------------|---------------------|
|應用程式|整個應用程式的使用者、 連絡人和參數。 這也會包含參考資料表的資料，可由多個結構描述|
|Purchasing|從供應商以及供應商的詳細購買股票項目。|  
|Sales|內建項目銷售零售客戶和客戶與銷售人員相關的詳細資料。 |  
|Warehouse|內建的項目清查和交易。|  

### <a name="secure-access-schemas"></a>安全存取結構描述

這些結構描述用於不允許直接存取資料表的外部應用程式。 它們包含檢視和外部的應用程式所使用的預存程序。

|結構描述|描述|
|-----------------------------|---------------------|
|網站|所有資料庫的存取權從公司網站都是透過此結構描述。|
|報表|所有資料庫的存取權從 Reporting Services 報表都是透過此結構描述。|
|PowerBI|所有資料庫的存取權透過企業閘道的 Power BI 儀表板都是透過此結構描述。|

請注意，報表和 power Bi 的範例資料庫的初始版本中不使用結構描述。 不過，此資料庫為基礎的所有 Reporting Services 和 Power BI 範例，建議使用這些結構描述。

### <a name="development-schemas"></a>開發結構描述

特殊用途的結構描述

|結構描述|描述|
|-----------------------------|---------------------|
|整合|物件和資料倉儲整合所需的程序 （也就是將資料移轉至 WideWorldImportersDW 資料庫）。|
|序列|保存應用程式中的所有資料表所都使用的序列。|

## <a name="tables"></a>資料表

在資料庫中的所有資料表都都在資料結構描述中。

### <a name="application-schema"></a>應用程式結構描述

參數和使用者 （使用者和連絡人），以及常見的參考資料表 （這常見於多個其他結構描述） 的詳細資料。

|資料表|描述|
|-----------------------------|---------------------|
|SystemParameters|包含全系統的可設定的參數。|
|人員|包含使用者名稱，所有使用應用程式，及 Wide World Importers 會處理在客戶組織之人員的連絡資訊。 這包括員工、 客戶、 供應商和其他的任何連絡人。 已授與使用的系統或網站的權限的人員，資訊會包括登入詳細資料。|
|城市|有多個地址儲存在系統中，對人來說，客戶組織傳遞地址，收取位址供應商，依此類推。只要儲存地址，沒有這個資料表中的城市的參考。 另外還有每個城市的空間位置。|
|StateProvinces|城市是州或是省份的一部分。 這個資料表會有這些包括描述界限的空間資料的詳細資料，每個州或省。|
|國家/地區|州或省是一部分的國家/地區。 這個資料表有這些包括描述每個國家/地區的界限的空間資料的詳細資料。|
|DeliveryMethods|選擇提供內建項目 （例如貨車/van、 post、 pickup，courier 等）|
|PaymentMethods|付款選項 (例如現金、 核取，EFT，等等。)|
|TransactionTypes|類型的客戶、 供應商或股票交易 （例如，發票、 通知單等等。）|

### <a name="purchasing-schema"></a>購買結構描述

供應商和的股票項目購買的詳細資料。

|資料表|描述|
|-----------------------------|---------------------|
|Suppliers|供應商 （組織） 的主要實體資料表|
|SupplierCategories|類別目錄的供應商 （例如 novelties、 玩具、 衣服、 封裝、 等等。）|
|SupplierTransactions|所有的財務交易供應商相關 （發票付款）。|
|PurchaseOrders|供應商採購訂單的詳細資料|
|PurchaseOrderLines|詳細資料行，從供應商採購訂單|

 
### <a name="sales-schema"></a>Sales 結構描述

客戶、 銷售人員，以及股票項目銷售詳細資料。

|資料表|描述|
|-----------------------------|---------------------|
|客戶|客戶 （組織或個人） 的主要實體資料表|
|CustomerCategories|類別 （亦即新奇存放區、 超級市場等） 的客戶|
|BuyingGroups|客戶組織可以執行更佳的購買能力的群組的一部分|
|CustomerTransactions|所有的財務交易客戶相關 （發票付款）。|
|SpecialDeals|優惠的價格。 這可以包含固定的價格、 折扣金額或折扣百分比。|
|Orders|客戶訂單的詳細資料|
|OrderLines|從客戶訂單的詳細資料行|
|發票|客戶發票的詳細資料|
|InvoiceLines|從客戶發票的詳細資料行|

### <a name="warehouse-schema"></a>倉儲結構描述

內建的項目、 其 holdings 和交易的詳細資料。

|資料表|描述|
|-----------------------------|---------------------|
|StockItems|主要實體資料表的內建的項目|
|StockItemHoldings|內建的項目有非時態性的資料行。 這些是經常更新的資料行。|
|StockGroups|用於將項目 （例如 novelties、 玩具、 edible novelties 等） 的內建的分類群組|
|StockItemStockGroups|內建的項目會在其中內建群組 （多對多）|
|色彩|內建的項目 （選擇性） 可以有色彩|
|PackageTypes|內建項目的方式可以封裝 （例如，方塊、 carton makers association，平板，kg 等。|
|StockItemTransactions|涵蓋所有的移動的所有內建項目 （回條、 銷售、 write-off） 的交易|
|VehicleTemperatures|車輛 chiller 的定期記錄的溫度|
|ColdRoomTemperatures|定期記錄的冷聊天室 chiller 的溫度|


## <a name="design-considerations"></a>設計考量

資料庫設計屬主觀看法，並沒有任何正確或錯誤的方法，來設計資料庫。 結構描述與此資料庫中的資料表會顯示您如何設計您自己的資料庫的想法。

### <a name="schema-design"></a>結構描述設計

WideWorldImporters 會使用一小部分的結構描述，讓您可以很容易了解資料庫系統，並示範資料庫原則。  

可能的話，資料庫來共置到相同的結構描述，將聯結複雜性降至最低經常一起查詢的資料表。

資料庫結構描述已產生程式碼以一系列的另一個資料庫 WWI_Preparation 中的中繼資料資料表。 這可讓 WideWorldImporters 非常高度的設計的一致性、 命名的一致性和完整性。 如需如何產生結構描述的詳細資訊，請參閱原始程式碼：[寬-世界-匯入工具/wwi-資料庫-指令碼](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

### <a name="table-design"></a>資料表設計

- 所有資料表都具有單一資料行加入簡單的主索引鍵。
- 所有結構描述、 資料表、 資料行、 索引和 check 條件約束都有擴充屬性，可用來識別物件或資料行的用途的描述。 記憶體最佳化資料表是這樣的例外狀況，因為它們目前不支援擴充的屬性。
- 除非有另一個非叢集索引具有相同的左側部分，會自動索引所有外部索引鍵。
- 自動編號資料表中，根據序列。 這些序列較容易在連結的伺服器與相似的環境，以上的身分識別資料行使用。 因為它們不支援 SQL Server 2016 中，記憶體最佳化資料表會使用身分識別資料行。
- 這些資料表會使用單一序列 (TransactionID):CustomerTransactions、 SupplierTransactions 和 StockItemTransactions。 這示範了一組資料表可以有單一序列的方式。
- 某些資料行具有適當的預設值。

### <a name="security-schemas"></a>安全性結構描述

為了安全性，WideWorldImporters 不允許直接存取資料的結構描述的外部應用程式。 若要隔離存取，WideWorldImporters 會使用未保留的資料，但包含檢視和預存程序的安全性存取結構描述。 外部應用程式會使用安全性結構描述，來擷取可檢視的資料。  如此一來，使用者只能執行之檢視和預存程序中的安全存取結構描述

例如，此範例包含 Power BI 儀表板。 為 power Bi 的結構描述具有唯讀權限的使用者，外部應用程式會存取這些 Power BI 儀表板從 Power BI 閘道。  唯讀權限，使用者只需要在 power Bi 的結構描述的 SELECT 和 EXECUTE 權限。 視需要資料庫管理員在 WWI 會指派這些權限。

## <a name="stored-procedures"></a>預存程序

預存程序被按照結構描述。 大部分的結構描述用於組態或範例的目的。

`Website`結構描述中包含可由 Web 前端的預存程序。

`Reports`和`PowerBI`結構描述供 reporting services 和 power Bi 之用。 任何延伸模組的範例，建議針對報告目的而使用這些結構描述。

### <a name="website-schema"></a>網站結構描述

這些是由用戶端應用程式，例如 Web 前端的程序。

|程序|用途|
|-----------------------------|---------------------|
|ActivateWebsiteLogon|可讓個人 (從`Application.People`) 擁有網站的存取權。|
|ChangePassword|變更使用者的密碼 （適用於不使用外部驗證機制的使用者）。|
|InsertCustomerOrders|允許插入 （包括訂單明細） 的一或多個客戶訂單。|
|InvoiceCustomerOrders|會採用一份訂單開立發票，並處理發票。|
|RecordColdRoomTemperatures|會使用感應器資料清單，作為資料表值參數 (TVP)，並套用資料`Warehouse.ColdRoomTemperatures`時態表。|
|RecordVehicleTemperature|會採用 JSON 陣列，並使用它來更新`Warehouse.VehicleTemperatures`。|
|SearchForCustomers|依名稱或部分名稱 （公司名稱或使用者名稱） 的客戶搜尋。|
|SearchForPeople|搜尋依名稱或名稱一部分的人員。|
|SearchForStockItems|依名稱或部分名稱或行銷註解的股票項目搜尋。|
|SearchForStockItemsByTags|依標記的股票項目搜尋。|
|SearchForSuppliers|依名稱或部分名稱 （公司名稱或使用者名稱） 的供應商的搜尋。|

### <a name="integration-schema"></a>整合的結構描述

在這個結構描述的預存程序會使用 ETL 程序。 他們會取得從各個資料表所需的時間範圍所需的資料[ETL 封裝](wide-world-importers-perform-etl.md)。

### <a name="dataloadsimulation-schema"></a>DataLoadSimulation 結構描述

模擬的工作負載，將銷售及購買項目。 主要的預存程序`PopulateDataToCurrentDate`，這用來插入到目前日期為止的範例資料。

|程序|用途|
|-----------------------------|---------------------|
|Configuration_ApplyDataLoadSimulationProcedures|重新建立程序所需的資料負載模擬。 這需要將到目前日期為止的資料。|
|Configuration_RemoveDataLoadSimulationProcedures|這會移除程序一次資料模擬完成之後。|
|DeactivateTemporalTablesBeforeDataLoad|移除所有時態表的時態性的本質和情況適用時，會套用觸發程序，以便可以進行變更，就好像它們在套用比 sys 時態資料表允許較早的日期。|
|PopulateDataToCurrentDate|用來帶到目前日期為止的資料。 應該在從初始的備份還原資料庫之後的任何其他設定選項之前執行。|
|ReactivateTemporalTablesAfterDataLoad|重新建立時態表，包括資料的一致性檢查。 （移除相關聯的觸發程序）。|


### <a name="application-schema"></a>應用程式結構描述

若要設定此範例會使用這些程序。 它們用來套用至標準版版本的範例，並將稽核及全文檢索索引的 enterprise edition 的功能。

|程序|用途|
|-----------------------------|---------------------|
|AddRoleMemberIfNonexistant|如果成員還未在角色中，將成員新增至角色|
|Configuration_ApplyAuditing|Adds 稽核。 伺服器稽核被適用於標準版資料庫;其他的資料庫稽核會新增適用於 enterprise edition。|
|Configuration_ApplyColumnstoreIndexing|適用於資料行存放區索引`Sales.OrderLines`和`Sales.InvoiceLines`和重新適當地編製索引。|
|Configuration_ApplyFullTextIndexing|適用於全文檢索索引`Application.People`， `Sales.Customers`， `Purchasing.Suppliers`，和`Warehouse.StockItems`。 會取代`Website.SearchForPeople`， `Website.SearchForSuppliers`， `Website.SearchForCustomers`， `Website.SearchForStockItems`，`Website.SearchForStockItemsByTags`搭配使用全文檢索索引的取代程序。|
|Configuration_ApplyPartitioning|適用於資料表資料分割`Sales.CustomerTransactions`和`Purchasing.SupplierTransactions`，並重新排列以符合索引。|
|Configuration_ApplyRowLevelSecurity|套用至篩選客戶的資料列層級安全性，方式是銷售領域相關的角色。|
|Configuration_ConfigureForEnterpriseEdition|適用於資料行存放區索引、 全文檢索、 記憶體、 polybase 及資料分割。|
|Configuration_EnableInMemory|新增記憶體最佳化檔案群組 （當不在 Azure 中運作） 時，會取代`Warehouse.ColdRoomTemperatures`，`Warehouse.VehicleTemperatures`與記憶體中對等項目，並將資料移轉，就會重新建立`Website.OrderIDList`， `Website.OrderList`， `Website.OrderLineList`，`Website.SensorDataList`資料表使用的類型記憶體最佳化對等項目、 卸除和重新建立程序`Website.InvoiceCustomerOrders`， `Website.InsertCustomerOrders`，和`Website.RecordColdRoomTemperatures`使用這些資料表類型。|
|Configuration_RemoveAuditing|移除的稽核設定。|
|Configuration_RemoveRowLevelSecurity|移除資料列層級安全性 （這所需的設定變更相關聯的資料表）。|
|CreateRoleIfNonExistant|如果不存在，請建立資料庫角色。|


### <a name="sequences-schema"></a>順序結構描述

若要設定資料庫中的序列的程序。

|程序|用途|
|-----------------------------|---------------------|
|ReseedAllSequences|呼叫程序 ReseedSequenceBeyondTableValue 所有序列 (sequence)。|
|ReseedSequenceBeyondTableValue|用來調整中使用的相同順序的任何資料表的位置超出值的下一個順序值。 （例如 DBCC CHECKIDENT 的身分識別資料行對等項目序列 (sequence)，但可能有多個資料表之間)。|
