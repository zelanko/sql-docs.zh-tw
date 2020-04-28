---
title: DW WideWorldImporters 資料庫中的主要功能
description: 瞭解 WideWorldImportersDW 資料庫如何展示適用于資料倉儲和分析的 SQL Server 主要功能。
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: 431ca4762b15003f49a5145eb603b7508f2d6844
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "79112421"
---
# <a name="wideworldimportersdw-use-of-sql-server-features-and-capabilities"></a>WideWorldImportersDW 使用 SQL Server 特性和功能
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
WideWorldImportersDW 的設計目的是要展示適用于資料倉儲和分析之 SQL Server 的許多主要功能。 以下是 SQL Server 特性和功能的清單，以及如何在 WideWorldImportersDW 中使用它們的描述。

## <a name="polybase"></a>PolyBase

[適用于 SQL Server （2016和更新版本）]

PolyBase 是用來結合 WideWorldImportersDW 的銷售資訊與人口統計的公用資料集，以瞭解哪些城市可能會有疑問，以便進一步擴展銷售。

若要啟用範例資料庫中的 PolyBase，請確定已安裝，並在資料庫中執行下列預存程式：

    EXEC [Application].[Configuration_ApplyPolyBase]

這會建立一個外部資料表`dbo.CityPopulationStatistics`來參考公用資料集，其中包含美國城市的人口資料（裝載于 Azure blob 儲存體中）。 建議您查看預存程式中的程式碼，以瞭解設定程式。 如果您想要在 Azure blob 儲存體中裝載自己的資料，並保護它免于一般公用存取，您將需要執行額外的設定步驟。 下列查詢會傳回來自外部資料集的資料：

    SELECT CityID, StateProvinceCode, CityName, YearNumber, LatestRecordedPopulation FROM dbo.CityPopulationStatistics;

若要瞭解哪些城市可能會對進一步擴充感疑問，下列查詢會查看城市的成長率，並傳回具有顯著成長的前100大城市，以及寬世界匯入工具沒有銷售狀態。 此查詢牽涉到遠端資料表`dbo.CityPopulationStatistics`和本機資料表`Dimension.City`之間的聯結，以及涉及本機資料表`Fact.Sales`的篩選。

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

叢集資料行存放區索引（CCI）可用於所有事實資料表，以減少儲存體使用量並提升查詢效能。 使用 CCI 時，事實資料表的基底儲存體會使用資料行壓縮。

非叢集索引是在叢集資料行存放區索引的頂端使用，以加速 primary key 和 foreign key 條件約束。 這些條件約束已新增過多的警告-ETL 程式會從 WideWorldImporters 資料庫中的資料中獲得強制執行完整性的條件約束。 移除主鍵和外鍵條件約束及其支援索引，會減少事實資料表的儲存使用量。

**資料大小**

範例資料庫的資料大小有限，可讓您輕鬆地下載並安裝範例。 不過，若要查看資料行存放區索引的實際效能優點，您會想要使用較大的資料集。

您可以執行下列語句，藉由插入另一個 12000000 `Fact.Sales`資料列的範例資料來增加資料表的大小。 這些資料列會插入2012年，因此不會與 ETL 進程產生干擾。

    EXECUTE [Application].[Configuration_PopulateLargeSaleTable]

此聲明需要大約5分鐘的時間來執行。 若要插入超過12000000個數據列，請傳遞所需的資料列數目做為參數插入此預存程式。

若要比較查詢效能與和不使用資料行存放區，您可以卸載和（或）重新建立叢集資料行存放區索引。

若要卸載索引：

    DROP INDEX [CCX_Fact_Order] ON [Fact].[Order]

若要重新建立：

    CREATE CLUSTERED COLUMNSTORE INDEX [CCX_Fact_Order] ON [Fact].[Order]

## <a name="partitioning"></a>資料分割

（完整版的範例）

資料倉儲中的資料大小可能會變得非常大。 因此，最佳做法是使用資料分割來管理資料庫中大型資料表的儲存體。

所有較大的事實資料表都會依年份進行分割。 唯一的例外是`Fact.Stock Holdings`，它不是以日期為基礎，而且與其他事實資料表相較之下，資料大小有限。

用於所有分割資料表的資料分割函數是`PF_Date`，而使用的資料分割配置是`PS_Date`。

## <a name="in-memory-oltp"></a>記憶體內部 OLTP

（完整版的範例）

WideWorldImportersDW 會使用 SCHEMA_ONLY 記憶體優化資料表來執行臨時表。 `Integration.` *所有`_Staging`資料表都是記憶體優化資料表 SCHEMA_ONLY。

SCHEMA_ONLY 資料表的優點是它們不會記錄下來，也不需要任何磁片存取。 這會改善 ETL 程式的效能。 由於不會記錄這些資料表，因此如果失敗，則會遺失其內容。 不過，仍然可以使用資料來源，因此如果發生失敗，ETL 程式就可以重新開機。
