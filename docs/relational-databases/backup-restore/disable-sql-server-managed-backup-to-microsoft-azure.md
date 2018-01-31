---
title: "啟用 SQL Server Managed Backup to Microsoft Azure | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3e02187f-363f-4e69-a82f-583953592544
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3f462b0563e37d528808f43b180435fa75a15dc3
ms.sourcegitcommit: 0a9c29c7576765f3b5774b2e087852af42ef4c2d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/29/2018
---
# <a name="disable-sql-server-managed-backup-to-microsoft-azure"></a>停用 SQL Server Managed Backup to Microsoft Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 本主題描述如何在資料庫和執行個體層級停用或暫停 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
  
##  <a name="DatabaseDisable"></a> 停用資料庫的 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
 您可以使用系統預存程序 [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md) 來停用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 設定。 *@enable_backup* 參數用於啟用和停用特定資料庫的 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 組態，其中的 1 會啟用而 0 會停用組態設定。  
  
#### <a name="to-disable-includesssmartbackupincludesss-smartbackup-mdmd-for-a-specific-database"></a>停用特定資料庫的 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] ：  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
```  
EXEC msdb.managed_backup.sp_backup_config_basic  
                @database_name = 'TestDB'   
                ,@enable_backup = 0;  
GO  
  
```  
  
##  <a name="DatabaseAllDisable"></a> 停用執行個體上所有資料庫的 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]   
 從近期在執行個體上啟用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的所有資料庫中，若您要停用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 組態設定，可使用下列程序。  組態設定 (例如儲存體 URL、保留項目和 SQL 認證) 都會保留在中繼資料中，如果稍後啟用資料庫的 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 即可使用。 如果您只是想暫停 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 服務，可使用主切換，本主題的以下章節會加以解釋。  
  
#### <a name="to-disable-includesssmartbackupincludesss-smartbackup-mdmd-for-all-the-databases"></a>停用所有資料庫的 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] ：  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 下列範例會識別 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 是否於執行個體層級進行設定，所有的 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 是否啟用執行個體的資料庫，該範例還會執行系統預存程序 **sp_backup_config_basic** 以停用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
  
```  
-- Create a working table to store the database names  
Declare @DBNames TABLE  
  
       (  
             RowID int IDENTITY PRIMARY KEY  
             ,DBName varchar(500)  
  
       )  
-- Define the variables  
DECLARE @rowid int  
DECLARE @dbname varchar(500)  
DECLARE @SQL varchar(2000)  
-- Get the database names from the system function  
  
INSERT INTO @DBNames (DBName)  
  
SELECT db_name  
       FROM   
  
       msdb.managed_backup.fn_backup_db_config (NULL)  
       WHERE is_managed_backup_enabled = 1 
       AND is_dropped = 0
  
       --Select DBName from @DBNames  
  
       select @rowid = min(RowID)  
       FROM @DBNames  
  
       WHILE @rowID IS NOT NULL  
       Begin  
  
             Set @dbname = (Select DBName From @DBNames Where RowID = @rowid)  
             Begin  
             Set @SQL = 'EXEC msdb.managed_backup.sp_backup_config_basic    
                @database_name= '''+'' + @dbname+ ''+''',   
                @enable_backup=0'  
  
            EXECUTE (@SQL)  
  
             END  
             Select @rowid = min(RowID)  
             From @DBNames Where RowID > @rowid  
  
       END  
```  
  
 若要檢閱執行個體上所有資料庫的組態設定，請使用下列查詢：  
  
```  
Use msdb;  
GO  
SELECT * FROM managed_backup.fn_backup_db_config (NULL);  
GO  
  
```  
  
##  <a name="InstanceDisable"></a> 停用執行個體的預設 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 設定  
 執行個體層級的預設設定會套用到建立在該執行個體上的所有新資料庫。  如果您不再需要或要求預設設定，可以使用 **managed_backup.sp_backup_config_basic** 系統預存程序，將 *@database_name* 參數設為 NULL 來停用此組態。 停用不會移除其他組態設定，像是儲存體 URL、保留設定或 SQL 認證名稱。 如果稍後啟用執行個體的 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] ，將會使用這些設定。  
  
#### <a name="to-disable-includesssmartbackupincludesss-smartbackup-mdmd-default-configuration-settings"></a>停用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 預設組態設定：  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    EXEC msdb.managed_backup.sp_backup_config_basic  
                    @database_name = 'TestDB'   
                    ,@enable_backup = 0;  
    GO  
  
    ```  
  
##  <a name="InstancePause"></a> 在執行個體層級暫停 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
 有些時候，您可能會需要暫停 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 服務一段時間。  **managed_backup.sp_backup_master_switch** 系統預存程序可讓您在執行個體層級停用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 服務。  使用同一個預存程序繼續執行 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。 @state 參數可用來定義是否應該關閉或開啟 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
  
#### <a name="to-pause-includesssmartbackupincludesss-smartbackup-mdmd-services-using-transact-sql"></a>使用 Transact-SQL 暫停 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 服務：  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
```  
Use msdb;  
GO  
EXEC managed_backup.sp_backup_master_switch @new_state=0;  
Go  
  
```  
  
#### <a name="to-resume-includesssmartbackupincludesss-smartbackup-mdmd-using-transact-sql"></a>使用 Transact-SQL 繼續進行 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。  
  
```  
Use msdb;  
Go  
EXEC managed_backup. sp_backup_master_switch @new_state=1;  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [啟用 SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)  
  
  
