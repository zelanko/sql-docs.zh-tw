---
title: sysdac_history_internal & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdac_history_internal
- sysdac_history_internal_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdac_history_internal
ms.assetid: 774a1678-0b27-42be-8adc-a6d7a4a56510
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 40696085bc8eb9980d1150feade91a9edd627be0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62471137"
---
# <a name="data-tier-application-tables---sysdachistoryinternal"></a>資料層應用程式資料表 - sysdac_history_internal
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含有關管理資料層應用程式 (DAC) 採取之動作的相關資訊。 這份資料表儲存在**dbo**的結構描述**msdb**資料庫。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**action_id**|**int**|動作的識別碼|  
|**sequence_id**|**int**|識別動作中的步驟。|  
|**instance_id**|**uniqueidentifier**|DAC 執行個體的識別碼。 可以聯結此資料行**instance_id**中的資料行[dbo.sysdac_instances &#40;-&#41;](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md)。|  
|**action_type**|**tinyint**|動作類型的識別碼：<br /><br /> **0** = 部署<br /><br /> **1** = 建立<br /><br /> **2** = 重新命名<br /><br /> **3** = 卸離<br /><br /> **4** = 刪除|  
|**action_type_name**|**varchar(19)**|動作類型的名稱：<br /><br /> **deploy**<br /><br /> **create**<br /><br /> **rename**<br /><br /> **detach**<br /><br /> **delete**|  
|**dac_object_type**|**tinyint**|受到動作影響之物件類型的識別碼：<br /><br /> **0** = dacpac<br /><br /> **1** = 登入<br /><br /> **2** = 資料庫|  
|**dac_object_type_name**|**varchar(8)**|受到動作影響之物件類型的名稱：<br /><br /> **dacpac** = DAC 執行個體<br /><br /> **login**<br /><br /> **資料庫**|  
|**action_status**|**tinyint**|識別動作目前狀態的代碼：<br /><br /> **0** = 暫止<br /><br /> **1** = 成功<br /><br /> **2** = 失敗|  
|**action_status_name**|**varchar(11)**|動作的目前狀態：<br /><br /> **pending**<br /><br /> **success**<br /><br /> **fail**|  
|**必要**|**bit**|在回復 DAC 作業時，由 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 使用。|  
|**dac_object_name_pretran**|**sysname**|認可包含動作之交易前的物件名稱。 僅用於資料庫與登入。|  
|**dac_object_name_posttran**|**sysname**|認可包含動作之交易後的物件名稱。 僅用於資料庫與登入。|  
|**sqlscript**|**nvarchar(max)**|在資料庫或登入上實作動作的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。|  
|**payload**|**varbinary(max)**|儲存在二進位編碼字串中的 DAC 封裝定義。|  
|**註解**|**varchar(max)**|記錄 DAC 升級中接受潛在資料流失之使用者的登入。|  
|**error_string**|**nvarchar(max)**|動作發生錯誤時所產生的錯誤訊息。|  
|**created_by**|**sysname**|啟動建立此項目之動作的登入。|  
|**date_created**|**datetime**|建立此項目的日期和時間。|  
|**date_modified**|**datetime**|上次修改此項目的日期和時間。|  
  
## <a name="remarks"></a>備註  
 DAC 管理動作 (例如，部署或刪除 DAC) 會產生多個步驟。 針對每個動作都會指派一個動作識別碼。 每個步驟都會指派一個序號和中的資料列**sysdac_history_internal**，步驟的狀態記錄的位置。 當動作步驟啟動時，會建立每個資料列，並在需要時進行更新，以反映作業的狀態。 例如，部署 DAC 動作中，可以指派**action_id** 12 並得到 4 個資料列中**sysdac_history_internal**:  
  
|||||  
|-|-|-|-|  
|**action_id**|**sequence_id**|**action_type_name**|**dac_object_type_name**|  
|12|0|建立|dacpac|  
|12|1|建立|login|  
|12|2|建立|database|  
|12|3|重新命名|database|  
  
 DAC 作業，例如刪除，不會移除資料列**sysdac_history_internal**。 您可以使用下列查詢手動刪除 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體上不再部署的之 DAC 的資料列：  
  
```sql  
DELETE FROM msdb.dbo.sysdac_history_internal  
WHERE instance_id NOT IN  
   (SELECT instance_id  
    FROM msdb.dbo.sysdac_instances_internal);  
```  
  
 刪除使用中 DAC 的資料列不會影響 DAC 作業；唯一的影響是，您將無法報告 DAC 的完整記錄。  
  
> [!NOTE]  
>  目前沒有任何機制可用於刪除**sysdac_history_internal**上的資料列[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
## <a name="permissions"></a>Permissions  
 需要系統管理員 (sysadmin) 固定伺服器角色中的成員資格。 唯讀存取此檢視會提供給有權連接到 master 資料庫的所有使用者。  
  
## <a name="see-also"></a>另請參閱  
 [資料層應用程式](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [dbo.sysdac_instances &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md)   
 [sysdac_instances_internal &#40;Transact-SQL&#41;](../../relational-databases/system-tables/data-tier-application-tables-sysdac-instances-internal.md)  
  
  
