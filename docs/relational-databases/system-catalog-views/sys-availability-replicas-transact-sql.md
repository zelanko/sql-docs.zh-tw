---
title: sys.availability_replicas (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 10/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- availability_replicas_TSQL
- availability_replicas
- sys.availability_replicas
- sys.availability_replicas_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_replicas catalog view
ms.assetid: 0a06e9b6-a1e4-4293-867b-5c3f5a8ff62c
caps.latest.revision: 62
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 215db72fe7432ab1d35a1bb4ca0ae63f28768f7c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sysavailabilityreplicas-transact-sql"></a>sys.availability_replicas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

每個屬於任何 Alwayson 可用性群組在 WSFC 容錯移轉叢集中的可用性複本傳回一個資料列。  
  
如果本機伺服器執行個體無法與 WSFC 容錯移轉叢集聯繫，例如由於叢集已關閉或仲裁已遺失，則只會傳回本機可用性複本的資料列。 這些資料列只會包含在本機快取於中繼資料內的資料行。  
  
 
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|複本的唯一識別碼。|  
|**group_id**|**uniqueidentifier**|複本所屬之可用性群組的唯一識別碼。|  
|**replica_metadata_id**|**int**|Database Engine 中可用性複本之本機中繼資料物件的識別碼。|  
|**replica_server_name**|**nvarchar(256)**|裝載這個複本之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的伺服器名稱，如果是非預設執行個體，則是它的執行個體名稱。|  
|**owner_sid**|**varbinary(85)**|針對這個可用性複本的外部擁有者，註冊給這個伺服器執行個體的安全性識別碼 (SID)。<br /><br /> 非本機可用性複本為 NULL。|  
|**endpoint_url**|**nvarchar(128)**|使用者指定之資料庫鏡像端點的字串表示法，該端點是由主要與次要複本之間的資料同步處理連接所使用。 如需這些端點 URL 語法的相關資訊，請參閱[在加入或修改可用性複本時指定端點 URL &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)。<br /><br /> NULL = 無法聯繫 WSFC 容錯移轉叢集。<br /><br /> 若要變更這個端點，請使用 ENDPOINT_URL 選項[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式。|  
|**availability_mode**|**tinyint**|複本的可用性模式，下列其中一項：<br /><br /> 0&#124;非同步認可。 主要複本可認可交易，而不需要等候次要複本將記錄寫入磁碟中。<br /><br /> 1&#124;同步認可。 主要複本會等候認可給定交易，直到次要複本將交易寫入磁碟為止。<br /><br />4&#124;只能的組態。 主要複本的可用性群組的組態中繼資料到複本會同步傳送。 使用者資料不會傳輸到複本。 在 SQL Server 2017 CU1 和更新版本可用。<br /><br /> 如需詳細資訊，請參閱 [可用性模式 &#40;AlwaysOn 可用性群組&#41;](../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)或 PowerShell，針對 AlwaysOn 可用性群組執行規劃的手動容錯移轉或強制手動容錯移轉 (強制容錯移轉)。|  
|**availability_mode_desc**|**nvarchar(60)**|描述**可用性\_模式**，下列其中一個的：<br /><br /> 非同步\_認可<br /><br /> 同步\_認可<br /><br /> 組態\_僅限<br /><br /> 若要變更可用性複本的可用性模式，請使用 AVAILABILITY_MODE 選項[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式。<br/><br>您無法變更複本的可用性模式組態\_僅限。 您無法變更組態\_只到次要或主要複本的複本。 |  
|**容錯移轉\_模式**|**tinyint**|[容錯移轉模式](../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)可用性複本，其中一個：<br /><br /> 0&#124;手動容錯移轉。 如果容錯移轉到次要複本的程序設定為手動容錯移轉，則必須由資料庫管理員手動起始。 執行的容錯移轉類型將取決於次要複本是否同步處理，如下所示：<br /><br /> 如果可用性複本並未同步處理或者依然在同步處理，只會發生強制容錯移轉 (可能會遺失資料)。<br /><br /> 如果設定為同步認可可用性模式 (**可用性\_模式**= 1)，可用性複本目前已同步處理、 手動容錯移轉不可能發生資料遺失。<br /><br /> 1&#124;自動容錯移轉。 此複本可能是自動容錯移轉的目標。  可用性模式設定為同步認可時，才支援自動容錯移轉 (**可用性\_模式**= 1) 和可用性複本目前同步處理。<br /><br /> 若要檢視可用性複本的每個可用性資料庫的資料庫同步處理健全狀況彙總，使用**同步\_健全狀況**和**同步\_健全狀況\_desc**的資料行[sys.dm_hadr_availability_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md)動態管理檢視。 此積存會考量每個可用性資料庫的同步處理狀態及其可用性複本的可用性模式。<br /><br /> **注意：**若要檢視給定的可用性資料庫的同步處理健全狀況，請查詢**同步\_狀態**和**同步\_健全狀況**資料行的[sys.dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)動態管理檢視。|  
|**容錯移轉\_模式\_desc**|**nvarchar(60)**|描述**容錯移轉\_模式**，下列其中一個的：<br /><br /> MANUAL<br /><br /> AUTOMATIC<br /><br /> 若要變更的容錯移轉模式，請使用 容錯移轉\_模式選項的[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式。|  
|**session\_timeout**|**int**|逾時期間 (以秒為單位)。 逾時期間是將主要複本與次要複本之間的連接視為失敗之前，複本等待接收另一個複本之訊息的時間上限。 工作階段逾時會偵測次要複本是否連接到主要複本。<br /><br /> 一旦偵測到失敗的連線，而且次要複本，主要複本會將次要複本不能\_已同步處理。 一旦偵測到與主要複本之間的連接失敗時，次要複本只會嘗試重新連接。<br /><br /> **注意：**工作階段逾時並不會造成自動容錯移轉。<br /><br /> 若要變更此值，請使用 SESSION_TIMEOUT 選項[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式。|  
|**主要\_角色\_允許\_連線**|**tinyint**|可用性允許所有連接還是只允許讀寫連接，下列其中一項：<br /><br /> 2 = 所有連接 (預設值)<br /><br /> 3 = 讀寫連接|  
|**primary\_role\_allow\_connections\_desc**|**nvarchar(60)**|描述**主要\_角色\_允許\_連線**，下列其中一個的：<br /><br /> ALL<br /><br /> 讀取\_寫入|  
|**次要\_角色\_允許\_連線**|**tinyint**|執行次要角色的可用性複本 (也就是次要複本) 是否可接受來自用戶端的連接，下列其中一個值：<br /><br /> 0 = 否。 不允許連接次要複本的資料庫，這些資料庫也不可用於讀取存取。 這是預設值。<br /><br /> 1 = 唯讀。 只允許與次要複本的資料庫進行唯讀連接。 可讀取複本中的所有資料庫。<br /><br /> 2 = 全部。 次要複本的資料庫允許所有連接進行唯讀存取。<br /><br /> 如需詳細資訊，請參閱 [使用中次要：可讀取的次要複本 &#40;AlwaysOn 可用性群組&#41;](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)中心概念。|  
|**secondary_role_allow_connections_desc**|**nvarchar(60)**|描述**secondary_role_allow_connections**，下列其中一個的：<br /><br /> 否<br /><br /> READ_ONLY<br /><br /> ALL|  
|**create_date**|**datetime**|建立複本的日期。<br /><br /> NULL = 複本不在這個伺服器執行個體上。|  
|**modify_date**|**datetime**|上次修改複本的日期。<br /><br /> NULL = 複本不在這個伺服器執行個體上。|  
|**backup_priority**|**int**|表示使用者為了在這個複本上執行備份所指定的優先權 (相對於相同可用性群組中的其他複本)。 這個值是 0 到 100 範圍之間的整數。<br /><br /> 如需詳細資訊，請參閱 [使用中次要：在次要複本上備份 &#40;AlwaysOn 可用性群組&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)。|  
|**read_only_routing_url**|**nvarchar(256)**|唯讀可用性複本的連接端點 (URL)。 如需詳細資訊，請參閱[設定可用性群組的唯讀路由 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)。|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 需要伺服器執行個體的 VIEW ANY DEFINITION 權限。  
  
## <a name="see-also"></a>另請參閱  
 [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [監視可用性群組 & #40;TRANSACT-SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [監視可用性群組 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
