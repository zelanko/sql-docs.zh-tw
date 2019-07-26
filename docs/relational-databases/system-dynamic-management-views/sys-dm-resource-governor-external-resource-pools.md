---
title: _resource_governor_external_resource_pools (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
ms.prod: sql
ms.technology: machine-learning
ms.reviewer: ''
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
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: cf77a073a1432df839bfd13046c66018496e79f1
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68468518"
---
# <a name="sysdmresourcegovernorexternalresourcepools-transact-sql"></a>sys.databases _resource_governor_external_resource_pools (Transact-sql)
[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

傳回目前外部資源集區狀態的相關資訊、資源集區的目前設定, 以及資源集區統計資料。 
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
|資料行名稱      |資料類型      |描述|  
|----------------|---------------|-----------------| 
| external_pool_id|**int**|資源集區的識別碼。 不可為 Null。 |
| name|**sysname**|資源集區的名稱。 不可為 Null。 
| pool_version|**int**|內部版本號碼。|
| max_cpu_percent|**int**|當 CPU 出現競爭時，資源集區中所有要求允許之最大平均 CPU 頻寬的目前組態。 不可為 Null。 |
| max_processes|**int**|並行外部進程的最大數目。 預設值為 0 時，不會指定任何限制。 不可為 Null。|
| max_memory_percent|**int**|在此資源集區中，可供要求所用之伺服器記憶體總量百分比的目前組態。 不可為 Null。 |
| statistics_start_time|**datetime**|重設此集區統計資料時的時間。 不可為 Null。 
| peak_memory_kb|**bigint**|資源集區使用的記憶體數量上限 (以 kb 為單位)。 不可為 Null。 |
| write_io_count|**int**|重設資源管理員統計資料之後發出的寫入 IO 總數。 不可為 Null。 |
| read_io_count|**int**|重設資源管理員統計資料之後發出的讀取 IO 總數。 不可為 Null。 |
| total_cpu_kernel_ms|**bigint**|重設資源管理員之後統計資料後的累計 CPU 使用者核心時間 (以毫秒為單位)。 不可為 Null。 |
| total_cpu_user_ms|**bigint**|已重設資源管理員之後統計資料後的累計 CPU 使用者時間 (以毫秒為單位)。 不可為 Null。 |
| active_processes_count|**int**|在要求當時執行的外部進程數目。 不可為 Null。 |

 
## <a name="permissions"></a>Permissions

需要 `VIEW SERVER STATE` 權限。

## <a name="see-also"></a>另請參閱  
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
