---
title: sys.dm_resource_governor_external_resource_pools (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 05/02/2018
ms.suite: sql
ms.prod: sql
ms.prod_service: database-engine
ms.technology: machine-learning
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_external_resource_pools_TSQL
- sys.dm_resource_governor_external_resource_pools
- dm_resource_governor_external_resource_pools
- dm_resource_governor_external_resource_pools_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_resource_governor_external_resource_pools
- sys.dm_resource_governor_external_resource_pools
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e6b46c15eb13c6d738abc28b32816ab690fb9abf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmresourcegovernorexternalresourcepools-transact-sql"></a>sys.dm_resource_governor_external_resource_pools (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

傳回目前的外部資源集區狀態、 資源集區和資源集區統計資料的目前組態的相關資訊。 
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
|資料行名稱      |資料類型      |Description|  
|----------------|---------------|-----------------| 
| external_pool_id|**int**|資源集區的識別碼。 不可為 Null。 |
| name|**sysname**|資源集區的名稱。 不可為 Null。 
| pool_version|**int**|nternal 版本號碼。|
| max_cpu_percent|**int**|當 CPU 出現競爭時，資源集區中所有要求允許之最大平均 CPU 頻寬的目前組態。 不可為 Null。 |
| max_processes|**int**|並行的外部處理序的數目上限。 預設值為 0 時，不會指定任何限制。 不可為 Null。|
| max_memory_percent|**int**|在此資源集區中，可供要求所用之伺服器記憶體總量百分比的目前組態。 不可為 Null。 |
| statistics_start_time|**datetime**|重設此集區統計資料時的時間。 不可為 Null。 
| peak_memory_kb|**bigint**|他最大記憶體數量，以 kb 為單位，資源集區使用。 不可為 Null。 |
| write_io_count|**int**|重設資源管理員統計資料之後發出的寫入 IO 總數。 不可為 Null。 |
| read_io_count|**int**|重設資源管理員統計資料之後發出的讀取 IO 總數。 不可為 Null。 |
| total_cpu_kernel_ms|**bigint**|累計 CPU 使用者時間 （毫秒） 重設資源管理員統計資料之後。 不可為 Null。 |
| total_cpu_user_ms|**bigint**|累計 CPU 使用者時間 （毫秒） 重設資源管理員統計資料之後。 不可為 Null。 |
| active_processes_count|**int**|外部處理序執行時的要求數目。 不可為 Null。 |

 
## <a name="permissions"></a>Permissions

需要 `VIEW SERVER STATE` 權限。

## <a name="see-also"></a>另請參閱  
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
