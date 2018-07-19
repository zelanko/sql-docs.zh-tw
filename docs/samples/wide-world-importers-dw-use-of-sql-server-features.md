---
title: WideWorldImporters OLAP 資料庫-使用 SQL Server |Microsoft Docs
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
ms.openlocfilehash: 7c3158def05148941105867f24205b199e6c6dba
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38023551"
---
# <a name="wideworldimportersdw-use-of-sql-server-features-and-capabilities"></a>WideWorldImportersDW 使用 SQL Server 功能和功能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
WideWorldImportersDW 被設計來展示支援許多 SQL server 適用於資料倉儲和分析的重要功能。 以下是一份 SQL Server 功能和功能，以及在 WideWorldImportersDW 的使用方式的描述。

## <a name="polybase"></a>PolyBase

[適用於 SQL Server （2016年和更新版本）]

使用 PolyBase 將 WideWorldImportersDW 的銷售資訊透過公用資料集相關的人口統計，了解哪一個城市也許會感興趣，來進一步展開 sales。

若要啟用範例資料庫中的使用 PolyBase，請確定它已安裝，並在資料庫中執行下列預存程序：

    EXEC [Application].[Configuration_ApplyPolybase]

這會建立外部資料表`dbo.CityPopulationStatistics`參考包含在美國境內，裝載於 Azure blob 儲存體中的城市的人口資料的公用資料集。 您可以建議檢閱預存程序，以了解設定程序中的程式碼。 如果您想要裝載您自己在 Azure blob 儲存體中的資料，並確保其安全的一般公用存取權，您必須進行其他設定步驟。 下列查詢會傳回資料，從外部資料集：

    SELECT CityID, StateProvinceCode, CityName, YearNumber, LatestRecordedPopulation FROM dbo.CityPopulationStatistics;

若要了解在哪個城市可能有興趣進一步擴充的下列查詢查看城市的成長率，並傳回大幅成長，前 100 個最大城市及 Wide World Importers 不需要有銷售的活動。 查詢牽涉到遠端資料表之間的聯結`dbo.CityPopulationStatistics`和本機資料表`Dimension.City`，以及與本機資料表有關的篩選`Fact.Sales`。

    WITH PotentialCities
    AS
    (
        SELECT cps.CityName,
               cps.StateProvinceCode,
               MAX(cps.LatestRecordedPopulation) AS PopulationIn2016,
               (MAX(cps.LatestRecordedPopulation) - MIN(cps.LatestRecordedPopulation)) * 100.0
                   / MIN(cps.LatestRecordedPopulation) AS GrowthRate
        FROM dbo.CityPopulationStatistics AS cps
        WHERE cps.LatestRecordedPopulation IS NOT NULL
        AND cps.LatestRecordedPopulation <> 0
        GROUP BY cps.CityName, cps.StateProvinceCode
    ),
    InterestingCities
    AS
    (
        SELECT DISTINCT pc.CityName,
                        pc.StateProvinceCode,
                        pc.PopulationIn2016,
                        FLOOR(pc.GrowthRate) AS GrowthRate
        FROM PotentialCities AS pc
        INNER JOIN Dimension.City AS c
        ON pc.CityName = c.City
        WHERE GrowthRate > 2.0
        AND NOT EXISTS (SELECT 1 FROM Fact.Sale AS s WHERE s.[City Key] = c.[City Key])
    )
    SELECT TOP(100) CityName, StateProvinceCode, PopulationIn2016, GrowthRate
    FROM InterestingCities
    ORDER BY PopulationIn2016 DESC;

## <a name="clustered-columnstore-indexes"></a>叢集資料行存放區索引

（完整版的範例）

叢集資料行存放區索引 (CCI) 可搭配所有事實資料表，以降低儲存體使用量，並改善查詢效能。 使用 CCI 的目的，事實資料表的基底儲存體，請使用資料行的壓縮。

非叢集索引上的叢集資料行存放區索引，來加速 primary key 和 foreign key 條件約束。 這些條件約束已新增出豐富的注意-ETL 程序來源 WideWorldImporters 資料庫，可強制使用參考完整性的條件約束中的資料。 移除主要與外部索引鍵條件約束，以及其支援的索引，會減少的事實資料表的儲存體使用量。

**資料大小**

範例資料庫具有有限的資料大小，以讓您輕鬆下載並安裝範例。 不過，若要查看資料行存放區索引的實際效能優點，您會想要使用較大的資料集。

您可以執行下列陳述式，增加的大小`Fact.Sales`插入另一個的 12 萬個資料列的範例資料的資料表。 這些資料列是所有插入的 2012 年使得 ETL 程序的任何負面影響。

    EXECUTE [Application].[Configuration_PopulateLargeSaleTable]

若要執行此陳述式需要大約 5 分鐘的時間。 若要插入超過 12 萬個資料列，傳遞所需的資料列插入做為此預存程序的參數數目。

若要比較查詢效能，而資料行存放區，您可以卸除及/或重新建立叢集資料行存放區索引。

若要卸除索引：

    DROP INDEX [CCX_Fact_Order] ON [Fact].[Order]

若要重新建立：

    CREATE CLUSTERED COLUMNSTORE INDEX [CCX_Fact_Order] ON [Fact].[Order]

## <a name="partitioning"></a>資料分割

（完整版的範例）

資料倉儲中的資料大小可以成長得相當大。 因此，它是最佳做法是使用資料分割來管理資料庫中的大型資料表的儲存體。

所有較大的事實資料表是依年份來分割。 唯一的例外是`Fact.Stock Holdings`，這不是以日期為基礎，並且具有有限的資料大小相較於其他事實資料表。

是用於所有資料分割資料表的資料分割函數`PF_Date`，而且正在使用的資料分割配置`PS_Date`。

## <a name="in-memory-oltp"></a>In-Memory OLTP

（完整版的範例）

WideWorldImportersDW 使用 SCHEMA_ONLY 記憶體最佳化資料表的暫存資料表。 所有`Integration.` * `_Staging`資料表是 SCHEMA_ONLY 記憶體最佳化的資料表。

SCHEMA_ONLY 資料表的優點是它們不會記錄，並不需要任何磁碟存取。 這可改善效能的 ETL 程序。 因為不會記錄這些資料表，其內容失敗時都會遺失。 不過，資料來源是仍然可用，因此 ETL 程序可以只是重新啟動發生錯誤。
