---
title: sys.availability_group_listener_ip_addresses (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- availability_group_listener_ip_addresses
- sys.availability_group_listener_ip_addresses
- availability_group_listener_ip_addresses_TSQL
- sys.availability_group_listener_ip_addresses_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], listeners
- sys.availability_group_listener_ip_addresses catalog view
ms.assetid: e515fa6b-1354-4110-9b70-ab2e6164c992
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 04266782711b0825e0766d9ea1edfd8f0d0ddce7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysavailabilitygrouplisteneripaddresses-transact-sql"></a>sys.availability_group_listener_ip_addresses (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回針對每個 IP 位址與任何 Alwayson 可用性群組接聽程式在 Windows Server 容錯移轉叢集 (WSFC) 叢集中相關聯的資料列。  
  
 主索引鍵： **listener_id** + **ip_address** + **ip_sub_mask**  
  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**listener_id**|**nvarchar(36)**|Windows Server 容錯移轉叢集 (WSFC) 叢集中的資源 GUID。|  
|**ip_address**|**nvarchar(48)**|可用性群組接聽程式之已設定的虛擬 IP 位址。 傳回單一 IPv4 或 IPv6 位址。|  
|**ip_subnet_mask**|**nvarchar(15)**|為 IPv4 位址設定的 IP 子網路遮罩 (如果有的話)，這是針對可用性群組接聽程式所設定。<br /><br /> NULL = IPv6 子網路|  
|**is_dhcp**|**bit**|IP 位址是否由 DHCP 設定，可為下列其中一個值：<br /><br /> 0 = IP 位址不是由 DHCP 設定。<br /><br /> 1 = IP 位址是由 DHCP 設定。|  
|**network_subnet_ip**|**nvarchar(48)**|網路的子網路 IP 位址，可指定此 IP 位址所屬的子網路。|  
|**network_subnet_prefix_length**|**int**|此 IP 位址所屬之子網路的網路子網路前置長度。|  
|**network_subnet_ipv4_mask**|**nvarchar(45)**|此 IP 位址所屬之子網路的網路子網路遮罩。 **network_subnet_ipv4_mask**的 WITH DHCP 子句中指定 DHCP < network_subnet_option > 選項[CREATE AVAILABILITY GROUP](../../t-sql/statements/create-availability-group-transact-sql.md)或[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式。<br /><br /> NULL = IPv6 子網路|  
|**狀態**|**tinyint**|WSFC 叢集中 IP 資源的 ONLINE/OFFLINE 狀態，可為下列其中一個值：<br /><br /> 1 = 線上。 IP 資源在線上。<br /><br /> 0 = 離線。 IP 資源離線。<br /><br /> 2 = 線上暫止。 IP 資源已離線，但是正在連線。<br /><br /> 3 = 失敗。 IP 資源已在連線，但卻失敗。|  
|**state_desc**|**nvarchar(60)**|描述**狀態**，下列其中一個的：<br /><br /> ONLINE<br /><br /> OFFLINE<br /><br /> ONLINE_PENDING<br /><br /> FAILED|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [查詢 SQL Server 系統目錄 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [目錄檢視 &#40;。TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
