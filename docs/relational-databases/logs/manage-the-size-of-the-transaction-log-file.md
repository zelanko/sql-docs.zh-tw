---
title: "管理交易記錄檔大小 |Microsoft 文件"
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-transaction-log
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transaction logs [SQL Server], size management
ms.assetid: 3a70e606-303f-47a8-96d4-2456a18d4297
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 6d75e0e40c5642993cb17b09e421fbfebf40f87a
ms.openlocfilehash: cd1931ef0f77c0a1e31c29833f38c51416e267c8
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="manage-the-size-of-the-transaction-log-file"></a>管理交易記錄檔的大小
本主題涵蓋如何監視[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]交易記錄檔大小、 壓縮交易記錄、 加入或加大交易記錄檔、 最佳化**tempdb**交易記錄成長率，以及控制交易記錄檔的成長。  

  ##  <a name="MonitorSpaceUse"></a> 監視記錄空間的使用  
使用監視記錄空間的使用[DBCC SQLPERF (LOGSPACE)](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-sqlperf-transact-sql)。 這個命令會傳回目前使用之記錄空間量的相關資訊，並指出交易記錄需要截斷的時機。 如需詳細資訊，請參閱[DBCC SQLPERF TRANSACT-SQL](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)。 如需目前的記錄檔大小、 大小上限及檔案自動成長選項，您也可以使用**大小**， **max_size**，和**成長**該記錄檔的資料行**sys.database_files**。 如需詳細資訊，請參閱 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)。  
  
**重要！** 請避免讓記錄磁碟多載！  

  
##  <a name="ShrinkSize"></a> 壓縮記錄檔大小  
 若要減少實體記錄檔的實體大小，則必須壓縮記錄檔。 當您知道交易記錄檔包含未使用的空間時，這非常有用。 只有當資料庫在線上，而且至少一個虛擬記錄檔可用時，您可以壓縮記錄檔。 在某些情況下，壓縮記錄可能要等到下一個記錄截斷之後才能進行。  
  
> [!NOTE]
>  像長時間執行的交易之類的因素，使虛擬記錄檔保持作用中一段很長的時間，可能限制記錄檔壓縮，甚至完全阻止記錄檔壓縮。 如需延遲記錄截斷可能因素的相關資訊，請參閱[交易記錄 &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)。  
  
 壓縮記錄檔會移除一或多個不保留任何邏輯記錄的虛擬記錄檔 (即「非使用中虛擬記錄檔」)。 當交易記錄檔壓縮之後時，非作用中虛擬記錄檔會移除從要記錄縮減至大約目標大小的記錄檔的結尾。  
  
 **壓縮記錄檔 (但不壓縮資料庫檔案)**  
  
-   [DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)  
  
-   [壓縮檔案](../../relational-databases/databases/shrink-a-file.md)  
  
 **監視記錄檔壓縮事件**  
  
-   [Log File Auto Shrink Event Class](../../relational-databases/event-classes/log-file-auto-shrink-event-class.md)。  
  
 **監視記錄空間**  
  
-   [DBCC SQLPERF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)  
  
-   [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) (請參閱一或多個記錄檔的 **size**、**max_size** 和 **growth** 資料行。)  
  
> [!NOTE]
>  您可以設定自動壓縮記錄檔。 不過，我們建議您不要進行自動壓縮，而且 **autoshrink** 資料庫屬性預設為 FALSE。 如果 **autoshrink** 設定為 TRUE，只有當超過 25% 的空間未使用時，自動壓縮才會減少檔案的大小。 此時，檔案會壓縮成只有 25% 的檔案是未使用空間的大小，或檔案的原始大小，以較大者為準。 如需變更 **autoshrink** 屬性設定的相關資訊，請參閱[檢視或變更資料庫的屬性](../../relational-databases/databases/view-or-change-the-properties-of-a-database.md)—使用 [選項] 頁面的 **Auto Shrink** 屬性—或 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)—使用 AUTO_SHRINK 選項。  
  

##  <a name="AddOrEnlarge"></a> 加入或加大記錄檔  
 您可以加大現有的記錄檔 （如果磁碟空間允許的話），或加入至資料庫，通常在不同磁碟上的記錄檔來取得空間。  
  
-   若要對資料庫新增一個記錄檔，請使用 ALTER DATABASE 陳述式的 ADD LOG FILE 子句。 新增記錄檔可讓記錄檔增大。  
  
-   若要加大記錄檔，可以使用 ALTER DATABASE 陳述式的 MODIFY FILE 子句，並指定 SIZE 與 MAXSIZE 語法。 如需詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)。  
    
  
##  <a name="tempdbOptimize"></a> 最佳化 tempdb 交易記錄的大小  
 重新啟動伺服器執行個體時，就會將 **tempdb** 資料庫的交易記錄大小重新調整為自動成長之前的原始大小。 這樣會降低 **tempdb** 交易記錄的效能。 您可以在啟動或重新啟動伺服器執行個體後，增加 **tempdb** 交易記錄的大小，藉以避免這項負擔。 如需詳細資訊，請參閱 [tempdb Database](../../relational-databases/databases/tempdb-database.md)。  
  
  
##  <a name="ControlGrowth"></a> 控制交易記錄檔的成長  
 使用[ALTER DATABASE (TRANSACT-SQL)](../../t-sql/statements/alter-database-transact-sql.md)陳述式來管理交易記錄檔的成長。 請注意下列事項：  
  
-   若要變更目前的檔案大小 (單位為 KB、MB、GB 和 TB)，請使用 SIZE 選項。  
  -   若要變更成長的增量，請使用 FILEGROWTH 選項。 0 的值表示將自動成長設為關閉，而且不允許任何其他空間。 記錄檔的少量自動成長增量可能會降低效能。 記錄檔的檔案成長量應夠大，才不用經常進行擴充。 通常適當的預設成長量為 10%。  

如需對記錄檔變更檔案成長屬性的相關資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/ms174269.aspx)。  
  
-   若要控制記錄檔大小的最大值 (單位為 KB、MB、GB 和 TB) 或是將成長設定為 UNLIMITED，請使用 MAXSIZE 選項。  
  
  
## <a name="see-also"></a>另請參閱  
 [備份 (TRANSACT-SQL)](../../t-sql/statements/backup-transact-sql.md)   
 [疑難排解完整交易記錄 （SQL Server 錯誤 9002）](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
  

