---
title: managed_backup.sp_backup_config_basic (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 10/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_backup_config_basic_TSQL
- sp_backup_config_basic
- managed_backup.sp_backup_config_basic
- managed_backup.sp_backup_config_basic_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- managed_backup.sp_backup_config_basic
- sp_backup_config_basic
ms.assetid: 3ad73051-ae9a-4e41-a889-166146e5508f
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8f8f6a2bb437982bdc40c70b9e53c6c864dbc5b4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33240058"
---
# <a name="managedbackupspbackupconfigbasic-transact-sql"></a>managed_backup.sp_backup_config_basic (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  設定[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]特定資料庫或執行個體的基本設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!NOTE]  
>  此程序可以呼叫自己建立基本的受管理備份設定。 不過，如果您打算新增進階的功能或自訂排程，先進行這些設定使用[managed_backup.sp_backup_config_advanced &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)和[managed_backup.sp_backup_config_schedule &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)之前啟用此程序的受管理的備份。  
   
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```Transact-SQL   
EXEC managed_backup.sp_backup_config_basic  
    [@enable_backup = ] { 0 | 1}    ,[@database_name = ] 'database_name'    ,[@container_url = ] 'Azure_Storage_blob_container  
    ,[@retention_days = ] 'retention_period_in_days'    ,[@credential_name = ] 'sql_credential_name'  
```  
  
##  <a name="Arguments"></a> 引數  
 @enable_backup  
 啟用或停用指定資料庫的[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。 @enable_backup是**元**。 設定時，所需參數[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]第一個執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果您要變更現有[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]組態，這是選擇性參數。 在此情況下，未指定任何組態值會保留其現有的值。  
  
 @database_name  
 啟用特定資料庫上的受管理的備份的資料庫名稱。  
  
 @container_url  
 URL，表示備份的位置。 當@credential_name是 NULL，此 URL 在 Azure 儲存體、 blob 容器的共用的存取簽章 (SAS) URL，而且備份使用新的備份至區塊 blob 的功能。 如需詳細資訊，請檢閱[了解 SAS](http://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)。 當@credential_name指定，則儲存體帳戶 URL，而且備份使用分頁 blob 功能已被取代的備份。  
  
> [!NOTE]  
>  這個參數支援 SAS URL 這一次。  
  
 @retention_days  
 備份檔案的保留期限，以天數為單位。 @storage_url為 int。 這是必要的參數設定時[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]第一次的執行個體上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 變更時[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]組態，這是選擇性參數。 如果未指定，則會保留現有的組態值。  
  
 @credential_name  
 用來驗證 Windows Azure 儲存體帳戶之 SQL 認證的名稱。 @credentail_name 是**SYSNAME**。 當指定，備份會儲存至分頁 blob。 如果這個參數是 NULL，則備份將儲存為區塊 blob。 已被取代的分頁 blob 的備份，因此最好使用新的區塊 blob 備份功能。 用來變更[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]組態時為選擇性參數。 如果未指定，會保留現有的組態值。  
  
> [!WARNING]  
>  **@credential_name**此時不支援參數。 支援只備份至區塊 blob，需要此參數為 NULL。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 需要的成員資格**db_backupoperator**與資料庫角色， **ALTER ANY CREDENTIAL**權限，和**EXECUTE**權限**sp_delete_backuphistory**預存程序。  
  
## <a name="examples"></a>範例  
 您可以使用最新的 Azure PowerShell 命令來建立儲存體帳戶容器和 SAS URL。 下例會 mystorageaccount 儲存體帳戶中建立新的容器，mycontainer，並接著為其取得 SAS URL 具有完整權限。  
  
```powershell  
$context = New-AzureStorageContext -StorageAccountName mystorageaccount -StorageAccountKey (Get-AzureStorageKey -StorageAccountName mystorageaccount).Primary  
New-AzureStorageContainer -Name mycontainer -Context $context  
New-AzureStorageContainerSASToken -Name mycontainer -Permission rwdl -FullUri -Context $context  
```  
  
 下列範例會啟用[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]如，執行 SQL Server 執行個體設定為 30 天的保留原則，設定目的地容器，名為 'mycontainer' 儲存體帳戶中的名為 'mystorageaccount'。  
  
```Transact-SQL 
Use msdb;  
Go  
   EXEC managed_backup.sp_backup_config_basic  
                @enable_backup=1  
                ,@container_url = 'https://mystorageaccount.blob.core.windows.net/mycontainer'  
                ,@retention_days=30;   
GO  
  
```
  
 下列範例停用執行所在之 SQL Server 執行個體的[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
  
```Transact-SQL  
Use msdb;  
Go  
EXEC managed_backup.sp_backup_config_basic  
                @enable_backup=0;  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)   
 [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
  
