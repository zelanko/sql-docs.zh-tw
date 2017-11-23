---
title: "sys.dm_hadr_cluster_networks (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_hadr_cluster_networks
- sys.dm_hadr_cluster_networks_TSQL
- sys.dm_hadr_cluster_networks
- dm_hadr_cluster_networks_TSQL
dev_langs: TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_cluster_networks dynamic management view
ms.assetid: ece32b15-d63f-4f93-92b7-e2930333e97a
caps.latest.revision: "15"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 77d2eaee6ce6ac28370a2c825eece9ade0440df0
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmhadrclusternetworks-transact-sql"></a>sys.dm_hadr_cluster_networks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對參與可用性群組之子網路組態的每個 WSFC 叢集成員，各傳回一個資料列。 您可以使用此動態管理檢視來驗證為每個可用性複本所設定的網路虛擬 IP。  
  
 主索引鍵： **member_name** + **network_subnet_IP** + **network_subnet_prefix_length**  
  
 > [!TIP]
 > 從開始[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，這個動態管理檢視支援 Alwayson 容錯移轉叢集執行個體除了 Alwayson 可用性群組。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**member_name**|**nvarchar （128)**|WSFC 叢集中節點的電腦名稱。|  
|**network_subnet_ip**|**nvarchar(48)**|此電腦所屬之子網路的網路 IP 位址。 這可以是 IPv4 或 IPv6 位址。|  
|**network_subnet_ipv4_mask**|**nvarchar(45)**|網路的子網路遮罩，可指定此 IP 位址所屬的子網路。 **network_subnet_ipv4_mask**的 WITH DHCP 子句中指定 DHCP < network_subnet_option > 選項[CREATE AVAILABILITY GROUP](../../t-sql/statements/create-availability-group-transact-sql.md)或[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式。<br /><br /> NULL = IPv6 子網路。|  
||||  
|**network_subnet_prefix_length**|**int**|網路 IP 前置長度，可指定此電腦所屬的子網路。|  
|**is_public**|**bit**|網路在 WSFC 叢集上為公用或私用，可為下列其中一個值：<br /><br /> 0 = 私用<br /><br /> 1 = 公用|  
|**is_ipv4**|**bit**|子網路的類型，下列其中一個值：<br /><br /> 1 = IPv4<br /><br /> 0 = IPv6|  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="see-also"></a>請參閱＜  
 [容錯移轉叢集和 AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [監視可用性群組 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [sys.dm_os_cluster_nodes &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [查詢 SQL Server 系統目錄 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
