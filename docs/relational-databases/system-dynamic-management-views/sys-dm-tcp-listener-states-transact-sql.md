---
title: "sys.dm_tcp_listener_states (TRANSACT-SQL) |Microsoft 文件"
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
- sys.dm_tcp_listener_states
- dm_tcp_listener_states
- sys.dm_tcp_listener_states_TSQL
- dm_tcp_listener_states_TSQL
dev_langs: TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], listeners
- sys.dm_tcp_listener_states dynamic management view
ms.assetid: 9997ffed-a4c1-428f-8bac-3b9e4b16d7cf
caps.latest.revision: "15"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d111ae8b610ca54516181fa6cfd6492b45d23211
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmtcplistenerstates-transact-sql"></a>sys.dm_tcp_listener_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對每個 TCP 接聽程式傳回一個包含動態狀態資訊的資料列。  
  
> [!NOTE]
> 可用性群組接聽程式可能會接聽與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的接聽程式相同的通訊埠。 在此情況下，接聽程式會個別列出，與 Service Broker 接聽程式一樣。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**listener_id**|**int**|接聽程式的內部識別碼。 不可為 Null。<br /><br /> 主索引鍵。|  
|**ip_address**|**nvarchar48**|目前在線上而且正在接聽的接聽程式 IP 位址。 允許 IPv4 和 IPv6。 如果接聽程式擁有這兩種位址，則會個別列出。 IPv4 萬用字元會顯示為 “0.0.0.0”。 IPv6 萬用字元會顯示為 “::”。<br /><br /> 不可為 Null。|  
|**is_ipv4**|**bit**|IP 位址的類型<br /><br /> 1 = IPv4<br /><br /> 0 = IPv6|  
|**port**|**int**|接聽程式正在接聽的通訊埠編號。 不可為 Null。|  
|**型別**|**tinyint**|接聽程式類型，下列其中一個值：<br /><br /> 0 = [!INCLUDE[tsql](../../includes/tsql-md.md)]<br /><br /> 1 = Service Broker<br /><br /> 2 = 資料庫鏡像<br /><br /> 不可為 Null。|  
|**type_desc**|**nvarchar （20)**|描述**類型**，下列其中一個的：<br /><br /> TSQL<br /><br /> SERVICE_BROKER<br /><br /> DATABASE_MIRRORING<br /><br /> 不可為 Null。|  
|**狀態**|**tinyint**|可用性群組接聽程式的狀態，可為下列其中一個值：<br /><br /> 1 = 線上。 接聽程式正在接聽和處理要求。<br /><br /> 2 = 暫止重新啟動。 接聽程式離線，暫止重新啟動。<br /><br /> 如果可用性群組接聽程式正在接聽與伺服器執行個體相同的通訊埠，這兩個接聽程式一定會擁有相同的狀態。<br /><br /> 不可為 Null。<br /><br /> 注意： 此資料行中的值來自 TSD_listener 物件。 資料行不支援離線狀態，因為 TDS_listener 離線時，無法查詢狀態。|  
|**state_desc**|**nvarchar(16)**|描述**狀態**，下列其中一個的：<br /><br /> ONLINE<br /><br /> PENDING_RESTART<br /><br /> 不可為 Null。|  
|**start_time**|**datetime**|指出何時已啟動接聽程式的時間戳記。 不可為 Null。|  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="see-also"></a>請參閱＜  
 [查詢 SQL Server 系統目錄 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [AlwaysOn 可用性群組目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Always On 可用性群組動態管理檢視和函數 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)  
  
  
