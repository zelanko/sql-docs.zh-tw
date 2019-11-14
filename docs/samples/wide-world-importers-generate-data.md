---
title: 在 SQL 範例中產生資料 WideWorldImporters
ms.date: 04/04/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 0f880ea881b53c2600fb1fffdf7da5d16ab8d423
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056278"
---
# <a name="wideworldimporters-data-generation"></a>WideWorldImporters 資料產生
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
WideWorldImporters 和 WideWorldImportersDW 資料庫的發行版本具有2013年1月1日的資料，最多可達產生資料庫的日期。

當您使用這些範例資料庫時，您可能會想要包含較新的範例資料。

## <a name="data-generation-in-wideworldimporters"></a>WideWorldImporters 中的資料產生

若要產生最多到目前日期的範例資料：

1. 如果您尚未這麼做，請安裝 WideWorldImporters 資料庫的全新版本。 如需安裝指示，請參閱[安裝和](wide-world-importers-oltp-install-configure.md)設定。
2. 在資料庫中執行下列語句：

    ```
        EXECUTE DataLoadSimulation.PopulateDataToCurrentDate
            @AverageNumberOfCustomerOrdersPerDay = 60,
            @SaturdayPercentageOfNormalWorkDay = 50,
            @SundayPercentageOfNormalWorkDay = 0,
            @IsSilentMode = 1,
            @AreDatesPrinted = 1;
    ```

    此語句會將範例銷售和購買資料新增至資料庫，直到目前的日期為止。 它會依日顯示資料產生的進度。 資料產生可能需要大約10分鐘的時間，每年需要資料。 由於資料產生中的隨機因素，在執行之間產生的資料會有一些差異。

    若要增加或減少每天針對訂單產生的資料量，請將參數的值變更 `@AverageNumberOfCustomerOrdersPerDay`。 使用 `@SaturdayPercentageOfNormalWorkDay` 和 `@SundayPercentageOfNormalWorkDay` 參數，以決定週末日期的訂單量。

## <a name="import-generated-data-in-wideworldimportersdw"></a>在 WideWorldImportersDW 中匯入產生的資料

若要將範例資料匯入到 WideWorldImportersDW OLAP 資料庫中的目前日期：

1. 使用上一節中的步驟，在 WideWorldImporters OLTP 資料庫中執行資料產生邏輯。
2. 如果您還沒有這麼做，請安裝 WideWorldImportersDW 資料庫的全新版本。 如需安裝指示，請參閱[安裝和](wide-world-importers-oltp-install-configure.md)設定。
3. 藉由在資料庫中執行下列語句，重新植入 OLAP 資料庫：

    ```sql
    EXECUTE [Application].Configuration_ReseedETL
    ```

4. 執行*每日的 .ispac* SQL Server Integration Services 封裝，將資料匯入 OLAP 資料庫。 若要瞭解如何執行 ETL 作業，請參閱[WIDEWORLDIMPORTERS ETL 工作流程](wide-world-importers-perform-etl.md)。

## <a name="generate-data-in-wideworldimportersdw-for-performance-testing"></a>在 WideWorldImportersDW 中產生資料以進行效能測試

WideWorldImportersDW 可以任意增加資料大小以進行效能測試。 例如，它可以增加資料大小以用於叢集資料行存放區索引。

其中一項挑戰是讓下載的大小變得很小，以方便下載，但夠大，足以示範 SQL Server 的效能功能。 例如，資料行存放區索引的重大優點只有在您使用較大量的資料列時才會達成。 

您可以使用 `Application.Configuration_PopulateLargeSaleTable` 程式來增加 `Fact.Sale` 資料表中的資料列數目。 資料列會插入2012行事歷年度，以避免與從2013年1月1日開始的現有全球匯入工具資料發生衝突。

### <a name="procedure-details"></a>程式詳細資料

#### <a name="name"></a>[名稱]

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>參數

  `@EstimatedRowsFor2012` **Bigint** （預設值為12000000）

#### <a name="result"></a>結果

大約在2012年中，會將所需的資料列數插入 `Fact.Sale` 資料表。 這個程式會將資料列的數目限制為每天50000。 您可以變更這項限制，但此限制可協助您避免意外 overinflations 資料表。

此程式也會套用叢集資料行存放區索引（如果尚未套用）。
