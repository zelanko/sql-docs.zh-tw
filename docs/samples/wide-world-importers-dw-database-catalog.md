---
title: WideWorldImporters OLAP 資料庫目錄-SQL |Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 08/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 757820680533cfa2eaff8403e2056f0a4d3b1a96
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39556948"
---
# <a name="wideworldimportersdw-database-catalog"></a>WideWorldImportersDW 資料庫目錄
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
結構描述、 資料表和預存程序 WideWorldImportersDW 資料庫中的說明。 

WideWorldImportersDW 資料庫使用於資料倉儲和分析處理。 WideWorldImporters 資料庫中產生並載入 WideWorldImportersDW 資料庫使用交易資料相關銷售和採購**每日 ETL 程序**。

WideWorldImportersDW 中的資料，因此鏡像 WideWorldImporters 中的資料，但資料表會以不同的方式組織。 雖然 WideWorldImporters 傳統的標準化結構描述，會使用 WideWorldImportersDW[星狀結構描述](https://wikipedia.org/wiki/Star_schema)其資料表設計的方法。 事實和維度資料表中，除了資料庫所包含的 ETL 程序中所使用的暫存資料表數目。

## <a name="schemas"></a>結構描述

不同類型的資料表會以三個結構描述組織。

|結構描述|描述|
|-----------------------------|---------------------|
|維度|維度資料表。|
|事實|事實資料表。|  
|整合|暫存資料表和其他物件所需的 ETL。|  

## <a name="tables"></a>資料表

以下列出的維度和事實資料表。 整合的結構描述中的資料表僅適用於使用 ETL 程序，並不會列出。

### <a name="dimension-tables"></a>維度資料表

WideWorldImportersDW 有下列維度資料表。 描述包含 WideWorldImporters 資料庫中的來源資料表的關聯性。

|Table|來源資料表|
|-----------------------------|---------------------|
|[縣/市]|`Application.Cities`, `Application.StateProvinces`, `Application.Countries`.|
|客戶|`Sales.Customers`, `Sales.BuyingGroups`, `Sales.CustomerCategories`.|
|date|新的資料表的資訊包括會計年度的日期 (根據年 11 月 1 日的會計年度開始)。|
|員工|`Application.People`。|
|StockItem|`Warehouse.StockItems`, `Warehouse.Colors`, `Warehouse.PackageType`.|
|供應商|`Purchasing.Suppliers`, `Purchasing.SupplierCategories`.|
|PaymentMethod|`Application.PaymentMethods`。|
|TransactionType|`Application.TransactionTypes`。|

### <a name="fact-tables"></a>事實資料表

WideWorldImportersDW 有以下的事實資料表。 描述會包含來源資料表的關聯性，WideWorldImporters 資料庫，以及分析/報告的查詢，每個事實資料表一般會搭配使用的類別。

|Table|來源資料表|範例分析|
|-----------------------------|---------------------|---------------------|
|單|`Sales.Orders` 和 `Sales.OrderLines`|銷售人員 」、 「 選擇器/packer 產能，，和在時間中挑選訂單。 此外，短的內建的情況下導致回訂單。|
|銷售|`Sales.Invoices` 和 `Sales.InvoiceLines`|銷售日期、 傳遞日期、 經過一段時間的獲利率、 銷售人員的獲利率。|
|採購單|`Purchasing.PurchaseOrderLines`|預期的與實際的前置時間|
|Transaction|`Sales.CustomerTransactions` 和 `Purchasing.SupplierTransactions`|測量問題日期與結束日期，以及數量。|
|移動|`Warehouse.StockTransactions`|經過一段時間的移動。|
|內建的保留|`Warehouse.StockItemHoldings`|庫存庫存和值。|

## <a name="stored-procedures"></a>預存程序

主要的 ETL 程序，並基於組態目的，會使用預存程序。

此範例的任何擴充功能，建議使用`Reports`Reporting Services 報表的結構描述和`PowerBI`Power BI 存取結構描述。

### <a name="application-schema"></a>應用程式結構描述

若要設定此範例會使用這些程序。 它們用來將 enterprise edition 的功能套用至標準版版本的範例中，加入 PolyBase，並重設 ETL。

|程序|目的|
|-----------------------------|---------------------|
|Configuration_ApplyPartitionedColumnstoreIndexing|適用於事實資料表的資料分割和資料行存放區索引。|
|Configuration_ConfigureForEnterpriseEdition|適用於資料分割資料行存放區索引和記憶體中。|
|Configuration_EnableInMemory|取代改善 ETL performance SCHEMA_ONLY 記憶體最佳化資料表中的接移資料表中整合。|
|Configuration_ApplyPolybase|設定外部資料來源、 檔案格式和資料表。|
|Configuration_PopulateLargeSaleTable|適用於企業版的變更，則會大量的資料填入 2012年日曆年度為額外的記錄。|
|Configuration_ReseedETL|移除現有的資料，並重新啟動的 ETL 種子。 這可讓重新擴展 OLAP 資料庫來比對 OLTP 資料庫中更新的資料列。|

### <a name="integration-schema"></a>整合的結構描述

ETL 程序中使用的程序可在這些類別：
- ETL 封裝-所有 Get * 程序的協助程式程序。
- ETL 封裝用於移轉的程序分段資料到 DW 資料表-所有移轉 * 程序。
- `PopulateDateDimensionForYear` -需要一年，並確保會在填入所有日期的年份`Dimension.Date`資料表。

### <a name="sequences-schema"></a>順序結構描述

若要設定資料庫中的序列的程序。

|程序|目的|
|-----------------------------|---------------------|
|ReseedAllSequences|呼叫程序`ReseedSequenceBeyondTableValue`所有序列 (sequence)。|
|ReseedSequenceBeyondTableValue|用來調整中使用的相同順序的任何資料表的位置超出值的下一個順序值。 (例如`DBCC CHECKIDENT`序列 (sequence)，但可能有多個資料表之間的身分識別的資料行相等的。)|
