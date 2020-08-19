---
description: 'sys. dm_exec_compute_pools (Transact-sql) '
title: sys. dm_exec_compute_pools (Transact-sql) |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: bb084b65a4b4e850b5e1966ceb2354d18a0ac095
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447602"
---
# <a name="sysdm_exec_compute_pools-transact-sql"></a>sys. dm_exec_compute_pools (Transact-sql) 
[!INCLUDE[sqlserver2019](../../includes/applies-to-version/sqlserver2019.md)]

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|NAME|`sysname`|計算集區的名稱。 不可為 Null。 `default`針對預設的計算集區傳回。 |
|compute_pool_id|`int`|集區的唯一識別碼。 此視圖的索引鍵。|  
|location|`sysname`|SQL Big Data 叢集中的端點至控制器。 不可為 Null。 |

## <a name="permissions"></a>權限

在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 許可權。

## <a name="see-also"></a>另請參閱

[什麼是 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)] ](../../big-data-cluster/big-data-cluster-overview.md)？
