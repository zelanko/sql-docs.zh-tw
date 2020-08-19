---
description: 使用記憶體最佳化的系統版本設定時態表
title: 使用記憶體最佳化的系統版本設定時態表 | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 691d4f80-6754-43f5-8b43-d4facf08f6fc
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6dfc85f00616cc37a6e6440e711a5f3abab6f40a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418942"
---
# <a name="working-with-memory-optimized-system-versioned-temporal-tables"></a>使用記憶體最佳化的系統版本設定時態表

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

本主題討論記憶體最佳化之系統版本設定時態表和以磁碟基礎之系統版本設定時態表的使用方式差異。

> [!NOTE]
> 搭配使用 Temporal 和記憶體最佳化資料表僅適用於 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，不適用於 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。

## <a name="discovering-metadata"></a>探索中繼資料

若要探索記憶體最佳化之系統版本設定時態表的相關中繼資料，您需要結合來自 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) 和 [sys.internal_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md) 的資訊。 系統版本設定時態表會呈現為內部記憶體中記錄資料表的 parent_object_id。

以下範例示範如何查詢及聯結這些資料表。

```sql
SELECT SCHEMA_NAME (T1.schema_id) as TemporalTableSchema
    , OBJECT_NAME(IT.parent_object_id) as TemporalTableName
    , T1.object_id as TemporalTableObjectId
    , IT.Name as InternalHistoryStagingName
    , SCHEMA_NAME (T2.schema_id) as HistoryTableSchema
    , OBJECT_NAME (T1.history_table_id) as HistoryTableName
FROM sys.internal_tables IT
JOIN sys.tables T1
    ON IT.parent_object_id = T1.object_id
JOIN sys.tables T2
    ON T1.history_table_id = T2.object_id
WHERE T1.is_memory_optimized = 1 AND T1.temporal_type = 2

```

## <a name="modifying-data"></a>修改資料

原生編譯的預存程序可讓您將非暫時記憶體最佳化的資料表轉換成系統版本設定，並保留現有的原生預存程序，因此您可以透過這些預存程序來修改系統版本設定的記憶體最佳化時態表。

以下範例展示如何在原生編譯的模組中修改先前建立的資料表。

```sql
CREATE PROCEDURE dbo.UpdateFXCurrencyPair
   (
      @ProviderID int
      , @CurrencyID1 int
      , @CurrencyID2 int
      , @BidRate decimal(8,4)
      , @AskRate decimal(8,4)
   )
WITH NATIVE_COMPILATION, SCHEMABINDING
   , EXECUTE AS OWNER
AS
   BEGIN ATOMIC WITH
   (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'English')
      UPDATE dbo.FXCurrencyPairs SET AskRate = @AskRate, BidRate = @BidRate
     WHERE ProviderID = @ProviderID AND CurrencyID1 = @CurrencyID1 AND CurrencyID2 = @CurrencyID2
END
GO ;

```

## <a name="see-also"></a>另請參閱

- [系統版本設定時態表與記憶體最佳化資料表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [建立記憶體最佳化的系統版本設定時態表](../../relational-databases/tables/creating-a-memory-optimized-system-versioned-temporal-table.md)
- [監視記憶體最佳化的系統建立版本時態表](../../relational-databases/tables/monitoring-memory-optimized-system-versioned-temporal-tables.md)
- [記憶體最佳化系統版本控制時態表的效能考量事項](../../relational-databases/tables/
- [時態表](../../relational-databases/tables/temporal-tables.md)
- [時態表系統一致性檢查](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [管理系統設定版本時態表中的歷程記錄資料保留](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [暫存資料表中繼資料檢視和函數](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
