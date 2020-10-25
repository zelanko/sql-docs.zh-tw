---
title: 在 SQL 範例中產生資料 WideWorldImporters
description: 使用這些 SQL 語句來產生範例資料，並將其匯入至 WideWorldImporters 範例資料庫的目前日期。
ms.date: 10/23/2020
ms.reviewer: ''
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: f60ad250ea68f58a98fb93da9f3c5853ad68bd47
ms.sourcegitcommit: 67befbf7435f256e766bbce6c1de57799e1db9ad
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/24/2020
ms.locfileid: "92523933"
---
# <a name="wideworldimporters-data-generation"></a>WideWorldImporters 資料產生
[!INCLUDE [SQL Server Azure SQL Database](../includes/applies-to-version/sql-asdb.md)]
WideWorldImporters 和 WideWorldImportersDW 資料庫的發行版本具有從2013年1月1日起，最多可達資料庫產生日期的資料。

當您使用這些範例資料庫時，您可能會想要包含較新的範例資料。

## <a name="data-generation-in-wideworldimporters"></a>WideWorldImporters 中的資料產生

若要產生最多至目前日期的範例資料：

1. 如果您尚未這麼做，請安裝 WideWorldImporters 資料庫的全新版本。 如需安裝指示，請參閱 [安裝和](wide-world-importers-oltp-install-configure.md)設定。
2. 在資料庫中執行下列語句：

    ```
        EXECUTE DataLoadSimulation.PopulateDataToCurrentDate
            @AverageNumberOfCustomerOrdersPerDay = 60,
            @SaturdayPercentageOfNormalWorkDay = 50,
            @SundayPercentageOfNormalWorkDay = 0,
            @IsSilentMode = 1,
            @AreDatesPrinted = 1;
    ```

    這個語句會將範例銷售和購買資料新增到資料庫，直到目前的日期為止。 它會依日期顯示資料產生的進度。 由於資料產生有隨機的因素，因此在執行之間產生的資料會有一些差異。

    若要增加或減少每日訂單所產生的資料量，請變更參數的值 `@AverageNumberOfCustomerOrdersPerDay` 。 使用參數 `@SaturdayPercentageOfNormalWorkDay` 並 `@SundayPercentageOfNormalWorkDay` 決定週末的訂單量。

> [!TIP]
> 在資料庫上強制 [延遲耐久性](../relational-databases/logs/control-transaction-durability.md) 可能會改善資料產生速度，特別是在資料庫交易記錄位於高延遲的儲存子系統上時。 使用延遲耐久性時，請留意潛在的 [資料遺失](../relational-databases/logs/control-transaction-durability.md#bkmk_DataLoss) 含意，並考慮只在資料產生期間啟用延遲的持久性。

## <a name="import-generated-data-in-wideworldimportersdw"></a>在 WideWorldImportersDW 中匯入產生的資料

若要將範例資料匯入到 WideWorldImportersDW OLAP 資料庫中的目前日期：

1. 使用上一節中的步驟執行 WideWorldImporters OLTP 資料庫中的資料產生邏輯。
2. 如果您還沒有這麼做，請安裝 WideWorldImportersDW 資料庫的全新版本。 如需安裝指示，請參閱 [安裝和](wide-world-importers-oltp-install-configure.md)設定。
3. 在資料庫中執行下列語句，以重設 OLAP 資料庫的種子：

    ```sql
    EXECUTE [Application].Configuration_ReseedETL
    ```

4. 執行 *每日 .ispac* SQL Server Integration Services 套件，以將資料匯入 OLAP 資料庫。 若要瞭解如何執行 ETL 作業，請參閱 [WIDEWORLDIMPORTERS etl 工作流程](wide-world-importers-perform-etl.md)。

## <a name="generate-data-in-wideworldimportersdw-for-performance-testing"></a>在 WideWorldImportersDW 中產生效能測試的資料

WideWorldImportersDW 可任意增加資料大小以進行效能測試。 例如，它可以增加資料大小以與叢集資料行存放區索引一起使用。

其中一項挑戰是讓下載的大小夠小，足以方便下載，但夠大，足以示範 SQL Server 的效能功能。 例如，只有當您使用較大量的資料列時，才會達到資料行存放區索引的重大優點。 

您可以使用此程式 `Application.Configuration_PopulateLargeSaleTable` 增加資料表中的資料列數目 `Fact.Sale` 。 資料列會插入2012日曆年度，以避免與從2013年1月1日開始的現有全球匯入工具資料發生衝突。

### <a name="procedure-details"></a>程式詳細資料

#### <a name="name"></a>名稱

`Application.Configuration_PopulateLargeSaleTable`

#### <a name="parameters"></a>參數

`@EstimatedRowsFor2012`**Bigint** (預設值為 12000000) 

#### <a name="result"></a>結果

大約將所需的資料列數插入 `Fact.Sale` 2012 年的資料表中。 人工程式會將資料列數限制為每天50000。 您可以變更這項限制，但此限制可協助您避免意外 overinflations 資料表。

此程式也會套用叢集資料行存放區索引（如果尚未套用）。
