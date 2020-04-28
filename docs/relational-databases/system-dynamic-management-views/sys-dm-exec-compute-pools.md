---
title: sys.databases dm_exec_compute_pools （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, big-data-clusters
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_compute_pools
- dm_exec_compute_pools_TSQL
- dm_exec_compute_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_compute_pools dynamic management view
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: d749b9a7d9689426bffafe20ee7ab46ce199ffbb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "75254606"
---
# <a name="sysdm_exec_compute_pools-transact-sql"></a>sys.databases dm_exec_compute_pools （Transact-sql）
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|NAME|`sysname`|計算集區的名稱。 不可為 Null。 `default`傳回預設計算集區的。 |
|compute_pool_id|`int`|集區的唯一識別碼。 此視圖的索引鍵。|  
|location|`sysname`|SQL Big 資料叢集中的控制器端點。 不可為 Null。 |

## <a name="permissions"></a>權限

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]上， `VIEW SERVER STATE`需要許可權。

## <a name="see-also"></a>另請參閱

[什麼是[!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)] ](../../big-data-cluster/big-data-cluster-overview.md)？
