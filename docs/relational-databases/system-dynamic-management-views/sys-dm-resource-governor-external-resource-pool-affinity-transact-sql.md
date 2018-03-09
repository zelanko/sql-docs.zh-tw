---
title: "sys.dm_resource_governor_external_resource_pool_affinity (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 11/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_external_resource_pool_affinity
- sys.dm_resource_governor_external_resource_pool_affinity_TSQL
- dm_resource_governor_external_resource_pool_affinity
- dm_resource_governor_external_resource_pool_affinity_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_resource_governor_external_resource_pool_affinity
- dm_resource_governor_external_resource_pool_affinity
ms.assetid: e32fac49-5161-47c0-8540-af3fe730c00c
caps.latest.revision: 
author: jeannt
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c1f5fa2851b5b03708eb28c42d4e2496258d187b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmresourcegovernorexternalresourcepoolaffinity-transact-sql"></a>sys.dm_resource_governor_external_resource_pool_affinity (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**適用於：** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]和[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

傳回目前的外部資源集區設定的 CPU 親和性資訊。
  
|資料行名稱|資料類型|Description|
|----------------|---------------|-----------------|
|pool_id|**int**|外部資源集區的識別碼。 不可為 Null。|
|processor_group|**smallint**|Windows 邏輯處理器群組的 ID。 不可為 Null。|
|cpu_mask|**bigint**|二進位遮罩，表示與此集區相關聯的 Cpu。 不可為 Null。|
  
## <a name="remarks"></a>備註

集區所建立的親和性`AUTO`沒有出現在此檢視，因為它們沒有相似性。 如需詳細資訊，請參閱[CREATE EXTERNAL RESOURCE POOL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)和[ALTER 外部資源集區 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)陳述式。

## <a name="permissions"></a>Permissions

需要 `VIEW SERVER STATE` 權限。

## <a name="see-also"></a>另請參閱

[SQL Server 中的機器學習資源管理](../../advanced-analytics/r/resource-governance-for-r-services.md)

[sys.dm_resource_governor_resource_pool_affinity &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[外部指令碼已啟用伺服器組態選項](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
