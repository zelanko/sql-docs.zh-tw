---
title: WideWorldImporters OLAP 資料庫-使用 SQL Server |Microsoft 文件
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
robots: noindex,nofollow
monikerRange: '>= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ec6d82cef1df31a280b124671a942cdb4f448dd2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="wideworldimportersdw-use-of-sql-server-features-and-capabilities"></a>WideWorldImportersDW 使用的 SQL Server 特性與功能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
WideWorldImportersDW 被為了展現許多適用於資料倉儲和分析 SQL Server 的主要功能。 以下是一份 SQL Server 功能和功能，以及在 WideWorldImportersDW 的使用方式的描述。

## <a name="polybase"></a>PolyBase

[適用於 SQL Server （2016年和更新版本）]

PolyBase 用來與公用的資料集的相關人口統計資料，以了解哪些城市可能感興趣的銷售進一步擴充的結合來自 WideWorldImportersDW 銷售資訊。

若要啟用 PolyBase 的範例資料庫中，請確定它已安裝，並在資料庫中執行下列預存程序：

    EXEC [Application].[Configuration_ApplyPolybase]

這會建立外部資料表`dbo.CityPopulationStatistics`參考公用的資料集，其中包含美國，裝載於 Azure blob 儲存體中的城市的人口資料。 您已檢閱了解組態程序的預存程序中的程式碼我們建議。 如果您想要裝載您自己在 Azure blob 儲存體中的資料，並將它保存在安全的一般公用存取，您必須進行其他設定步驟。 下列查詢會傳回資料的外部資料設定：

    SELECT CityID, StateProvinceCode, CityName, YearNumber, LatestRecordedPopulation FROM dbo.CityPopulationStatistics;

了解哪些城市可能的進一步擴充感興趣，下列查詢會成長率的城市，查看並傳回前 100 個最大城市，具有明顯成長，而其中 Wide World Importers 並沒有銷售是否存在。 查詢牽涉到遠端資料表之間的聯結`dbo.CityPopulationStatistics`和本機資料表`Dimension.City`，以及與本機資料表有關的篩選`Fact.Sales`。

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

叢集資料行存放區索引 (CCI) 可用的事實資料表，來減少儲存體使用量和改善查詢效能。 CCI 使用，事實資料表的基底儲存體使用資料行壓縮。

非叢集索引會使用於叢集資料行存放區索引之上，以便 primary key 和 foreign key 條件約束。 這些條件約束加入超出豐富的警告-ETL 程序來源的資料從 WideWorldImporters 資料庫中，有條件約束來強制執行完整性。 移除主要與外部索引鍵條件約束，以及其支援的索引會減少的事實資料表的儲存體使用量。

**資料大小**

範例資料庫具有有限的資料大小，讓您輕鬆，若要下載並安裝範例。 不過，若要查看資料行存放區索引的實際效能優點，您會想要使用較大的資料集。

您可以執行下列陳述式，增加的大小`Fact.Sales`插入其他的 12 百萬個資料列的範例資料的資料表。 這些會插入資料列所有年度 2012，因此會有與 ETL 處理序沒有干擾。

    EXECUTE [Application].[Configuration_PopulateLargeSaleTable]

若要執行此陳述式會大約 5 分鐘。 若要插入超過 12 百萬個資料列，傳遞為參數，此預存程序來插入資料列數目。

若要比較逾時或無資料行存放區的查詢效能，您可以卸除及/或重新建立叢集資料行存放區索引。

若要卸除索引：

    DROP INDEX [CCX_Fact_Order] ON [Fact].[Order]

若要重新建立：

    CREATE CLUSTERED COLUMNSTORE INDEX [CCX_Fact_Order] ON [Fact].[Order]

## <a name="partitioning"></a>資料分割

（完整版的範例）

資料倉儲中的資料大小可以成長得相當大。 因此，它是最佳作法是將資料分割來管理資料庫中的大型資料表的儲存體。

所有較大的事實資料表會依年份分割。 唯一的例外是`Fact.Stock Holdings`、 其中不是日期為基礎，而且具有有限的資料大小相較於其他事實資料表。

用於所有資料分割資料表的資料分割函數是`PF_Date`，且正在使用資料分割配置為`PS_Date`。

## <a name="in-memory-oltp"></a>In-Memory OLTP

（完整版的範例）

WideWorldImportersDW 使用 SCHEMA_ONLY 記憶體最佳化資料表的臨時資料表。 所有`Integration.` * `_Staging`資料表是 SCHEMA_ONLY 記憶體最佳化資料表。

SCHEMA_ONLY 資料表的優點是它們不會記錄，而且不需要任何磁碟存取。 這可改善效能的 ETL 程序。 因為不會記錄這些資料表，其內容失敗時都會遺失。 不過，資料來源是仍然可用，因此 ETL 程序可以只是重新啟動發生失敗時。
