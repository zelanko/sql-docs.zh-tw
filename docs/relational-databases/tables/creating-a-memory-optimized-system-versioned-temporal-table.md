---
title: 建立記憶體最佳化的系統版本設定時態表 | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1c1fc682-bf5b-4096-a0ff-3235d71c205a
caps.latest.revision: 14
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b742111490567ee1a10ce22fbd8c2c6592d10361
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="creating-a-memory-optimized-system-versioned-temporal-table"></a>建立記憶體最佳化的系統版本設定時態表
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  類似於建立以磁碟為基礎的記錄資料表，您也可以用數種方式建立記憶體最佳化的時態表。  
  
> [!NOTE]  
>  若要建立記憶體最佳化資料表，您必須先建立 [記憶體最佳化檔案群組](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)。  
  
 當您想要控制命名，但仍依賴系統以預設組態建立記錄資料表時，建立具有預設記錄資料表的時態表是一個方便的選項。 在下列範例中，新系統版本設定時態表與記憶體最佳化資料表連結到以磁碟為基礎的新記錄資料表。  
  
```  
CREATE SCHEMA History  
GO  
CREATE TABLE dbo.Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY NONCLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
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
  
```  
  
--Existing table   
CREATE TABLE Department_History   
(  
    DepartmentNumber char(10) NOT NULL,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 NOT NULL,   
    SysEndTime datetime2 NOT NULL   
);  
--Temporal table  
CREATE TABLE Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY NONCLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID INT  NULL,   
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
    );  
```  
 
## <a name="see-also"></a>另請參閱  
 [系統版本設定時態表與記憶體最佳化資料表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [使用記憶體最佳化的系統版本設定時態表](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)   
 [監視記憶體最佳化的系統建立版本時態表](../../relational-databases/tables/monitoring-memory-optimized-system-versioned-temporal-tables.md)   
 [記憶體最佳化系統版本設定時態表的效能考量](../../relational-databases/tables/memory-optimized-system-versioned-temporal-tables-performance.md)   
 [時態表](../../relational-databases/tables/temporal-tables.md)   
 [時態表系統一致性檢查](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [管理系統設定版本之時態表中的歷程記錄資料保留](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [暫存資料表中繼資料檢視和函數](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
