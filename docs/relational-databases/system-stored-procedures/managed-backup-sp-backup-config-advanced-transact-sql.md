---
title: managed_backup. sp_backup_config_advanced （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 786028df8e421580b5a994175223d21a20d44f41
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: zh-TW
ms.lasthandoff: 07/07/2020
ms.locfileid: "86053504"
---
# <a name="managed_backupsp_backup_config_advanced-transact-sql"></a>managed_backup. sp_backup_config_advanced （Transact-sql）
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  設定的 advanced 設定 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
EXEC managed_backup.sp_backup_config_advanced   
    [@database_name = ] 'database_name'  
    ,[@encryption_algorithm = ] 'name of the encryption algorithm'  
    ,[@encryptor_type = ] {'CERTIFICATE' | 'ASYMMETRIC_KEY'}  
    ,[@encryptor_name = ] 'name of the certificate or asymmetric key'  
    ,[@local_cache_path = ] 'NOT AVAILABLE'  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a>參量  
 @database_name  
 在特定資料庫上啟用受管理備份的資料庫名稱。 如果是 Null 或 *，則此受管理的備份會套用至伺服器上的所有資料庫。  
  
 @encryption_algorithm  
 備份期間用來加密備份檔案的加密演算法名稱。 @encryption_algorithm為**SYSNAME**。 第一次設定資料庫的[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]時為必要參數。 如果您不想要加密備份檔案，請指定**NO_ENCRYPTION** 。 變更設定時 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] ，此參數是選擇性的，如果未指定參數，則會保留現有的設定值。 此參數允許的值為：  
  
-   AES_128  
  
-   AES_192  
  
-   AES_256  
  
-   TRIPLE_DES_3KEY  
  
-   NO_ENCRYPTION  
  
 如需有關加密演算法的詳細資訊，請參閱＜ [Choose an Encryption Algorithm](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)＞。  
  
 @encryptor_type  
 加密子的類型，可以是「憑證」或「ASYMMETRIC_KEY」。 @encryptor_type是**Nvarchar （32）**。 如果您為參數指定 NO_ENCRYPTION，此參數是選擇性的 @encryption_algorithm 。  
  
 @encryptor_name  
 用來加密備份之現有憑證或非對稱金鑰的名稱。 @encryptor_name為**SYSNAME**。 如果使用非對稱金鑰，則必須透過可延伸金鑰管理 (EKM) 設定。 如果您為參數指定 NO_ENCRYPTION，此參數是選擇性的 @encryption_algorithm 。  
  
 如需詳細資訊，請參閱[可延伸金鑰管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)。  
  
 @local_cache_path  
 尚不支援此參數。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>權限  
 需要**db_backupoperator**資料庫角色中的成員資格、具有**ALTER ANY CREDENTIAL**許可權，以及**Sp_delete_backuphistory**預存程式的**EXECUTE**許可權。  
  
## <a name="examples"></a>範例  
 下列範例會針對 SQL Server 的實例，設定的 advanced configuration 選項 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 。  
  
```sql
Use msdb;  
Go  
   EXEC managed_backup.sp_backup_config_advanced  
                @encryption_algorithm ='AES_128'  
                ,@encryptor_type = 'CERTIFICATE'  
                ,@encryptor_name = 'MyTestDBBackupEncryptCert'  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [managed_backup. sp_backup_config_basic （Transact-sql）](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
  
