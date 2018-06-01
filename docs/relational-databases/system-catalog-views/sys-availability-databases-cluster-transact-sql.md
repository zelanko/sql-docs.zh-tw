---
title: sys.availability_databases_cluster (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.availability_databases_cluster_TSQL
- sys.availability_databases_cluster
- availability_databases_cluster_TSQL
- availability_databases_cluster
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.availability_databases_cluster catalog view
- Availability Groups [SQL Server], databases
ms.assetid: 8d9c57e5-7f39-4315-b466-92748231140a
caps.latest.revision: 14
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5b0c0cd91b58c4e59cba2440d8f02cd01a93c870
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2018
ms.locfileid: "33179184"
---
# <a name="sysavailabilitydatabasescluster-transact-sql"></a>sys.availability_databases_cluster (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  包含每個可用性資料庫的執行個體上的一個資料列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]裝載之可用性複本的任何 Alwayson 可用性群組在 Windows Server 容錯移轉叢集 (WSFC) 叢集中，不論是否在本機複製資料庫已聯結至可用性群組。  
  
> [!NOTE]  
>  當資料庫加入至可用性群組時，主要資料庫會自動聯結至此群組。 次要資料庫必須先在每個次要複本上備妥，然後才能聯結至可用性群組。   
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|可用性群組的唯一識別碼，資料庫會參與此可用性群組 (如果有的話)。<br /><br /> NULL = 資料庫不是可用性群組中可用性複本的一部分。|  
|**group_database_id**|**uniqueidentifier**|資料庫參與之可用性群組 (如果有的話) 內資料庫的唯一識別碼。 **group_database_id**是相同的主要複本上和每個次要複本所在的資料庫已加入至可用性群組的這個資料庫。<br /><br /> NULL = 資料庫不是任何可用性群組中可用性複本的一部分。|  
|**database_name**|**sysname**|已經加入至可用性群組的資料庫名稱。|  
  
## <a name="permissions"></a>Permissions  
 如果呼叫端的**sys.availability_databases_cluster**不是資料庫、 最小權限，才能查看對應的資料列是 ALTER ANY DATABASE 或 VIEW ANY DATABASE 伺服器層級權限或建立的擁有者中的資料庫權限**主要**資料庫。  
  
## <a name="see-also"></a>另請參閱  
 [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.dm_hadr_database_replica_states &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)   
 [sys.dm_hadr_database_replica_cluster_states &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)   
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
