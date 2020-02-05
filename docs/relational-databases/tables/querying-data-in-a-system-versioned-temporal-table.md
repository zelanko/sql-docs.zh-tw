---
title: 查詢系統建立版本時態表中的資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 2d358c2e-ebd8-4eb3-9bff-cfa598a39125
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 415e966e2ecebb9004e64ddedd6b96d87cedee35
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "74165613"
---
# <a name="querying-data-in-a-system-versioned-temporal-table"></a>查詢系統建立版本時態表中的資料

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

當您想要取得時態表中資料的最新 (實際) 狀態，您能夠以您查詢非時態表完全一樣的方式查詢。 如果 PERIOD 資料行未隱藏，其值會出現在 SELECT \* 查詢中。 如果您將 **PERIOD** 資料行指定為隱藏，其值不會出現在 SELECT \* 查詢中。 當 **PERIOD** 資料行隱藏時，請特別參考 SELECT 子句中的 **PERIOD** 資料行，以傳回這些資料行的值。

若要執行任何以時間為基礎之類型的分析，請搭配四個特定時態次子句使用新的 **FOR SYSTEM_TIME** 子句來查詢在目前和歷程記錄資料表之間的資料。 如需這些子句的詳細資訊，請參閱[時態表](../../relational-databases/tables/temporal-tables.md)和 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)

- AS OF <date_time>
- FROM <start_date_time> TO <end_date_time>
- BETWEEN <start_date_time> AND <end_date_time>
- CONTAINED IN (<start_date_time> , <end_date_time>)
- ALL

在查詢中，可以針對每個資料表個別指定**FOR SYSTEM_TIME** 。 它可以在通用資料表運算式、資料表值函式和預存程序內使用。

## <a name="query-for-a-specific-time-using-the-as-of-sub-clause"></a>使用 AS OF 次子句查詢特定的時間

當您需要重新建構資料於過去特定時間的狀態，請使用 **AS OF** 次子句。 您可以使用 **PERIOD** 資料行定義中指定之 datetime2 類型的有效位數，重新建構資料。

**AS OF** 次子句可以搭配常數常值或變數使用，這可讓您以動態方式指定時間的情況。 提供的值會解譯為 UTC 時間。

第一個範例傳回 dbo.Department 資料表 AS OF 過去特定時間的狀態。

```sql
/*State of entire table AS OF specific date in the past*/
SELECT [DeptID], [DeptName], [SysStartTime],[SysEndTime]
FROM [dbo].[Department]
FOR SYSTEM_TIME AS OF '2015-09-01 T10:00:00.7230011' ;
```

第二個範例針對資料列子集比較兩個時間點之間的值。

```sql
DECLARE @ADayAgo datetime2
SET @ADayAgo = DATEADD (day, -1, sysutcdatetime())
/*Comparison between two points in time for subset of rows*/
SELECT D_1_Ago.[DeptID], D.[DeptID],
D_1_Ago.[DeptName], D.[DeptName],
D_1_Ago.[SysStartTime], D.[SysStartTime],
D_1_Ago.[SysEndTime], D.[SysEndTime]
FROM [dbo].[Department] FOR SYSTEM_TIME AS OF @ADayAgo AS D_1_Ago
JOIN [Department] AS D ON D_1_Ago.[DeptID] = [D].[DeptID]
AND D_1_Ago.[DeptID] BETWEEN 1 and 5 ;
```

### <a name="using-views-with-as-of-sub-clause-in-temporal-queries"></a>在暫時查詢中搭配 AS-OF 次子句使用檢視

在需要複雜時間點分析時，使用檢視非常有用。 常見範例是產生一份今天的商務報表，包含上個月的值。

通常，客戶會有一個許多資料表牽涉到外部索引鍵關聯性的正規化資料庫模型。 該正規化模型的資料在過去某個時間點看起來的樣子，這個問題要回答並不是很容易，因為所有的資料表都會以自己的步調獨立變更。

在此情況下，最好的選擇是建立檢視，並套用 **AS OF** 次子句到整個檢視。 使用這種方法可讓您將資料存取層的模型從時間點分析中分離，同時 SQL Server 會以透明的方式將 **AS OF** 子句套用至所有加入檢視定義的時態表。 此外，您可以在相同的檢視中將時態表與非時態表結合，而 **AS OF** 將只會套用至時態表。 如果檢視未至少參考一個暫存資料表，則套用暫時查詢子句至檢視會失敗，並產生錯誤。

```sql
/* Create view that joins three temporal tables: Department, CompanyLocation, LocationDepartments */
CREATE VIEW [dbo].[vw_GetOrgChart]
AS
SELECT
    [CompanyLocation].LocID
   , [CompanyLocation].LocName
   , [CompanyLocation].City
   , [Department].DeptID
   , [Department].DeptName
FROM [dbo].[CompanyLocation]
LEFT JOIN [dbo].[LocationDepartments]
   ON [CompanyLocation].LocID = LocationDepartments.LocID
LEFT JOIN [dbo].[Department]
   ON LocationDepartments.DeptID = [Department].DeptID ;
GO
/* Querying view AS OF */
SELECT * FROM [vw_GetOrgChart]
FOR SYSTEM_TIME AS OF '2015-09-01 T10:00:00.7230011' ;
```

## <a name="query-for-changes-to-specific-rows-over-time"></a>查詢一段時間的特定資料列變更

當您想要執行資料稽核 (也就是當您需要取得目前資料表中特定資料列的所有變更歷程記錄時)，時態次子句 **FROM...TO**、 **BETWEEN...AND** 和 **CONTAINED IN** 很有用。

前兩個次子句會傳回與指定期間重疊的資料列版本 (也就是指定週期開始之前和指定週期結束之後)，而 CONTAINED IN 只傳回存在於指定期間內的那些資料列版本。

> [!IMPORTANT]
> 如果您只搜尋非目前資料列版本，建議您直接查詢記錄資料表，因為這樣可獲得最佳查詢效能。 當您需要查詢目前和和歷程記錄資料，沒有任何限制時，請使用 **ALL** 。

```sql
/* Query using BETWEEN...AND sub-clause*/
SELECT
     [DeptID]
   , [DeptName]
   , [SysStartTime]
   , [SysEndTime]
   , IIF (YEAR(SysEndTime) = 9999, 1, 0) AS IsActual
FROM [dbo].[Department]
FOR SYSTEM_TIME BETWEEN '2015-01-01' AND '2015-12-31'
WHERE DeptId = 1
ORDER BY SysStartTime DESC;

/* Query using CONTAINED IN sub-clause */
SELECT [DeptID], [DeptName], [SysStartTime],[SysEndTime]
FROM [dbo].[Department]
FOR SYSTEM_TIME CONTAINED IN ('2015-04-01', '2015-09-25')
WHERE DeptId = 1
ORDER BY SysStartTime DESC ;

/* Query using ALL sub-clause */
SELECT
     [DeptID]
   , [DeptName]
   , [SysStartTime]
   , [SysEndTime]
   , IIF (YEAR(SysEndTime) = 9999, 1, 0) AS IsActual
FROM [dbo].[Department] FOR SYSTEM_TIME ALL
ORDER BY [DeptID], [SysStartTime] Desc
```

## <a name="next-steps"></a>後續步驟

- [時態表](../../relational-databases/tables/temporal-tables.md)
- [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)
- [建立系統設定版本時態表](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)
- [修改系統建立版本時態表中的資料](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)
- [變更系統建立版本時態表的結構描述](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)
- [停止系統設定版本時態表上的系統版本設定功能](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)
