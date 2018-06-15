---
title: sys.availability_groups_cluster (TRANSACT-SQL) |Microsoft 文件
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
- sys.availability_groups_cluster
- availability_groups_cluster
- availability_groups_cluster_TSQL
- sys.availability_groups_cluster_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_groups_cluster catalog view
- Availability Groups [SQL Server], WSFC clusters
ms.assetid: d0f4683f-cdf0-4227-8b68-720ffe58f158
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6ffcb675b106536741a9edd298296485773a3ac1
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33182104"
---
# <a name="sysavailabilitygroupscluster-transact-sql"></a>sys.availability_groups_cluster (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回每個 Alwayson 可用性群組的資料列在 Windows Server 容錯移轉叢集 (WSFC)。 每個資料列都包含 WSFC 叢集中的可用性群組中繼資料。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|可用性群組的唯一識別碼 (GUID)。|  
|**name**|**sysname**|可用性群組的名稱。 這是使用者指定的名稱，它在 Windows Server 容錯移轉叢集 (WSFC) 內必須是唯一的。|  
|**resource_id**|**nvarchar(40)**|WSFC 叢集資源的資源識別碼。|  
|**resource_group_id**|**nvarchar(40)**|可用性群組之 WSFC 叢集資源群組的資源群組識別碼。|  
|**failure_condition_level**|**int**|觸發自動容錯移轉所必須根據的使用者定義失敗狀況層級，可為下列其中一個整數值：<br /><br /> 1： 指定應該起始自動容錯移轉發生下列任一項時： <br />-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務已關閉。<br />-由於伺服器執行個體不收到任何通知用於連接到 WSFC 容錯移轉叢集的可用性群組租用已到期。 如需詳細資訊，請參閱 [How It Works: SQL Server Always On Lease Timeout](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx)(運作方式：SQL Server AlwaysOn 租用逾時)。<br /><br /> 2： 指定應該起始自動容錯移轉發生下列任一項時：  <br />-執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不會連線到叢集，以及使用者指定**health_check_timeout**超過臨界值的可用性群組。 <br />-可用性複本處於失敗狀態。 <br />3： 指定應該在嚴重時起始自動容錯移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]內部錯誤，例如遺棄、 嚴重的寫入存取違規或是傾印過多。 這是預設值。 <br />4： 指定應在 「 中 」 時起始自動容錯移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]內部錯誤，例如持續發生記憶體不足的狀況[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]內部資源集區。<br />5： 指定應在包括任何合格的失敗狀況時起始自動容錯移轉：<br />-SQL 引擎工作者執行緒已耗盡。 <br />-無法解決的死結偵測。<br /><br /> 失敗狀況層級 (1–5) 的範圍從最低限制 (層級 1) 到最高限制 (層級 5)。 給定的狀況層級包含所有較少限制的層級。 因此，最嚴格的狀況層級 5 包含四個較少限制的狀況層級 (1-4)，層級 4 則包含層級 1-3，依此類推。<br /><br /> 若要變更此值，請使用 FAILURE_CONDITION_LEVEL 選項[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式。|  
|**health_check_timeout**|**int**|等候時間 （以毫秒為單位） [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)系統預存程序假設伺服器執行個體很慢或無回應之前，傳回伺服器健全狀況資訊。 預設值為 30000 毫秒 (30 秒)。<br /><br /> 若要變更此值，使用的 HEALTH_CHECK_TIMEOUT 選項[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式。|  
|**automated_backup_preference**|**tinyint**|針對此可用性群組中的可用性資料庫執行備份的慣用位置。 為下列其中一個值：<br /><br /> 0： 主要。 備份一定要在主要複本上進行。<br />1： 只在次要資料庫。 偏好針對次要複本執行備份。<br />2： 慣用次要。 偏好針對次要複本執行備份，但是如果沒有次要複本可用來執行備份作業，可以接受針對主要複本執行備份。 這是預設行為。<br />3： 任何複本。 針對主要複本或次要複本執行備份沒有任何偏好。<br /><br /> 如需詳細資訊，請參閱 [使用中次要：在次要複本上備份 &#40;AlwaysOn 可用性群組&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)。|  
|**automated_backup_preference_desc**|**nvarchar(60)**|描述**automated_backup_preference**，下列其中一個的：<br /><br /> PRIMARY<br /><br /> SECONDARY_ONLY<br /><br /> SECONDARY<br /><br /> 無|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 需要伺服器執行個體的 VIEW ANY DEFINITION 權限。  
  
## <a name="see-also"></a>另請參閱  
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [監視可用性群組 & #40;TRANSACT-SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [監視可用性群組 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
