---
title: managed_backup.fn_backup_db_config (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- smart_admin.fn_backup_db_config
- smart_admin.fn_backup_db_config_TSQL
- fn_backup_db_config
- fn_backup_db_config_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_backup_db_config
- fn_backup_db_config
ms.assetid: 7c755d8a-64dd-44b2-be5e-735d30758900
caps.latest.revision: 14
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2a3cf62f8d658136c7bab304a6f4c73d62c77ba4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="managedbackupfnbackupdbconfig-transact-sql"></a>managed_backup.fn_backup_db_config (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  將 0、1 或更多資料列和[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]組態設定一起傳回。 針對指定的資料庫傳回 1 個資料列，或是傳回執行個體上以[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]設定之所有資料庫的資訊。  
  
 使用此預存程序可檢閱或判斷 SQL Server 執行個體上某個資料庫或所有資料庫的目前[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]組態設定。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
managed_backup.fn_backup_db_config (‘database_name’ | ‘’ | NULL)  
```  
  
##  <a name="Arguments"></a> 引數  
 @db_name  
 資料庫的名稱。 @db_name參數是**SYSNAME**。 如果將空字串或 NULL 值傳遞給此參數，則會傳回 SQL Server 執行個體上所有資料庫的相關資訊。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|db_name|SYSNAME|資料庫名稱。|  
|db_guid|UNIQUEIDENTIFIER|唯一識別資料庫的識別碼。|  
|is_availability_database|BIT|資料庫是否參與可用性群組。 值 1 表示資料庫為可用性資料庫，0 表示不是。|  
|is_dropped|BIT|值 1 表示這是已卸除的資料庫。|  
|credential_name|SYSNAME|用來驗證儲存體帳戶之 SQL 認證的名稱。 NULL 值表示未設定 SQL 認證。|  
|retention_days|INT|目前的保留期限 (以天為單位)。 NULL 值表示從未設定此資料庫的[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。|  
|is_smart_backup_enabled|INT|指出目前是否已啟用此資料庫的[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。 值 1 表示目前已啟用[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]，值 0 表示已停用此資料庫的[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。|  
|storage_url|NVARCHAR （1024)|儲存體帳戶的 URL。|  
|Encryption_algorithm|NCHAR(20)|傳回加密備份時所使用的目前加密演算法。|  
|Encryptor_type|NCHAR(15)|傳回加密程式設定：憑證或非對稱金鑰。|  
|Encryptor_name|NCHAR(max_length_of_cert/asymm_key_name)|憑證或非對稱金鑰的名稱。|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 需要的成員資格**db_backupoperator**與資料庫角色**ALTER ANY CREDENTIAL**權限。 使用者不應被拒絕**VIEW ANY DEFINITION**權限。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 'TestDB' 的[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]組態  
  
 針對每個程式碼片段，請在語言屬性欄位中選取 'tsql'。  
  
```  
Use msdb  
GO  
SELECT * FROM managed_backup.fn_backup_db_config('TestDB')  
```  
  
 下列範例會為執行所在之 SQL Server 執行個體上的所有資料庫傳回 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 組態。  
  
```  
Use msdb  
GO  
SELECT * FROM managed_backup.fn_backup_db_config (NULL)  
```  
  
  
