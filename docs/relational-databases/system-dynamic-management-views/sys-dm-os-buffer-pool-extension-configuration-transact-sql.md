---
title: sys.dm_os_buffer_pool_extension_configuration (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_buffer_pool_extension_configuration
- sys.dm_os_buffer_pool_extension_configuration_TSQL
- dm_os_buffer_pool_extension_configuration_TSQL
- sys.dm_os_buffer_pool_extension_configuration
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_buffer_pool_extension_configuration dynamic management view
ms.assetid: d52cc481-4d29-4f33-b63d-231ec35d092f
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c04646c8eb9598ffa293f577996ea0357bcdb89f
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmosbufferpoolextensionconfiguration-transact-sql"></a>sys.dm_os_buffer_pool_extension_configuration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  傳回有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中緩衝集區延伸模組的組態資訊。 針對每個緩衝集區延伸模組檔案，各傳回一個資料列。  
  

  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|路徑|**nvarchar**(256)|緩衝集區延伸模組快取的路徑和檔案名稱。 可為 Null。|  
|file_id|**int**|緩衝集區延伸模組檔案的識別碼。 不可為 Null。|  
|state|**int**|緩衝集區延伸模組功能的狀態。 不可為 Null。<br /><br /> 0 - 緩衝集區延伸模組已停用<br /><br /> 1 - 緩衝集區延伸模組停用中<br /><br /> 2-保留供未來使用<br /><br /> 3 - 緩衝集區延伸模組啟用中<br /><br /> 4 - 保留供日後使用<br /><br /> 5 - 緩衝集區延伸模組已啟用|  
|state_description|**nvarchar**(60)|描述緩衝集區延伸模組功能的狀態。 可為 Null。<br /><br /> 0 = BUFFER POOL EXTENSION DISABLED<br /><br /> 1 = BUFFER POOL EXTENSION ENABLED|  
|current_size_in_kb|**bigint**|緩衝集區延伸模組檔案的目前大小。 不可為 Null。|  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-configuration-buffer-pool-extension-information"></a>A. 傳回組態緩衝集區延伸模組資訊  
 下列範例會從 sys.dm_os_buffer_pool_extension_configruation DMV 傳回所有資料行。  
  
```sql  
SELECT path, file_id, state, state_description, current_size_in_kb  
FROM sys.dm_os_buffer_pool_extension_configuration;  
```  
  
### <a name="b-returning-the-number-of-cached-pages-in-the-buffer-pool-extension-file"></a>B. 傳回緩衝集區延伸模組檔案中的快取頁面數目  
 下列範例會傳回每個緩衝集區延伸模組檔案中的快取頁面數目。  
  
```sql  
SELECT COUNT(*) AS cached_pages_count  
FROM sys.dm_os_buffer_descriptors  
WHERE is_in_bpool_extension <> 0  
;  
```  
  
## <a name="see-also"></a>另請參閱  
 [緩衝集區擴充](../../database-engine/configure-windows/buffer-pool-extension.md)   
 [sys.dm_os_buffer_descriptors & #40;TRANSACT-SQL & #41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-descriptors-transact-sql.md)  
  
  
