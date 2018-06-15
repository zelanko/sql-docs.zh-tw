---
title: WideWorldImporters OLAP 資料庫目錄 SQL |Microsoft 文件
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
monikerRange: '>= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7b4533ec0667bc59317ba213578db7301c15b241
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33033855"
---
# <a name="wideworldimportersdw-database-catalog"></a>WideWorldImportersDW 資料庫目錄
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
結構描述、 資料表和預存程序 WideWorldImportersDW 資料庫中的說明。 

WideWorldImportersDW 資料庫用於資料倉儲和分析的處理。 交易資料的相關銷售額與購買項目會產生在 WideWorldImporters 資料庫中，並載入到 WideWorldImportersDW 資料庫使用**每日的 ETL 程序**。

因此 WideWorldImportersDW 中的資料會反映 WideWorldImporters 中的資料，但資料表會以不同的方式組織。 WideWorldImportersDW WideWorldImporters 具有傳統標準化結構描述，而使用[星狀結構描述](https://wikipedia.org/wiki/Star_schema)其資料表設計的方法。 事實和維度資料表中，除了資料庫所包含的數字所使用的暫存資料表的 ETL 程序中。

## <a name="schemas"></a>結構描述

三個結構描述會組織不同類型的資料表。

|結構描述|Description|
|-----------------------------|---------------------|
|維度|維度資料表。|
|事實|事實資料表。|  
|整合|暫存資料表與其他所需的 ETL 的物件。|  

## <a name="tables"></a>資料表

維度和事實資料表如下所示。 整合的結構描述中的資料表僅用於 ETL 程序，並不會列出。

### <a name="dimension-tables"></a>維度資料表

WideWorldImportersDW 有下列維度資料表。 描述 WideWorldImporters 資料庫中包含的來源資料表關聯性。

|Table|來源資料表|
|-----------------------------|---------------------|
|City|`Application.Cities`, `Application.StateProvinces`, `Application.Countries`.|
|客戶|`Sales.Customers`, `Sales.BuyingGroups`, `Sales.CustomerCategories`.|
|日期|新的資料表，包括財務年份的日期的相關資訊 (根據年 11 月 1 日開始的財務一年)。|
|員工|`Application.People`。|
|StockItem|`Warehouse.StockItems`, `Warehouse.Colors`, `Warehouse.PackageType`.|
|供應商|`Purchasing.Suppliers`, `Purchasing.SupplierCategories`.|
|PaymentMethod|`Application.PaymentMethods`。|
|TransactionType|`Application.TransactionTypes`。|

### <a name="fact-tables"></a>事實資料表

WideWorldImportersDW 有下列的事實資料表。 描述 WideWorldImporters 資料庫，以及每個事實資料表通常會搭配 reporting 分析/查詢的類別中包含的來源資料表關聯性。

|Table|來源資料表|範例分析|
|-----------------------------|---------------------|---------------------|
|單|`Sales.Orders`和`Sales.OrderLines`|銷售人員、 選擇器/packer 產能，然後在挑選訂單。 此外，低導致回訂單內建的情況。|
|銷售點|`Sales.Invoices`和`Sales.InvoiceLines`|銷售日期、 傳遞日期、 經過一段時間的獲利率、 依銷售員的獲利率。|
|採購單|`Purchasing.PurchaseOrderLines`|預期的與實際時間|
|Transaction|`Sales.CustomerTransactions`和`Purchasing.SupplierTransactions`|測量問題的日期與結束日期，與金額。|
|移動|`Warehouse.StockTransactions`|經過一段時間的移動。|
|內建控股公司|`Warehouse.StockItemHoldings`|現有的庫存和值。|

## <a name="stored-procedures"></a>預存程序

主要 ETL 處理序和基於組態目的，會使用預存程序。

我們鼓勵使用任何擴充功能範例的`Reports`Reporting Services 報表的結構描述和`PowerBI`Power BI 存取結構描述。

### <a name="application-schema"></a>應用程式結構描述

這些程序可用來設定範例。 它們可用來套用此範例中，標準版版本企業版功能加入 PolyBase，並重設 ETL。

|程序|目的|
|-----------------------------|---------------------|
|Configuration_ApplyPartitionedColumnstoreIndexing|適用於事實資料表的資料分割和資料行存放區索引。|
|Configuration_ConfigureForEnterpriseEdition|適用於資料分割資料行存放區索引和記憶體中。|
|Configuration_EnableInMemory|改善 ETL 效能 SCHEMA_ONLY 記憶體最佳化資料表，取代整合臨時區域資料表。|
|Configuration_ApplyPolybase|設定外部資料來源、 檔案格式和資料表。|
|Configuration_PopulateLargeSaleTable|適用於企業版的變更，則會更大量的資料填入 2012年日曆年度為額外的記錄。|
|Configuration_ReseedETL|移除現有的資料，並重新啟動 ETL 種子。 這樣可讓重新擴展 OLAP 資料庫符合 OLTP 資料庫中更新的資料列。|

### <a name="integration-schema"></a>整合的結構描述

ETL 程序中使用的程序可在這些分類中：
- ETL 封裝-所有 Get * 程序的協助程式程序。
- ETL 封裝用於移轉的程序在其中暫存資料 DW 資料表的所有移轉 * 程序。
- `PopulateDateDimensionForYear` -採用一年，並確保該年的所有日期會以都擴展`Dimension.Date`資料表。

### <a name="sequences-schema"></a>順序結構描述

程序來設定資料庫中的順序。

|程序|目的|
|-----------------------------|---------------------|
|ReseedAllSequences|呼叫程序`ReseedSequenceBeyondTableValue`所有序列 (sequence)。|
|ReseedSequenceBeyondTableValue|用來在任何資料表，可使用相同的順序重新定位下一個順序值超過值。 (例如`DBCC CHECKIDENT`針對識別資料行對等項目序列 (sequence)，但可能多個資料表。)|
