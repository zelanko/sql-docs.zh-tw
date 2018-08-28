---
title: 延展性 | Microsoft Docs
ms.custom: ''
ms.date: 08/27/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a4891c57-56bb-49f4-9bb5-f11b745279e5
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f1e928ac8f91947be9c529ce00f82f10684cacb4
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43072680"
---
# <a name="scalability"></a>延展性
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  SQL Server 2016 包含記憶體最佳化資料表之磁碟上儲存體的延展性增強功能。  
  
-   **保存記憶體最佳化資料表的多個執行緒**  
  
     在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，具有單一離線檢查點執行緒可掃描交易記錄中是否有記憶體最佳化資料表變更，並將它們保存在檢查點檔案 (例如資料和差異檔案) 中。 如果使用較多的核心，單一離線檢查點執行緒可能會落後。  
  
     在 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]中，有多個並行執行緒負責保存記憶體最佳化資料表的變更。  
  
-   **多執行緒復原**  
  
     在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，作為部分復原作業的記錄套用為單一執行緒。 在 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]中，記錄套用為多執行緒。  
  
-   **MERGE 作業**  
  
     MERGE 作業現在為多執行緒。  
  
-   **動態管理檢視**  
  
     [sys.dm_db_xtp_checkpoint_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-stats-transact-sql.md) 和 [sys.dm_db_xtp_checkpoint_files &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md) 已大幅變更。  
  
 已停用手動合併，因為多執行緒合併預期會跟上負載。  
  
 記憶體內部 OLTP 引擎會根據 FILESTREAM 繼續使用記憶體最佳化檔案群組，但是會從 FILESTREAM 中分離檔案群組中的個別檔案。 記憶體內部 OLTP 引擎會完全管理這些檔案 (例如，用於建立、卸除和記憶體回收)。 不支援 [DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)。  
  
  
