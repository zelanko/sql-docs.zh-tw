---
title: sys.databases availability_databases_cluster （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2c36c1574ae1ad289c9980e1df9bfbe3b241e164
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829148"
---
# <a name="sysavailability_databases_cluster-transact-sql"></a>sys.availability_databases_cluster (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 裝載 Windows Server 容錯移轉叢集（WSFC）叢集中任何 Always On 可用性群組之可用性複本的實例上的每個可用性資料庫，各包含一個資料列，無論本機複製資料庫是否已經聯結至可用性群組。  
  
> [!NOTE]  
>  當資料庫加入至可用性群組時，主要資料庫會自動聯結至此群組。 次要資料庫必須先在每個次要複本上備妥，然後才能聯結至可用性群組。   
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|可用性群組的唯一識別碼，資料庫會參與此可用性群組 (如果有的話)。<br /><br /> NULL = 資料庫不是可用性群組中可用性複本的一部分。|  
|**group_database_id**|**uniqueidentifier**|資料庫參與之可用性群組 (如果有的話) 內資料庫的唯一識別碼。 對於主要複本上的這個資料庫和資料庫已加入可用性群組的每個次要複本而言， **group_database_id**都相同。<br /><br /> NULL = 資料庫不是任何可用性群組中可用性複本的一部分。|  
|**database_name**|**sysname**|已經加入至可用性群組的資料庫名稱。|  
  
## <a name="permissions"></a>權限  
 如果**availability_databases_cluster sys.databases**的呼叫端不是資料庫的擁有者，則查看對應資料列所需的最小許可權是 ALTER any DATABASE 或 VIEW any database 伺服器層級許可權，或是**master**資料庫中的 CREATE database 許可權。  
  
## <a name="see-also"></a>另請參閱  
 [availability_groups &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [dm_hadr_database_replica_states &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)   
 [dm_hadr_database_replica_cluster_states &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)   
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
