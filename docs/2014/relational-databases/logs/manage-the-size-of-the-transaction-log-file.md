---
title: 管理交易記錄檔的大小 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], size management
ms.assetid: 3a70e606-303f-47a8-96d4-2456a18d4297
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9fc03b150dba90839b5a2b54b016103a33cd13cf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37264814"
---
# <a name="manage-the-size-of-the-transaction-log-file"></a>管理交易記錄檔的大小
  在某些情況下，很適合用來實際壓縮或展開實體記錄檔的交易記錄檔[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。 本主題包含下列作業的資訊：如何監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 交易記錄大小、壓縮交易記錄、加入或加大交易記錄檔、最佳化 **tempdb** 交易記錄成長率，以及控制交易記錄檔的成長。  
  
  
##  <a name="MonitorSpaceUse"></a> 監視記錄空間的使用  
 您可以使用 DBCC SQLPERF (LOGSPACE) 來監視記錄空間的使用。 這個命令會傳回目前使用之記錄空間量的相關資訊，並指出交易記錄需要截斷的時機。 如需詳細資訊，請參閱 [DBCC SQLPERF &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-sqlperf-transact-sql)。 如需記錄檔的目前大小、大小上限及檔案的自動成長選項等相關資訊，您也可以在 **sys.database_files** 中使用該記錄檔的 **size**、**max_size** 和 **growth** 資料行。 如需詳細資訊，請參閱 [sys.database_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)。  
  
> [!IMPORTANT]  
>  我們建議您應避免讓記錄磁碟超過負載。  
  
  
##  <a name="ShrinkSize"></a> 壓縮記錄檔的大小  
 若要減少實體記錄檔的實體大小，則必須壓縮記錄檔。 如果您知道交易記錄檔包含不再需要的未使用空間，則這十分有用。 只有當資料庫已上線，而且至少有一個虛擬記錄檔可用時，才會壓縮記錄檔。 在某些情況下，壓縮記錄可能要等到下一個記錄截斷之後才能進行。  
  
> [!NOTE]  
>  像長時間執行的交易之類的因素，使虛擬記錄檔保持作用中一段很長的時間，可能限制記錄檔壓縮，甚至完全阻止記錄檔壓縮。 如需延遲記錄截斷可能因素的相關資訊，請參閱[交易記錄 &#40;SQL Server&#41;](the-transaction-log-sql-server.md)。  
  
 壓縮記錄檔時，會移除一個或多個未保留邏輯記錄任何部分的虛擬記錄檔 (即 *「非使用中虛擬記錄檔」*(Inactive virtual log file))。 當交易記錄檔壓縮之後，就會從記錄檔的結尾移除將記錄縮減至大約目標大小所需的非使用中虛擬記錄檔。  
  
 **若要壓縮記錄檔 （但不壓縮資料庫檔案）**  
  
-   [DBCC SHRINKFILE &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-shrinkfile-transact-sql)  
  
-   [壓縮檔案](../databases/shrink-a-file.md)  
  
 **若要監視記錄檔壓縮事件**  
  
-   [Log File Auto Shrink Event Class](../event-classes/log-file-auto-shrink-event-class.md)。  
  
 `To monitor log space`  
  
-   [DBCC SQLPERF &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-sqlperf-transact-sql)  
  
-   [sys.database_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql) (請參閱一或多個記錄檔的 **size**、**max_size** 和 **growth** 資料行。)  
  
> [!NOTE]  
>  壓縮資料庫和記錄檔的作業可設定為自動進行。 不過，我們建議您不要進行自動壓縮，而且 `autoshrink` 資料庫屬性預設為 FALSE。 如果 `autoshrink` 設定為 TRUE，只有當超過 25% 的空間未使用時，自動壓縮才會減少檔案的大小。 此時，檔案會壓縮成只有 25% 的檔案是未使用空間的大小，或檔案的原始大小，以較大者為準。 如需有關變更的設定資訊`autoshrink`屬性，請參閱 <<c2> [ 檢視或變更資料庫的屬性](../databases/view-or-change-the-properties-of-a-database.md)— 使用**Auto Shrink**屬性**選項**頁面，或[ALTER DATABASE SET 選項&#40;-&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)— 使用 AUTO_SHRINK 選項。</c2>  
  
  
##  <a name="AddOrEnlarge"></a> 加入或加大記錄檔  
 或者，您可以加大現有的記錄檔 (如果磁碟空間允許的話)，或是將記錄檔加入資料庫 (通常是在不同的磁碟上)，來取得空間。  
  
-   若要對資料庫新增一個記錄檔，請使用 ALTER DATABASE 陳述式的 ADD LOG FILE 子句。 新增記錄檔可讓記錄檔增大。  
  
-   若要加大記錄檔，可以使用 ALTER DATABASE 陳述式的 MODIFY FILE 子句，並指定 SIZE 與 MAXSIZE 語法。 如需詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)。  
  
  
##  <a name="tempdbOptimize"></a> 最佳化 tempdb 交易記錄檔的大小  
 重新啟動伺服器執行個體時，就會將 **tempdb** 資料庫的交易記錄大小重新調整為自動成長之前的原始大小。 這樣會降低 **tempdb** 交易記錄的效能。 您可以在啟動或重新啟動伺服器執行個體後，增加 **tempdb** 交易記錄的大小，藉以避免這項負擔。 如需詳細資訊，請參閱 [tempdb Database](../databases/tempdb-database.md)。  
  
  
##  <a name="ControlGrowth"></a> 控制交易記錄檔的成長  
 您可以使用 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql) 陳述式來管理交易記錄檔的成長。 請注意下列事項：  
  
-   若要變更目前的檔案大小 (單位為 KB、MB、GB 和 TB)，請使用 SIZE 選項。  
  
-   若要變更成長的增量，請使用 FILEGROWTH 選項。 0 的值表示將自動成長設為關閉，而且不允許任何其他空間。 記錄檔的少量自動成長增量可能會降低效能。 記錄檔的檔案成長量應夠大，才不用經常進行擴充。 通常適當的預設成長量為 10%。  
  
     如需變更的記錄檔的檔案成長屬性的詳細資訊，請參閱[ALTER DATABASE &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)。  
  
-   若要控制記錄檔大小的最大值 (單位為 KB、MB、GB 和 TB) 或是將成長設定為 UNLIMITED，請使用 MAXSIZE 選項。  
  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [為寫滿交易記錄疑難排解 &#40;SQL Server 錯誤 9002&#41;](troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
  
