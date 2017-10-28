---
title: "資料產生 |Microsoft 文件"
ms.custom: 
ms.date: 01/30/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.technology:
- " database-engine "
ms.topic: article
ms.assetid: f387273b-8b5f-4687-b033-09499ea2d68f
caps.latest.revision: 4
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c17ad40220d46ab6e19054818ce2abfdce7251f4
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="wideworldimporters-data-generation"></a>WideWorldImporters 資料產生
WideWorldImporters 和 WideWorldImportersDW 資料庫的發行的版本包含啟動年 1 月 1 日 2013，最多天這些資料庫所產生的資料。

如果範例資料庫可用來在日後用於示範或圖例的用途，可能很有幫助包含資料庫中的較新的範例資料。

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

此陳述式會將在資料庫中，到目前日期為止的範例銷售和訂單資料。 它會產生--天輸出資料的進度。 它將需要 rougly 10 分鐘後需要資料每年。 請注意，在產生執行，因為在資料產生隨機因素之間的資料，有些差異。

若要增加或減少的產生，根據每日，訂單的資料量將變更參數的值`@AverageNumberOfCustomerOrdersPerDay`。 參數`@SaturdayPercentageOfNormalWorkDay`和`@SundayPercentageOfNormalWorkDay`可用來判斷週末天訂單量。

## <a name="importing-generated-data-in-wideworldimportersdw"></a>匯入 WideWorldImportersDW 產生的資料

若要匯入到 WideWorldImportersDW OLAP 資料庫中目前的日期為止的範例資料，請遵循下列步驟：

1. 執行資料產生邏輯在 WideWorldImporters OLTP 資料庫中，使用上述步驟。
2. 如果您尚未這樣做，請安裝 WideWorldImportersDW 資料庫的全新版本。 如需安裝指示**WideWorldImporters 安裝和設定**。
3. Reseed OLAP 資料庫的資料庫中執行下列陳述式：

```
    EXECUTE [Application].Configuration_ReseedETL
```

4. 執行 SSIS 封裝**每日 ETL.ispac** OLAP 資料庫將資料匯入。 如需有關如何執行 ETL 作業的指示，請參閱**WideWorldImporters ETL 工作流程**。

## <a name="generating-data-in-wideworldimportersdw-for-performance-testing"></a>WideWorldImportersDW 中產生資料的效能測試

WideWorldImportersDW 能夠以任意增加資料大小，為了測試，例如具有叢集資料行存放區的效能。

其中一個挑戰寄像 World Wide Importers 是保留的下載大小不夠小，無法轉散發，但夠大，能夠示範 SQL Server 效能功能的範例。 這是其中一個區域特定的挑戰是當使用資料行存放區索引。 只在使用較大的數字的資料列時，就會開始重要的優點。 

此程序`Application.Configuration_PopulateLargeSaleTable`可用來大幅增加中的資料列數目`Fact.Sale`資料表。 請注意，插入資料列是在 2012年日曆年度，以避免與現有的 World Wide Importers 資料開始第 1 個月的 2013年互相衝突。

### <a name="procedure-details"></a>程序的詳細資料

#### <a name="name"></a>名稱： 

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>參數：

  `@EstimatedRowsFor2012`**bigint** （具有預設值是 12000000）

#### <a name="result"></a>結果：

大約所需的資料列數目會插入到`Fact.Sale`2012 年中的資料表。 程序以人為方式限制為 50000 每天的資料列數目。 這可能會變更，但要避免 accidential overinflations 的資料表已存在。

此外，此程序適用於叢集資料行存放區索引，如果它已不套用。

