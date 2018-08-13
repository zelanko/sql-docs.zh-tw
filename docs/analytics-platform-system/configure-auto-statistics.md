---
title: 自動統計資料 (Analytics Platform System)
description: 描述 Analytics Platform System AU7 中引進的自動統計資料功能。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: 448c9de27422c01d68602c00945b1ea72bcddd61
ms.sourcegitcommit: 2e038db99abef013673ea6b3535b5d9d1285c5ae
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2018
ms.locfileid: "39400911"
---
# <a name="configure-auto-statistics"></a>設定自動統計資料

了解如何設定要用於建立和自動更新統計資料的自動統計資料的平行處理資料倉儲。  使用這項功能來改善查詢計劃，並因而改善查詢效能。

**適用於：** AP （從 2016 AU7 開始）

## <a name="what-are-statistics"></a>統計資料有哪些？
查詢最佳化統計資料是包含資料表的一個或多個資料行中值分佈的統計資訊的物件。 查詢最佳化工具會使用這些統計資料來預估基數，或數字的資料列，在查詢中產生結果。 這些的基數估計值，讓查詢最佳化工具建立高品質的查詢計劃。 例如，在 AP，MPP 查詢最佳化工具使用基數估計值選擇隨機播放或複寫中較小的兩個資料表，用在 join 子句，並在此情況下會改善查詢效能。  如需詳細資訊，請參閱 <<c0> [ 統計資料](../relational-databases/statistics/statistics.md)和[DBCC SHOW_STATISTICS](../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)

## <a name="what-are-auto-statistics"></a>什麼是自動統計資料？
自動統計資料是查詢最佳化工具會建立，並會自動更新以改善查詢計劃的統計資料。 統計資料可能過期之後載入、 插入、 更新和刪除作業。 沒有自動統計資料，您必須執行您自己的分析，以了解哪些資料行需要統計資料，以及何時更新統計資料。

自動統計資料包含下列三項設定： 

### <a name="autocreatestatistics"></a>AUTO_CREATE_STATISTICS
自動建立統計資料選項，當 AUTO_CREATE_STATISTICS 為 ON 時，查詢最佳化工具會在查詢述詞中，必要時，若要改善查詢計劃的基數估計值的個別資料行上建立統計資料。 這些單一資料行統計資料是針對在現有統計資料物件中尚未具有長條圖的資料行建立的。

### <a name="autoupdatestatistics"></a>AUTO_UPDATE_STATISTICS 
開啟自動更新統計資料選項 AUTO_UPDATE_STATISTICS 時，查詢最佳化工具就會判斷統計資料可能過期的時間，然後在查詢使用統計資料時加以更新。 當作業插入、更新、刪除或合併變更資料表或索引檢視表中的資料分佈之後，統計資料就會變成過期。 查詢最佳化工具會計算自從上次更新統計資料以來資料修改的次數，並且比較修改次數與臨界值，藉以判斷統計資料可能過期的時間。 此臨界值是以資料表或索引檢視表中的資料列數目為基礎。

### <a name="autoupdatestatisticsasync"></a>AUTO_UPDATE_STATISTICS_ASYNC
非同步統計資料更新選項 AUTO_UPDATE_STATISTICS_ASYNC 會決定查詢最佳化工具要使用同步或非同步統計資料更新。 AP，非同步統計資料更新選項是 ON，根據預設，以及查詢最佳化工具會以非同步方式更新統計資料。 AUTO_UPDATE_STATISTICS_ASYNC 選項會套用至針對索引所建立的統計資料物件、查詢述詞中的單一資料行，以及使用CREATE STATISTICS 陳述式所建立的統計資料。

## <a name="configuration-settings-for-system-administrators"></a>系統管理員的組態設定
升級至 AP AU7 之後，預設會啟用自動統計資料。 系統管理員可以啟用或停用自動統計資料[功能切換](appliance-feature-switch.md)設備 Configuration Manager 中的選項。  啟用之後，使用者可以變更每個資料庫的統計資料設定。
變更任何功能參數值需要 AP 上的重新啟動服務。

## <a name="change-auto-statistics-settings-on-a-database"></a>變更資料庫的自動統計資料設定
啟用自動統計資料時，系統管理員，您可以使用[ALTER DATABASE （平行資料倉儲）](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)變更資料庫的統計資料設定。 如果系統管理員會啟用自動統計資料功能的參數，以 AU7 升級之後建立任何新資料庫必須啟用自動統計資料。 以 AU7 升級之前就存在的所有資料庫都已停用自動統計資料。 下列範例會啟用現有的資料庫 myPDW 上的自動統計資料。

```sql
ALTER DATABASE myPDW SET AUTO_CREATE_STATISTICS ON
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS ON 
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS_ASYNC ON
```
 
AUTO_UPDATE STATISTICS_ASYNC 選項僅適用於 AUTO_UPDATE_STATISTICS 是 ON。  因此，統計資料時沒有更新 AUTO_UPDATE_STATISTICS 是 OFF 和 AUTO_UPDATE_STATISTICS_ASYNC 是 ON。 

### <a name="error-messages"></a>錯誤訊息
您可能會收到錯誤訊息 「 此選項不支援在 PDW 中 」。  當系統管理員尚未啟用自動統計資料，而且您嘗試設定任何自動統計資料選項的 ALTER DATABASE 時，就會發生此錯誤。 

### <a name="limitations-and-restrictions"></a>限制事項
自動統計資料在外部資料表上無法運作。 

### <a name="check-the-current-values"></a>檢查目前的值
下列查詢會傳回所有資料庫的自動統計資料設定的目前值。

```sql
SELECT NAME
    , IS_AUTO_CREATE_STATS_ON 
    , IS_AUTO_UPDATE_STATS_ON
    , IS_AUTO_UPDATE_STATS_ASYNC_ON
FROM
    sys.databases;
```

傳回值 1 表示的設定，而 0 表示設定為關閉。 

## <a name="next-steps"></a>後續步驟
若要查看您的查詢執行的方式，請參閱[監視使用中的查詢](monitoring-active-queries.md)
