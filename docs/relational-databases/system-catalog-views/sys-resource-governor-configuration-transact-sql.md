---
title: sys.databases resource_governor_configuration （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_configuration_TSQL
- sys.resource_governor_configuration
- resource_governor_configuration_TSQL
- resource_governor_configuration
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor_configuration catalog view
ms.assetid: 89099668-1dc6-4b07-9d8b-49bc95c7bfc0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8e4068d9763460995335fe5adbd6684ecb70d8b7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73982621"
---
# <a name="sysresource_governor_configuration-transact-sql"></a>sys.resource_governor_configuration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回儲存的資源管理員狀態。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|classifier_function_id|**int**|分類函數儲存在中繼資料時的識別碼。 不可為 Null。<br /><br /> **注意**此函式是用來分類新的會話，並使用規則將工作負載路由傳送至適當的工作負載群組。 如需詳細資訊，請參閱 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)。|  
|is_enabled|**bit**|指出資源管理員的目前狀態：<br /><br /> 0 = 未啟用 Resource Governor。<br /><br /> 1 = 已啟用 Resource Governor。<br /><br /> 不可為 Null。|  
|max_outstanding_io_per_volume|**int**|**適用對象**：[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 及更新版本。<br /><br /> 每個磁碟區未完成的 I/O 數目上限。|  
  
## <a name="remarks"></a>備註  
 目錄檢視會顯示儲存在中繼資料中時的資源管理員組態。 若要查看記憶體中組態，請使用對應的動態管理檢視。  
  
## <a name="permissions"></a>權限  
 需要 VIEW ANY DEFINITION 權限檢視內容；需要 CONTROL SERVER 權限變更內容。  
  
## <a name="examples"></a>範例  
 下列範例顯示如何取得並比較儲存的中繼資料值與資源管理員組態的記憶體中值。  
  
```  
USE master;  
GO  
-- Get the stored metadata.  
SELECT   
object_schema_name(classifier_function_id) AS 'Classifier UDF schema in metadata',   
object_name(classifier_function_id) AS 'Classifier UDF name in metadata'  
FROM   
sys.resource_governor_configuration;  
GO  
-- Get the in-memory configuration.  
SELECT   
object_schema_name(classifier_function_id) AS 'Active classifier UDF schema',   
object_name(classifier_function_id) AS 'Active classifier UDF name'  
FROM   
sys.dm_resource_governor_configuration;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [Resource Governor 目錄檢視 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [dm_resource_governor_configuration &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql.md)   
 [資源管理員](../../relational-databases/resource-governor/resource-governor.md)  
  
  
