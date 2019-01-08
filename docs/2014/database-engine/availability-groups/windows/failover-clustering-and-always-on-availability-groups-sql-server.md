---
title: 容錯移轉叢集和 AlwaysOn 可用性群組 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- clustering [SQL Server]
- Availability Groups [SQL Server], WSFC clusters
- Failover Cluster Instances [SQL Server], see failover clustering [SQL Server]
- quorum [SQL Server]
- failover clustering [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], Failover Cluster Instances
ms.assetid: 613bfbf1-9958-477b-a6be-c6d4f18785c3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e8d4858d55d9c37529e44cdf7759bf9fe6ce2630
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53352315"
---
# <a name="failover-clustering-and-alwayson-availability-groups-sql-server"></a>容錯移轉叢集和 AlwaysOn 可用性群組 (SQL Server)
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] (也就是 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中所引進的高可用性和災害復原解決方案) 需要 Windows Server 容錯移轉叢集 (WSFC)。 此外，雖然 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 不依賴 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集，但是您可以使用容錯移轉叢集執行個體 (FCI) 來裝載可用性群組的可用性複本。 請務必了解每個叢集技術的角色，也要知道設計您的 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 環境時所必須考量的事項。  
  
> [!NOTE]  
>  如需 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 概念的相關資訊，請參閱 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)。  
  

  
##  <a name="WSFC"></a> Windows Server 容錯移轉叢集和可用性群組  
 部署 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 需要一個 Windows Server 容錯移轉叢集 (WSFC) 叢集。 若要啟用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體必須位於 WSFC 節點上，而且 WSFC 叢集和節點必須在線上。 此外，給定可用性群組的每個可用性複本都必須位在相同 WSFC 叢集的不同節點上。 唯一的例外狀況是在移轉至另一個 WSFC 叢集期間，可用性群組可以暫時跨兩個叢集。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 依賴 Windows 容錯移轉叢集 (WSFC) 叢集來監視及管理屬於給定可用性群組之可用性複本的目前角色，並判斷容錯移轉事件對於可用性複本的影響程度。 對於您建立的每個可用性群組，系統會建立一個 WSFC 資源群組。 WSFC 叢集會監視此資源群組，以評估主要複本的健康情況。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 的仲裁會以 WSFC 叢集中的所有節點為基礎，而不論給定叢集節點是否裝載任何可用性複本。 相較於資料庫鏡像， [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]沒有見證角色。  
  
 WSFC 叢集的整體健全狀況是由叢集節點的仲裁投票所決定。 如果 WSFC 叢集因為未規劃的災害或由於持續硬體或通訊失敗而離線，則需要手動管理介入。 Windows Server 或 WSFC 叢集管理員需要強制仲裁，然後使非容錯組態中的存活叢集節點恢復上線。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 登錄機碼是 WSFC 叢集的子機碼。 如果您刪除然後重新建立 WSFC 叢集，則必須在原始 WSFC 叢集上裝載可用性複本的每個 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 執行個體，停用然後重新啟用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 功能。  
  
 如需在 Windows Server 容錯移轉叢集 (WSFC) 節點上執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以及 WSFC 仲裁的資訊，請參閱 [SQL Server 的 Windows Server 容錯移轉叢集&#40;WSFC&#41; ](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)。  
  
### <a name="cross-cluster-migration-of-alwayson-availability-groups-for-os-upgrade"></a>針對作業系統升級進行 AlwaysOn 可用性群組的跨叢集移轉  
 從 [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] 開始，[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 對於部署至新的 Windows Server 容錯移轉叢集 (WSFC) 叢集的情況，支援跨叢集移轉可用性群組。 跨叢集移轉是指以最短的停機時間，將一個可用性群組或一批可用性群組移到新的目的地 WSFC 叢集。 跨叢集移轉程序可讓您在升級至 [!INCLUDE[win8srv](../../../includes/win8srv-md.md)] 叢集的同時，維護您的服務等級協定 (SLA)。 [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] (或更新版本) 必須針對目的地 WSFC 叢集上的 AlwaysOn 安裝及啟用。 跨叢集移轉是否成功，取決於目的地 WSFC 叢集整套計畫和準備工作。  
  
 如需詳細資訊，請參閱[針對作業系統升級進行 AlwaysOn 可用性群組的跨叢集移轉](https://msdn.microsoft.com/library/jj873730.aspx)。  
  
##  <a name="SQLServerFC"></a> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體 (FCI) 和可用性群組  
 您可以藉由實作 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集連同 WSFC 叢集，在伺服器執行個體層級設定容錯移轉的第二層。 可用性複本可由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 獨立執行個體或 FCI 執行個體所裝載。 只有一個 FCI 夥伴可以裝載給定可用性群組的複本。 在 FCI 上執行可用性複本時，可用性群組的可能擁有者清單只包含使用中 FCI 節點。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 不依賴任何形式的共用儲存體。 不過，如果您使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體 (FCI) 來裝載一個或多個可用性複本，依照標準 SQL Server 容錯移轉叢集執行個體安裝，這些 FCI 都需要共用儲存體。  
  
 如需其他必要條件的詳細資訊，請參閱 [AlwaysOn 可用性群組的必要條件、限制和建議 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md) 的＜使用 SQL Server 容錯移轉叢集執行個體 (FCI) 裝載可用性複本的必要條件和限制＞一節。  
  
### <a name="comparison-of-failover-cluster-instances-and-availability-groups"></a>容錯移轉叢集執行個體和可用性群組的比較  
 無論 FCI 中節點的數目有多少，整個 FCI 只能裝載可用性群組的單一複本。 下表描述 FCI 節點和可用性群組複本之間的概念差異。  
  
||FCI 內的節點|可用性群組內的複本|  
|-|-------------------------|-------------------------------------------|  
|**使用 WSFC 叢集**|是|是|  
|**保護等級**|執行個體|[資料庫]|  
|**儲存類型**|共用|非共用<br /><br /> 請注意，雖然可用性群組中的複本不會共用儲存體，但是 FCI 裝載的複本會使用該 FCI 所需的共用儲存方案。 只有 FCI 內的節點共用儲存方案，可用性群組的複本之間不共用儲存方案。|  
|**儲存方案**|直接附加、SAN、掛接點、SMB|取決於節點類型|  
|**可讀取次要**|否*|是|  
|**適用的容錯移轉原則設定**|WSFC 仲裁<br /><br /> FCI 特定<br /><br /> 可用性群組設定**|WSFC 仲裁<br /><br /> 可用性群組設定|  
|**容錯移轉資源**|伺服器、執行個體和資料庫|僅資料庫|  
  
 *可用性群組中的同步次要複本一律在其各自的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上執行，而 FCI 中的次要節點實際上尚未啟動其各自的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體，因此不可讀取。 在 FCI 中，次要節點只在 FCI 容錯移轉期間資源群組擁有權轉移到它自己時才會啟動其 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體。 不過，在使用中 FCI 節點上，當 FCI 裝載的資料庫屬於可用性群組時，如果本機可用性複本以可讀取的次要複本方式執行，資料庫就是可讀取的。  
  
 **可用性群組的容錯移轉原則設定適用於所有複本，無論複本裝載於獨立執行個體或 FCI 執行個體。  
  
> [!NOTE]  
>  如需詳細資訊**的節點數目**中容錯移轉叢集並**AlwaysOn 可用性群組**針對不同版本的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，請參閱[支援的功能SQL Server 2012 版本](https://go.microsoft.com/fwlink/?linkid=232473)(https://go.microsoft.com/fwlink/?linkid=232473)。  
  
### <a name="considerations-for-hosting-an-availability-replica-on-an-fci"></a>FCI 裝載可用性複本的考量  
  
> [!IMPORTANT]  
>  如果您計劃在 SQL Server 容錯移轉叢集執行個體 (FCI) 裝載可用性複本，請確定 Windows Server 2008 主機節點符合容錯移轉叢集執行個體 (FCI) 的 AlwaysOn 必要條件和限制。 如需詳細資訊，請參閱 [AlwaysOn 可用性群組的必要條件、限制和建議 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體 (FCI) 不支援依照可用性群組進行自動容錯移轉，因此任何由 FCI 裝載的可用性複本只能設定為手動容錯移轉。  
  
 您可能需要設定 Windows Server 容錯移轉叢集 (WSFC) 叢集，使其包含並非在所有節點都可使用的共用磁碟。 例如，假設有一個 WSFC 叢集跨兩個資料中心，其共有三個節點。 在主要資料中心的兩個節點裝載 SQL Server 容錯移轉叢集執行個體 (FCI)，而且可存取相同的共用磁碟。 在另一個資料中心，第三個節點裝載 SQL Server 獨立執行個體，而且無法存取主要資料中心的共用磁碟。 如果 FCI 裝載主要複本，而且獨立執行個體裝載次要複本，此 WSFC 叢集組態就會支援可用性群組的部署。  
  
 當您選擇讓 FCI 裝載給定可用性群組的可用性複本時，請確定 FCI 容錯移轉不會使單一 WSFC 節點嘗試裝載同一個可用性群組的兩個可用性複本。  
  
 下列範例案例說明這個組態可能會如何導致問題的發生：  
  
 Marcel 設定包含兩個節點 `NODE01` 和 `NODE02`的 WSFC 叢集。 他將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體 `fciInstance1`同時安裝在 `NODE01` 和 `NODE02` 上，其中 `NODE01` 是 `fciInstance1`的目前擁有者。  
 Marcel 會在 `NODE02`上安裝另一個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體 `Instance3`，這是獨立執行個體。  
 Marcel 在 `NODE01`上讓 fciInstance1 啟用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]。 他在 `NODE02`上讓 `Instance3` 啟用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]。 接著他設定可用性群組，由 `fciInstance1` 裝載其主要複本，並由 `Instance3` 裝載其次要複本。  
 在某個時間點， `fciInstance1` 變得無法在 `NODE01`上使用，而且 WSFC 叢集會造成 `fciInstance1` 容錯移轉到 `NODE02`。 在容錯移轉之後， `fciInstance1` 就是具有 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]功能的執行個體，於 `NODE02`的主要角色之下執行。 但是， `Instance3` 現在位於與 `fciInstance1`相同的 WSFC 節點上。 這樣會違反 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 條件約束。  
 若要更正此案例所呈現的問題，獨立執行個體 `Instance3` 必須位於與 `NODE01` 和 `NODE02` 相同的 WSFC 叢集內的另一個節點上。  
  
 如需 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集的詳細資訊，請參閱 [AlwaysOn 容錯移轉叢集執行個體 &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)。  
  
##  <a name="FCMrestrictions"></a> WSFC 容錯移轉叢集管理員與可用性群組一起使用的限制  
 不要使用容錯移轉叢集管理員操作可用性群組，例如：  
  
-   請勿在可用性群組的叢集服務 (資源群組) 中加入或移除資源。  
  
-   請勿變更任何可用性群組屬性，例如可能的擁有者和慣用擁有者。 可用性群組會自動設定這些屬性。  
  
-   請勿使用容錯移轉叢集管理員來將可用性群組移到不同的節點或容錯移轉可用性群組。 容錯移轉叢集管理員不會察覺可用性複本的同步處理狀態，而且這樣做可能會造成停機時間延長。 您必須使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]。  
  
##  <a name="RelatedContent"></a> 相關內容  
  
-   **部落格：**  
  
     [以有限安全性設定 SQL Server 的 Windows 容錯移轉叢集 (可用性群組或 FCI)](https://blogs.msdn.com/b/sqlalwayson/archive/2012/06/05/configure-windows-failover-clustering-for-sql-server-availability-group-or-fci-with-limited-security.aspx)  
  
     [SQL Server AlwaysOn 團隊部落格：官方 SQL Server AlwaysOn 團隊部落格](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server 工程師部落格](https://blogs.msdn.com/b/psssql/)  
  
-   **白皮書：**  
  
     [AlwaysOn 架構指南：使用容錯移轉叢集執行個體和可用性群組建置高可用性和災害復原解決方案](https://msdn.microsoft.com/library/jj215886.aspx)  
  
     [Microsoft SQL Server AlwaysOn 解決方案指南高可用性和災害復原](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Microsoft 的 SQL Server 2012 白皮書](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 客戶諮詢團隊白皮書](http://sqlcat.com/)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀&#40;SQL Server&#41; ](overview-of-always-on-availability-groups-sql-server.md) [啟用和停用 AlwaysOn 可用性群組&#40;SQL Server&#41; ](enable-and-disable-always-on-availability-groups-sql-server.md) [監視可用性群組&#40;Transact SQL&#41;](monitor-availability-groups-transact-sql.md)  
 [AlwaysOn 容錯移轉叢集執行個體&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md) 
  
  
