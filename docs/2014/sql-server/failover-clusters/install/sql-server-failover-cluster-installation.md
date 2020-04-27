---
title: SQL Server 容錯移轉叢集安裝 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: c0e75a7c-85c5-423c-a218-77247bf071aa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 49fce70b4fc01f77fe7ca54e3951f0372ba18489
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63067644"
---
# <a name="sql-server-failover-cluster-installation"></a>SQL Server 容錯移轉叢集安裝
  若要安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集，您必須執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式來建立及設定容錯移轉叢集執行個體。  
  
## <a name="installing-a-failover-cluster"></a>安裝容錯移轉叢集  
 若要安裝容錯移轉叢集，您必須使用具有本機系統管理員權限的網域帳戶，而且在容錯移轉叢集的所有節點上具有權限，能夠登入為服務以及做為作業系統的一部分。 若要使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式安裝容錯移轉叢集，請遵循下列步驟：  
  
1.  若要安裝、設定和維護 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集，請使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式。  
  
    -   確認建立容錯移轉叢集執行個體 (例如：叢集磁碟資源、IP 位址和網路名稱) 以及可用於容錯移轉之節點所需的資訊。 其他資訊：  
  
        -   [安裝容錯移轉叢集之前](before-installing-failover-clustering.md)  
  
        -   [SQL Server 安裝的安全性考量](../../install/security-considerations-for-a-sql-server-installation.md)  
  
    -   您必須先完成組態設定步驟，才能執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式；請使用 [Windows 叢集系統管理員] 執行這些步驟。針對您所要設定的每個容錯移轉叢集執行個體，都必須要有一個 WSFC 群組。  
  
    -   您必須確定系統符合最低需求。 如需 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集之特定需求的詳細資訊，請參閱 [安裝容錯移轉叢集之前](before-installing-failover-clustering.md)。  
  
2.  新增或移除容錯移轉叢集組態中的節點並不會影響其他叢集節點。 如需詳細資訊，請參閱[在 SQL Server 容錯移轉叢集中新增或移除節點 &#40;安裝程式&#41;](add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)。  
  
    -   容錯移轉叢集中的所有節點必須為相同平台 (即 32 位元或 64 位元)，而且必須在相同的作業系統版本上執行。 此外，您必須將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 64 位元版本安裝在執行 Windows 64 位元版本作業系統的 64 位元硬體上。 這一版沒有容錯移轉叢集的 WOW64 支援。  
  
3.  為每個容錯移轉叢集執行個體指定多個 IP 位址。 您可以為每個子網路指定多個 IP 位址。 若在相同的子網路上有多重 IP 位址， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式會將相依性設定為 AND。 若正跨多重子網路進行節點的叢集作業， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式會將相依性設定為 OR。  
  
## <a name="ssnoversion-failover-cluster-installation-options"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集安裝選項  
  
##### <a name="option-1-integrated-installation-with-add-node"></a>選項 1：整合式安裝與加入節點  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 整合式容錯移轉叢集安裝包含兩個步驟：  
  
1.  建立並設定單一節點的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體。 節點設定完成時，您就擁有可完整運作的容錯移轉叢集執行個體。 此時，它仍沒有高可用性，因為容錯移轉叢集只有單一節點。  
  
2.  在要加入至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集的每個節點上，使用「加入節點」功能來執行安裝程式，以便加入該節點。  
  
##### <a name="option-2-advancedenterprise-installation"></a>選項 2：進階/企業型安裝  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 進階/企業型容錯移轉叢集安裝包含兩個步驟：  
  
1.  在即將成為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集一部分的每個節點上，使用「準備容錯移轉叢集」功能來執行安裝程式。 雖然這個步驟會準備即將建立叢集的節點，不過在這個步驟結束時，不會提供任何可運作的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體。  
  
2.  備妥要建立叢集的節點之後，請在擁有共用磁碟的節點上，使用「完成容錯移轉叢集」功能來執行安裝程式。 這個步驟會設定並完成容錯移轉叢集執行個體。 在這個步驟結束時，您將擁有可運作的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體。  
  
    > [!NOTE]  
    >  兩種安裝選項都允許多節點 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集安裝。 已經建立 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集之後，「加入節點」可用來針對任何一個選項加入其他節點。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝位置的作業系統磁碟機代號在加入至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集的所有節點上都必須符合。  
  
#### <a name="ip-address-configuration-during-setup"></a>安裝期間的 IP 位址組態  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式可在執行下列動作時，設定或變更 IP 資源的相依性設定：  
  
-   整合式安裝 - [建立新的 SQL Server 容錯移轉叢集 &#40;安裝程式&#41;](create-a-new-sql-server-failover-cluster-setup.md)  
  
-   CompleteFailoverCluster (進階安裝) - [建立新的 SQL Server 容錯移轉叢集 &#40;安裝程式&#41;](create-a-new-sql-server-failover-cluster-setup.md)  
  
-   加入節點 - [在 SQL Server 容錯移轉叢集中加入或移除節點 &#40;安裝程式&#41;](add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  
  
-   移除節點 - [在 SQL Server 容錯移轉叢集中加入或移除節點 &#40;安裝程式&#41;](add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  
  
 **備註** ：支援 IPV6 IP 位址。  如果您同時設定了 IPV4 和 IPV6，而且兩者被視為不同子網路，則 IPV6 預期會先上線。  
  
##### <a name="ssnoversion-multi-subnet-failover-cluster"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 多重子網路容錯移轉叢集  
 當叢集中的節點位於不同的子網路時，您可以設定 OR 相依性。 但是， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 多重子網路容錯移轉叢集中的每一個節點，必須至少是一個已指定之 IP 位址的可能擁有者。  
  
## <a name="see-also"></a>另請參閱  
 [安裝容錯移轉叢集之前](before-installing-failover-clustering.md)   
 [建立新的 SQL Server 容錯移轉叢集 &#40;安裝程式&#41;](create-a-new-sql-server-failover-cluster-setup.md)   
 [從命令提示字元安裝 SQL Server 2014](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [升級 SQL Server 容錯移轉叢集](../windows/upgrade-a-sql-server-failover-cluster-instance.md)  
  
  
