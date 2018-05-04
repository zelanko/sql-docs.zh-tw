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
robots: noindex,nofollow
ms.openlocfilehash: 1530d3f517cc449ee77d6466904d9460483b725a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="wideworldimporters-data-generation"></a>WideWorldImporters 資料產生
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
WideWorldImporters 和 WideWorldImportersDW 資料庫的發行的版本包含啟動年 1 月 1 2013，最多天這些資料庫所產生的資料。

使用時的範例資料庫，可能很有幫助包含較新的範例資料。

## <a name="data-generation-in-wideworldimporters"></a>WideWorldImporters 中的資料產生

若要產生到目前日期為止的範例資料，請遵循下列步驟：

1. 如果您尚未這樣做，請安裝 WideWorldImporters 資料庫的全新版本。 如需安裝指示**WideWorldImporters 安裝和設定**。
2. 在資料庫中執行下列陳述式：

```
    EXECUTE DataLoadSimulation.PopulateDataToCurrentDate
        @AverageNumberOfCustomerOrdersPerDay = 60,
        @SaturdayPercentageOfNormalWorkDay = 50,
        @SundayPercentageOfNormalWorkDay = 0,
        @IsSilentMode = 1,
        @AreDatesPrinted = 1;
```

此陳述式會將在資料庫中，到目前日期為止的範例銷售和訂單資料。 它會產生--天輸出資料的進度。 可能需要大約 10 分鐘讓需要資料每年。 有一些差異，在產生執行，因為在資料產生隨機因素之間的資料。

若要增加或減少的產生，根據每日，訂單的資料量將變更參數的值`@AverageNumberOfCustomerOrdersPerDay`。 參數`@SaturdayPercentageOfNormalWorkDay`和`@SundayPercentageOfNormalWorkDay`可用來判斷週末天訂單量。

## <a name="importing-generated-data-in-wideworldimportersdw"></a>匯入 WideWorldImportersDW 產生的資料

若要匯入到 WideWorldImportersDW OLAP 資料庫中目前的日期為止的範例資料，請遵循下列步驟：

1. 執行資料產生邏輯在 WideWorldImporters OLTP 資料庫中，使用上述步驟。
2. 如果您尚未這樣做，請安裝 WideWorldImportersDW 資料庫的全新版本。 如需安裝指示**WideWorldImporters 安裝和設定**。
3. Reseed OLAP 資料庫的資料庫中執行下列陳述式：

    ```sql
    EXECUTE [Application].Configuration_ReseedETL
    ```

4. 執行 SSIS 封裝**每日 ETL.ispac** OLAP 資料庫將資料匯入。 如需有關如何執行 ETL 作業的指示，請參閱**WideWorldImporters ETL 工作流程**。

## <a name="generating-data-in-wideworldimportersdw-for-performance-testing"></a>WideWorldImportersDW 中產生資料的效能測試

WideWorldImportersDW 能夠以任意增加資料大小，為了測試，例如具有叢集資料行存放區的效能。

挑戰之一就是將下載的大小夠小，無法下載輕鬆，但大足以示範 SQL Server 效能功能。 例如，使用較大的數字的資料列時，才會發生重要的資料行存放區索引的優點。 

此程序`Application.Configuration_PopulateLargeSaleTable`可用來大幅增加中的資料列數目`Fact.Sale`資料表。 請注意，插入資料列是在 2012年日曆年度，以避免與現有的 World Wide Importers 資料開始年 1 月 1 2013年互相衝突。

### <a name="procedure-details"></a>程序的詳細資料

#### <a name="name"></a>名稱： 

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>參數：

  `@EstimatedRowsFor2012` **bigint** （具有預設值是 12000000）

#### <a name="result"></a>結果：

大約所需的資料列數目會插入到`Fact.Sale`2012 年中的資料表。 程序以人為方式限制為 50000 每天的資料列數目。 這項限制可能變更，但要避免不小心 overinflations 的資料表已存在。

此外，此程序適用於叢集資料行存放區索引，如果它已不套用。
