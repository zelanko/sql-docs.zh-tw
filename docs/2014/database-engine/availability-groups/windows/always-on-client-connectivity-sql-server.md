---
title: AlwaysOn 用戶端連接 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- Availability Groups [SQL Server], prerequisites and restrictions
- Availability Groups [SQL Server], client connectivity
ms.assetid: b456448d-1757-48c8-8bbb-2d1c2d6d61e9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 446a0f709c35028efd5a39b347919b1e0b40b4b4
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937176"
---
# <a name="always-on-client-connectivity-sql-server"></a>AlwaysOn 用戶端連接性 (SQL Server)
  本主題描述 AlwaysOn 可用性群組之用戶端連接的考量，包括用戶端組態和設定的必要條件、限制和建議。  
  
 
  
##  <a name="client-connectivity-support"></a><a name="ClientConnSupport"></a>用戶端連線性支援  
 底下章節提供有關 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 支援用戶端連接性的資訊。  
  
 **驅動程式支援**  
  
 下表摘要說明 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]的驅動程式支援：  
  
|驅動程式|多重子網路容錯移轉|應用程式的意圖|唯讀路由|多重子網路容錯移轉：快速單一子網路端點容錯移轉|多重子網路容錯移轉：SQL 叢集執行個體的具名執行個體解析|  
|------------|----------------------------|------------------------|------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------|  
|SQL Native Client 11.0 ODBC|是|是|是|是|是|  
|SQL Native Client 11.0 OLEDB|否|是|是|否|否|  
|具有連接修補程式的 .NET Framework 4.0 ADO.NET**<sup>*</sup>** |是|是|是|是|是|  
|具有連接修補程式的 .NET Framework 3.5 SP1 ADO.NET**<sup>**</sup>** |是|是|是|是|是|  
|Microsoft JDBC Driver 4.0 for SQL Server|是|是|是|是|是|  
  
 **<sup>*</sup>** 下載 ADO .NET 的連線修補程式，.NET Framework 4.0： [https://support.microsoft.com/kb/2600211](https://support.microsoft.com/kb/2600211) 。  
  
 **<sup>**</sup>* * 下載 ADO.NET 與 .NET Framework 3.5 SP1 的連線修補程式： [https://support.microsoft.com/kb/2654347](https://support.microsoft.com/kb/2654347) 。  
  
> [!IMPORTANT]  
>  若要連接到可用性群組接聽程式，用戶端必須使用 TCP 連接字串。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
  
-   [建立及設定可用性群組 &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [建立或設定可用性群組接聽程式 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  

  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [容錯移轉叢集和 AlwaysOn 可用性群組 &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server 的必要條件、限制和建議&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [可用性群組接聽程式、用戶端連接性及應用程式容錯移轉 &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [關於可用性複本的用戶端連線存取 &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)   
 [適用于高可用性和嚴重損壞修復的 Microsoft SQL Server AlwaysOn 解決方案指南](https://go.microsoft.com/fwlink/?LinkId=227600)   
 [SQL Server AlwaysOn 小組 Blog：官方 SQL Server AlwaysOn 小組的 Blog](https://blogs.msdn.com/b/sqlalwayson/)   
 [當您從執行 Windows Server 2003、Windows Vista、Windows Server 2008、Windows 7 或 Windows Server 2008 R2 的電腦重新連接 IPSec 連線時發生長時間延遲](https://support.microsoft.com/kb/980915)   
 [叢集服務需要大約30秒的時間來故障轉 Windows Server 2008 R2 中的 IPv6 IP 位址](https://support.microsoft.com/kb/2578113)   
 [如果叢集與應用程式伺服器之間不存在任何路由器，就會緩慢地進行容錯移轉作業](https://support.microsoft.com/kb/2582281)  
  
  
