---
title: WideWorldImporters OLAP 資料庫目錄-SQL |Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 7c3da2af72743cc8f89273bfce24fe74fc7e4dc1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68104291"
---
# <a name="wideworldimportersdw-database-catalog"></a>WideWorldImportersDW 資料庫目錄
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
WideWorldImportersDW 資料庫中的架構、資料表和預存程式的說明。 

WideWorldImportersDW 資料庫用於資料倉儲和分析處理。 關於銷售和購買的交易資料是在 WideWorldImporters 資料庫中產生，並使用**每日 ETL**程式載入 WideWorldImportersDW 資料庫中。

因此，WideWorldImportersDW 中的資料會鏡像 WideWorldImporters 中的資料，但資料表的組織方式不同。 雖然 WideWorldImporters 具有傳統的正規化架構，但 WideWorldImportersDW 會針對其資料表設計使用[星型架構](https://wikipedia.org/wiki/Star_schema)方法。 除了事實和維度資料表以外，資料庫還包含一些在 ETL 進程中使用的臨時表。

## <a name="schemas"></a>結構描述

不同類型的資料表會組織成三個架構。

|結構描述|描述|
|-----------------------------|---------------------|
|維度|維度資料表。|
|事實|事實資料表。|  
|整合|ETL 所需的臨時表和其他物件。|  

## <a name="tables"></a>資料表

以下列出維度和事實資料表。 整合架構中的資料表僅供 ETL 程式使用，而且不會列出。

### <a name="dimension-tables"></a>維度資料表

WideWorldImportersDW 具有下列維度資料表。 此描述包含與 WideWorldImporters 資料庫中來源資料表的關聯性。

|Table|來源資料表|
|-----------------------------|---------------------|
|City|`Application.Cities`, `Application.StateProvinces`, `Application.Countries`.|
|客戶|`Sales.Customers`, `Sales.BuyingGroups`, `Sales.CustomerCategories`.|
|Date|含有日期相關資訊的新資料表，包括財務年度（以財務年度的第1年11月開始）。|
|員工|`Application.People`.|
|StockItem|`Warehouse.StockItems`, `Warehouse.Colors`, `Warehouse.PackageType`.|
|供應商|`Purchasing.Suppliers`, `Purchasing.SupplierCategories`.|
|PaymentMethod|`Application.PaymentMethods`.|
|TransactionType|`Application.TransactionTypes`.|

### <a name="fact-tables"></a>事實資料表

WideWorldImportersDW 具有下列事實資料表。 此描述包含與 WideWorldImporters 資料庫中來源資料表的關聯性，以及每個事實資料表通常用於的分析/報告查詢類別。

|Table|來源資料表|範例分析|
|-----------------------------|---------------------|---------------------|
|單|`Sales.Orders` 和 `Sales.OrderLines`|銷售人員、選擇器/packer 生產力，以及挑選訂單的時間。 此外，低庫存狀況也會導致訂單。|
|銷售|`Sales.Invoices` 和 `Sales.InvoiceLines`|銷售的日期、傳遞日期、一段時間的獲利，以及銷售人員的獲利。|
|購買|`Purchasing.PurchaseOrderLines`|預期的 vs 實際前置時間|
|交易|`Sales.CustomerTransactions` 和 `Purchasing.SupplierTransactions`|測量問題日期與最終日期和金額。|
|引起|`Warehouse.StockTransactions`|一段時間的移動。|
|庫存持有|`Warehouse.StockItemHoldings`|庫存量與價值。|

## <a name="stored-procedures"></a>預存程序

預存程式主要用於 ETL 進程和設定用途。

建議將範例的任何延伸模組用於 Reporting Services 報表`Reports`的架構，並使用 Power BI `PowerBI`存取的架構。

### <a name="application-schema"></a>應用程式架構

這些程式是用來設定範例。 它們可用來將 enterprise edition 功能套用至範例的 standard edition 版本、新增 PolyBase，以及重新植入 ETL。

|程序|目的|
|-----------------------------|---------------------|
|Configuration_ApplyPartitionedColumnstoreIndexing|適用于事實資料表的資料分割和資料行存放區索引。|
|Configuration_ConfigureForEnterpriseEdition|套用資料分割、資料行存放區索引和記憶體內部。|
|Configuration_EnableInMemory|以 SCHEMA_ONLY 的記憶體優化資料表取代整合臨時表，以改善 ETL 效能。|
|Configuration_ApplyPolyBase|設定外部資料源、檔案格式和資料表。|
|Configuration_PopulateLargeSaleTable|會套用 enterprise edition 變更，然後將2012行事歷年度的大量資料填入額外的歷程記錄。|
|Configuration_ReseedETL|移除現有的資料，並重新啟動 ETL 種子。 這可讓重新填入 OLAP 資料庫，以符合 OLTP 資料庫中更新的資料列。|

### <a name="integration-schema"></a>整合架構

ETL 進程中使用的程式分為下列幾個類別：
- ETL 套件的 Helper 程式-所有取得 * 程式。
- ETL 封裝用來將分段資料移轉至 DW 資料表的程式-所有遷移 * 程式。
- `PopulateDateDimensionForYear`-需要一年的時間，並確保該年份的所有日期都已`Dimension.Date`填入資料表中。

### <a name="sequences-schema"></a>順序架構

在資料庫中設定順序的程式。

|程序|目的|
|-----------------------------|---------------------|
|ReseedAllSequences|`ReseedSequenceBeyondTableValue`針對所有序列呼叫程式。|
|ReseedSequenceBeyondTableValue|用來將下一個序列值重新置放到任何使用相同序列之資料表中的值之後。 （像是`DBCC CHECKIDENT`適用于順序的對應識別欄位，但可能跨多個資料表）。|
