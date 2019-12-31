---
title: 自動統計資料
description: 說明分析平臺系統 AU7 中引進的自動統計資料功能。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: 7071c9cb46bde6e2d353293cec9f01451c0b4f67
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401279"
---
# <a name="configure-auto-statistics"></a>設定自動統計資料

瞭解如何設定平行處理資料倉儲，以使用自動統計資料來自動建立和更新統計資料。  使用此功能可改善查詢計劃，因而改善查詢效能。

**適用物件：** AP （從 2016-AU7 開始）

## <a name="what-are-statistics"></a>什麼是統計資料？
查詢優化的統計資料是物件，其中包含有關資料表的一或多個資料行中值分佈的統計資訊。 查詢最佳化工具會使用這些統計資料來估計查詢結果中的「基數」(Cardinality) 或資料列數目。 這些「基數估計值」(Cardinality Estimate) 可讓查詢最佳化工具建立高品質的查詢計劃。 例如，在 AP 中，MPP 查詢最佳化工具會使用基數估計值來選擇隨機播放或複寫聯結子句中所使用的兩個數據表中較小的一個，如此便可改善查詢效能。  如需詳細資訊，請參閱[統計資料](../relational-databases/statistics/statistics.md)和[DBCC SHOW_STATISTICS](../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)

## <a name="what-are-auto-statistics"></a>什麼是自動統計資料？
自動統計資料是查詢最佳化工具建立的統計資料，而且會自動更新以改善查詢計劃。 在載入、插入、更新和刪除作業之後，統計資料可能會變成過期狀態。 如果沒有自動統計資料，您必須執行自己的分析，以瞭解需要統計資料的資料行，以及何時需要更新統計資料。

自動統計資料包含下列三個設定： 

### <a name="auto_create_statistics"></a>AUTO_CREATE_STATISTICS
當自動建立統計資料選項 AUTO_CREATE_STATISTICS 為 ON 時，查詢最佳化工具就會視需要針對查詢述詞中的個別資料行來建立統計資料，以便改善查詢計劃的基數估計值。 這些單一資料行統計資料是針對在現有統計資料物件中尚未具有長條圖的資料行建立的。

### <a name="auto_update_statistics"></a>AUTO_UPDATE_STATISTICS 
開啟自動更新統計資料選項 AUTO_UPDATE_STATISTICS 時，查詢最佳化工具就會判斷統計資料可能過期的時間，然後在查詢使用統計資料時加以更新。 當作業插入、更新、刪除或合併變更資料表或索引檢視表中的資料分佈之後，統計資料就會變成過期。 查詢最佳化工具會計算自從上次更新統計資料以來資料修改的次數，並且比較修改次數與臨界值，藉以判斷統計資料可能過期的時間。 此臨界值是以資料表或索引檢視表中的資料列數目為基礎。

### <a name="auto_update_statistics_async"></a>AUTO_UPDATE_STATISTICS_ASYNC
非同步統計資料更新選項 AUTO_UPDATE_STATISTICS_ASYNC 會決定查詢最佳化工具要使用同步或非同步統計資料更新。 對於 AP，非同步統計資料更新選項預設為開啟，而且查詢最佳化工具會以非同步方式更新統計資料。 AUTO_UPDATE_STATISTICS_ASYNC 選項會套用至針對索引所建立的統計資料物件、查詢述詞中的單一資料行，以及使用CREATE STATISTICS 陳述式所建立的統計資料。

## <a name="configuration-settings-for-system-administrators"></a>系統管理員的配置設定
升級至 [AP] AU7 之後，預設會啟用 [自動統計資料]。 系統管理員可以使用設備 Configuration Manager 中的[功能切換](appliance-feature-switch.md)選項來啟用或停用自動統計資料。  啟用之後，使用者可以變更每個資料庫的統計資料設定。
變更任何功能切換值需要在 AP 上重新開機服務。

## <a name="change-auto-statistics-settings-on-a-database"></a>變更資料庫上的自動統計資料設定
當系統管理員啟用自動統計資料時，您可以使用[ALTER DATABASE （平行處理資料倉儲）](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)來變更資料庫上的統計資料設定。 如果系統管理員已啟用自動統計資料功能參數，則在升級至 AU7 之後所建立的任何新資料庫都會啟用自動統計資料。 升級至 AU7 之前已存在的所有資料庫都會停用自動統計資料。 下列範例會在現有的資料庫 myPDW 上啟用自動統計資料。

```sql
ALTER DATABASE myPDW SET AUTO_CREATE_STATISTICS ON
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS ON 
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS_ASYNC ON
```
 
只有在 AUTO_UPDATE_STATISTICS 為 ON 時，AUTO_UPDATE STATISTICS_ASYNC 選項才有效。  因此，當 AUTO_UPDATE_STATISTICS 關閉且 AUTO_UPDATE_STATISTICS_ASYNC 為 ON 時，不會更新統計資料。 

### <a name="error-messages"></a>錯誤訊息
您可能會收到錯誤訊息「PDW 中不支援此選項」。  當系統管理員尚未啟用自動統計資料，而且您嘗試在 ALTER DATABASE 中設定任何自動統計資料選項時，就會發生此錯誤。 

### <a name="limitations-and-restrictions"></a>限制事項
自動統計資料不適用於外部資料表。 

### <a name="check-the-current-values"></a>檢查目前的值
下列查詢會傳回所有資料庫之 [自動統計資料] 設定的目前值。

```sql
SELECT NAME
    , IS_AUTO_CREATE_STATS_ON 
    , IS_AUTO_UPDATE_STATS_ON
    , IS_AUTO_UPDATE_STATS_ASYNC_ON
FROM
    sys.databases;
```

1的傳回值表示設定為 on，而0表示設定為關閉。 

## <a name="next-steps"></a>接下來的步驟
若要查看查詢的執行方式，請參閱監視使用中[查詢](monitoring-active-queries.md)
