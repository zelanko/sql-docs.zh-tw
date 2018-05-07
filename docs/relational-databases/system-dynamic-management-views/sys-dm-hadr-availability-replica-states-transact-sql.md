---
title: sys.dm_hadr_availability_replica_states (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 10/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_hadr_availability_replica_states
- sys.dm_hadr_availability_replica_states_TSQL
- sys.dm_hadr_availability_replica_states
- dm_hadr_availability_replica_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_availability_replica_states dynamic management view
ms.assetid: d2e678bb-51e8-4a61-b223-5c0b8d08b8b1
caps.latest.revision: 65
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: eeb949d9bdd664a942f75157296312cdf00d32b9
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmhadravailabilityreplicastates-transact-sql"></a>sys.dm_hadr_availability_replica_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回針對每個本機複本的資料列和每個遠端複本的資料列相同 Always On 可用性群組中當做本機複本。 每個資料列包含給定複本的狀態資訊。  
  
> [!IMPORTANT]  
>  若要取得有關給定的可用性群組中的每個複本的資訊，請查詢**sys.dm_hadr_availability_replica_states**裝載主要複本的伺服器執行個體。 在裝載可用性群組之次要複本的伺服器執行個體上查詢時，這個動態管理檢視只會傳回此可用性群組的本機資訊。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|複本的唯一識別碼。|  
|**group_id**|**uniqueidentifier**|可用性群組的唯一識別碼。|  
|**is_local**|**bit**|複本是否為本機，其中一個：<br /><br /> 0 = 表示可用性群組中的遠端次要複本，該群組的主要複本是由本機伺服器執行個體所裝載。 這個值只會出現在主要複本位置。<br /><br /> 1 = 表示本機複本。 在次要複本上，這是該複本所屬之可用性群組的唯一可用值。|  
|**角色**|**tinyint**|目前[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]的本機複本或連接的遠端複本，其中一個角色：<br /><br /> 0 = 正在解析<br /><br /> 1 = 主要<br /><br /> 2 = 次要<br /><br /> 如需 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 角色的詳細資訊，請參閱 [Always On 可用性群組概觀 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)。|  
|**role_desc**|**nvarchar(60)**|描述**角色**，下列其中一個的：<br /><br /> RESOLVING<br /><br /> PRIMARY<br /><br /> SECONDARY|  
|**operational_state**|**tinyint**|目前的複本，其中一個操作狀態：<br /><br /> 0 = 暫止容錯移轉<br /><br /> 1 = 暫止<br /><br /> 2 = 線上<br /><br /> 3 = 離線<br /><br /> 4 = 失敗<br /><br /> 5 = 失敗，無仲裁<br /><br /> NULL = 複本不是本機。<br /><br /> 如需詳細資訊，請參閱[角色和操作狀態](#RolesAndOperationalStates)稍後在本主題中。|  
|**operational\_state\_desc**|**nvarchar(60)**|描述**操作\_狀態**，下列其中一個的：<br /><br /> PENDING_FAILOVER<br /><br /> PENDING<br /><br /> ONLINE<br /><br /> OFFLINE<br /><br /> FAILED<br /><br /> FAILED_NO_QUORUM<br /><br /> NULL|  
|**復原\_健全狀況**|**tinyint**|彙總套件的**資料庫\_狀態**資料行[sys.dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)動態管理檢視。 以下是可能的值和它們的描述。<br /><br /> 0： 正在進行中。  至少一個聯結的資料庫的資料庫狀態不是 ONLINE (**資料庫\_狀態**是不是 0)。<br /><br /> 1： 線上。 所有聯結的資料庫都有 ONLINE 資料庫狀態 (**database_state**為 0)。<br /><br /> NULL: **is_local** = 0|  
|**recovery_health_desc**|**nvarchar(60)**|描述**recovery_health**，下列其中一個的：<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**同步處理\_健全狀況**|**tinyint**|會反映資料庫同步處理狀態的彙總 (**synchronization_state**) 所有聯結可用性資料庫 (也稱為*複本*) 和複本 （的可用性模式同步認可或非同步認可模式）。 彙總套件會反映最不健康的累積的狀態之資料庫複本上。 以下是可能的值和其說明。<br /><br /> 0： 非狀況良好。   至少有一個聯結資料庫處於 NOT SYNCHRONIZING 狀態下。<br /><br /> 1： 部分狀況良好。 某些複本未處於目標同步處理狀態：同步認可複本應該已同步處理，而非同步認可複本應該正在同步處理。<br /><br /> 2： 狀況良好。 所有複本都處於目標同步處理狀態：同步認可複本已同步處理，而非同步認可複本正在同步處理。|  
|**synchronization_health_desc**|**nvarchar(60)**|描述**synchronization_health**，下列其中一個的：<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
|**connected_state**|**tinyint**|次要複本目前是否連接到主要複本。 可能的值如下所示使用它們的描述。<br /><br /> 0： 中斷連接。 可用性複本對 DISCONNECTED 狀態的回應取決於其角色： 主要複本，如果次要複本已中斷連接，次要資料庫會標示為 NOT SYNCHRONIZED 在主要複本會等候次要重新連線。次要複本上，一旦偵測到它已中斷連接，次要複本會嘗試重新連接到主要複本。<br /><br /> 1： 連接。<br /><br /> 每個主要複本都會針對相同可用性群組中的每一個次要複本來追蹤連接狀態。 次要複本只會追蹤主要複本的連接狀態。|  
|**connected_state_desc**|**nvarchar(60)**|描述**connection_state**，下列其中一個的：<br /><br /> DISCONNECTED<br /><br /> CONNECTED|  
|**last_connect_error_number**|**int**|上次連接錯誤的號碼。|  
|**last_connect_error_description**|**nvarchar(1024)**|文字**last_connect_error_number**訊息。|  
|**last_connect_error_timestamp**|**datetime**|日期和時間戳記，指出當**last_connect_error_number**時發生錯誤。|  
  
##  <a name="RolesAndOperationalStates"></a> 角色和操作狀態  
 角色、**角色**，會反映給定的可用性複本的狀態和操作狀態， **operational_state**，描述此複本是否已準備就緒可以處理所有的用戶端要求可用性複本的資料庫。 下列是可能使用的每個角色的操作狀態的摘要： 解析、 主要和次要。  
  
 **正在解析：** RESOLVING 角色中的可用性複本時，可能的操作狀態是下表所示。  
  
|操作狀態|Description|  
|-----------------------|-----------------|  
|PENDING_FAILOVER|正在針對可用性群組處理容錯移轉命令。|  
|OFFLINE|可用性複本的所有組態資料都已經在 WSFC 叢集和本機中繼資料中更新，但是可用性群組目前缺少主要複本。|  
|FAILED|嘗試從 WSFC 叢集中擷取資訊時發生讀取失敗。|  
|FAILED_NO_QUORUM|本機 WSFC 節點沒有仲裁。 這是推斷的狀態。|  
  
 **PRIMARY:** 當可用性複本正在扮演主要角色時，它目前是主要複本。 可能的操作狀態會在下表所示。  
  
|操作狀態|Description|  
|-----------------------|-----------------|  
|PENDING|這是暫時性狀態，但是如果沒有工作者可處理要求，則主要複本可能會陷在這個狀態中。|  
|ONLINE|可用性群組資源在線上，而且所有資料庫工作者執行緒都已收取。|  
|FAILED|可用性複本無法從 WSFC 叢集讀取及/或將資料寫入其中。|  
  
 **次要資料庫：**當可用性複本執行次要角色時，它目前是次要複本。 可能的操作狀態會在下表中所示。  
  
|操作狀態|Description|  
|-----------------------|-----------------|  
|ONLINE|本機次要複本已連接到主要複本。|  
|FAILED|本機次要複本無法從 WSFC 叢集讀取及/或將資料寫入其中。|  
|NULL|在主要複本上，當資料列與次要複本有關時就會傳回這個值。|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [監視可用性群組 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
