---
title: sys.databases resource_governor_external_resource_pools （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/13/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_external_resource_pools
- sys.resource_governor_external_resource_pools_TSQL
- resource_governor_external_resource_pools
- resource_governor_external_resource_pools_TSQL
helpviewer_keywords:
- sys.resource_governor_external_resource_pools
- resource_governor_external_resource_pools
ms.assetid: 75063e36-a91b-496f-9936-88f3d57bd447
author: stevestein
ms.author: sstein
ms.openlocfilehash: 79c81cafe588fd827ece6184cab5470df8ec4c42
ms.sourcegitcommit: eef5ab1966062e190dc1cd49409bc0429ba6d1e4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/26/2020
ms.locfileid: "80290849"
---
# <a name="sysresource_governor_external_resource_pools-transact-sql"></a>sys.databases resource_governor_external_resource_pools （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**適用於：** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] 和 [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

傳回中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]儲存的外部資源集區設定。 檢視的每個資料列都會決定集區的組態。
  
|資料行名稱|資料類型|描述|
|-----------------|---------------|-----------------|
|external_pool_id|**int**|資源集區的唯一識別碼。 不可為 Null。|
|NAME|**sysname**|資源集區的名稱。 不可為 Null。|
|max_cpu_percent|**int**|當 CPU 出現瓶頸時，針對資源集區中的所有要求所允許的最大平均 CPU 頻寬。 不可為 Null。|
|max_memory_percent|**int**|在此資源集區中，可供要求所用的伺服器記憶體總量百分比。 不可為 Null。 有效的最大值取決於集區最小值。 例如，max_memory_percent 可以設定為 100，但有效的最大值比較低。|
|max_processes|**int**|並行外部進程的最大數目。 預設值為 0 時，不會指定任何限制。 不可為 Null。|
|version|**bigint**|內部版本號碼。|
  
## <a name="permissions"></a>權限

需要 VIEW SERVER STATE 權限。

## <a name="see-also"></a>另請參閱

[SQL Server 中機器學習服務的資源管理](../../advanced-analytics/r/resource-governance-for-r-services.md)

[Resource Governor 目錄檢視 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)

[dm_resource_governor_resource_pools &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)

[資源管理員](../../relational-databases/resource-governor/resource-governor.md)

[dm_resource_governor_resource_pool_affinity &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[外部指令碼已啟用伺服器組態選項](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
