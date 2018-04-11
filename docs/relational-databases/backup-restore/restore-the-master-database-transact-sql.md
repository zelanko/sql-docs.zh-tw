---
title: 還原 master 資料庫 (Transact-SQL) | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- master database [SQL Server], restoring
ms.assetid: c83d802c-e84e-4458-b3ca-173d9ba32f73
caps.latest.revision: 42
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: bdcb8f41a3eb6abd20f905f573f84fb1b426f014
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/10/2018
---
# <a name="restore-the-master-database-transact-sql"></a>還原 master 資料庫 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主題說明如何從完整資料庫備份中還原 **master** 資料庫。  
  
### <a name="to-restore-the-master-database"></a>還原 master 資料庫  
  
1.  以單一使用者模式啟動伺服器執行個體。  
  
     如需如何指定單一使用者啟動參數資訊 (**-m**) 的相關資訊，請參閱[設定伺服器啟動選項 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md)。  
  
2.  若要還原 **master**的完整資料庫備份，請使用下列 [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
     `RESTORE DATABASE master FROM`  *&lt;備份裝置&gt;*  `WITH REPLACE`  
  
     即使有同名的資料庫，REPLACE 選項還是會指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 還原指定的資料庫。 現有的資料庫 (如果有的話) 會遭到刪除。 在單一使用者模式中，我們建議您在 [sqlcmd 公用程式](../../tools/sqlcmd-utility.md)中輸入 RESTORE DATABASE 陳述式。 如需詳細資訊，請參閱 [使用 sqlcmd 公用程式](../../relational-databases/scripting/sqlcmd-use-the-utility.md)。  
  
    > [!IMPORTANT]  
    >  在還原 **master** 之後， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體會關閉，並終止 **sqlcmd** 處理序。 在重新啟動伺服器執行個體之前，請移除單一使用者啟動參數。 如需詳細資訊，請參閱[設定伺服器啟動選項 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md)。  
  
3.  重新啟動伺服器執行個體，然後繼續其他復原步驟，例如還原其他資料庫、附加資料庫，以及更正使用者不符的項目。  
  
## <a name="example"></a>範例  
 下列範例會在預設伺服器執行個體上還原 `master` 資料庫。 此範例假設伺服器執行個體已經在單一使用者模式中執行。 此範例會啟動 `sqlcmd`，並執行 `RESTORE DATABASE` 陳述式，從磁碟裝置還原 `master` 的完整資料庫備份：`Z:\SQLServerBackups\master.bak`。  
  
> [!NOTE]  
>  對於具名執行個體，**sqlcmd** 命令必須指定 **-S**\<電腦名稱>**\\\<執行個體名稱> 選項。  
  
```  
  
      C:\> sqlcmd  
1> RESTORE DATABASE master FROM DISK = 'Z:\SQLServerBackups\master.bak' WITH REPLACE;  
2> GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [完整資料庫還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [完整資料庫還原 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [孤立的使用者疑難排解 &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)   
 [資料庫卸離和附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [重建系統資料庫](../../relational-databases/databases/rebuild-system-databases.md)   
 [Database Engine 服務啟動選項](../../database-engine/configure-windows/database-engine-service-startup-options.md)   
 [SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)   
 [系統資料庫的備份與還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [以單一使用者模式啟動 SQL Server](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)  
  
  
