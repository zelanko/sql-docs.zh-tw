---
title: sys.databases dm_cluster_endpoints （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, big-data-clusters
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_cluster_endpoints
- dm_cluster_endpoints_TSQL
- dm_cluster_endpoints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cluster_endpoints dynamic management view
ms.assetid: ''
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: fe06d6b7c00fe60c44b19468f9ef0cc814d25e5d
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86913227"
---
# <a name="sysdm_cluster_endpoints-transact-sql"></a>sys.databases dm_cluster_endpoints （Transact-sql）
[!INCLUDE[sqlserver2019](../../includes/applies-to-version/sqlserver2019.md)]

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|NAME|`sysname`|在 SQL big data 叢集中外部公開的服務名稱。 端點的唯一識別碼。 此視圖的索引鍵。 不可為 Null。 |  
|description|`nvarchar(4000)`|服務的描述。 不可為 Null。 |
|端點|`sysname`|端點 url 或連接屬性。 不可為 Null。 |
|protocol_desc|`sysname`|端點通訊協定的描述 |

## <a name="permissions"></a>權限

在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 許可權。

## <a name="see-also"></a>另請參閱

[什麼是 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)] ](../../big-data-cluster/big-data-cluster-overview.md)？
