---
title: sys.dm_resource_governor_external_resource_pool_affinity & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 11/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4439cddb4af80a5d76a5b4e3600fd5e5ede6b900
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47636476"
---
# <a name="sysdmresourcegovernorexternalresourcepoolaffinity-transact-sql"></a>sys.dm_resource_governor_external_resource_pool_affinity & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**適用對象**：[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)][!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] 和 [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

傳回目前的外部資源集區設定的 CPU 親和性資訊。
  
|資料行名稱|資料類型|描述|
|----------------|---------------|-----------------|
|pool_id|**int**|外部資源集區的識別碼。 不可為 Null。|
|processor_group|**smallint**|Windows 邏輯處理器群組的 ID。 不可為 Null。|
|cpu_mask|**bigint**|二進位遮罩，表示與此集區相關聯的 Cpu。 不可為 Null。|
  
## <a name="remarks"></a>備註

集區所建立的親和性`AUTO`不會出現在此檢視中因為它們沒有相似性。 如需詳細資訊，請參閱 < [CREATE EXTERNAL RESOURCE POOL &#40;TRANSACT-SQL&#41; ](../../t-sql/statements/create-external-resource-pool-transact-sql.md)並[ALTER EXTERNAL RESOURCE POOL &#40;-&#41; ](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)陳述式。

## <a name="permissions"></a>Permissions

需要 `VIEW SERVER STATE` 權限。

## <a name="see-also"></a>另請參閱

[SQL Server 中的機器學習資源管理](../../advanced-analytics/r/resource-governance-for-r-services.md)

[sys.dm_resource_governor_resource_pool_affinity &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[外部指令碼已啟用伺服器組態選項](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
