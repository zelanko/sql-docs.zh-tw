---
title: "設定 Microsoft Azure 的 SQL Server 受管理備份進階選項 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ffd28159-8de8-4d40-87da-1586bfef3315
caps.latest.revision: 8
author: "MightyPen"
ms.author: "genemi"
manager: "jhubbard"
caps.handback.revision: 7
---
# 設定 Microsoft Azure 的 SQL Server 受管理備份進階選項
  下列教學課程說明如何設定 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]的進階選項。 這些程序只有在您需要它們所提供的功能時才有必要。 否則，您可以啟用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 並依據預設行為。  
  
 每個案例中都是使用 `database_name` 參數指定備份。 當 `database_name` 是 NUL 或 * 時，這些變更就會影響執行個體層級的預設設定。 執行個體層級設定也會影響在變更之後所建立的新資料庫。  
  
 一旦指定這些設定，您就可以使用系統預存程序 [managed_backup.sp_backup_config_basic &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md) 來啟用資料庫或執行個體的受管理備份。 如需詳細資訊，請參閱 [Enable SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)。  
  
> [!WARNING]  
>  您應該一律先設定進階選項和自訂排程選項，再啟用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 與 [managed_backup.sp_backup_config_basic &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)。 否則，在啟用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 和設定這些設定的時間裡，便可能發生不想要的備份作業。  
  
## 設定加密  
 下列步驟說明如何使用預存程序 [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md) 來指定加密設定。  
  
1.  **決定加密演算法︰** 先決定要使用的加密演算法名稱。 從下列演算法中選取一個：  
  
    -   AES_128  
  
    -   AES_192  
  
    -   AES_256  
  
    -   TRIPLE_DES_3KEY  
  
    -   NO_ENCRYPTION  
  
2.  **建立資料庫主要金鑰︰** 選擇要儲存在資料庫中之主要金鑰複本的加密密碼。  
  
    ```  
    -- Creates a database master key.  
    -- The key is encrypted using the password "<master key password>"  
    USE Master;  
    GO  
       CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
    ```  
  
3.  **建立備份憑證或非對稱金鑰︰** 加密可以搭配憑證或非對稱金鑰使用。 下例會建立用來加密的備份憑證。  
  
    ```tsql  
    USE Master;  
    GO  
       CREATE CERTIFICATE MyTestDBBackupEncryptCert  
          WITH SUBJECT = 'MyTestDBBackupEncryptCert';  
    GO  
    ```  
  
4.  **設定受管理的備份加密︰**呼叫有對應值的 **managed_backup.sp_backup_config_advanced** 預存程序。 例如，下例會使用名為 `MyDB` 的憑證和 `MyTestDBBackupEncryptCert` 加密演算法來設定 `AES_128` 資料庫加密。  
  
    ```  
    USE msdb;  
    GO  
       EXEC managed_backup.sp_backup_config_advanced  
          @database_name = 'MyDB'                
          ,@encryption_algorithm ='AES_128'  
          ,@encryptor_type = 'CERTIFICATE'  
          ,@encryptor_name = 'MyTestDBBackupEncryptCert';  
    GO  
    ```  
  
    > [!WARNING]  
    >  如果前一個範例中的 `@database_name` 是 NULL，則設定會套用到 SQL Server 執行個體。  
  
## 設定自訂的備份排程  
 下列步驟說明如何使用預存程序 [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md) 來設定自訂排程。  
  
1.  **決定完整備份的頻率︰** 決定進行資料庫完整備份的頻率。 完整備份可以選擇「每日」或「每週」。  
  
2.  **決定記錄備份的頻率︰** 決定進行記錄備份的頻率。 這個值為分鐘或小時。  
  
3.  **決定週幾進行每週備份︰** 如果每週備份，請選擇於星期幾進行完整備份。  
  
4.  **決定備份的開始時間︰**使用 24 小時制，選擇開始備份的時間。  
  
5.  **決定允許備份的時長︰** 這會指定備份必須完成的時間長度。  
  
6.  **設定自訂的備份排程︰** 下列預存程序會定義 `MyDB` 資料庫的自訂排程。 每週的完整備份於 `Monday` 的 `17:30`進行。 記錄備份每 `5` 分鐘進行。 備份完成時間為兩小時。  
  
    ```  
    USE msdb;  
    GO  
    EXEC managed_backup.sp_backup_config_schedule   
         @database_name =  'MyDB'  
        ,@scheduling_option = 'Custom'  
        ,@full_backup_freq_type = 'Weekly'  
        ,@days_of_week = 'Monday'  
        ,@backup_begin_time =  '17:30'  
        ,@backup_duration = '02:00'  
        ,@log_backup_freq = '00:05'  
    GO  
  
    ```  
  
## 後續步驟  
 設定進階選項和自訂排程之後，您必須啟用目標資料庫或 SQL Server 執行個體上的 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 。 如需詳細資訊，請參閱 [Enable SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)。  
  
## 另請參閱  
 [SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  