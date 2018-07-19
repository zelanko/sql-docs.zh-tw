---
title: 記憶體最佳化資料表的統計資料 | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e644766d-1d1c-43d7-83ff-8ccfe4f3af9f
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b1c664857e75b8f647b02905a26effb8e8b2c5e2
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
ms.locfileid: "34328279"
---
# <a name="statistics-for-memory-optimized-tables"></a>記憶體最佳化資料表的統計資料
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  查詢最佳化工具會使用有關資料行的統計資料來建立可改善查詢效能的查詢計劃。 統計資料是從資料庫中的資料表收集，並且儲存在資料庫中繼資料內。  
  
 統計資料是自動建立的，但也可以手動建立。 例如，建立索引時就會自動建立索引鍵資料行的統計資料。 如需有關建立統計資料的詳細資訊，請參閱 [統計資料](../../relational-databases/statistics/statistics.md)。  
  
 資料表資料通常會隨資料列插入、更新和刪除而變更。 這表示，統計資料需要定期更新。 根據預設，資料表上的統計資料會在查詢最佳化工具判斷統計資料可能過期時自動更新。  
  
 記憶體最佳化資料表上統計資料的考量：  
  
-   從 SQL Server 2016 和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]開始，當使用至少 130 的資料庫相容性層級時，記憶體最佳化的資料表支援自動更新統計資料。 請參閱 [ALTER DATABASE 相容性層級 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。 如果資料庫中有先前使用較低相容性層級建立的資料表，則需要以手動方式更新一次統計資料，讓統計資料的自動更新能夠繼續。
  
-   若是原生編譯預存程序，程序中查詢的執行計畫會在編譯程序時最佳化，也就是在建立時進行。 它們不會在統計資料更新時自動重新編譯。 因此，在建立程序之前，資料表應該包含代表性的資料集。  
  
-   原生編譯的預存程序可以使用 [sp_recompile (TRANSACT-SQL)](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md)以手動方式重新編譯，如果資料庫離線後再次上線，或發生資料庫容錯移轉或伺服器重新啟動，它們就會自動重新編譯。  
  
## <a name="enabling-automatic-update-of-statistics-in-existing-tables"></a>在現有資料表中啟用統計資料的自動更新

在相容性層級至少為 130 的資料庫中建立資料表時，會針對該資料表的所有統計資料啟用統計資料自動更新，不需任何進一步的動作。

如果資料庫中有在較低 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本建立的記憶體最佳化資料表，或是資料庫的相容性層級低於 130，則需要以手動方式更新一次統計資料，讓自動更新能夠繼續。

若要啟用以較舊相容性層級建立之記憶體最佳化資料表的統計資料自動更新，請遵循下列步驟︰

1. 更新資料庫相容性層級： `ALTER DATABASE CURRENT SET COMPATIBILITY_LEVEL=130`

2. 以手動方式更新記憶體最佳化資料表的統計資料。 以下是執行相同作業的範例指令碼。

3. 以手動方式重新編譯原生編譯的預存程序，可因更新過的統計資料而受益。

*統計資料的一次性指令碼︰* 相容性層級建立的記憶體最佳化資料表，您可以執行一次下列 Transact-SQL 指令碼，更新所有記憶體最佳化資料表的統計資料，並啟用往後的統計資料自動更新 (假設資料庫已啟用 AUTO_UPDATE_STATISTICS)︰

```
-- Assuming AUTO_UPDATE_STATISTICS is already ON for your database:
-- ALTER DATABASE CURRENT SET AUTO_UPDATE_STATISTICS ON;

ALTER DATABASE CURRENT SET COMPATIBILITY_LEVEL = 130;
GO
DECLARE @sql NVARCHAR(MAX) = N'';
SELECT
      @sql += N'UPDATE STATISTICS '
         + quotename(schema_name(t.schema_id))
         + N'.'
         + quotename(t.name)
         + ';' + CHAR(13) + CHAR(10)
   FROM sys.tables AS t
   WHERE t.is_memory_optimized = 1 AND 
        t.object_id IN (SELECT object_id FROM sys.stats WHERE no_recompute=1)
;
EXECUTE sp_executesql @sql;
GO
-- Each row appended to @sql looks roughly like:
-- UPDATE STATISTICS [dbo].[MyMemoryOptimizedTable];
```

*驗證已啟用自動更新︰* 下列指令碼會驗證是否已啟用記憶體最佳化資料表統計資料的自動更新。 執行上述指令碼之後，它會針對所有統計資料物件，在資料行中 `1` 傳回 `auto-update enabled` 。

```
SELECT 
    quotename(schema_name(o.schema_id)) + N'.' + quotename(o.name) AS [table],
    s.name AS [statistics object],
    1-s.no_recompute AS [auto-update enabled]
FROM sys.stats s JOIN sys.tables o ON s.object_id=o.object_id
WHERE o.is_memory_optimized=1
```

## <a name="guidelines-for-deploying-tables-and-procedures"></a>資料表和程序的部署指導方針  
 為確保查詢最佳化工具在建立查詢計劃時擁有最新的統計資料，請利用下列四個步驟部署記憶體最佳化的資料表，和存取這些資料表的原生編譯預存程序：  
  
1.  確保資料庫的相容性層級為至少 130。 請參閱 [ALTER DATABASE 相容性層級 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。

2.  建立資料表及索引。 應該以內嵌方式在 **CREATE TABLE** 陳述式指定索引。  
  
3.  將資料載入資料表中。  
  
4.  建立存取資料表的預存程序。  
  
 在您載入資料後建立原生編譯預存程序，可確保最佳化工具具有記憶體最佳化資料表的統計資料。 這樣將可確保編譯程序時，查詢計劃能夠保持效率。  

## <a name="see-also"></a>另請參閱  
 [記憶體最佳化資料表](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
