---
title: WideWorldImporters OLAP 資料庫目錄-SQL |Microsoft Docs
description: 瞭解 WideWorldImportersDW 資料庫中用於資料倉儲和分析處理的架構、資料表和預存程式。
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=azuresqldb-mi-current'
ms.openlocfilehash: e246d516d3c05b9a2c6725f7fd3e3f787066b8aa
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461399"
---
# <a name="wideworldimportersdw-database-catalog"></a>WideWorldImportersDW 資料庫目錄
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
WideWorldImportersDW 資料庫中的架構、資料表和預存程式的說明。 

WideWorldImportersDW 資料庫用於資料倉儲和分析處理。 銷售和購買相關的交易資料會在 WideWorldImporters 資料庫中產生，並使用 **每日 ETL** 程式載入 WideWorldImportersDW 資料庫中。

因此，WideWorldImportersDW 中的資料會鏡像 WideWorldImporters 中的資料，但資料表的組織方式不同。 雖然 WideWorldImporters 具有傳統的正規化架構，但 WideWorldImportersDW 會使用 [星型架構](https://wikipedia.org/wiki/Star_schema) 方法來設計其資料表。 除了事實和維度資料表之外，資料庫還包含一些用於 ETL 程式的臨時表。

## <a name="schemas"></a>結構描述

不同類型的資料表會組織成三個架構。

|結構描述|描述|
|-----------------------------|---------------------|
|維度|維度資料表。|
|事實| 事實資料表。|  
|整合|ETL 所需的臨時表和其他物件。|  

## <a name="tables"></a>資料表

維度和事實資料表如下所示。 整合架構中的資料表只會用於 ETL 程式，且不會列出。

### <a name="dimension-tables"></a>維度資料表

WideWorldImportersDW 具有下列維度資料表。 描述包含與 WideWorldImporters 資料庫中之來源資料表的關聯性。

|Table|來源資料表|
|-----------------------------|---------------------|
|City|`Application.Cities`, `Application.StateProvinces`, `Application.Countries`.|
|客戶|`Sales.Customers`, `Sales.BuyingGroups`, `Sales.CustomerCategories`.|
|Date|新的資料表，其中包含日期的相關資訊，包括財務年度的 (，) 財務年度的第1年11月1日開始。|
|員工|`Application.People`.|
|StockItem|`Warehouse.StockItems`, `Warehouse.Colors`, `Warehouse.PackageType`.|
|供應商|`Purchasing.Suppliers`, `Purchasing.SupplierCategories`.|
|PaymentMethod|`Application.PaymentMethods`.|
|TransactionType|`Application.TransactionTypes`.|

### <a name="fact-tables"></a>事實資料表

WideWorldImportersDW 具有下列事實資料表。 描述包含與 WideWorldImporters 資料庫中之來源資料表的關聯性，以及每個事實資料表通常搭配使用的分析/報告查詢類別。

|Table|來源資料表|範例分析|
|-----------------------------|---------------------|---------------------|
|順序|`Sales.Orders` 和 `Sales.OrderLines`|銷售人員、選擇器/packer 生產力，以及準時挑選訂單。 此外，低庫存情況會導致訂單。|
|銷售|`Sales.Invoices` 和 `Sales.InvoiceLines`|銷售日期、交貨日期、一段時間的獲利率、依銷售人員的獲利率。|
|購買|`Purchasing.PurchaseOrderLines`|預期的 vs 實際前置時間|
|交易|`Sales.CustomerTransactions` 和 `Purchasing.SupplierTransactions`|測量問題日期與最終日期和金額。|
|移動|`Warehouse.StockTransactions`|經過一段時間的移動。|
|庫存保留|`Warehouse.StockItemHoldings`|內部股票層級和價值。|

## <a name="stored-procedures"></a>預存程序

預存程式主要用於 ETL 程式和設定用途。

建議任何範例延伸模組使用 `Reports` Reporting Services 報表的架構，以及 `PowerBI` Power BI 存取的架構。

### <a name="application-schema"></a>應用程式架構

這些程式是用來設定範例。 它們可用來將企業版功能套用至範例的 standard edition 版本、新增 PolyBase，以及重設種子。

|程序|目的|
|-----------------------------|---------------------|
|Configuration_ApplyPartitionedColumnstoreIndexing|適用于事實資料表的資料分割和資料行存放區索引。|
|Configuration_ConfigureForEnterpriseEdition|套用資料分割、資料行存放區索引和記憶體內部。|
|Configuration_EnableInMemory|以 SCHEMA_ONLY 記憶體優化資料表取代整合臨時表，以改善 ETL 效能。|
|Configuration_ApplyPolyBase|設定外部資料源、檔案格式和資料表。|
|Configuration_PopulateLargeSaleTable|套用企業版的變更，然後將2012日曆年度的大量資料填入為額外的歷程記錄。|
|Configuration_ReseedETL|移除現有的資料，並重新啟動 ETL 種子。 這可讓您重新填入 OLAP 資料庫，以符合 OLTP 資料庫中更新的資料列。|

### <a name="integration-schema"></a>整合架構

ETL 程式中使用的程式屬於下列類別：
- ETL 封裝的 Helper 程式-All Get * 程式。
- ETL 套件用來將暫存資料移轉至 DW 資料表的程式-所有遷移 * 程式。
- `PopulateDateDimensionForYear` -需要一年的時間，並確保該年度的所有日期都已填入 `Dimension.Date` 資料表中。

### <a name="sequences-schema"></a>順序架構

在資料庫中設定順序的程式。

|程序|目的|
|-----------------------------|---------------------|
|ReseedAllSequences|`ReseedSequenceBeyondTableValue`針對所有序列呼叫程式。|
|ReseedSequenceBeyondTableValue|用來將下一個序列值重新放置於任何使用相同順序之資料表中的值之後。  (，像是 `DBCC CHECKIDENT` 適用于序列但可能在多個資料表之間的識別資料行。 ) |
