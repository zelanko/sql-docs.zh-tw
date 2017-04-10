---
title: "檔案狀態 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "還原檔案狀態 [SQL Server]"
  - "確認檔案狀態"
  - "目前的檔案狀態"
  - "確認檔案群組狀態"
  - "檔案狀態 [SQL Server]"
  - "線上檔案狀態"
  - "離線檔案狀態 [SQL Server]"
  - "檢視檔案群組狀態"
  - "檢視檔案狀態"
  - "有問題的檔案狀態"
  - "復原檔案狀態 [SQL Server]"
  - "目前的檔案群組狀態"
  - "復原暫止檔案狀態 [SQL Server]"
  - "顯示檔案狀態"
  - "狀態 [SQL Server], 檔案"
  - "顯示檔案群組狀態"
  - "無用的檔案狀態"
ms.assetid: b426474d-8954-4df0-b78b-887becfbe8d6
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# 檔案狀態
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，資料庫檔案的狀態是與資料庫的狀態分開維護。 檔案永遠處於特定狀態，例如 ONLINE 或 OFFLINE。 若要檢視檔案目前的狀態，請使用 [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) 或 [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) 目錄檢視。 如果資料庫是離線的，就可以從 [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) 目錄檢視來檢視檔案的狀態。  
  
 檔案群組中的檔案狀態將決定整個檔案群組的可用性。 若要使某個檔案群組為可用的，則在檔案群組中的所有檔案必須都在線上。 若要檢視檔案群組目前的狀態，請使用 [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md) 目錄檢視。 如果檔案群組離線而您嘗試透過 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式存取檔案群組，就會發生錯誤。 當查詢最佳化工具建立 SELECT 陳述式的查詢計畫時，它可避免使用離線檔案群組中所存在的非叢集索引和叢集檢視，以利陳述式成功。 不過，如果離線檔案群組包含目標資料表的堆積或叢集索引，SELECT 陳述式將會失敗。 除此之外，在離線檔案群組中，以 INSERT、UPDATE 或 DELETE 陳述式修改含有索引的資料表將會失敗。  
  
## 檔案狀態定義  
 下表定義檔案狀態。  
  
|State|定義|  
|-----------|----------------|  
|ONLINE|檔案可供所有的作業使用。 如果資料庫本身是在線上，則主要檔案群組中的檔案將永遠在線上。 如果在主要檔案群組中的檔案不在線上，則資料庫也不會在線上且次要檔案的狀態是未定義的。|  
|OFFLINE|檔案無法存取且可能不在磁碟上。 明確的使用者動作會使檔案變成離線，而且在採取其他使用者動作之前都是離線狀態。<br /><br /> **\*\* 注意 \*\*** 當檔案損毀時，應該只能將檔案設為離線狀態，但是它是可以還原的。 設為離線的檔案只能透過從備份還原檔案來將它設為線上。 如需有關還原單一檔案的詳細資訊，請參閱 [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)。|  
|RESTORING|正在還原檔案。 檔案會輸入還原狀態，因為還原命令會影響整個檔案，而不是只有頁面還原，而且會一直保留此狀態，直到完成還原並復原檔案為止。|  
|RECOVERY PENDING|已延遲檔案復原。 檔案會自動輸入此狀態，因為在分次還原處理序中，有未還原和未復原的檔案。 需要使用者執行其他動作以解決錯誤並允許完成復原處理。 如需詳細資訊，請參閱[分次還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)。|  
|SUSPECT|在線上還原處理期間檔案復原失敗。 如果檔案是在主要檔案群組中，資料庫也會標示為有疑問。 否則，只有檔案是有疑問的，資料庫仍會在線上。<br /><br /> 檔案仍然會在有疑問的狀態下，直到可以使用下列其中一個方法：<br /><br /> 還原和復原<br /><br /> DBCC CHECKDB with REPAIR_ALLOW_DATA_LOSS|  
|DEFUNCT|當它在線上時，就會卸除檔案。 當移除了離線檔案群組，在檔案群組中的所有檔案就會變成無用。|  
  
## 相關內容  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
 [資料庫狀態](../../relational-databases/databases/database-states.md)  
  
 [鏡像狀態 &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)  
  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
  
 [資料庫檔案與檔案群組](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  