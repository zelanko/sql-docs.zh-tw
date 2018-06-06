---
title: 自動統計資料 (Analytics Platform System)
description: 描述分析平台系統 AU7 中所引進的自動統計資料功能。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1c0f4623adad35ab874330b42aa54f6e1b91d961
ms.sourcegitcommit: fc3cd23685c6b9b6972d6a7bab2cc2fc5ebab5f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/25/2018
---
# <a name="configure-auto-statistics"></a>設定自動統計資料

了解如何設定要用於建立和自動更新統計資料的自動統計資料的平行處理資料倉儲。  使用這項功能，以便改善查詢計畫，因而改善查詢效能。

**適用於：** AP （起 AU7）

## <a name="what-are-statistics"></a>統計資料有哪些？
為達到查詢最佳化統計資料是包含資料表的一個或多個資料行中值分佈相關統計資料的物件。 查詢最佳化工具會使用這些統計資料來預估基數或查詢中資料列數目。 這些基數估計值會讓查詢最佳化工具建立高品質查詢計劃。 例如，ap，MPP 查詢最佳化工具使用基數估計值選擇隨機播放或複製中較小的兩個資料表用於 join 子句中，而在此情況下會改善查詢效能。  如需詳細資訊，請參閱[統計資料](../relational-databases/statistics/statistics.md)和[DBCC SHOW_STATISTICS](../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)

## <a name="what-are-auto-statistics"></a>什麼是自動統計資料？
自動統計資料是查詢最佳化工具會建立並自動更新以改善查詢計劃的統計資料。 統計資料可能會變成過期之後載入、 插入、 更新和刪除作業。 不自動統計資料，您必須進行您自己的分析，以了解哪些資料行需要統計資料，以及當需要更新統計資料。

自動統計資料包含下列三個設定： 

### <a name="autocreatestatistics"></a>AUTO_CREATE_STATISTICS
自動建立統計資料選項，當 AUTO_CREATE_STATISTICS 是 ON，查詢最佳化工具會在查詢述詞，在必要時，若要改善查詢計劃的基數估計值的個別資料行上建立統計資料。 這些單一資料行統計資料是針對在現有統計資料物件中尚未具有長條圖的資料行建立的。

### <a name="autoupdatestatistics"></a>AUTO_UPDATE_STATISTICS 
開啟自動更新統計資料選項 AUTO_UPDATE_STATISTICS 時，查詢最佳化工具就會判斷統計資料可能過期的時間，然後在查詢使用統計資料時加以更新。 變更資料表中的資料分佈統計資料就會變成過期之後作業插入、 更新、 刪除或合併或索引檢視表。 查詢最佳化工具會計算自從上次更新統計資料以來資料修改的次數，並且比較修改次數與臨界值，藉以判斷統計資料可能過期的時間。 此臨界值是以資料表或索引檢視表中的資料列數目為基礎。

### <a name="autoupdatestatisticsasync"></a>AUTO_UPDATE_STATISTICS_ASYNC
非同步統計資料更新選項 AUTO_UPDATE_STATISTICS_ASYNC 會決定查詢最佳化工具要使用同步或非同步統計資料更新。 Ap，非同步統計資料更新選項是 ON，根據預設，以及查詢最佳化工具會以非同步方式更新統計資料。 AUTO_UPDATE_STATISTICS_ASYNC 選項會套用至針對索引，查詢述詞，以及使用 CREATE STATISTICS 陳述式建立的統計資料中的單一資料行所建立的統計資料物件。

## <a name="configuration-settings-for-system-administrators"></a>系統管理員的組態設定
升級到 AP AU7 之後，預設會啟用自動統計資料。 系統管理員可以啟用或停用自動統計資料與[功能切換](appliance-feature-switch.md)應用裝置 Configuration Manager 中的選項。  啟用之後，使用者可以變更每個資料庫的統計資料設定。
變更任何功能的參數值需要 AP 上的重新啟動服務。

## <a name="change-auto-statistics-settings-on-a-database"></a>變更資料庫的自動統計資料設定
啟用自動統計資料時，系統管理員，您可以使用[ALTER DATABASE (Parallel Data Warehouse)](/sql/t-sql/statements/alter-database-parallel-data-warehouse)若要變更資料庫的統計資料設定。 如果啟用自動統計資料功能切換時，系統管理員，在升級至 AU7 之後建立任何新資料庫必須已啟用自動統計資料。 以 AU7 升級之前就存在的所有資料庫都有停用自動統計資料。 下列範例會啟用現有的資料庫 myPDW 上的自動統計資料。

```sql
ALTER DATABASE myPDW SET AUTO_CREATE_STATISTICS ON
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS ON 
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS_ASYNC ON
```
 
如果 AUTO_UPDATE_STATISTICS 是 ON，AUTO_UPDATE STATISTICS_ASYNC 選項才有用。  因此，統計資料時沒有更新 AUTO_UPDATE_STATISTICS 是 OFF 和 AUTO_UPDATE_STATISTICS_ASYNC 是 ON。 

### <a name="error-messages"></a>錯誤訊息
您可能會收到錯誤訊息 「 PDW 中不支援此選項 」。  當系統管理員尚未啟用自動統計資料，而且您嘗試設定任何自動統計資料選項的 ALTER DATABASE 時，就會發生此錯誤。 

### <a name="limitations-and-restrictions"></a>限制事項
自動統計資料在外部資料表上無法運作。 

### <a name="check-the-current-values"></a>請檢查目前的值
下列查詢會傳回所有資料庫的自動統計資料設定的目前值。

```sql
SELECT NAME
    , IS_AUTO_CREATE_STATS_ON 
    , IS_AUTO_UPDATE_STATS_ON
    , IS_AUTO_UPDATE_STATS_ASYNC_ON
FROM
    sys.databases;
```

傳回值 1 表示設定的影響，而 0 表示設定為關閉。 

## <a name="next-steps"></a>後續的步驟
若要查看您的查詢執行的方式，請參閱[監視使用中的查詢](monitoring-active-queries.md)
