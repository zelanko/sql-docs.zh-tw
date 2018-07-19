---
title: 重新命名 SQL Server 容錯移轉叢集執行個體 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- clusters [SQL Server], virtual servers
- renaming virtual servers
- virtual servers [SQL Server], failover clustering
- failover clustering [SQL Server], virtual servers
ms.assetid: 2a49d417-25fb-4760-8ae5-5871bfb1e6f3
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 006abb7b37e67938a060ed05ced726c3699dfbd3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37294008"
---
# <a name="rename-a-sql-server-failover-cluster-instance"></a>重新命名 SQL Server 容錯移轉叢集執行個體
  當 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體是容錯移轉叢集的一部份時，重新命名虛擬伺服器的程序會不同於重新命名獨立執行個體的程序。 如需詳細資訊，請參閱 [重新命名主控 SQL Server 獨立執行個體的電腦](../../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)。  
  
 虛擬伺服器的名稱一定跟「SQL 網路名稱」(SQL 虛擬伺服器網路名稱) 的名稱相同。 雖然您可以變更虛擬伺服器的名稱，但無法變更執行個體名稱。 例如，您可以將名稱為 VS1\instance1 的虛擬伺服器變更為其他的名稱，例如 SQL35\instance1，但名稱的執行個體部份 instance1 會維持不變。  
  
 在開始重新命名的程序之前，請檢閱以下項目。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不支援與複寫有關之伺服器的重新命名作業。 如果主要伺服器永久失去了，就可以重新命名記錄傳送中的次要伺服器。 如需詳細資訊，請參閱[記錄傳送和複寫 &#40;SQL Server&#41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md)。  
  
-   在重新命名設定為使用資料庫鏡像的虛擬伺服器時，您必須在重新命名作業之前關閉資料庫鏡像，然後使用新的虛擬伺服器名稱，重新建立資料庫鏡像。 資料庫鏡像的中繼資料並不會自動更新來反映新的虛擬伺服器名稱。  
  
### <a name="to-rename-a-virtual-server"></a>若要重新命名虛擬伺服器  
  
1.  使用 [叢集管理員]，將「SQL 網路名稱」變更為新的名稱。  
  
2.  使網路名稱資源離線。 這會連帶使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資源以及其他相依的資源離線。  
  
3.  使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資源回到線上。  
  
## <a name="verify-the-renaming-operation"></a>確認重新命名作業  
 重新命名虛擬伺服器之後，任何使用舊名稱的連接現在都必須使用新名稱進行連接。  
  
 若要確認重新命名作業已經完成，請選取資訊從其中`@@servername`或`sys.servers`。 `@@servername` 函數會傳回新的虛擬伺服器名稱，而 `sys.servers` 資料表則會顯示新的虛擬伺服器名稱。 若要確認容錯移轉程序可以使用新名稱正常運作，使用者應該同時嘗試將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資源容錯移轉至其他節點。  
  
 對於來自叢集內任何節點的連接，幾乎可以立即使用新的名稱。 不過，對於來自用戶端電腦使用新名稱的連接，必須在該用戶端電腦看到新名稱之後，才能使用新名稱連接到伺服器。 新名稱透過網路傳播所需的時間長度可以是幾秒鐘，或長達 3 到 5 分鐘，視網路組態而定；可能也需要額外的時間，才不會在網路上看到舊的虛擬伺服器名稱。  
  
 若要最小化虛擬伺服器重新命名作業的網路傳播延遲，請使用下列步驟：  
  
#### <a name="to-minimize-network-propagation-delay"></a>若要最小化網路傳播延遲  
  
1.  從伺服器節點的命令提示字元發出下列命令：  
  
    ```  
    ipconfig /flushdns  
    ipconfig /registerdns  
    nbtstat –RR  
    ```  
  
## <a name="additional-considerations-after-the-renaming-operation"></a>重新命名作業之後的其他考量  
 將容錯移轉叢集的網路名稱重新命名之後，我們必須確認並執行下列指示，才能啟用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 和 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中的所有案例。  
  
 **[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]：** 在您使用 Windows 叢集系統管理員工具來變更 [!INCLUDE[ssASCurrent](../../../includes/ssascurrent-md.md)] 容錯移轉叢集執行個體的網路名稱之後，未來的升級或解除安裝作業可能會失敗。 若要解決此問題的更新**ClusterName**登錄項目中的解決方法章節的指示[這](http://go.microsoft.com/fwlink/?LinkId=244002)(http://go.microsoft.com/fwlink/?LinkId=244002)。  
  
 **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 服務：** 請針對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 服務確認並執行下列其他動作：  
  
-   如果 SQL 代理程式設定為事件轉送，請修正登錄設定。 如需詳細資訊，請參閱[指定事件轉送伺服器 &#40;SQL Server Management Studio&#41;](../../../ssms/agent/designate-an-events-forwarding-server-sql-server-management-studio.md)。  
  
-   當電腦/叢集網路名稱已重新命名時，請修正主要伺服器 (MSX) 和目標伺服器 (TSX) 執行個體名稱。 如需詳細資訊，請參閱下列主題：  
  
    -   [從主要伺服器脫離多個目標伺服器](../../../ssms/agent/defect-multiple-target-servers-from-a-master-server.md)  
  
    -   [建立多伺服器環境](../../../ssms/agent/create-a-multiserver-environment.md)  
  
-   重新設定記錄傳送，以便使用更新的伺服器名稱來備份和還原記錄。 如需詳細資訊，請參閱下列主題：  
  
    -   [設定記錄傳送 &#40;SQL Server&#41;](../../../database-engine/log-shipping/configure-log-shipping-sql-server.md)  
  
    -   [移除記錄傳送 &#40;SQL Server&#41;](../../../database-engine/log-shipping/remove-log-shipping-sql-server.md)  
  
-   更新相依於伺服器名稱的作業步驟。 如需詳細資訊，請參閱 [Manage Job Steps](../../../ssms/agent/manage-job-steps.md)。  
  
## <a name="see-also"></a>另請參閱  
 [重新命名主控 SQL Server 獨立執行個體的電腦](../../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)  
  
  
