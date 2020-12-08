---
title: SQL Server 的 Databases 物件 | Microsoft Docs
description: 了解 SQLServer:Databases 物件，其所提供計數器可監視大量複製作業、備份和還原輸送量以及交易記錄活動。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Databases object
- SQLServer:Databases
- Availability Groups [SQL Server], performance counters
ms.assetid: a7f9e7d4-fff4-4c72-8b3e-3f18dffc8919
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 0c98d04b9b82feabe1c6ad96cc28faf828223e68
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505739"
---
# <a name="sql-server-databases-object"></a>SQL Server、Databases 物件
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  SQL Server 中的 **SQLServer:Databases** 物件提供計數器，可用來監視大量複製作業、備份和還原輸送量以及交易記錄活動。 監視交易和交易記錄檔，可以判斷資料庫中有多少使用者活動，以及交易記錄檔有多滿。 使用者活動量可用來判斷資料庫的效能，並且會影響記錄檔大小、鎖定和複寫。 監視低階記錄檔活動，則可量測使用者活動和資源使用量，以協助您找出效能瓶頸。  
  
 您可同時監視 **Databases** 物件的多個執行個體，每個執行個體都代表一個資料庫。  
  
 下表描述 SQL Server **Databases** 計數器。  
  
|SQL Server Databases 計數器|描述|  
|-----------------------------------|-----------------|  
|**Active Transactions**|資料庫的使用中交易數。|  
|**Avg Dist From EOL/LP Request**|從每個記錄集區要求的記錄檔結尾之平均距離 (以位元組為單位)，供最後一個 VLF 中的要求之用。| 
|**Backup/Restore Throughput/sec**|每秒的資料庫備份和還原作業之讀取/寫入輸送量。 例如，您可以測量同時使用更多個備份裝置或是使用了更快的裝置時，資料庫備份作業的效能改變情形。 資料庫備份或還原作業的輸送量，可讓您判斷備份和還原作業的進度和效能。|  
|**Bulk Copy Rows/sec**|每秒大量複製 (Bulk Copy) 的資料列數。|  
|**Bulk Copy Throughput/sec**|每秒大量複製的資料量 (以 KB 為單位)。|  
|**Commit table entries**|資料庫認可資料表之記憶體內部部分的大小 (資料列計數)。 如需詳細資訊，請參閱 [sys.dm_tran_commit_table &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/change-tracking-sys-dm-tran-commit-table.md)。|  
|**Data File(s) Size (KB)**|資料庫內的所有資料檔案總計大小 (以 KB 為單位)，包含任何自動的成長。 監視此計數器很有用，例如可決定 **tempdb** 的正確大小。|  
|**DBCC Logical Scan Bytes/sec**|資料庫主控台命令 (DBCC) 每秒的邏輯讀取掃描位元組數。|  
|**Group Commit Time/sec**|每秒的群組延遲時間 (百萬分之一秒)。|
|**Log Bytes Received/sec**|轉存的記錄檔位元組總數。|  
|**Log Cache Hit Ratio**|記錄檔快取所滿足的記錄檔快取讀取百分比。|  
|**Log Cache Hit Ratio Base**|僅供內部使用。| 
|**Log Cache Reads/sec**|每秒透過記錄檔管理員快取所執行的讀取數。|  
|**Log File(s) Size (KB)**|資料庫內所有交易記錄檔的總計大小 (以位元組為單位)。|  
|**Log File(s) Used Size (KB)**|資料庫中所有記錄檔的總計使用大小。|  
|**Log Flush Wait Time**|排清記錄檔的等候時間總計 (以毫秒為單位)。 在 AlwaysOn 次要資料庫上，此值表示記錄檔記錄強行寫入磁碟的等候時間。|  
|**Log Flush Waits/sec**|每秒鐘等候記錄檔排清的認可數。|  
|**Log Flush Write Time (ms)**|執行在最後一筆記錄中完成之記錄檔排清寫入的時間 (以毫秒為單位)。|  
|**Log Flushes/sec**|每秒的記錄檔排清數目。|  
|**Log Growths**|資料庫之交易記錄檔的擴大總次數。|  
|**Log Pool Cache Misses/sec**|記錄檔區塊無法在記錄檔集區中使用的要求數目。 「記錄集區」是交易記錄的記憶體中快取。 此快取是用來最佳化記錄的讀取，以便進行復原、交易複寫、回復和 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]。|  
|**Log Pool Disk Reads/sec**|由記錄檔集區發出來提取記錄檔區塊的磁碟讀取數目。|  
|**Log Pool Hash Deletes/sec**|從記錄集區刪除原始雜湊項目的比率。|
|**Log Pool Hash Inserts/sec**|原始雜湊項目插入記錄集區的速率。|
|**Log Pool Invalid Hash Entry/sec**|因為無效而導致雜湊查閱失敗的比率。|
|**Log Pool Log Scan Pushes/sec**|可能來自於磁碟或記憶體而由記錄掃描所發送的記錄區塊比率。|
|**Log Pool LogWriter Pushes/sec**|記錄寫入器執行緒所發送的記錄區塊比率。|
|**Log Pool Push Empty FreePool/sec**|因可用集區空白而造成記錄區塊發送失敗的比率。|
|**Log Pool Push Low Memory/sec**|因記憶體不足而造成記錄區塊發送失敗的比率。|
|**Log Pool Push No Free Buffer/sec**|因可用緩衝區無法使用而造成記錄區塊發送失敗的比率。|
|**Log Pool Req.Behind Trunc/sec**|因為要求的區塊在截斷 LSN 後面，所以遺漏了記錄集區快取。|
|**Log Pool Requests Base**|僅供內部使用。| 
|**Log Pool Requests Old VLF/sec**|不在日誌最後一個 VLF 中的記錄集區要求。|  
|**Log Pool Requests/sec**|記錄檔集區處理的記錄檔區塊要求數目。|  
|**Log Pool Total Active Log Size**|儲存在共用快取緩衝區管理員中的目前使用中記錄總計 (位元組)。|
|**Log Pool Total Shared Pool Size**|共用快取緩衝區管理員的目前憶體使用量總記 (位元組)。|
|**Log Shrinks**|這個資料庫的記錄壓縮總數。|  
|**Log Truncations**|交易記錄截斷的次數 (在簡單復原模式下)。|  
|**Percent Log Used**|使用中的記錄檔空間百分比。|  
|**Repl.Pending Xacts**|標示成複寫、但未傳送到散發資料庫的發行集資料庫內的交易記錄檔之交易數。|  
|**Repl.Trans.Rate**|每秒自發行集資料的交易記錄檔讀取並傳送至散發資料庫的交易數。|  
|**Shrink Data Movement Bytes/sec**|經由自動壓縮作業或是 DBCC SHRINKDATABASE 或 DBCC SHRINKFILE 陳述式移動的每秒資料量。|  
|**Tracked transactions/sec**|資料庫的認可資料表中記錄的已認可交易數目。|  
|**Transactions/sec**|每秒針對資料庫啟動的交易數。<br /><br /> [Transactions/sec] 並未計入僅限 XTP 交易 (由原生編譯的預存程序啟動的交易)。|  
|**Write Transactions/sec**|上一秒寫入資料庫並認可的交易數目。|  
|**XTP Controller DLC Latency Base**|僅供內部使用。| 
|**XTP Controller DLC Latency/Fetch**|從記錄區塊輸入直接記錄取用者到 XTP 控制器加以擷取之間，每秒的平均延遲 (微秒)。|
|**XTP Controller DLC Peak Latency**|XTP 控制器所記錄，從直接記錄取用者提取的最長延遲時間 (微秒)。|
|**XTP Controller Log Processed/sec**|XTP 控制器執行緒每秒處理的記錄檔位元組數量。|
|**XTP Memory Used (KB)**|資料庫中 XTP 所使用的記憶體數量。| 
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用量 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server 的 Database Replica](../../relational-databases/performance-monitor/sql-server-database-replica.md)  
  
  
