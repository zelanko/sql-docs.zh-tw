---
title: sys.databases dm_dm_compute_pools （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, big-data-clusters
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_dm_compute_pools
- dm_dm_compute_pools_TSQL
- dm_dm_compute_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_dm_compute_pools dynamic management view
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 0b21f517b540c69822dd8b1da4aa6a4cf8b8616f
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532964"
---
# <a name="sysdm_dm_compute_pools-transact-sql"></a>sys.databases dm_dm_compute_pools （Transact-sql）
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

|資料行名稱|資料類型|說明|  
|-----------------|---------------|-----------------|  
|name|`sysname`|計算集區的名稱。 不可為 Null。 傳回預設計算集區 `default`。 |
|compute_pool_id|`int`|集區的唯一識別碼。 此視圖的索引鍵。|  
|location|`sysname`|SQL Big 資料叢集中的控制器端點。 不可為 Null。 |

## <a name="permissions"></a>Permissions

在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 上，需要 `VIEW SERVER STATE` 許可權。

## <a name="see-also"></a>另請參閱

[什麼是 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)]](../../big-data-cluster/big-data-cluster-overview.md)？
