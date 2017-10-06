---
title: "SQL Server Database Engine 和 Azure SQL Database 的效能中心 | Microsoft Docs"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 04/08/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.service: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- Performance (SQL Server)
- Performance (SQL Database)
helpviewer_keywords:
- SQL Server, performance
- performance (SQL Server)
- database performance (SQL Server)
- SQL Database (Performance)
- performance (SQL Database)
- database performance (SQL Database)
ms.assetid: 301204b2-140d-4495-98ed-021a9b5025f5
caps.latest.revision: 14
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 6490c2356c0753f68e7ef5261ede3d699a08b863
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# <a name="performance-center-for-sql-server-database-engine-and-azure-sql-database"></a>SQL Server Database Engine 和 Azure SQL Database 的效能中心
  本頁提供的連結有助於您尋找所需之 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 和 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]中的效能相關資訊。  
  
 **圖例**  
  
 ![security-center-legend](../../relational-databases/performance/media/security-center-legend.PNG "security-center-legend")  
  
## <a name="this-is-a-work-in-process-does-this-performance-center-help-you-how-can-we-improve-it"></a>這是正在處理的工作。 這個效能中心對您有幫助嗎？ 我們該如何改善它？  
 您要尋找哪些資訊？找到了嗎？ 我們是否遺漏了什麼？ 您想要在這裡看到什麼？ 我們會持續聽取您的意見來改進內容。 請將您的意見傳送到 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Temporal%20Tables%20page)  
  
## <a name="configuration-options-for-performance"></a>效能的組態選項  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可讓您透過許多組態選項來影響 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 層級的資料庫引擎效能。 使用 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]，Microsoft 會為您執行其中的大部分 (但非全部) 最大化。  
  
|||  
|-|-|  
|**磁碟組態選項**|-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [磁碟分割和 RAID](https://technet.microsoft.com/library/ms190764\(v=sql.105\).aspx)|  
|**資料和記錄檔組態選項**|-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [將資料與記錄檔放在不同的磁碟機上](../../relational-databases/policy-based-management/place-data-and-log-files-on-separate-drives.md)<br />-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [檢視或變更資料與記錄檔的預設位置 &#40;SQL Server Management Studio&#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md)|  
|**TempDB 組態選項**|-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [TempDB 中的效能改進](https://msdn.microsoft.com/library/ms190768.aspx#Anchor_1)<br />-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [資料庫引擎組態 - TempDB](http://msdn.microsoft.com/library/7aabd304-f3c9-4c2d-bf9d-5479ee2498da)<br />-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [在 Azure VM 中使用 SSD 來儲存 SQL Server TempDB 與緩衝集區延伸](http://blogs.technet.com/b/dataplatforminsider/archive/2014/09/25/using-ssds-in-azure-vms-to-store-sql-server-tempdb-and-buffer-pool-extensions.aspx)<br />-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [Azure 虛擬機器中 SQL Server 暫存磁碟的磁碟與效能最佳做法](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-performance-best-practices/)|  
|![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") **伺服器組態選項**|<ul><li>**處理器組態選項**<br /><br /> <ul><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [親和性遮罩伺服器組態選項](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)</li><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [親和性輸入 - 輸出遮罩伺服器組態選項](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)</li><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [affinity64 遮罩伺服器組態選項](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md)</li><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [affinity64 輸入 - 輸出遮罩伺服器組態選項](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md)</li><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [設定最大背景工作執行緒伺服器組態選項](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)</li></ul></li><li>**記憶體組態選項**<br /><br /> <ul><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [伺服器記憶體伺服器組態選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)</li></ul></li><li>**索引組態選項**<br /><br /> <ul><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [設定填滿因數伺服器組態選項](../../database-engine/configure-windows/configure-the-fill-factor-server-configuration-option.md)</li><li></li></ul></li><li>**查詢組態選項**<br /><br /> <ul><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [設定每個查詢的最小記憶體伺服器組態選項](../../database-engine/configure-windows/configure-the-min-memory-per-query-server-configuration-option.md)</li><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [設定查詢管理員成本限制伺服器組態選項](../../database-engine/configure-windows/configure-the-query-governor-cost-limit-server-configuration-option.md)</li><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [設定平行處理原則的最大程度伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)</li><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [設定平行處理原則的成本閾值伺服器組態選項](../../database-engine/configure-windows/configure-the-cost-threshold-for-parallelism-server-configuration-option.md)</li><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [將臨機操作工作負載最佳化伺服器組態選項](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md)</li></ul></li><li>**備份組態選項**<br /><br /> <ul><li>![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [檢視或設定備份壓縮預設伺服器組態選項](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)</li></ul></li></ul>|  
|**資料庫組態最佳化選項**|-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [資料壓縮](../../relational-databases/data-compression/data-compression.md)<br />-   ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") [檢視或變更資料庫的相容性層級](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)<br />-   ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)|  
|**資料表組態最佳化**|-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [資料分割資料表與索引](../../relational-databases/partitions/partitioned-tables-and-indexes.md)<br />-|  
|**Azure 虛擬機器中的 Database Engine 效能**|-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [快速檢查清單](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-performance-best-practices/)<br />-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [虛擬機器大小與儲存體帳戶考量](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-sql-server-performance-best-practices/)<br />-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [磁碟與效能考量](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-performance-best-practices/)<br />-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [I/O 效能考量](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-sql-server-performance-best-practices/)<br />-   ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [功能特定效能考量](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-performance-best-practices/)|  
  
## <a name="query-performance-options"></a>查詢效能選項  
  
|||  
|-|-|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both")  **[索引](../../relational-databases/indexes/indexes.md)**|-   [重新組織與重建索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)<br />-   [指定索引的填滿因素](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)<br />-   [設定平行索引作業](../../relational-databases/indexes/configure-parallel-index-operations.md)<br />-   [索引的 SORT_IN_TEMPDB 選項](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)<br />-   [改善全文檢索索引的效能](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both")  **[資料分割資料表與索引](../../relational-databases/partitions/partitioned-tables-and-indexes.md)**|-   [資料分割的優點](https://msdn.microsoft.com/library/ms190787.aspx#Anchor_0)|  
|![security-center-both](../stored-procedures/stored-procedures-database-engine.md)|  
|![security-center-both](../user-defined-functions/user-defined-functions.md)|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") **平行處理原則最佳化**|-   [設定 max worker threads 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)<br />-   [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") **查詢最佳化工具最佳化**|-   [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both")  **[統計資料](../../relational-databases/statistics/statistics.md)**|-   [何時更新統計資料](https://msdn.microsoft.com/library/ms190397.aspx#Anchor_3)<br />-   [更新統計資料](../../relational-databases/statistics/update-statistics.md)|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both")  **[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)**|-   [記憶體最佳化資料表](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)<br />-   [原生編譯的預存程序](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)<br />-   [從原生編譯預存程序建立及存取 TempDB 中的資料表](../../relational-databases/in-memory-oltp/create-and-access-tables-in-tempdb-from-stored-procedures.md)<br />-   [疑難排解記憶體最佳化雜湊索引的常見效能問題](http://msdn.microsoft.com/library/1954a997-7585-4713-81fd-76d429b8d095)<br />-   [示範：記憶體中 OLTP 的效能改善](../../relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp.md)|  
  
## <a name="see-also"></a>另請參閱  
 [效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [使用查詢存放區監視效能](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [單一資料庫的 Azure SQL Database 效能指引](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)   
 [使用彈性集區最佳化 Azure SQL Database 效能](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-guidance/)   
 [Azure 查詢效能深入解析](https://azure.microsoft.com/documentation/articles/sql-database-query-performance/)  
  
  

