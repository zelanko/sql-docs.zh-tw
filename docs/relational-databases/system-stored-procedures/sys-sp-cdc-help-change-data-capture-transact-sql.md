---
title: sys.databases sp_cdc_help_change_data_capture （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_help_change_data_capture_TSQL
- sys.sp_cdc_help_change_data_capture_TSQL
- sp_cdc_help_change_data_capture
- sys.sp_cdc_help_change_data_capture
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], querying metadata
- sys.sp_cdc_help_change_data_capture
- sp_cdc_help_change_data_capture
ms.assetid: 91fd41f5-1b4d-44fe-a3b5-b73eff65a534
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7935bc8e0472b90d22a93190f5af81c8e5910e67
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891090"
---
# <a name="syssp_cdc_help_change_data_capture-transact-sql"></a>sys.sp_cdc_help_change_data_capture (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  針對在目前資料庫中啟用異動資料擷取的每個資料表，傳回異動資料擷取組態。 每個來源資料表最多可傳回兩個資料列 (每個擷取執行個體一個資料列)。 並非每個 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中都無法異動資料擷取。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.sp_cdc_help_change_data_capture   
  [ [ @source_schema = ] 'source_schema' ]  
  [, [ @source_name = ] 'source_name' ]  
```  
  
## <a name="arguments"></a>引數  
 [ @source_schema =] '*source_schema*'  
 這是來源資料表所屬的結構描述名稱。 *source_schema*是**sysname**，預設值是 Null。 當指定*source_schema*時，也必須指定*source_name* 。  
  
 如果非 Null， *source_schema*必須存在於目前的資料庫中。  
  
 如果*source_schema*為非 null， *source_name*也必須是非 null。  
  
 [ @source_name =] '*source_name*'  
 這是來源資料表的名稱。 *source_name*是**sysname**，預設值是 Null。 當指定*source_name*時，也必須指定*source_schema* 。  
  
 如果非 Null， *source_name*必須存在於目前的資料庫中。  
  
 如果*source_name*為非 null， *source_schema*也必須是非 null。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|source_schema|**sysname**|來源資料表結構描述的名稱。|  
|source_table|**sysname**|來源資料表的名稱。|  
|capture_instance|**sysname**|擷取執行個體的名稱。|  
|object_id|**int**|與來源資料表相關聯之變更資料表的識別碼。|  
|source_object_id|**int**|來源資料表的識別碼。|  
|start_lsn|**binary(10)**|代表查詢變更資料表之低端點的記錄序號 (LSN)。<br /><br /> NULL = 尚未建立低端點。|  
|end_lsn|**binary(10)**|代表查詢變更資料表之高端點的 LSN。 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中，這個資料行一律是 NULL。|  
|supports_net_changes|**bit**|淨變更支援已啟用。|  
|has_drop_pending|**bit**|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中不使用。|  
|role_name|**sysname**|用來控制變更資料之存取權的資料庫角色名稱。<br /><br /> NULL = 不使用角色。|  
|index_name|**sysname**|在來源資料表中，用來唯一識別資料列的索引名稱。|  
|filegroup_name|**sysname**|變更資料表所在的檔案群組名稱。<br /><br /> NULL = 變更資料表位於資料庫的預設檔案群組中。|  
|create_date|**datetime**|啟用擷取執行個體的日期。|  
|index_column_list|**nvarchar(max)**|在來源資料表中，用來唯一識別資料列的索引資料行清單。|  
|captured_column_list|**nvarchar(max)**|擷取的來源資料行清單。|  
  
## <a name="remarks"></a>備註  
 當*source_schema*和*SOURCE_NAME*預設為 null，或明確設定為 null 時，這個預存程式會傳回呼叫端已選取存取權之所有資料庫捕捉實例的資訊。 當*source_schema*和*SOURCE_NAME*不是 Null 時，只會傳回特定已啟用資料表的相關資訊。  
  
## <a name="permissions"></a>權限  
 當*source_schema*和*source_name*為 Null 時，呼叫端的授權會決定哪些已啟用的資料表會包含在結果集中。 呼叫端必須擁有擷取執行個體之所有擷取資料行的 SELECT 權限，以及要包含之資料表資訊的任何已定義控制角色中的成員資格。 db_owner 資料庫角色的成員可以檢視所有已定義之擷取執行個體的相關資訊。 要求特定啟用資料表的資訊時，就會針對具名資料表套用相同的 SELECT 和成員資格準則。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-change-data-capture-configuration-information-for-a-specified-table"></a>A. 針對指定的資料表傳回異動資料擷取組態資訊  
 下列範例會針對 `HumanResources.Employee` 資料表傳回異動資料擷取組態。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_help_change_data_capture   
    @source_schema = N'HumanResources',   
    @source_name = N'Employee';  
GO  
```  
  
### <a name="b-returning-change-data-capture-configuration-information-for-all-tables"></a>B. 針對所有資料表傳回異動資料擷取組態資訊  
 下列範例會針對資料庫中包含呼叫端經授權可存取之變更資料的所有啟用資料表，傳回組態資訊。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_help_change_data_capture;  
GO  
```  
  
  
