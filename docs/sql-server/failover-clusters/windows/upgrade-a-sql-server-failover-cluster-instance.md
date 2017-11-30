---
title: "升級 SQL Server 容錯移轉叢集執行個體 | Microsoft Docs"
ms.custom: 
ms.date: 10/01/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading failover clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], upgrading
ms.assetid: daac41fe-7d0b-4f14-84c2-62952ad8cbfa
caps.latest.revision: "47"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 7edcc0b0142562d998d3c7c1b2774b47716a4a06
ms.sourcegitcommit: fa030c0d644bae31f9688b1cc3523f60834f13c5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/14/2017
---
# <a name="upgrade-a-sql-server-failover-cluster-instance"></a>升級 SQL Server 容錯移轉叢集執行個體
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集升級至新版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、新的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Service Pack 或累積更新，或在所有容錯移轉叢集節點上個別安裝至新的 Windows Service Pack 或累積更新時，可將停機時間限制為僅單一手動容錯移轉 (回復為原始主要複本時則為兩次手動容錯移轉)。  
  
 [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)] 之前的作業系統不支援升級容錯移轉叢集的 Windows 作業系統。 若要升級在 [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)] 或以上版本上執行的叢集節點，請參閱[執行輪流升級或更新](#perform-a-rolling-upgrade-or-update)。  
  
 支援詳細資料如下：  
  
-   支援從使用者介面和命令提示字元進行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 升級。 您可以在每個容錯移轉叢集節點上，透過命令提示字元執行升級，也可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式 UI 來升級每個叢集節點。  如需詳細資訊，請參閱[升級 SQL Server 容錯移轉叢集執行個體 &#40;安裝程式&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md) 和[從命令提示字元安裝 SQL Server](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 升級不支援下列狀況：  
  
    -   您無法從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的獨立執行個體升級至容錯移轉叢集。  
  
    -   您無法將功能加入容錯移轉叢集。 例如，您無法將 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 加入至現有的僅限 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]容錯移轉叢集。  
  
    -   您無法將容錯移轉叢集節點降級為獨立執行個體。  
  
    -   變更容錯移轉叢集的版本會受限於特定狀況。 如需詳細資訊，請參閱 [支援的版本與版本升級](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)。  
  
-   在容錯移轉叢集升級期間，停機時間僅包含容錯移轉時間以及執行升級指令碼所需的時間。 在開始升級程序之前，如果您遵循下方的容錯移轉叢集輪流升級程序，且所有節點都符合必要條件，就可將停機時間降至最低。 在記憶體最佳化資料表使用中時升級 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 將會花費額外時間。 如需詳細資訊，請參閱 [Plan and Test the Database Engine Upgrade Plan](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md)。  
  
## <a name="prerequisites"></a>必要條件  
 在開始之前，請檢閱以下重要資訊：  
  
-   [支援的版本和版本升級](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)︰確認您可從 Windows 作業系統版本和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本升級至 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。 例如，您無法直接從 SQL Server 2005 容錯移轉叢集執行個體升級至 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，也無法升級在 [!INCLUDE[winxpsvr-md](../../../includes/winxpsvr-md.md)] 上執行的容錯移轉叢集。  
  
-   [Choose a Database Engine Upgrade Method](../../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md)︰根據您檢閱的支援版本與版本升級，選取適當的升級方法和步驟，此外亦根據作業環境中安裝的其他元件，依正確順序升級元件。  
  
-   [計劃和測試資料庫引擎升級計劃](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md)︰檢閱版本資訊與已知的升級問題、升級前檢查清單，並開發和測試升級計畫。  
  
-   [安裝 SQL Server 的硬體和軟體需求](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)：檢閱安裝 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 的軟體需求。 如果需要其他軟體，請先將其安裝在每個節點上，然後開始升級程序，以將任何停機時間降到最低。  
  
## <a name="perform-a-rolling-upgrade-or-update"></a>執行輪流升級或更新  
 若要將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集升級為 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，請使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式升級每個容錯移轉叢集節點 (從被動節點開始，一次一個)。 當您升級每個節點時，它就不會包含在容錯移轉叢集的可能擁有者中。 如果發生非預期的容錯移轉，則在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式將叢集資源群組擁有權移至升級的節點之前，升級的節點都不會參與容錯移轉。  
  
 根據預設， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式會自動決定容錯移轉至升級節點的時機。 這個時機會取決於容錯移轉叢集執行個體中的節點總數以及已經升級的節點數目而定。 如果半數以上的節點都已經升級，當您在下一個節點上執行升級時， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式就會將容錯移轉導至升級的節點。 容錯移轉至升級的節點之後，叢集群組就會移至升級的節點。 系統會將所有升級的節點都放置在可能擁有者的清單中，並從可能擁有者的清單中移除尚未升級的所有節點。 當您升級其餘每個節點時，它就會加入至容錯移轉叢集的可能擁有者。  
  
 這個程序會導致停機時間僅會包含整個容錯移轉叢集升級期間的單一容錯移轉時間和資料庫升級指令碼執行時間。  
  
 若要在升級程序期間控制叢集節點的容錯移轉行為，請從命令提示字元執行升級作業，然後使用 /FAILOVERCLUSTERROLLOWNERSHIP 參數。 如需詳細資訊，請參閱 [從命令提示字元安裝 SQL Server](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)。  
  
## <a name="next-steps"></a>後續的步驟  
 [使用安裝精靈升級 SQL Server &#40;安裝程式&#41;](../../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [從命令提示字元安裝 SQL Server](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [升級 SQL Server 容錯移轉叢集執行個體 &#40;安裝程式&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)  
  
  
