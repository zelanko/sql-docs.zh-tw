---
title: "AlwaysOn 用戶端連接 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- Availability Groups [SQL Server], prerequisites and restrictions
- Availability Groups [SQL Server], client connectivity
ms.assetid: b456448d-1757-48c8-8bbb-2d1c2d6d61e9
caps.latest.revision: 22
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3cc7edad792e454ba3008ae53f4ae934be529ea6
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="always-on-client-connectivity-sql-server"></a>AlwaysOn 用戶端連接性 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主題描述 AlwaysOn 可用性群組之用戶端連接的考量，包括用戶端組態和設定的必要條件、限制和建議。  
  
 **本主題內容：**  
  
-   [用戶端連接性支援](#ClientConnSupport)  
  
-   [相關工作](#RelatedTasks)  
  
##  <a name="ClientConnSupport"></a> 用戶端連接性支援  
 底下章節提供有關 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 支援用戶端連接性的資訊。  
  
 **驅動程式支援**  
  
 下表摘要說明 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]的驅動程式支援：  
  
|驅動程式|多重子網路容錯移轉|應用程式的意圖|唯讀路由|多重子網路容錯移轉：快速單一子網路端點容錯移轉|多重子網路容錯移轉：SQL 叢集執行個體的具名執行個體解析|  
|------------|----------------------------|------------------------|------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------|  
|SQL Native Client 11.0 ODBC|是|是|是|是|是|  
|SQL Native Client 11.0 OLEDB|否|是|是|否|否|  
|具有連接修補程式的 ADO.NET 與 .NET Framework 4.0*|是|是|是|是|是|  
|具有連接修補程式的 ADO.NET 與 .NET Framework 3.5 SP1**|是|是|是|是|是|  
|Microsoft JDBC Driver 4.0 for SQL Server|是|是|是|是|是|  
  
 *下載 ADO.NET 與 .NET Framework 4.0 連接修補程式： [http://support.microsoft.com/kb/2600211](http://support.microsoft.com/kb/2600211)。  
  
 *下載 ADO.NET 與 .NET Framework 3.5 SP1 連接修補程式： [http://support.microsoft.com/kb/2654347](http://support.microsoft.com/kb/2654347)。  
  
> [!IMPORTANT]  
>  若要連接到可用性群組接聽程式，用戶端必須使用 TCP 連接字串。  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [建立及設定可用性群組 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [建立或設定可用性群組接聽程式 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [容錯移轉叢集和 AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性群組的必要條件、限制和建議 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [可用性群組接聽程式、用戶端連線及應用程式容錯移轉 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [關於可用性複本的用戶端連線存取 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)   
 [Microsoft SQL Server AlwaysOn 高可用性和災害復原解決方案指南](http://go.microsoft.com/fwlink/?LinkId=227600)   
 [SQL Server AlwaysOn Team Blog: The official SQL Server AlwaysOn Team Blog](https://blogs.msdn.microsoft.com/sqlalwayson/) (SQL Server AlwaysOn 團隊部落格：官方 SQL Server AlwaysOn 團隊部落格)   
 [當您從執行 Windows Server 2003、Windows Vista、Windows Server 2008、Windows 7 或 Windows Server 2008 R2 的電腦重新連接 IPSec 連接時發生長時間延遲](http://support.microsoft.com/kb/980915)   
 [叢集服務大約需要 30 秒來容錯移轉 Windows Server 2008 R2 中的 IPv6 IP 位址](http://support.microsoft.com/kb/2578113)   
 [如果叢集與應用程式伺服器之間不存在任何路由器，就會緩慢地進行容錯移轉作業](http://support.microsoft.com/kb/2582281)  
  
  

