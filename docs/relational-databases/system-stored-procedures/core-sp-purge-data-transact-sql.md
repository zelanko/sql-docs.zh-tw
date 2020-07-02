---
title: core. sp_purge_data （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_purge_data_TSQL
- sp_purge_data
dev_langs:
- TSQL
helpviewer_keywords:
- sp_purge_data
- management data warehouse, data collector stored procedures
- core.sp_purge_data stored procedure
- data collector [SQL Server], stored procedures
ms.assetid: 056076c3-8adf-4f51-8a1b-ca39696ac390
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2c01cfb6e469ef33c897d581eadf2da757cdb06f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85646878"
---
# <a name="coresp_purge_data-transact-sql"></a>core.sp_purge_data (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  根據保留原則，從管理資料倉儲中移除資料。 mdw_purge_data [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業會每天針對與指定之執行個體相關聯的管理資料倉儲執行這項程序。 您可以使用這個預存程序，從管理資料倉儲執行視需要的資料移除動作。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
core.sp_purge_data  
    [ [ @retention_days = ] retention_days ]  
    [ , [ @instance_name = ] 'instance_name' ]  
    [ , [ @collection_set_uid = ] 'collection_set_uid' ]  
    [ , [ @duration = ] duration ]  
```  
  
## <a name="arguments"></a>引數  
 [ @retention_days =] *retention_days*  
 要將資料保留在管理資料倉儲資料表中的天數。 已移除時間戳記早于*retention_days*的資料。 *retention_days*是**Smallint**，預設值是 Null。 如果已指定，此值必須是正數。 如果為 NULL，core.snapshots 檢視表中 valid_through 資料行的值就會決定適合移除的資料列。  
  
 [ @instance_name =] '*instance_name*'  
 收集組的執行個體名稱。 *instance_name*是**sysname**，預設值是 Null。  
  
 *instance_name*必須是完整的實例名稱，其中包含電腦名稱稱和實例名稱，其格式為*computername* \\ *instancename*。 如果為 NULL，就會使用本機伺服器上的預設執行個體。  
  
 [ @collection_set_uid =] '*collection_set_uid*'  
 收集組的 GUID。 *collection_set_uid*是**uniqueidentifier**，預設值是 Null。 如果為 NULL，就會從所有收集組中移除合格的資料列。 若要取得這個值，請查詢 syscollector_collection_sets 目錄檢視。  
  
 [ @duration =]*持續時間*  
 清除作業應該執行的最大分鐘數。 *duration*是**Smallint**，預設值是 Null。 如果已指定，此值必須是零或正整數。 如果為 NULL，此作業就會一直執行，直到移除所有合格的資料列或手動停止此作業為止。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 這個程序會根據保留週期，在 core.snapshots 檢視表中選取符合移除資格的資料列。 然後，系統會從 core.snapshots_internal 資料表中刪除符合移除資格的所有資料列。 刪除先前的資料列會在所有管理資料倉儲資料表中觸發串聯刪除動作。 這項作業是使用 ON DELETE CASCADE 子句所完成，而該子句是針對儲存所收集之資料的所有資料表所定義。  
  
 系統會在明確交易內刪除每個快照集及其相關聯的資料，然後進行認可。 因此，如果手動停止清除作業，或超過指定的值，則 @duration 只會保留未認可的資料。 這項資料可能會在下一次執行作業時移除。  
  
 此程序必須在管理資料倉儲資料庫的內容中執行。  
  
## <a name="permissions"></a>權限  
 需要**mdw_admin** （具有 EXECUTE 許可權）固定資料庫角色中的成員資格。  
  
## <a name="examples"></a>範例  
  
### <a name="a-running-sp_purge_data-with-no-parameters"></a>A. 執行不含任何參數的 sp_purge_data  
 下列範例會執行 core.sp_purge_data，但不指定任何參數。 因此，預設值 NULL 會用於所有參數，而且具有關聯的行為。  
  
```  
USE <management_data_warehouse>;  
EXECUTE core.sp_purge_data;  
GO  
```  
  
### <a name="b-specifying-retention-and-duration-values"></a>B. 指定保留和持續時間值  
 下列範例會從管理資料倉儲中移除超過 7 天的資料。 此外， @duration 系統會指定參數，讓作業的執行時間不超過5分鐘。  
  
```  
USE <management_data_warehouse>;  
EXECUTE core.sp_purge_data @retention_days = 7, @duration = 5;  
GO  
```  
  
### <a name="c-specifying-an-instance-name-and-collection-set"></a>C. 指定執行個體名稱和收集組  
 下列範例會針對指定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上的給定收集組，從管理資料倉儲中移除資料。 由於 @retention_days 未指定，因此會使用 [core. 快照] 視圖中 [valid_through] 資料行中的值來判斷適合移除之收集組的資料列。  
  
```  
USE <management_data_warehouse>;  
GO  
-- Get the collection set unique identifier for the Disk Usage system collection set.  
DECLARE @disk_usage_collection_set_uid uniqueidentifier = (SELECT collection_set_uid   
    FROM msdb.dbo.syscollector_collection_sets WHERE name = N'Disk Usage');   
  
EXECUTE core.sp_purge_data @instance_name = @@SERVERNAME, @collection_set_uid = @disk_usage_collection_set_uid;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [資料收集器預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
