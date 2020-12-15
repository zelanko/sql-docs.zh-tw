---
title: DW WideWorldImporters 資料庫中的主要功能
description: 瞭解 WideWorldImportersDW 資料庫如何展示適用于資料倉儲和分析之 SQL Server 的主要功能。
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 07/01/2020
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: dea493c6c46536367d3251579d60c731bde1bb84
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97424556"
---
# <a name="wideworldimportersdw-use-of-sql-server-features-and-capabilities"></a>WideWorldImportersDW SQL Server 特性和功能的使用
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
WideWorldImportersDW 的設計目的在於展示適用于資料倉儲和分析之 SQL Server 的許多重要功能。 以下是 SQL Server 特性和功能的清單，以及如何在 WideWorldImportersDW 中使用這些功能的說明。

## <a name="polybase"></a>PolyBase

[適用于 SQL Server (2016 和更新版本) ]

PolyBase 用來將 WideWorldImportersDW 中的銷售資訊與有關人口統計資料的公用資料集合併，以瞭解進一步擴展銷售時可能會有興趣的城市。

若要在範例資料庫中啟用 PolyBase，請確定已安裝，並在資料庫中執行下列預存程式：

```sql
EXECUTE [Application].[Configuration_ApplyPolyBase]
```

這會建立 `dbo.CityPopulationStatistics` 參考公用資料集的外部資料表，此資料集包含位於美國的城市人口資料（裝載于 Azure blob 儲存體中）。 建議您檢查預存程式中的程式碼，以瞭解設定流程。 如果您想要在 Azure blob 儲存體中裝載您自己的資料，並使其免于受到一般公用存取的保護，您將需要執行其他設定步驟。 下列查詢會傳回該外部資料集的資料：

```sql
SELECT
        CityID, StateProvinceCode, CityName,
        YearNumber, LatestRecordedPopulation
    FROM
        dbo.CityPopulationStatistics;
```

若要瞭解進一步擴充可能有興趣的城市，下列查詢會查看城市的成長率，並傳回具有大幅成長的前100大城市，以及 Wide World 的匯入工具沒有銷售狀態。 此查詢牽涉到遠端資料表 `dbo.CityPopulationStatistics` 和本機資料表之間的聯結 `Dimension.City` ，以及涉及本機資料表的篩選 `Fact.Sales` 。

```sql
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
```

## <a name="clustered-columnstore-indexes"></a>叢集資料行存放區索引

 (完整版的範例) 

 (CCI) 的叢集資料行存放區索引會與所有事實資料表搭配使用，以減少儲存空間的使用量並提升查詢效能。 使用 CCI 時，事實資料表的基底儲存體會使用資料行壓縮。

非叢集索引會使用於叢集資料行存放區索引之上，以促進 primary key 和 foreign key 條件約束。 已新增這些條件約束，因為 ETL 程式會將來自 WideWorldImporters 資料庫的資料，而其具有強制執行完整性的條件約束。 移除 primary 和 foreign key 條件約束，以及其支援的索引，將會減少事實資料表的儲存空間使用量。

**資料大小**

範例資料庫的資料大小有限，可讓您輕鬆地下載和安裝範例。 不過，若要查看資料行存放區索引的實際效能優勢，您會想要使用較大的資料集。

您可以執行下列語句，藉 `Fact.Sales` 由插入另一個12000000資料列的範例資料來增加資料表的大小。 這兩個數據列都是在2012年插入，因此不會與 ETL 進程產生任何干擾。

```sql
    EXECUTE [Application].[Configuration_PopulateLargeSaleTable]
```

此語句大約需要5分鐘的時間來執行。 若要插入12000000個以上的資料列，請將想要插入的資料列數目傳遞給這個預存程式的參數。

若要比較查詢效能與或不使用資料行存放區，您可以卸載和/或重新建立叢集資料行存放區索引。

若要卸載索引：

```sql
 DROP INDEX [CCX_Fact_Order] ON [Fact].[Order]
```

若要重新建立：

```sql
CREATE CLUSTERED COLUMNSTORE INDEX [CCX_Fact_Order] ON [Fact].[Order]
```

## <a name="partitioning"></a>資料分割

 (完整版的範例) 

資料倉儲中的資料大小可能會變得很大。 因此，最佳作法是使用資料分割來管理資料庫中大型資料表的儲存體。

所有較大的事實資料表都會依年度進行分割。 唯一的例外狀況是 `Fact.Stock Holdings` ，它不是以日期為基礎，且與其他事實資料表的資料大小有所限制。

用於所有資料分割資料表的資料分割函數是 `PF_Date` ，而使用的資料分割配置是 `PS_Date` 。

## <a name="in-memory-oltp"></a>記憶體內部 OLTP

 (完整版的範例) 

WideWorldImportersDW 使用臨時表 SCHEMA_ONLY 記憶體優化資料表。 所有 `Integration.` * `_Staging` 資料表都 SCHEMA_ONLY 記憶體優化資料表。

SCHEMA_ONLY 資料表的優點是它們不會記錄下來，且不需要任何磁片存取。 這可改善 ETL 程式的效能。 因為不會記錄這些資料表，所以如果發生失敗，則其內容會遺失。 不過，資料來源仍可供使用，因此 ETL 程式只要在發生失敗時就可以重新開機。
