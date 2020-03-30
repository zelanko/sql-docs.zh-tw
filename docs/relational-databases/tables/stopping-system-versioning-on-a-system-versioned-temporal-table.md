---
title: 停止系統設定版本時態表上的系統版本設定功能 | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: dddd707e-bfb1-44ff-937b-a84c5e5d1a94
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 74b222b8014b3a0e41e34d588d5893b7f4aaf9b8
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "74165450"
---
# <a name="stopping-system-versioning-on-a-system-versioned-temporal-table"></a>停止系統建立版本時態表上的系統版本設定功能

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

您可能想要暫時或永久停止在時態表上的版本設定。 您可以藉由將 **SYSTEM_VERSIONING** 子句設定為 **OFF**來完成。

## <a name="setting-system_versioning--off"></a>設定 SYSTEM_VERSIONING = OFF

如果您想要對時態表執行特定維護作業，或不再需要版本設定的資料表，即可停止系統版本設定功能。 此作業將會產生兩個獨立的資料表：

- 含週期定義的目前資料表

- 為一般資料表的記錄資料表

### <a name="important-remarks"></a>重要備註

- 記錄資料表會在 **SYSTEM_VERSIONING = OFF** 的期間**停止**擷取更新。
- 當您設定 **SYSTEM_VERSIONING = OFF** 或卸除 **SYSTEM_TIME** 期間時，**時態表**上不會遺失任何資料。
- 若您設定 **SYSTEM_VERSIONING = OFF** 但沒有捨棄 **SYSTEM_TIME** 週期，系統將就會繼續為每個插入和更新作業更新週期資料行。 目前資料表上的刪除作業都是永久性的。
- 捨棄 **SYSTEM_TIME** 週期即會完全移除週期資料行。
- 在設定 **SYSTEM_VERSIONING = OFF**時，所有具足夠權限的使用者都可以修改結構描述和歷程記錄資料表的內容，甚至可以永久刪除歷程記錄資料表。

### <a name="permanently-remove-system_versioning"></a>永久移除 SYSTEM_VERSIONING

此範例會永久移除 SYSTEM_VERSIONING，並完全移除週期資料行。 您可以選擇性移除週期資料行。

```sql
ALTER TABLE dbo.Department SET (SYSTEM_VERSIONING = OFF);
/*Optionally, DROP PERIOD if you want to revert temporal table to a non-temporal*/
ALTER TABLE dbo.Department
DROP PERIOD FOR SYSTEM_TIME;
```

### <a name="temporarily-remove-system_versioning"></a>暫時移除 SYSTEM_VERSIONING

下列為需要將系統版本設定設為 **OFF**的作業清單：

- 從歷程記錄 (**DELETE** 或 **TRUNCATE**) 移除不必要的資料
- 從目前資料表 (**DELETE**、 **TRUNCATE**) 移除資料，而不進行版本設定
- 從目前的資料表進行 **SWITCH OUT** 資料分割
- 將 **SWITCH IN** 資料分割至歷程記錄資料表

此範例會暫時停止 SYSTEM_VERSIONING 以讓您執行特定維護作業。 如果暫時停止版本設定是進行資料表維護的必要條件，強烈建議您在交易內執行此動作以保持資料一致性。

> [!NOTE]
> 當重新開啟系統版本控制時，請不要忘記指定 HISTORY_TABLE 引數。 若沒有執行此動作，將會建立新的記錄資料表，並與目前的資料表建立關聯。 原始記錄資料表仍會作為一般的資料表存在，但不會與目前的資料表建立關聯。

```sql
BEGIN TRAN
ALTER TABLE dbo.Department SET (SYSTEM_VERSIONING = OFF);
TRUNCATE TABLE [History].[DepartmentHistory]
WITH (PARTITIONS (1,2))
ALTER TABLE dbo.Department SET
(
SYSTEM_VERSIONING = ON (HISTORY_TABLE = History.DepartmentHistory)
);
COMMIT ;
```

## <a name="next-steps"></a>後續步驟

- [時態表](../../relational-databases/tables/temporal-tables.md)
- [開始使用系統建立版本的時態表](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [管理系統設定版本時態表中的歷程記錄資料保留](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [系統版本設定時態表與記憶體最佳化資料表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [建立系統設定版本時態表](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)
- [修改系統建立版本時態表中的資料](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)
- [查詢系統建立版本時態表中的資料](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)
- [變更系統建立版本時態表的結構描述](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)
