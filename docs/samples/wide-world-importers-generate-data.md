---
title: WideWorldImporters 產生資料-SQL 範例資料庫 |Microsoft 文件
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6ace1f771ef3a77a6f7db0072442affe181d7872
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
---
# <a name="wideworldimporters-data-generation"></a>WideWorldImporters 資料產生
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
WideWorldImporters 和 WideWorldImportersDW 資料庫發行的版本有從 2013 年 1 月 1 日到整天資料庫所產生的資料。

當您使用這些範例資料庫時，您可能想要包含較新的範例資料。

## <a name="data-generation-in-wideworldimporters"></a>WideWorldImporters 中的資料產生

若要產生到目前日期為止的範例資料：

1. 如果您尚未這樣做，請安裝 WideWorldImporters 資料庫的全新版本。 如需安裝指示，請參閱[安裝和設定](wide-world-importers-oltp-install-configure.md)。
2. 在資料庫中執行下列陳述式：

    ```
        EXECUTE DataLoadSimulation.PopulateDataToCurrentDate
            @AverageNumberOfCustomerOrdersPerDay = 60,
            @SaturdayPercentageOfNormalWorkDay = 50,
            @SundayPercentageOfNormalWorkDay = 0,
            @IsSilentMode = 1,
            @AreDatesPrinted = 1;
    ```

    這個陳述式將加入資料庫，到目前日期為止的範例銷售和訂單資料。 它將顯示進度資料產生的一天。 產生資料可能需要大約 10 分鐘讓需要資料每年。 資料產生的隨機因素，因為有一些差異會產生執行之間的資料。

    若要增加或減少資料產生的每日的訂單數量，將變更參數的值`@AverageNumberOfCustomerOrdersPerDay`。 您可以使用參數`@SaturdayPercentageOfNormalWorkDay`和`@SundayPercentageOfNormalWorkDay`判斷週末訂單量。

## <a name="import-generated-data-in-wideworldimportersdw"></a>產生的匯入 WideWorldImportersDW 資料

若要匯入到 WideWorldImportersDW OLAP 資料庫中目前的日期為止的範例資料：

1. 使用上一節中的步驟，WideWorldImporters OLTP 資料庫中執行的資料產生邏輯。
2. 如果您尚未尚未這麼做，請安裝 WideWorldImportersDW 資料庫的全新版本。 如需安裝指示，請參閱[安裝和設定](wide-world-importers-oltp-install-configure.md)。
3. Reseed OLAP 資料庫的資料庫中執行下列陳述式：

    ```sql
    EXECUTE [Application].Configuration_ReseedETL
    ```

4. 執行*每日 ETL.ispac* OLAP 資料庫將資料匯入的 SQL Server Integration Services 封裝。 若要了解如何執行 ETL 工作，請參閱[WideWorldImporters ETL 工作流程](wide-world-importers-perform-etl.md)。

## <a name="generate-data-in-wideworldimportersdw-for-performance-testing"></a>產生 WideWorldImportersDW 中的資料效能測試

WideWorldImportersDW 可以任意增加效能測試的資料的大小。 例如，它可以增加要使用具有叢集資料行存放區索引的資料大小。

挑戰之一就是將下載的大小夠小，無法下載輕鬆，但大足以示範 SQL Server 效能功能。 比方說，只有當您使用較大的數字的資料列時，可達到重要的資料行存放區索引的優點。 

您可以使用`Application.Configuration_PopulateLargeSaleTable`程序中的資料列數目增加`Fact.Sale`資料表。 若要避免正在與現有開始 2013 年 1 月 1 日的 World Wide Importers 資料 2012年日曆年度中插入資料列。

### <a name="procedure-details"></a>程序的詳細資料

#### <a name="name"></a>名稱

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>參數

  `@EstimatedRowsFor2012` **bigint** （具有預設值是 12000000）

#### <a name="result"></a>結果

大約所需的資料列數目會插入到`Fact.Sale`2012 年中的資料表。 此程序以人為方式限制為 50000，每日的資料列數目。 您可以變更這項限制，但限制可協助您避免意外 overinflations 的資料表。

此程序也適用於叢集資料行存放區索引，如果它尚未已經套用。
