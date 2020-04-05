---
title: 系統dm_resource_governor_external_resource_pool_affinity(轉算-SQL) |微軟文件
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
ms.openlocfilehash: 77d0d322139be1f1c6086622855600a7c24fc4c9
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664326"
---
# <a name="sysdm_resource_governor_external_resource_pool_affinity-transact-sql"></a>系統dm_resource_governor_external_resource_pool_affinity(轉算-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**適用於：** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] 和 [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

返回有關當前外部資源池配置的 CPU 關聯資訊。
  
|資料行名稱|資料類型|描述|
|----------------|---------------|-----------------|
|pool_id|**int**|外部資源池的 ID。 不可為 Null。|
|processor_group|**小林特**|Windows 邏輯處理器群組的 ID。 不可為 Null。|
|cpu_mask|**bigint**|表示與此池關聯的 CPU 的二進位遮罩。 不可為 Null。|
  
## <a name="remarks"></a>備註

創建具有的關聯池`AUTO`不會顯示在此視圖中,因為它們沒有關聯。 有關詳細資訊,請參閱[創建外部資源池&#40;處理-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)和[更改外部資源池&#40;處理-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)語句。

## <a name="permissions"></a>權限

需要 `VIEW SERVER STATE` 權限。

## <a name="see-also"></a>另請參閱

[SQL Server 中的機器學習資源管理](../../machine-learning/administration/resource-governor.md)

[系統dm_resource_governor_resource_pool_affinity&#40;轉算-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[開啟外部文稿伺服器設定選項](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
