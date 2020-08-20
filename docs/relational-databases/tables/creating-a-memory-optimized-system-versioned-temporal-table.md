---
description: 建立記憶體最佳化的系統版本設定時態表
title: 建立記憶體最佳化的系統版本設定時態表 | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 1c1fc682-bf5b-4096-a0ff-3235d71c205a
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 432c61f69e8d03126d78113989c83172b8ac2e3d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473058"
---
# <a name="creating-a-memory-optimized-system-versioned-temporal-table"></a>建立記憶體最佳化的系統版本設定時態表

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

類似於建立以磁碟為基礎的記錄資料表，您也可以用數種方式建立記憶體最佳化的時態表。

> [!NOTE]
> 若要建立記憶體最佳化資料表，您必須先建立 [記憶體最佳化檔案群組](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)。

當您想要控制命名，但仍依賴系統以預設組態建立記錄資料表時，建立具有預設記錄資料表的時態表是一個方便的選項。 在以下範例中，新系統版本控制的記憶體最佳化時態表已連結到新的磁碟式記錄資料表。

```sql
CREATE SCHEMA History
GO
CREATE TABLE dbo.Department
   (  
      DepartmentNumber char(10) NOT NULL PRIMARY KEY NONCLUSTERED,
      DepartmentName varchar(50) NOT NULL,
      ManagerID int NULL,
      ParentDepartmentNumber char(10) NULL,
      SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,
      SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,
      PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)
   )
WITH
   (
       MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA,
          SYSTEM_VERSIONING = ON ( HISTORY_TABLE = History.DepartmentHistory )
    );
```

當您想要使用現有的資料表加入系統建立版本功能時 (例如當您想要將自訂的暫時解決方案移轉至內建支援)，建立時態表與現有的記錄資料表連結會十分有用。 下列範例中，新時態表建立了與現有的記錄資料表的連結。

```sql
--Existing table
CREATE TABLE Department_History
   (
      DepartmentNumber char(10) NOT NULL,
      DepartmentName varchar(50) NOT NULL,
      ManagerID int NULL,
      ParentDepartmentNumber char(10) NULL,
      SysStartTime datetime2 NOT NULL, SysEndTime datetime2 NOT NULL
   )
;
--Temporal table
CREATE TABLE Department
   (
      DepartmentNumber char(10) NOT NULL PRIMARY KEY NONCLUSTERED,
      DepartmentName varchar(50) NOT NULL,
      ManagerID INT NULL,
      ParentDepartmentNumber char(10) NULL,
      SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,
      SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,
      PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)
   )
WITH
   (
      SYSTEM_VERSIONING = ON
         (  
            HISTORY_TABLE = dbo.Department_History
            , DATA_CONSISTENCY_CHECK = ON
         )  
      , MEMORY_OPTIMIZED = ON
      , DURABILITY = SCHEMA_AND_DATA
   )
;
```

## <a name="see"></a>請參閱

- [系統版本設定時態表與記憶體最佳化資料表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [使用記憶體最佳化的系統版本設定時態表](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)
- [監視記憶體最佳化的系統建立版本時態表](../../relational-databases/tables/monitoring-memory-optimized-system-versioned-temporal-tables.md)
- [記憶體最佳化系統版本設定時態表的效能考量](../../relational-databases/tables/memory-optimized-system-versioned-temporal-tables-performance.md)
- [時態表](../../relational-databases/tables/temporal-tables.md)
- [時態表系統一致性檢查](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [管理系統設定版本時態表中的歷程記錄資料保留](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [暫存資料表中繼資料檢視和函數](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
