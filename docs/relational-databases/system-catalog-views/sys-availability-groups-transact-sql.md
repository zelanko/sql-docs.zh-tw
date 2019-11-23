---
title: sys.databases availability_groups （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.availability_groups_TSQL
- availability_groups_TSQL
- sys.availability_groups
- availability_groups
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_groups catalog view
ms.assetid: da7fa55f-c008-45d9-bcfc-3513b02d9e71
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ca82c64d2d0269564567de175b9d6f778f76d4d7
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874263"
---
# <a name="sysavailability_groups-transact-sql"></a>sys.availability_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對裝載可用性複本的 SQL Server 主機本機執行個體的每一個可用性群組，各傳回一個資料列。 每一個資料列都包含可用性群組中繼資料的快取副本。  
   
|資料行名稱|[名稱]|描述|  
|-----------------|---------------|-----------------|  
|**group_id**|**ssNoversion**|可用性群組的唯一識別碼 (GUID)。|  
|**name**|**sysname**|可用性群組的名稱。 這是使用者指定的名稱，它在 Windows Server 容錯移轉叢集 (WSFC) 內必須是唯一的。|  
|**resource_id**|**nvarchar(40)**|WSFC 叢集資源的資源識別碼。|  
|**resource_group_id**|**nvarchar(40)**|可用性群組之 WSFC 叢集資源群組的資源群組識別碼。|  
|**failure_condition_level**|**int**|使用者定義的失敗狀況層級，在此情況下，必須觸發自動容錯移轉，這是此資料表正下方之表格中所顯示的其中一個整數值。<br /><br /> 失敗狀況層級 (1-5) 的範圍從最低限制 (層級 1) 到最高限制 (層級 5)。 給定的狀況層級包含所有較少限制的層級。 因此，最嚴格的狀況層級 5 包含四個較少限制的狀況層級 (1-4)，層級 4 則包含層級 1-3，依此類推。<br /><br /> 若要變更此值，請使用[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 語句的 FAILURE_CONDITION_LEVEL 選項。|  
|**health_check_timeout**|**int**|[Sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)系統預存程式傳回伺服器健全狀況資訊的等候時間（以毫秒為單位），在假設伺服器實例變慢或沒有回應之前。 預設值為 30000 毫秒 (30 秒)。<br /><br /> 若要變更此值，請使用[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 語句的 HEALTH_CHECK_TIMEOUT 選項。|  
|**automated_backup_preference**|**tinyint**|針對此可用性群組中的可用性資料庫執行備份的慣用位置。 以下是可能的值及其描述。<br /><br /> <br /><br /> 0：主要。 備份一定要在主要複本上進行。<br /><br /> 1：僅限次要。 偏好針對次要複本執行備份。<br /><br /> 2：偏好次要。 偏好針對次要複本執行備份，但是如果沒有次要複本可用來執行備份作業，可以接受針對主要複本執行備份。 這是預設行為。<br /><br /> 3：任何複本。 針對主要複本或次要複本執行備份沒有任何偏好。<br /><br /> <br /><br /> 如需詳細資訊，請參閱 [使用中次要：在次要複本上備份 &#40;AlwaysOn 可用性群組&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)。|  
|**automated_backup_preference_desc**|**nvarchar(60)**|**Automated_backup_preference**的描述，下列其中一個：<br /><br /> PRIMARY<br /><br /> SECONDARY_ONLY<br /><br /> SECONDARY<br /><br /> NONE|  
|**version**|**smallint**|儲存在 Windows 容錯移轉叢集中的可用性群組中繼資料版本。 新增功能時，此版本號碼會遞增。|  
|**basic_features**|**bit**|指定這是否為基本可用性群組。 如需詳細資訊，請參閱[基本可用性群組 &#40;AlwaysOn 可用性群組&#41;](../../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md)。|  
|**dtc_support**|**bit**|指定是否已啟用此可用性群組的 DTC 支援。 [**建立可用性群組**] 的 [ **DTC_SUPPORT** ] 選項會控制此設定。|  
|**db_failover**|**bit**|指定可用性群組是否支援資料庫健康情況的容錯移轉。 [**建立可用性群組**] 的 [ **DB_FAILOVER** ] 選項會控制此設定。|  
|**is_distributed**|**bit**|指定這是否為分散式可用性群組。 如需詳細資訊，請參閱[分散式可用性群組 &#40;AlwaysOn 可用性群組&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)。|  
  
## <a name="failure-condition-level--values"></a>失敗狀況層級值  
 下表描述**failure_condition_level**資料行可能的失敗狀況層級。  
  
|ReplTest1|失敗狀況|  
|-----------|-----------------------|  
|1|指定在發生以下任何情況時應該起始自動容錯移轉：<br /><br /> <br /><br /> -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務已關閉。<br /><br /> -用來連接到 WSFC 容錯移轉叢集的可用性群組租用已過期，因為沒有從伺服器實例收到 ACK。 如需詳細資訊，請參閱 [How It Works: SQL Server Always On Lease Timeout](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx)(運作方式：SQL Server AlwaysOn 租用逾時)。|  
|2|指定在發生以下任何情況時應該起始自動容錯移轉：<br /><br /> <br /><br /> -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的實例未連接到叢集，而且已超過可用性群組的使用者指定**health_check_timeout**臨界值。<br /><br /> -可用性複本處於失敗狀態。|  
|3|指定應該在嚴重 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部錯誤發生時起始自動容錯移轉，例如執行緒同步鎖定遭到遺棄、嚴重的寫入存取違規或是傾印過多。<br /><br /> 這是預設值。|  
|4|指定應該在發生中度 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部錯誤時起始自動容錯移轉，例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部資源集區中持續的記憶體不足狀況。|  
|5|指定應該在發生任何符合的失敗狀況時起始自動容錯移轉，這些狀況包括：<br /><br /> <br /><br /> -已耗盡 SQL 引擎背景工作執行緒。<br /><br /> -偵測死結的鎖死。|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 需要伺服器執行個體的 VIEW ANY DEFINITION 權限。  
  
## <a name="see-also"></a>另請參閱  
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [監視可用性群組 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [監視可用性群組 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
