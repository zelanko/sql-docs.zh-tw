---
title: sys.availability_group_listeners (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- availability_group_listeners_TSQL
- sys.availability_group_listeners
- sys.availability_group_listeners_TSQL
- availability_group_listeners
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_group_listeners catalog view
- Availability Groups [SQL Server], listeners
ms.assetid: b5e7d1fb-3ffb-4767-8135-604c575016b1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 839e471e8861f081762f6129dff731e66bed77a7
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52403483"
---
# <a name="sysavailabilitygrouplisteners-transact-sql"></a>sys.availability_group_listeners (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對每個 Always On 可用性群組，傳回表示沒有網路名稱與可用性群組相關聯，或傳回一個資料列，每個可用性群組接聽程式組態中 Windows Server 容錯移轉叢集 (WSFC) 可能是零個資料列叢集。 此檢視會顯示從叢集蒐集的即時組態。  
  
> [!NOTE]  
>  此目錄檢視不會描述 WSFC 叢集中所定義之 IP 組態的詳細資料。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|可用性群組識別碼 (**group_id**) 從[sys.availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)。|  
|**listener_id**|**nvarchar(36)**|叢集資源識別碼中的 GUID。|  
|**dns_name**|**nvarchar(63)**|可用性群組接聽程式的已設定網路名稱 (主機名稱)。|  
|**port**|**int**|為可用性群組接聽程式設定的 TCP 通訊埠編號。<br /><br /> NULL = 接聽程式已在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 外面設定，而且其通訊埠編號尚未加入至可用性群組。 修改的 LISTENER 選項加入的連接埠，listener [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式。|  
|**is_conformant**|**bit**|此 IP 組態是否符合標準，可為下列其中一個值：<br /><br /> 1 = 接聽程式符合標準。 只有"OR"關聯性中不存在其網際網路通訊協定 (IP) 位址。 *符合標準*包含每個所建立的 IP 組態[CREATE AVAILABILITY GROUP](../../t-sql/statements/create-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式。 此外，如果已在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 外面建立 IP 組態 (例如，藉由使用 WSFC 容錯移轉叢集管理員)，但是可由 ALTER AVAILABILITY GROUP tsql 陳述式加以修改，則表示 IP 組態符合標準。<br /><br /> 0 = 接聽程式不符合標準。 一般來說，這表示 IP 位址無法使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 命令加以設定，但是已直接在 WSFC 叢集中定義。|  
|**ip_configuration_string_from_cluster**|**nvarchar(max)**|此接聽程式的叢集 IP 組態字串 (如果有的話)。 NULL = 接聽程式沒有虛擬 IP 位址。 例如：<br /><br /> IPv4 位址：`65.55.39.10`。<br /><br /> IPv6 位址：`2001::4898:23:1002:20f:1fff:feff:b3a3`|  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組動態管理檢視和函式 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 可用性群組目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [監視可用性群組 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
