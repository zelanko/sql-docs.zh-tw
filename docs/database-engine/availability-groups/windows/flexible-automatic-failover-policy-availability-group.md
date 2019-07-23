---
title: 為可用性群組設定彈性的自動容錯移轉原則
description: '決定 Always On 可用性群組的容錯移轉原則彈性程度時，各種可用選項的描述。 '
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], flexible failover policy
- Availability Groups [SQL Server], failover
- flexible failover policy
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 8c504c7f-5c1d-4124-b697-f735ef0084f0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 40376a81eb1a51bc903a7a4ab81f00c187d5f8f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008379"
---
# <a name="configure-a-flexible-automatic-failover-policy-for-an-always-on-availability-group"></a>為 Always On 可用性群組設定彈性的自動容錯移轉原則
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  彈性容錯移轉原則可讓您更精確地控制造成可用性群組之 [自動容錯移轉](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md) 的狀況。 透過變更觸發自動容錯移轉的失敗狀況和健全狀況檢查的頻率，您可以提高或降低自動容錯移轉的可能性，以便支援高可用性的 SLA。  
  
 可用性群組的彈性容錯移轉原則是由其失敗狀況層級和健全狀況檢查逾時臨界值所定義。 一旦偵測到可用性群組超過其失敗狀況層級或健全狀況檢查逾時臨界值時，可用性群組的資源 DLL 就會回應至 Windows Server 容錯移轉叢集 (WSFC) 叢集。 然後，WSFC 叢集就會起始自動容錯移轉至次要複本。  
  
> [!IMPORTANT]  
>  如果可用性群組超過其 WSFC 失敗臨界值，WSFC 叢集將不會嘗試進行可用性群組的自動容錯移轉。 此外，可用性群組的 WSFC 資源群組會維持失敗狀態，直到叢集管理員手動讓失敗的資源群組上線，或者資料庫管理員執行可用性群組的手動容錯移轉為止。 *「WSFC 失敗臨界值」* (WSFC Failure Threshold) 定義為可用性群組在給定的時間週期內支援的失敗次數上限。 預設的時間週期為六小時，而且在這段時間內失敗次數上限的預設值為 *n*-1，其中 *n* 是 WSFC 節點的數目。 若要變更給定可用性群組得失敗臨界值，請使用 WSFC 容錯移轉管理員主控台。  
  
 本主題包含下列幾節：  
  
-   [健全狀況檢查逾時臨界值](#HCtimeout)  
  
-   [失敗狀況層級](#FClevel)  
  
-   [相關工作](#RelatedTasks)  
  
-   [相關內容](#RelatedContent)  
  
##  <a name="HCtimeout"></a> 健全狀況檢查逾時臨界值  
 可用性群組的 WSFC 資源 DLL 會在裝載主要複本的 SQL Server 執行個體上呼叫 [sp_server_diagnostics](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) 預存程序，藉以執行主要複本的「健全狀況檢查」  。 **sp_server_diagnostics** 會以等於可用性群組之健全狀況檢查逾時臨界值 1/3 的間隔傳回結果。 預設的健全狀況檢查逾時臨界值為 30 秒，因此 **sp_server_diagnostics** 會以 10 秒的間隔傳回結果。 如果 **sp_server_diagnostics** 變慢或未傳回資訊，資源 DLL 會先等候健全狀況檢查逾時臨界值的完整間隔，然後再判斷主要複本是否沒有回應。 如果主要複本沒有回應，就會起始自動容錯移轉 (如果目前支援的話)。  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** 不會在資料庫層級執行健全狀況檢查。  
  
##  <a name="FClevel"></a> 失敗狀況層級  
 **sp_server_diagnostics** 所傳回的診斷資料和健全狀況資訊是否保證自動容錯移轉主要取決於可用性群組的失敗狀況層級。 「失敗狀況層級」  會指定觸發自動容錯移轉的失敗狀況。 失敗狀況層級共有五層，範圍從最低限制 (第一層級) 到最高限制 (第五層級)。 給定的層級包含較低限制的層級。 因此，最嚴格的層級 (五) 包括了四個較低限制的狀況，依此類推。  
  
> [!IMPORTANT]  
>  任何失敗狀況層級不會偵測到損毀的資料庫和可疑的資料庫。 因此，損毀或可疑的資料庫 (不論是因為硬體故障、資料損毀或其他問題) 都絕對不會觸發自動容錯移轉。  
  
 下表描述對應至每個層級的失敗狀況。  
  
|層級|失敗狀況|[!INCLUDE[tsql](../../../includes/tsql-md.md)] 值|PowerShell 值|  
|-----------|-----------------------|------------------------------|----------------------|  
|一|伺服器關閉時。 指定在發生下列任何狀況時起始自動容錯移轉：<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務關閉。<br /><br /> 由於未從伺服器執行個體收到 ACK，所以用於連接到 WSFC 叢集的可用性群組租用已到期。 如需詳細資訊，請參閱 [How It Works:SQL Server Always On Lease Timeout](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx) (運作方式：SQL Server Always On 租用逾時)。<br /><br /> <br /><br /> 這是最低限制層級。|1|**OnServerDown**|  
|二|伺服器沒有回應時。 指定在發生下列任何狀況時起始自動容錯移轉：<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的執行個體未連接到叢集，而且已超出使用者指定之可用性群組的健全狀況檢查逾時臨界值。<br /><br /> 可用性複本處於失敗狀態。|2|**OnServerUnresponsive**|  
|三|發生嚴重伺服器錯誤時。 指定在發生嚴重 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 內部錯誤時起始自動容錯移轉，例如執行緒同步鎖定遭到遺棄、嚴重的寫入存取違規或是傾印過多。<br /><br /> 這是預設層級。|3|**OnCriticalServerError**|  
|四|發生一般伺服器錯誤時。 指定在發生一般 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 內部錯誤時起始自動容錯移轉，例如 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 內部資源集區持續發生記憶體不足的狀況。|4|**OnModerateServerError**|  
|五|發生任何限定的失敗狀況時。 指定在發生任何限定的失敗狀況時起始自動容錯移轉，這些狀況包括：<br /><br /> 偵測排程器死結。<br /><br /> 偵測到無法解決的死結。<br /><br /> <br /><br /> 這是最高限制層級。|5|**OnAnyQualifiedFailureConditions**|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體對用戶端要求缺少回應與可用性群組無關。  
  
##  <a name="RelatedTasks"></a> 相關工作  
 **若要設定自動容錯移轉**  
  
-   [變更可用性複本的可用性模式 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md) (自動容錯移轉需要同步認可的可用性模式)  
  
-   [變更可用性複本的容錯移轉模式 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [設定彈性容錯移轉原則以控制自動容錯移轉的條件 &#40;AlwaysOn 可用性群組&#41;](../../../database-engine/availability-groups/windows/configure-flexible-automatic-failover-policy.md)  
  
##  <a name="RelatedContent"></a> 相關內容  
  
-   [How It Works:SQL Server Always On Lease Timeout](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx) (運作方式：SQL Server Always On 租用逾時)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性模式 &#40;AlwaysOn 可用性群組&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [容錯移轉及容錯移轉模式 &#40;AlwaysOn 可用性群組&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)   
 [SQL Server 的 Windows Server 容錯移轉叢集 &#40;WSFC&#41;](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [容錯移轉叢集執行個體的容錯移轉原則](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)   
 [sp_server_diagnostics &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)  
  
  
