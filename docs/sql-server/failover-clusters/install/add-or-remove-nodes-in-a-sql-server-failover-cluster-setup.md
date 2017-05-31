---
title: "在 SQL Server 容錯移轉叢集中加入或移除節點 (安裝程式) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- adding nodes
- nodes [Faillover Clustering], removing
- nodes [Faillover Clustering], adding
- failover clustering [SQL Server], nodes
- deleting nodes
- cluster maintenance [SQL Server]
- removing nodes
ms.assetid: fe20dca9-a4c1-4d32-813d-42f1782dfdd3
caps.latest.revision: 49
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0d61da5ddef04a1edacf6f5b8bf98bb04b53fa5a
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="add-or-remove-nodes-in-a-sql-server-failover-cluster-setup"></a>在 SQL Server 容錯移轉叢集中加入或移除節點 (安裝程式)
  您可以使用此程序來管理現有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體的節點。  
  
 若要更新或移除 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集，您必須是本機管理員，而且擁有在容錯移轉叢集之所有節點上登入成為服務的權限。 如果是本機安裝，您必須以管理員身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，則必須使用對遠端共用位置具有讀取和執行權限的網域帳戶。  
  
 若要將節點加入至現有的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集，您必須在要加入至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體的節點上執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式。 請勿在使用中節點上執行安裝程式。  
  
 若要從現有的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集中移除節點，您必須在即將從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體中移除的節點上執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式。  
  
 若要檢視加入或移除節點的程序性步驟，請選取下列其中一個作業：  
  
-   [將節點加入現有的 SQL Server 容錯移轉叢集](#Add)  
  
-   [從現有的 SQL Server 容錯移轉叢集中移除節點](#Remove)  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝位置的作業系統磁碟機代號在加入至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集的所有節點上都必須符合。  
  
##  <a name="Add"></a> 加入節點  
  
#### <a name="to-add-a-node-to-an-existing-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>將節點加入現有的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集  
  
1.  插入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝媒體，然後在根資料夾中，按兩下 Setup.exe。 若要從網路共用進行安裝，請導覽至共用上的根資料夾，然後按兩下 Setup.exe。  
  
2.  安裝精靈將會啟動 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝中心。 若要將節點加入至現有的容錯移轉叢集執行個體，請在左側窗格中按一下 [安裝]。 然後，請選取 [將節點加入到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集]。  
  
3.  系統組態檢查將會在電腦上執行探索作業。 若要繼續，請 [!INCLUDE[clickOK](../../../includes/clickok-md.md)]。  
  
4.  如果您在當地語系化的作業系統上安裝，而且安裝媒體包含英文以及與作業系統對應之語言的語言套件，您便可以在 [語言選擇] 頁面上指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的語言。 如需跨語言支援和安裝考量的詳細資訊，請參閱 [SQL Server 中的地區語言版本](../../../sql-server/install/local-language-versions-in-sql-server.md)。  
  
     若要繼續進行，請按 **[下一步]**。  
  
5.  在 [產品金鑰] 頁面上，針對產品的實際執行版本指定 PID 金鑰。 請注意，您針對此安裝輸入的產品金鑰必須與安裝在使用中節點上的版本具有相同的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本。  
  
6.  在 [授權條款] 頁面上，閱讀授權合約，然後選取要接受授權條款和條件的核取方塊。 若要協助提升 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，您也可以啟用功能使用方式選項，並傳送報告給 [!INCLUDE[msCoName](../../../includes/msconame-md.md)]。 若要繼續進行，請按 **[下一步]**。 若要結束安裝程式，請按一下 **[取消]**。  
  
7.  系統組態檢查將會先確認電腦的系統狀態，然後安裝程式才會繼續進行。 檢查完成之後，請按 **[下一步]** 繼續進行。  
  
8.  在 [叢集節點組態] 頁面上，使用下拉式方塊來指定將要在此安裝程式作業期間修改之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體的名稱。  
  
9. 在 [伺服器組態 - 服務帳戶] 頁面中，指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務的登入帳戶。 在這個頁面上所設定的實際服務隨著您選取要安裝的功能而不同。 若為容錯移轉叢集安裝，系統就會根據針對使用中節點所提供的設定，在這個頁面上預先填入帳戶名稱和啟動類型資訊。 不過，您必須提供每個帳戶的密碼。 如需詳細資訊，請參閱 [伺服器組態 - 服務帳戶](http://msdn.microsoft.com/library/c283702d-ab20-4bfa-9272-f0c53c31cb9f) 和 [設定 Windows 服務帳戶與權限](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
     **安全性注意事項** [!INCLUDE[ssNoteStrongPass](../../../includes/ssnotestrongpass-md.md)]  
  
     當您完成針對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務指定登入資訊之後，請按 **[下一步]**。  
  
10. 在 [報告] 頁面上，指定您想要傳送給 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 的資訊，以便改善 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 錯誤報告選項預設為啟用。  
  
11. 系統組態檢查將會執行一組額外的規則，以便使用您已指定的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 功能來驗證電腦組態。  
  
12. [準備加入節點] 頁面會顯示在安裝期間指定之安裝選項的樹狀檢視。  
  
13. [加入節點進度] 頁面會提供狀態，所以您可以在安裝程式進行時監視安裝進度。  
  
14. 安裝之後，[完成] 頁面會提供安裝和其他重要注意事項之摘要記錄檔的連結。 若要完成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程序，請按一下 **[關閉]**。  
  
15. 如果指示您重新啟動電腦，請立刻執行。 當您完成安裝時，請務必閱讀安裝精靈所提供的訊息。 如需安裝程式記錄檔的詳細資訊，請參閱 [檢視與讀取 SQL Server 安裝程式記錄檔](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)。  
  
##  <a name="Remove"></a> 移除節點  
  
#### <a name="to-remove-a-node-from-an-existing-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>從現有的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集中移除節點  
  
1.  插入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝媒體。 在根資料夾中，按兩下 setup.exe。 若要從網路共用進行安裝，請導覽至共用上的根資料夾，然後按兩下 Setup.exe。  
  
2.  安裝精靈會啟動 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝中心。 若要從現有的容錯移轉叢集執行個體中移除節點，請在左側窗格中按一下 [維護]，然後選取 [從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集移除節點]。  
  
3.  系統組態檢查將會在電腦上執行探索作業。 若要繼續，請 [!INCLUDE[clickOK](../../../includes/clickok-md.md)]。  
  
4.  按一下 [安裝程式支援檔案] 頁面上的 [安裝] 後，[系統組態檢查] 會在安裝程式繼續前檢查系統狀態。 檢查完成之後，請按 **[下一步]** 繼續進行。  
  
5.  在 [叢集節點組態] 頁面上，使用下拉式方塊來指定將要在此安裝程式作業期間修改之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體的名稱。 將要移除的節點就會列在 **[此節點的名稱]** 欄位中。  
  
6.  [準備移除節點] 頁面會顯示在安裝期間指定之選項的樹狀檢視。 若要繼續，請按一下 **[移除]**。  
  
7.  在移除作業期間，[移除節點進度] 頁面將提供狀態。  
  
8.  [完成] 頁面會提供移除節點作業和其他重要注意事項之摘要記錄檔的連結。 若要完成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 移除節點作業，請按一下 **[關閉]**。 如需安裝程式記錄檔的詳細資訊，請參閱 [檢視與讀取 SQL Server 安裝程式記錄檔](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)。  
  
## <a name="see-also"></a>另請參閱  
 [檢視與讀取 SQL Server 安裝程式記錄檔](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
