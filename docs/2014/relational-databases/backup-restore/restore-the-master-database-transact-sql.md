---
title: 還原 master 資料庫 (Transact-SQL) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- master database [SQL Server], restoring
ms.assetid: c83d802c-e84e-4458-b3ca-173d9ba32f73
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 823a6455616b412a41179d831b565e10b3286fb7
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54127388"
---
# <a name="restore-the-master-database-transact-sql"></a>還原 master 資料庫 (Transact-SQL)
  本主題說明如何從完整資料庫備份中還原 **master** 資料庫。  
  
### <a name="to-restore-the-master-database"></a>還原 master 資料庫  
  
1.  以單一使用者模式啟動伺服器執行個體。  
  
     如需如何指定單一使用者啟動參數資訊 (**-m**) 的相關資訊，請參閱[設定伺服器啟動選項 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md)。  
  
2.  若要還原 **master**的完整資料庫備份，請使用下列 [RESTORE DATABASE](/sql/t-sql/statements/restore-statements-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
     `RESTORE DATABASE master FROM`  *<備份裝置>*  `WITH REPLACE`  
  
     即使有同名的資料庫，REPLACE 選項還是會指示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 還原指定的資料庫。 現有的資料庫 (如果有的話) 會遭到刪除。 在單一使用者模式中，我們建議您在 [sqlcmd 公用程式](../../tools/sqlcmd-utility.md)中輸入 RESTORE DATABASE 陳述式。 如需詳細資訊，請參閱 [使用 sqlcmd 公用程式](../scripting/sqlcmd-use-the-utility.md)。  
  
    > [!IMPORTANT]  
    >  在還原 **master** 之後， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的執行個體會關閉，並終止 **sqlcmd** 處理序。 在重新啟動伺服器執行個體之前，請移除單一使用者啟動參數。 如需詳細資訊，請參閱[設定伺服器啟動選項 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md)。  
  
3.  重新啟動伺服器執行個體，然後繼續其他復原步驟，例如還原其他資料庫、附加資料庫，以及更正使用者不符的項目。  
  
## <a name="example"></a>範例  
 下列範例會在預設伺服器執行個體上還原 `master` 資料庫。 此範例假設伺服器執行個體已經在單一使用者模式中執行。 此範例會啟動 `sqlcmd` ，並執行 `RESTORE DATABASE` 陳述式，從磁碟裝置還原 `master` 的完整資料庫備份： `Z:\SQLServerBackups\master.bak`。  
  
> [!NOTE]
>  對於具名執行個體，**sqlcmd** 命令必須指定 **-S**_\<電腦名稱>_\\*\<執行個體名稱>* 選項。  
  
```  
  
      C:\> sqlcmd  
1> RESTORE DATABASE master FROM DISK = 'Z:\SQLServerBackups\master.bak' WITH REPLACE;  
2> GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [完整資料庫還原 &#40;簡單復原模式&#41;](complete-database-restores-simple-recovery-model.md)   
 [完整資料庫還原 &#40;完整復原模式&#41;](complete-database-restores-full-recovery-model.md)   
 [孤立的使用者疑難排解 &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)   
 [資料庫卸離和附加 &#40;SQL Server&#41;](../databases/database-detach-and-attach-sql-server.md)   
 [重建系統資料庫](../databases/system-databases.md)   
 [Database Engine 服務啟動選項](../../database-engine/configure-windows/database-engine-service-startup-options.md)   
 [SQL Server 組態管理員](../sql-server-configuration-manager.md)   
 [系統資料庫的備份與還原 &#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [以單一使用者模式啟動 SQL Server](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)  
  
  
