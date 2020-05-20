---
title: sp_help_downloadlist （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_downloadlist_TSQL
- sp_help_downloadlist
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_downloadlist
ms.assetid: 745b265b-86e8-4399-b928-c6969ca1a2c8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9dd52e6d2e4bf8a1a099ea2391a2c6ce2d6decdc
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827722"
---
# <a name="sp_help_downloadlist-transact-sql"></a>sp_help_downloadlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出所提供之作業的**sysdownloadlist**系統資料表中的所有資料列，如果未指定任何工作，則為所有資料列。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_downloadlist { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }   
     [ , [ @operation = ] 'operation' ]   
     [ , [ @object_type = ] 'object_type' ]   
     [ , [ @object_name = ] 'object_name' ]   
     [ , [ @target_server = ] 'target_server' ]   
     [ , [ @has_error = ] has_error ]   
     [ , [ @status = ] status ]   
     [ , [ @date_posted = ] date_posted ]  
```  
  
## <a name="arguments"></a>引數  
`[ @job_id = ] job_id`要傳回其資訊的作業識別碼。 *job_id*是**uniqueidentifier**，預設值是 Null。  
  
`[ @job_name = ] 'job_name'`作業的名稱。 *job_name*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  必須指定*job_id*或*job_name* ，但不能同時指定兩者。  
  
`[ @operation = ] 'operation'`指定之作業的有效操作。 *operation*是**Varchar （64）**，預設值是 Null，它可以是下列值之一。  
  
|值|說明|  
|-----------|-----------------|  
|**包裝箱**|要求目標伺服器脫離主要**SQLServerAgent**服務的伺服器操作。|  
|**DELETE**|移除整項作業的作業動作。|  
|**INSERT**|插入整項作業或重新整理現有作業的作業動作。 適當的話，這個動作包括所有作業步驟和排程。|  
|**RE-ENLIST**|使目標伺服器將編列資訊 (包括輪詢間隔和時區) 重新傳送到多伺服器網域的伺服器作業。 目標伺服器也會 redownloads **MSXOperator**詳細資料。|  
|**SET-POLL**|設定目標伺服器輪詢多伺服器網域的間隔 (以秒為單位) 之伺服器作業。 如果指定，*值*會被視為所需的間隔值，而且可以是從**10**到**28800**的值。|  
|**「**|要求開始執行作業的作業動作。|  
|**停止**|要求停止執行作業的作業動作。|  
|**SYNC-TIME**|使目標伺服器將它的系統時鐘和多伺服器網域同步化的伺服器作業。 由於這項作業成本很高，因此，請盡量不要太常執行這項作業。|  
|**UPDATE**|作業只會更新作業的**sysjobs**資訊，而不是作業步驟或排程。 **Sp_update_job**會自動呼叫。|  
  
`[ @object_type = ] 'object_type'`指定之作業的物件類型。 *object_type*是**Varchar （64）**，預設值是 Null。 *object_type*可以是 [作業] 或 [伺服器]。 如需有效*object_type*值的詳細資訊，請參閱[sp_add_category &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)。  
  
`[ @object_name = ] 'object_name'`物件的名稱。 *object_name*是**sysname**，預設值是 Null。 如果*object_type*是工作， *object_name*就是作業名稱。 如果*object_type*是 server， *object_name*就是伺服器名稱。  
  
`[ @target_server = ] 'target_server'`目標伺服器的名稱。 *target_server*是**Nvarchar （128）**，預設值是 Null。  
  
`[ @has_error = ] has_error`這是指作業是否應該認可錯誤。 *has_error*是**Tinyint**，預設值是 Null，表示不應該認可任何錯誤。 **1**表示應認可所有錯誤。  
  
`[ @status = ] status`作業的狀態。 *狀態*為**Tinyint**，預設值為 Null。  
  
`[ @date_posted = ] date_posted`在指定的日期和時間之前或之後，所有專案都應該包含在結果集內的日期和時間。 *date_posted*是**datetime**，預設值是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|指示的唯一整數識別碼。|  
|**source_server**|**nvarchar(30)**|指示的來源伺服器電腦名稱。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 版中，這一律是主伺服器（MSX）的電腦名稱稱。|  
|**operation_code**|**nvarchar(4000)**|指示的作業碼。|  
|**object_name**|**sysname**|指示所影響的物件。|  
|**object_id**|**uniqueidentifier**|受指令影響的物件識別碼（工作物件的**job_id** ，或伺服器物件的0x00），或**operation_code**特定的資料值。|  
|**target_server**|**nvarchar(30)**|將下載這個指示的目標伺服器。|  
|**error_message**|**nvarchar(1024)**|當目標伺服器在處理這個指示發生問題時，所發出的錯誤訊息 (如果有的話)。<br /><br /> 注意：任何錯誤訊息都會封鎖目標伺服器所有進一步的下載。|  
|**date_posted**|**datetime**|將指示公佈到資料表中的日期。|  
|**date_downloaded**|**datetime**|目標伺服器下載指示的日期。|  
|**status**|**tinyint**|作業的狀態：<br /><br /> **0** = 尚未下載<br /><br /> **1** = 已成功下載。|  
  
## <a name="permissions"></a>權限  
 執行此程式的許可權預設為**系統管理員（sysadmin** ）固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
 下列範例會列出 `sysdownloadlist` 作業之 `NightlyBackups` 中的資料列。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_downloadlist  
    @job_name = N'NightlyBackups',  
    @operation = N'UPDATE',   
    @object_type = N'JOB',   
    @object_name = N'NightlyBackups',  
    @target_server = N'SEATTLE2',   
    @has_error = 1,   
    @status = NULL,   
    @date_posted = NULL ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
