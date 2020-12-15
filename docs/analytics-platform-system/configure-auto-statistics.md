---
title: 自動統計資料
description: 描述在 Analytics Platform System AU7 中引進的自動統計資料功能。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
monikerRange: '>= aps-pdw-2016-au7'
ms.openlocfilehash: fc204c5c4fd37ef4621c4376142662b7a9164ade
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97420185"
---
# <a name="configure-auto-statistics"></a>設定自動統計資料

瞭解如何設定平行資料倉儲，以使用自動統計資料自動建立和更新統計資料。  您可以使用這項功能來改善查詢計劃，進而改善查詢效能。

**適用于：** 從 2016-AU7) 開始的 AP (

## <a name="what-are-statistics"></a>什麼是統計資料？
查詢優化的統計資料是物件，其中包含有關資料表的一或多個資料行中值分佈的統計資訊。 查詢最佳化工具會使用這些統計資料來估計查詢結果中的「基數」(Cardinality) 或資料列數目。 這些「基數估計值」(Cardinality Estimate) 可讓查詢最佳化工具建立高品質的查詢計劃。 例如，在 AP 中，MPP 查詢最佳化工具會使用基數估計值來選擇將聯結子句中所使用的兩個數據表中的較小值，或將它複製到其中，以改善查詢效能。  如需詳細資訊，請參閱 [統計資料](../relational-databases/statistics/statistics.md) 和 [DBCC SHOW_STATISTICS](../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)

## <a name="what-are-auto-statistics"></a>什麼是自動統計資料？
自動統計資料是查詢最佳化工具會自動建立和更新的統計資料，以改善查詢計劃。 在載入、插入、更新和刪除作業之後，統計資料可能會變成過期狀態。 如果沒有自動統計資料，您必須自行分析以瞭解哪些資料行需要統計資料，以及何時需要更新統計資料。

自動統計資料包含下列三項設定： 

### <a name="auto_create_statistics"></a>AUTO_CREATE_STATISTICS
當自動建立統計資料選項 AUTO_CREATE_STATISTICS 為 ON 時，查詢最佳化工具就會視需要針對查詢述詞中的個別資料行來建立統計資料，以便改善查詢計劃的基數估計值。 這些單一資料行統計資料是針對在現有統計資料物件中尚未具有長條圖的資料行建立的。

### <a name="auto_update_statistics"></a>AUTO_UPDATE_STATISTICS 
開啟自動更新統計資料選項 AUTO_UPDATE_STATISTICS 時，查詢最佳化工具就會判斷統計資料可能過期的時間，然後在查詢使用統計資料時加以更新。 當作業插入、更新、刪除或合併變更資料表或索引檢視表中的資料分佈之後，統計資料就會變成過期。 查詢最佳化工具會計算自從上次更新統計資料以來資料修改的次數，並且比較修改次數與臨界值，藉以判斷統計資料可能過期的時間。 此臨界值是以資料表或索引檢視表中的資料列數目為基礎。

### <a name="auto_update_statistics_async"></a>AUTO_UPDATE_STATISTICS_ASYNC
非同步統計資料更新選項 AUTO_UPDATE_STATISTICS_ASYNC 會決定查詢最佳化工具要使用同步或非同步統計資料更新。 針對 [AP]，[非同步統計資料更新] 選項預設為開啟，而查詢最佳化工具會以非同步方式更新統計資料。 AUTO_UPDATE_STATISTICS_ASYNC 選項會套用至針對索引所建立的統計資料物件、查詢述詞中的單一資料行，以及使用CREATE STATISTICS 陳述式所建立的統計資料。

## <a name="configuration-settings-for-system-administrators"></a>系統管理員的配置設定
升級至 AP AU7 之後，預設會啟用自動統計資料。 系統管理員可以使用設備 Configuration Manager 中的 [功能切換](appliance-feature-switch.md) 選項來啟用或停用自動統計資料。  啟用之後，使用者就可以變更每個資料庫的統計資料設定。
變更任何功能參數值時，需要在 AP 上重新開機服務。

## <a name="change-auto-statistics-settings-on-a-database"></a>變更資料庫上的自動統計資料設定
當系統管理員啟用自動統計資料時，您可以使用 [ALTER DATABASE (平行資料倉儲) ](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) 來變更資料庫上的統計資料設定。 如果系統管理員已啟用自動統計資料功能切換，則在升級至 AU7 之後建立的任何新資料庫都會啟用自動統計資料。 升級至 AU7 之前存在的所有資料庫都已停用自動統計資料。 下列範例會在現有的資料庫 myPDW 上啟用自動統計資料。

```sql
ALTER DATABASE myPDW SET AUTO_CREATE_STATISTICS ON
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS ON 
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS_ASYNC ON
```
 
只有在 AUTO_UPDATE_STATISTICS 為 ON 時，AUTO_UPDATE STATISTICS_ASYNC 選項才能運作。  因此，當 AUTO_UPDATE_STATISTICS 為 OFF 且 AUTO_UPDATE_STATISTICS_ASYNC 為 ON 時，不會更新統計資料。 

### <a name="error-messages"></a>錯誤訊息
您可能會收到錯誤訊息「PDW 中不支援此選項」。  當系統管理員尚未啟用自動統計資料，而且您嘗試在 ALTER DATABASE 中設定任何自動統計資料選項時，就會發生這個錯誤。 

### <a name="limitations-and-restrictions"></a>限制事項
自動統計資料無法在外部資料表上運作。 

### <a name="check-the-current-values"></a>檢查目前的值
下列查詢會傳回所有資料庫的自動統計資料設定目前的值。

```sql
SELECT NAME
    , IS_AUTO_CREATE_STATS_ON 
    , IS_AUTO_UPDATE_STATS_ON
    , IS_AUTO_UPDATE_STATS_ASYNC_ON
FROM
    sys.databases;
```

傳回值1表示設定為開啟，0表示設定為關閉。 

## <a name="next-steps"></a>後續步驟
若要查看查詢的執行方式，請參閱監視使用中的 [查詢](monitoring-active-queries.md)
