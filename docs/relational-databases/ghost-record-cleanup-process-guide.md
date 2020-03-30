---
title: 準刪除清除程序指南 | Microsoft Docs
ms.custom: ''
ms.date: 05/02/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- ghost cleanup
- ghost records
- ghost clean up process
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 34be16d305bbb42a23c686e9b2befdd83792d523
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "72890491"
---
# <a name="ghost-cleanup-process-guide"></a>準刪除清除程序指南

準刪除清除程序是單一執行緒背景程序，會將已標示為要刪除的記錄從頁面刪除。 下文提供此程序的概觀。

## <a name="ghost-records"></a>準刪除記錄

從索引頁的分葉層級刪除的記錄不會實際從頁面移除；相反地，該記錄會標示為「要刪除」或「準刪除」  。 這表示資料列會保留在頁面上，但資料列標頭會稍微變更，以指出資料列實際上是準刪除。 這是為了最佳化刪除作業期間的效能。 準刪除不僅對於資料列層級鎖定是必要的，對於需要維護舊版資料列的快照隔離也是必要的。

## <a name="ghost-record-cleanup-task"></a>準刪除記錄清除工作

標示為要刪除或「準刪除」  的記錄會由背景準刪除清除程序清除。 此背景程序有時會在認可刪除交易之後執行，並從頁面實際移除準刪除記錄。 準刪除清除程序會每隔一段時間自動執行 (SQL Server 2012+ 為每隔 5 秒，SQL Server 2008/2008R2 為每隔 10 秒)，並檢查是否有任何頁面已標示為準刪除記錄。 如果找到任何項目，則會直接刪除標示為要刪除或「準刪除」  的記錄，每次執行最多處理 10 頁。

當記錄為準刪除時，資料庫會標示為具有準刪除項目，而且準刪除清除程序只會掃描這些資料庫。 一旦刪除所有準刪除記錄，準刪除清除程序也會將資料庫標示為「沒有任何準刪除記錄」，並在下次執行時略過此資料庫。 此程序也會略過無法採用共用鎖定的任何資料庫，並在下次執行時再試一次。

以下查詢可以識別單一資料庫中存在的準刪除記錄數目。 

 ```sql
 SELECT sum(ghost_record_count) total_ghost_records, db_name(database_id) 
 FROM sys.dm_db_index_physical_stats (NULL, NULL, NULL, NULL, 'SAMPLED')
 group by database_id
 order by total_ghost_records desc
```

## <a name="disable-the-ghost-cleanup"></a>停用準刪除清除

在具有多項刪除的高負載系統上，準刪除清除程序可能會在緩衝集區中保留頁面及產生 IO 時導致效能問題。 因此，您可以使用追蹤旗標 661 停用此程序。 如需詳細資訊，請參閱 [Tuning options for SQL Server when running high performance workloads](https://support.microsoft.com/help/920093/tuning-options-for-sql-server-when-running-in-high-performance-workloa) (執行高效能工作負載時，SQL Server 的微調選項)。 不過，停用此程序會對效能造成影響。

停用準刪除清除程序可能會造成資料庫成長過大，而可能導致效能問題。 因為準刪除清除程序會移除標示為準刪除的記錄，所以停用此程序會將這些記錄保留在頁面上，使得 SQL Server 無法重複使用此空間。 這會強制 SQL Server 改為將資料新增至新頁面，而導致資料庫檔案膨脹，也可能會造成[頁面分割](indexes/specify-fill-factor-for-an-index.md)。 建立執行計畫及執行掃描作業時，頁面分割會導致效能問題。 

一旦停用準刪除清除程序，您必須採取一些動作才能移除準刪除記錄。 一個選項是執行索引重建，這會在頁面上移動資料。 另一個選項是手動執行 [sp_clean_db_free_space](system-stored-procedures/sp-clean-db-free-space-transact-sql.md) (以清除所有資料庫資料檔案) 或 [sp_clean_db_file_free_space](system-stored-procedures/sp-clean-db-file-free-space-transact-sql.md) (以清除單一資料庫資料檔案)，這會刪除準刪除記錄。

 >[!warning]
 > 通常不建議停用準刪除清除程序。 您應該在受控制的環境中完整測試此做法，再於生產環境中永久實作。


## <a name="next-steps"></a>後續步驟  
[停用準刪除清除程序](https://support.microsoft.com/help/920093/tuning-options-for-sql-server-when-running-in-high-performance-workloa)
<br>[從單一資料庫檔案移除準刪除記錄](system-stored-procedures/sp-clean-db-file-free-space-transact-sql.md)
<br>[從所有資料庫資料檔案移除準刪除記錄](system-stored-procedures/sp-clean-db-free-space-transact-sql.md)


