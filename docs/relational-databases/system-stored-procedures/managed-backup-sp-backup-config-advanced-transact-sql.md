---
title: managed_backup.sp_backup_config_advanced (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_backup_config_optional
- sp_backup_config_optional_TSQL
- managed_backup.sp_backup_config_optional_TSQL
- managed_backup.sp_backup_config_optional
dev_langs:
- TSQL
helpviewer_keywords:
- sp_backup_config_optional
- managed_backup.sp_backup_config_optional
ms.assetid: 4fae8193-1f88-48fd-a94a-4786efe8d6af
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 46c4fa67915703250f3ec7fa17054905d471d2f0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="managedbackupspbackupconfigadvanced-transact-sql"></a>managed_backup.sp_backup_config_advanced (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  設定進階的設定[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```vb  
EXEC managed_backup.sp_backup_config_advanced   
    [@database_name = ] 'database_name'  
    ,[@encryption_algorithm = ] 'name of the encryption algorithm'  
    ,[@encryptor_type = ] {'CERTIFICATE' | 'ASYMMETRIC_KEY'}  
    ,[@encryptor_name = ] 'name of the certificate or asymmetric key'  
    ,[@local_cache_path = ] 'NOT AVAILABLE'  
```  
  
##  <a name="Arguments"></a> 引數  
 @database_name  
 啟用特定資料庫上的受管理的備份的資料庫名稱。 如果是 NULL 或 *，則此受管理的備份適用於在伺服器上的所有資料庫。  
  
 @encryption_algorithm  
 備份期間用來加密備份檔案的加密演算法名稱。 @encryption_algorithm是**SYSNAME**。 第一次設定資料庫的[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]時為必要參數。 指定**NO_ENCRYPTION**如果您不想加密備份檔案。 變更 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 組態設定時為選擇性參數；如果未指定參數，則保留現有的組態值。 此參數允許的值為：  
  
-   AES_128  
  
-   AES_192  
  
-   AES_256  
  
-   TRIPLE_DES_3KEY  
  
-   NO_ENCRYPTION  
  
 如需有關加密演算法的詳細資訊，請參閱＜ [Choose an Encryption Algorithm](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)＞。  
  
 @encryptor_type  
 加密程式，它可以是任一個 'CERTIFICATE' 的類型或 ' ASYMMETRIC_KEY"。 @encryptor_type是**nvarchar （32)**。 這個參數是選擇性，如果您指定的 NO_ENCRYPTION@encryption_algorithm參數。  
  
 @encryptor_name  
 用來加密備份之現有憑證或非對稱金鑰的名稱。 @encryptor_name是**SYSNAME**。 如果使用非對稱金鑰，則必須透過可延伸金鑰管理 (EKM) 設定。 這個參數是選擇性，如果您指定的 NO_ENCRYPTION@encryption_algorithm參數。  
  
 如需詳細資訊，請參閱[可延伸金鑰管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)。  
  
 @local_cache_path  
 不支援此參數。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 需要的成員資格**db_backupoperator**與資料庫角色， **ALTER ANY CREDENTIAL**權限，和**EXECUTE**權限**sp_delete_backuphistory**預存程序。  
  
## <a name="examples"></a>範例  
 下列範例會設定的進階的設定選項[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]SQL Server 執行個體。  
  
```  
Use msdb;  
Go  
   EXEC managed_backup.sp_backup_config_advanced  
                @encryption_algorithm ='AES_128'  
                ,@encryptor_type = 'CERTIFICATE'  
                ,@encryptor_name = 'MyTestDBBackupEncryptCert'  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
  
