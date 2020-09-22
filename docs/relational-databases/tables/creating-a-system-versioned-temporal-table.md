---
description: 建立系統建立版本的時態表
title: 建立系統建立版本的時態表 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 21e6d74f-711f-40e6-a8b7-85f832c5d4b3
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 035b1793515779102b9b6b24d0377a4d33cba3c1
ms.sourcegitcommit: c74bb5944994e34b102615b592fdaabe54713047
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90990390"
---
# <a name="creating-a-system-versioned-temporal-table"></a>建立系統建立版本的時態表


[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]


若要建立由系統設定版本的時態表，您可選擇三種方式，其依指定記錄資料表的方式而異︰

- 具有匿名記錄資料表的時態表︰請指定目前資料表的結構描述，讓系統以自動產生的名稱建立對應的記錄資料表。
- 具有預設記錄資料表的時態表︰請指定記錄資料表結構描述名稱和資料表名稱，讓系統在該結構描述中建立記錄資料表。
- 具有事先建立之使用者定義記錄資料表的時態表︰請建立最符合需求的記錄資料表，然後在建立時態表期間參考該資料表。

## <a name="creating-a-temporal-table-with-an-anonymous-history-table"></a>建立具有匿名記錄資料表的時態表

建立具有「匿名」記錄資料表的時態表，是建立快速物件的方便選項，特別是在原型和測試環境中。 這也是建立時態表最簡單的方式，因為它在 **SYSTEM_VERSIONING** 子句中不需要任何參數。 下例會建立新的資料表，啟用了系統建立版本，但未定義記錄資料表的名稱。

```sql
CREATE TABLE Department
(
    DeptID INT NOT NULL PRIMARY KEY CLUSTERED
  , DeptName VARCHAR(50) NOT NULL
  , ManagerID INT NULL
  , ParentDeptID INT NULL
  , SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START NOT NULL
  , SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END NOT NULL
  , PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)
)
WITH (SYSTEM_VERSIONING = ON);
```

### <a name="important-remarks"></a>重要備註

- 由系統設定版本的時態表必須定義主索引鍵，且只能有一個 **PERIOD FOR SYSTEM_TIME** 使用兩個 datetime2 資料行定義，其宣告為 **GENERATED ALWAYS AS ROW START / END**。
- **PERIOD** 資料行一律假定為不可為 Null，即使未指定可 Null 性亦同。 如果 **PERIOD** 資料行明確定義為可為 Null，則 **CREATE TABLE** 陳述式會失敗。
- 記錄資料表和目前資料表或時態表的結構描述，在資料行數量、資料行名稱、順序和資料類型上必須一致。
- 匿名的記錄資料表會自動使用與目前資料表或時態表相同的結構描述建立。
- 匿名的記錄資料表名稱格式如下：MSSQL_TemporalHistoryFor_<現有暫存料表物件識別碼>_[尾碼]  。 後置詞是選用的，只有在資料表名稱前半部分不是唯一的時候，才會加入。
- 記錄資料表會建立為資料列存放區資料表。 如果可能，會套用 PAGE 壓縮，否則不壓縮記錄資料表。 例如，有些資料表組態，像 SPARSE 資料行，就不允許壓縮。
- 為記錄資料表建立的預設叢集索引，會使用自動產生的名稱，格式為：IX_<記錄資料表名稱 >  。 叢集索引包含 **PERIOD** 資料行 (結尾、開頭)。
- 若要將目前的資料表建立為記憶體最佳化資料表，請參閱 [系統版本設定時態表與記憶體最佳化資料表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)。

## <a name="creating-a-temporal-table-with-a-default-history-table"></a>建立具有預設記錄資料表的時態表

若您想要控制命名，但仍依賴系統以預設設定建立記錄資料表時，就很適合建立具有預設記錄資料表的時態表。 下例會建立新的資料表，啟用了系統建立版本，並有明確定義的記錄資料表名稱。

```sql
CREATE TABLE Department
(
    DeptID INT NOT NULL PRIMARY KEY CLUSTERED
  , DeptName VARCHAR(50) NOT NULL
  , ManagerID INT NULL
  , ParentDeptID INT NULL
  , SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START NOT NULL
  , SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END NOT NULL
  , PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime)
)
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.DepartmentHistory));
```

### <a name="important-remarks"></a>重要備註

建立記錄資料表所用的規則，與建立「匿名」記錄資料表所套用的規則相同，並使用只套用在具名記錄資料表的下列規則。

- 結構描述名稱是 **HISTORY_TABLE** 參數的必要項目。
- 如果指定的結構描述不存在，則 **CREATE TABLE** 陳述式會失敗。
- 如果 **HISTORY_TABLE** 參數指定的資料表已經存在，就會根據新建立的時態表驗證 [結構描述一致性和暫存資料一致性](https://msdn.microsoft.com/library/dn935015.aspx)。 如果您指定無效的記錄資料表，則 **CREATE TABLE** 陳述式會失敗。

## <a name="creating-a-temporal-table-with-a-user-defined-history-table"></a>建立具有使用者定義記錄資料表的時態表

當使用者想要以特定的儲存體選項和其他索引來指定記錄資料表時，就很適合建立具有使用者定義記錄資料表的時態表。 下例會使用與要建立的時態表一致的結構描述，建立使用者定義的記錄資料表。 對這個使用者定義的記錄資料表，會建立叢集資料行存放區索引和其他非叢集資料列存放區 (B-tree) 索引以進行點查閱。 這個使用者定義的記錄資料表建立之後，就會建立系統建立版本的時態表，將使用者定義的記錄資料表指定為預設的記錄資料表。

```sql
CREATE TABLE DepartmentHistory
(
    DeptID INT NOT NULL
  , DeptName VARCHAR(50) NOT NULL
  , ManagerID INT NULL
  , ParentDeptID INT NULL
  , SysStartTime DATETIME2 NOT NULL
  , SysEndTime DATETIME2 NOT NULL
);
GO

CREATE CLUSTERED COLUMNSTORE INDEX IX_DepartmentHistory
    ON DepartmentHistory;
CREATE NONCLUSTERED INDEX IX_DepartmentHistory_ID_PERIOD_COLUMNS
    ON DepartmentHistory (SysEndTime, SysStartTime, DeptID);
GO

CREATE TABLE Department
(
    DeptID int NOT NULL PRIMARY KEY CLUSTERED
  , DeptName VARCHAR(50) NOT NULL
  , ManagerID INT NULL
  , ParentDeptID INT NULL
  , SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START NOT NULL
  , SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END NOT NULL
  , PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)
)
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.DepartmentHistory));
```

### <a name="important-remarks"></a>重要備註

- 如果您打算對採用彙總或視窗型函數的記錄資料執行分析查詢，為取得良好的資料壓縮和查詢效能，強烈建議您建立叢集資料行存放區作為主要索引。
- 如果主要使用案例是資料稽核 (也就是從目前的資料表中搜尋單一資料列的記錄變更)，就很適合建立具有叢集索引的資料列存放區記錄資料表。
- 記錄資料表不能有主索引鍵、外部索引鍵、唯一索引、資料表條件約束或觸發程序。 它不能設定處理異動資料擷取、變更追蹤，交易式或合併式複寫。

## <a name="alter-non-temporal-table-to-be-a-system-versioned-temporal-table"></a>將非時態表變更為系統建立版本的時態表

當您需要使用現有的資料表啟用系統建立版本功能時，例如當您想要將自訂的暫時解決方案移轉至內建支援。
例如，您可能有一組資料表，要使用觸發程序實作版本控制。 使用暫時的系統版本建立較不複雜，還有其他好處，包括︰

- 不可變的記錄
- 時間移動查詢的新語法
- 更好的 DML 效能
- 最低的維護成本

 當轉換現有的資料表時，請考慮使用 **HIDDEN** 子句隱藏新的 **PERIOD** 資料行 (datetime2 資料行 **SysStartTime** 和 **SysEndTime**)，以免影響未明確指定資料行名稱 (亦即沒有資料行清單的 SELECT * 或 INSERT) 且無處理新資料行設計的現有應用程式。

### <a name="adding-versioning-to-non-temporal-tables"></a>在非時態表中加入版本控制

如果您想要開始追蹤包含資料的非時態表變更，您需要加入 **PERIOD** 定義，並選擇性地提供 SQL Server 將為您建立之空白記錄資料表的名稱︰

```sql
CREATE SCHEMA History;
GO

ALTER TABLE InsurancePolicy
    ADD
        SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START HIDDEN
            CONSTRAINT DF_SysStart DEFAULT SYSUTCDATETIME()
      , SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END HIDDEN
            CONSTRAINT DF_SysEnd DEFAULT CONVERT(DATETIME2, '9999-12-31 23:59:59.9999999'),
        PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime);
GO

ALTER TABLE InsurancePolicy
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = History.InsurancePolicy));
```

> [!IMPORTANT]
> DATETIME2 的精確度必須符合基礎資料表的精確度，請參閱下列備註。

#### <a name="important-remarks"></a>重要備註

- 將使用預設值不可為 Null 的資料行加入現有的資料表時，其大小是所有版本的資料作業大小，(中繼資料作業的) SQL Server Enterprise Edition 除外。 使用具有 SQL Server Standard Edition 資料的大型現有記錄資料表，加入一個非 Null 資料行會是很昂貴的作業。
- 必須小心選擇時段開始和時段結束資料行的條件約束︰
  - 開始資料行的預設值會指定您認為現有資料列有效的時間點。 它不能指定為未來的日期時間點。
  - 結束時間必須指定為所指定 datetime2 精確度的最大值，例如 `9999-12-31 23:59:59` 或 `9999-12-31 23:59:59.9999999`。
- 加入時段時，系統會執行目前資料表的資料一致性檢查，以確定時段資料行的預設值為有效。
- 在啟用 **SYSTEM_VERSIONING**時指定現有的記錄資料表，系統會對目前的資料表和記錄資料表執行資料一致性檢查。 如果您將 **DATA_CONSISTENCY_CHECK = OFF** 指定為額外的參數，即可略過此檢查。

### <a name="migrate-existing-tables-to-built-in-support"></a>將現有的資料表移轉至內建支援

本例會示範如何根據觸發程序，將現有的方案移轉至內建的暫時支援。 在這個範例中，我們假設自訂方案會將目前資料和記錄資料分割成兩個不同的使用者資料表 (**ProjectTaskCurrent** 和 **ProjectTaskHistory**)。 如果您現有的方案使用單一資料表儲存實際資料列和記錄資料列，您就應該先將資料分割成兩個資料表，再執行本範例的移轉步驟︰

```sql
/*Drop trigger on future temporal table*/
DROP TRIGGER ProjectCurrent_OnUpdateDelete;
/*Make sure that future period columns are non-nullable*/
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [ValidFrom] datetime2 NOT NULL;
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [ValidTo] datetime2 NOT NULL;
ALTER TABLE ProjectTaskHistory ALTER COLUMN [ValidFrom] datetime2 NOT NULL;
ALTER TABLE ProjectTaskHistory ALTER COLUMN [ValidTo] datetime2 NOT NULL;
ALTER TABLE ProjectTaskCurrent
    ADD PERIOD FOR SYSTEM_TIME ([ValidFrom], [ValidTo])
ALTER TABLE ProjectTaskCurrent
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.ProjectTaskHistory, DATA_CONSISTENCY_CHECK = ON));
```

#### <a name="important-remarks"></a>重要備註

- 參考 **PERIOD** 定義中現有的資料行時，系統會隱含地將 generated_always_type 變更成這些資料行的 **AS_ROW_START** 和 **AS_ROW_END** 。
- 加入 **PERIOD** 時，系統會執行目前資料表的資料一致性檢查，以確定時段資料行的現有值為有效。
- 強烈建議您將 **SYSTEM_VERSIONING** 設為 **DATA_CONSISTENCY_CHECK = ON** ，以強制執行現有資料的資料一致性檢查。
- 如果慣用隱藏的資料行，請使用命令 `ALTER TABLE [tableName] ALTER COLUMN [columnName] ADD HIDDEN;`。

## <a name="next-steps"></a>後續步驟

- [時態表](../../relational-databases/tables/temporal-tables.md)
 [開始使用系統建立版本的時態表](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [管理系統設定版本時態表中的歷程記錄資料保留](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [系統版本設定時態表與記憶體最佳化資料表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)
- [修改系統建立版本時態表中的資料](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)
- [查詢系統建立版本時態表中的資料](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)
- [變更系統建立版本時態表的結構描述](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)
- [停止系統設定版本時態表上的系統版本設定功能](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
