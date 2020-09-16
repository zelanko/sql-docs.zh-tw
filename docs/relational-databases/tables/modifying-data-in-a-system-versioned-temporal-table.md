---
description: 修改系統建立版本時態表中的資料
title: 修改系統版本設定時態表中的資料 |Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 5f398470-c531-47b5-84d5-7c67c27df6e5
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f6c431669d89f87c49cfd96d48e6b3c53c8d866e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548865"
---
# <a name="modifying-data-in-a-system-versioned-temporal-table"></a>修改系統建立版本時態表中的資料


[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]


系統建立版本時態表中的資料是使用一般的 DML 陳述式來修改但有一個重要差異：無法直接修改期間資料行的資料。 更新資料時，即會為它建立版本，將每個更新資料列的舊版本插入至記錄資料表。 刪除資料時，刪除是邏輯性的，會將該資料列從記錄資料表移至目前的資料表 - 不會將它永久刪除。

## <a name="inserting-data"></a>插入資料

當您插入新資料時，必須說明 **PERIOD** 資料行 (如果它們不是 **HIDDEN**)。 您也可以搭配系統建立版本時態表使用資料分割切換。

### <a name="insert-new-data-with-visible-period-columns"></a>使用可見的期間資料行插入新資料

當您擁有如下的可見 **PERIOD** 資料行來說明新的 **PERIOD** 資料行時，可以建構 **INSERT** 陳述式︰

- 如果您在 **INSERT** 陳述式中指定資料行清單，則可省略 **PERIOD** 資料行，因為系統將自動產生這些資料行的值。

  ```sql
  -- Insert with column list and without period columns
  INSERT INTO [dbo].[Department]
    (  [DeptID]
          , [DeptName]
          , [ManagerID]
          ,[ParentDeptID]
    )
       VALUES
         (  10
         , 'Marketing'
         , 101
         , 1
         ) ;
   ```

- 如果您在 **INSERT** 陳述式的資料行清單中指定 **PERIOD** 資料行，就必須將 **DEFAULT** 指定為其值。

  ```sql
  INSERT INTO [dbo].[Department]
    (  [DeptID]
          , [DeptName]
          , [ManagerID]
          , [ParentDeptID]
          , SysStartTime
          , SysEndTime
    )
       VALUES
         (  11
          , 'Sales'
          , 101
          , 1
          , default
          , default) ;
   ```

- 如果您未在 **INSERT** 陳述式中指定資料行清單，請為 **PERIOD** 資料行指定 **DEFAULT** 。

  ```sql
    -- Insert without column list and DEFAULT values for period columns
    INSERT INTO [dbo].[Department]
    VALUES(12, 'Production', 101, 1, default, default);

  ```

### <a name="insert-data-into-a-table-with-hidden-period-columns"></a>將資料插入含有 HIDDEN 期間資料行的資料表

如果將 **PERIOD** 資料行指定為 HIDDEN，則您只需在使用 INSERT 時指定可見資料行的值，而不需指定資料行清單。 您不需要在 **INSERT** 陳述式中說明新的 **PERIOD** 的資料行。 此行為可確保舊版應用程式在啟用將受益於建立版本的資料表上啟用系統建立版本時仍能繼續運作。

```sql
CREATE TABLE [dbo].[CompanyLocation]
(
     [LocID] [int] IDENTITY(1,1) NOT NULL PRIMARY KEY
   , [LocName] [varchar](50) NOT NULL
   , [City] [varchar](50) NOT NULL
   , [SysStartTime] [datetime2] GENERATED ALWAYS AS ROW START HIDDEN NOT NULL
   , [SysEndTime] [datetime2] GENERATED ALWAYS AS ROW END HIDDEN NOT NULL
   , PERIOD FOR SYSTEM_TIME ([SysStartTime], [SysEndTime])
)
WITH ( SYSTEM_VERSIONING = ON );
GO
INSERT INTO [dbo].[CompanyLocation]
VALUES ('Headquarters', 'New York');

```

### <a name="inserting-data-using-partition-switch"></a>使用 PARTITION SWITCH 插入資料

如果目前的資料表已進行資料分割，您可以使用資料分割切換做為有效率的機制，來將資料載入至空的分割區，或以平行方式載入至多個分割區。

在 **PARTITION SWITCH IN** 陳述式中，與系統設定版本之時態表搭配使用的暫存表格必須定義 **SYSTEM_TIME PERIOD** ，但不需是系統設定版本的時態表。
這確保時態一致性檢查會在資料插入暫存表格期間執行，或是在將 SYSTEM_TIME 期間加入預先填入的暫存表格時執行。

```sql
/*Create staging table with period definition for SWITCH IN temporal table*/
CREATE TABLE [dbo].[Staging_Department_Partition2]
(
     [DeptID] [int] NOT NULL
   , [DeptName] [varchar](50) NOT NULL
   , [ManagerID] [int] NULL
   , [ParentDeptID] [int] NULL
   , [SysStartTime] [datetime2] GENERATED ALWAYS AS ROW START NOT NULL
   , [SysEndTime] [datetime2] GENERATED ALWAYS AS ROW END NOT NULL
   , PERIOD FOR SYSTEM_TIME ( [SysStartTime], [SysEndTime] )
) ON [PRIMARY]

/*Create aligned primary key*/
ALTER TABLE [dbo].[Staging_Department_Partition2]
ADD CONSTRAINT [Staging_Department_Partition2_PK]
   PRIMARY KEY CLUSTERED
   ( [DeptID] ASC )
   ON [PRIMARY]
  
/*
Create and enforce constraints for partition boundaries.
Partition 2 contains rows with DeptID > 100 and DeptID <=200
*/
ALTER TABLE [dbo].[Staging_Department_Partition2]
   WITH CHECK ADD  CONSTRAINT [chk_staging_Department_partition_2]
   CHECK  ([DeptID]>N'100' AND [DeptID]<=N'200')
ALTER TABLE [dbo].[Staging_Department_Partition2]
   CHECK CONSTRAINT [chk_staging_Department_partition_2]

/*Load data into staging table*/
INSERT INTO [dbo].[staging_Department] ([DeptID],[DeptName],[ManagerID],[ParentDeptID])
VALUES (101,'D101',1,NULL)

/*Use PARTITION SWITCH IN to efficiently add data to current table */
ALTER TABLE [Staging_Department]
SWITCH TO [dbo].[Department] PARTITION 2;
```

如果您嘗試從不含期間定義的資料表執行 PARTITION SWITCH，將會得到錯誤訊息︰`Msg 13577, Level 16, State 1, Line 25 ALTER TABLE SWITCH statement failed on table 'MyDB.dbo.Staging_Department_2015_09_26' because target table has SYSTEM_TIME PERIOD while source table does not have it.`

## <a name="updating-data"></a>更新資料

您可以利用一般的 **UPDATE** 陳述式，來更新目前資料表中的資料。 您可以針對「糟糕」案例從記錄資料表中更新目前資料表中的資料。 但是，您不能更新 **PERIOD** 資料行，而且當 **SYSTEM_VERSIONING = ON** 時，您無法直接更新記錄資料表中的資料。

設定 **SYSTEM_VERSIONING = OFF** 並從目前和記錄資料表更新資料列，但請注意，這樣一來，系統將不會保留變更的記錄。

### <a name="updating-the-current-table"></a>更新目前的資料表

在此範例中，針對每個 DeptID = 10 的資料列更新 ManagerID 資料行 。 您不能以任何方式參考 **PERIOD** 資料行。

```sql
UPDATE [dbo].[Department] SET [ManagerID] = 501 WHERE [DeptID] = 10
```

但是，您不能更新 **PERIOD** 資料行，而且您無法更新記錄資料表。 在此範例中，嘗試更新 **PERIOD** 資料行會產生錯誤。

```sql
UPDATE [dbo].[Department]
SET SysStartTime = '2015-09-23 23:48:31.2990175'
WHERE DeptID = 10 ;

Msg 13537, Level 16, State 1, Line 3
Cannot update GENERATED ALWAYS columns in table 'TmpDev.dbo.Department'.
```

### <a name="updating-the-current-table-from-the-history-table"></a>從記錄資料表更新目前的資料表

您可以在目前資料表中使用 **UPDATE**，將實際資料列狀態還原為過去某個特定時間點的有效狀態 (還原為「上次已知良好的資料列版本」)。 下列範例顯示還原至記錄資料表中截至 2015 年 4 月 25 日且 DeptID = 10 的值。

```sql
UPDATE Department
SET DeptName = History.DeptName
FROM Department
FOR SYSTEM_TIME AS OF '2015-04-25' AS History
WHERE History.DeptID = 10
AND Department.DeptID = 10 ;
```

## <a name="deleting-data"></a>刪除資料

您可以利用一般的 **DELETE** 陳述式，來刪除目前資料表中的資料。 已刪除資料列的結束期間資料行將填入基礎交易的開始時間。 當 **SYSTEM_VERSIONING = ON**時，您無法從記錄資料表直接刪除資料列。 設定 **SYSTEM_VERSIONING = OFF** 並從目前和記錄資料表刪除資料列，但請注意，這樣一來，系統將不會保留變更的記錄。 當**SWITCH PARTITION IN**, **TRUNCATE** 、 **SWITCH PARTITION OUT** 和 **SWITCH PARTITION IN**記錄資料表。

## <a name="using-merge-to-modify-data-in-temporal-table"></a>使用 MERGE 修改時態表中的資料

**MERGE** 作業是透過與 **INSERT** 和 **UPDATE** 陳述式都有相關 **PERIOD** 資料行的相同限制來支援。

```sql
CREATE TABLE DepartmentStaging (DeptId INT, DeptName varchar(50));
GO
INSERT INTO DepartmentStaging VALUES (1, 'Company Management');
INSERT INTO DepartmentStaging VALUES (10, 'Science & Research');
INSERT INTO DepartmentStaging VALUES (15, 'Process Management');

MERGE dbo.Department AS target
USING (SELECT DeptId, DeptName FROM DepartmentStaging) AS source (DeptId, DeptName)
ON (target.DeptId = source.DeptId)
WHEN MATCHED THEN
    UPDATE
   SET DeptName = source.DeptName
WHEN NOT MATCHED THEN
   INSERT (DeptName)
   VALUES (source.DeptName);
```

## <a name="next-steps"></a>後續步驟

- [時態表](../../relational-databases/tables/temporal-tables.md)
- [建立系統設定版本時態表](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)
- [查詢系統建立版本時態表中的資料](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)
- [變更系統建立版本時態表的結構描述](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)
- [停止系統設定版本時態表上的系統版本設定功能](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)
