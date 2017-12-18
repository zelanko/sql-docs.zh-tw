---
title: "升級 SQL Server 容錯移轉叢集執行個體 (安裝程式) | Microsoft Docs"
ms.custom: 
ms.date: 01/22/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: failover-clusters
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], creating clusters
- clusters [SQL Server], creating
- failover clustering [SQL Server], upgrading
ms.assetid: ea8b7d66-e5a1-402f-9928-8f7310e84f5c
caps.latest.revision: "63"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9e35eab411af665d7758d76fa7e9f3f1353be7ce
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="upgrade-a-sql-server-failover-cluster-instance-setup"></a>升級 SQL Server 容錯移轉叢集執行個體 (安裝程式)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 您可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式 UI 或命令提示字元，將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集升級為 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 容錯移轉叢集。  
  
 若是本機安裝，您必須以管理員身分執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，則必須使用對遠端共用位置具有讀取權限的網域帳戶。  
  
 在升級之前，請參閱 [升級 SQL Server 容錯移轉叢集執行個體](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)。  
  
##  <a name="UpgradeSteps"></a> 若要升級 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集  
  
#### <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>若要升級 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集  
  
1.  從符合您要升級的版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝媒體版本，按兩下根資料夾中的 setup.exe。 如果您之前未安裝必要元件，系統可能會要求您安裝。  
  
2.  安裝必要元件之後，安裝精靈會啟動 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝中心。 若要升級現有的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體，請選取您的執行個體。  
  
3.  如果需要 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式支援檔案， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式就會安裝這些檔案。 如果系統指示您重新啟動電腦，請先重新啟動，然後再繼續進行。  
  
4.  系統組態檢查會在電腦上執行探索作業。 若要繼續，請 [!INCLUDE[clickOK](../../../includes/clickok-md.md)]。  
  
5.  在 [產品金鑰] 頁面上，針對符合舊產品版本的新版本輸入 PID 金鑰。 例如，若要升級 Enterprise 容錯移轉叢集，您必須提供 [!INCLUDE[ssEnterprise](../../../includes/ssenterprise-md.md)]的 PID 金鑰。 按 **[下一步]** ，繼續進行。 請注意，您針對容錯移轉叢集升級所使用的 PID 金鑰在相同 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的所有容錯移轉叢集節點之間必須一致。  
  
6.  在 [授權條款] 頁面上，閱讀授權合約，然後選取要接受授權條款和條件的核取方塊。 若要協助提升 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，您也可以啟用功能使用方式選項，並傳送報告給 [!INCLUDE[msCoName](../../../includes/msconame-md.md)]。 按一下 [下一步]，繼續進行。 若要結束安裝程式，請按一下 **[取消]**。  
  
7.  在 [選取執行個體] 頁面中，指定要升級為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 執行個體。 按一下 [下一步]，繼續進行。  
  
8.  在 [特徵選取] 頁面上，系統會預先選取要升級的功能。 當您選取功能名稱之後，每一個元件群組的描述就會出現在右窗格中。 請注意，您無法變更要升級的功能，而且您無法在升級作業期間加入功能。 若要在完成升級作業後，將功能加入升級的 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 執行個體，請參閱 [將功能加入 SQL Server 2016 的執行個體 &#40;安裝程式&#41;](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)。  
  
     右窗格會顯示選取功能的必要條件。 SQL Server 安裝程式將會在這個程序稍後說明的安裝步驟期間安裝尚未安裝的必要條件。 為了節省時間，您應該在每個節點上預先安裝這些必要條件。  
  
9. 在 [執行個體組態] 頁面上，系統會根據舊的執行個體自動填入欄位。 您可以選擇指定新的 InstanceID 值。  
  
     **執行個體識別碼** - 根據預設，此執行個體名稱會當做執行個體識別碼使用。 這是用來識別 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體的安裝目錄和登錄機碼。 這是預設執行個體和具名執行個體的狀況。 如果是預設執行個體，執行個體名稱和執行個體識別碼將會是 MSSQLSERVER。 若要使用非預設的執行個體識別碼，請選取 [執行個體識別碼] 核取方塊並提供值。 如果您覆寫預設值，就必須針對在所有容錯移轉叢集節點上升級的執行個體指定相同的執行個體識別碼。 升級之執行個體的執行個體識別碼在這些節點之間必須相符。  
  
     **偵測到的執行個體和功能** - 此方格會顯示執行安裝程式之電腦上的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體。 按一下 [下一步]，繼續進行。  
  
10. [磁碟空間需求] 頁面會計算您所指定之功能的所需磁碟空間，並且比較空間需求與執行安裝程式之電腦的可用磁碟空間。  
  
11. 在 [全文檢索搜尋升級] 頁面上，針對升級的資料庫指定升級選項。 如需詳細資訊，請參閱 [全文檢索搜尋升級選項](http://msdn.microsoft.com/library/16c9376b-5fbb-4495-a429-06a2493849c9)。  
  
12. 在 **[錯誤報告]** 頁面上，指定您想要傳送給 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 的資訊，這可協助改善 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 錯誤報告選項預設為啟用。  
  
13. 在升級作業開始之前，系統組態檢查會執行一組額外的規則，以便使用您已指定的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 功能來驗證電腦組態。  
  
14. [叢集升級報表] 頁面會顯示容錯移轉叢集執行個體中的節點清單以及每個節點上 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 元件的執行個體版本資訊。 它會顯示資料庫指令碼狀態和複寫指令碼狀態。 此外，它也會顯示當您按一下 [下一步] 時所進行之動作的參考用訊息。 根據已經升級的容錯移轉叢集節點數目和節點總數，安裝程式會顯示當您按一下 [下一步] 時所發生的容錯移轉行為。 如果您尚未安裝必要元件，它也會發出可能產生不必要停機時間的警告。  
  
15. [準備升級] 頁面會顯示在安裝期間指定之安裝選項的樹狀檢視。 若要繼續，請按一下 **[升級]**。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式會先安裝選取功能所需的必要條件，之後再進行功能安裝。  
  
16. 在升級期間，[進度] 頁面會提供狀態，好讓您可以在安裝程式進行時監視目前節點的升級進度。  
  
17. 升級目前的節點之後，[叢集升級報表] 頁面就會顯示所有容錯移轉叢集節點的升級狀態資訊、每個容錯移轉叢集節點的功能，以及其版本資訊。 請確認所顯示的版本資訊並且繼續進行其餘節點的升級作業。 如果發生容錯移轉至升級節點的行為，這也會出現在狀態頁面上。 您也可以在 Windows 叢集管理員工具中檢查，然後確認。  
  
18. 升級之後，[完成] 頁面會提供安裝和其他重要注意事項之摘要記錄檔的連結。 若要完成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程序，請按一下 **[關閉]**。  
  
19. 如果指示您重新啟動電腦，請立刻執行。 當您完成安裝時，請務必閱讀安裝精靈所提供的訊息。 如需安裝程式記錄檔的詳細資訊，請參閱 [檢視與讀取 SQL Server 安裝程式記錄檔](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)。  
  
20. 若要完成升級程序，請在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集的所有其他節點上重複這些步驟。  
  
## <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster"></a>若要升級 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 多重子網路容錯移轉叢集  
  
#### <a name="to-upgrade-to-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster-existing-includessnoversionincludesssnoversion-mdmd-cluster-is-a-non-multi-subnet-cluster"></a>若要升級到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 多重子網路容錯移轉叢集 (現有的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 叢集為非多重子網路叢集)。  
  
1.  請遵循上述步驟，將您的叢集升級到 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。  
  
2.  使用 AddNode 安裝程式動作將節點加入到不同的子網路，並在 [叢集網路組態] 頁面確認 IP 位址資源相依性為 OR。 如需詳細資訊，請參閱[在 SQL Server 容錯移轉叢集中新增或移除節點 &#40;安裝程式&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)。  
  
#### <a name="to-upgrade-a-multi-subnet-cluster-currently-using-stretch-v-lan"></a>若要升級目前使用延展 V-Lan 的多重子網路叢集。  
  
1.  請遵循上述步驟，將您的叢集升級到 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。  
  
2.  變更網路設定，將遠端節點移到不同的子網路。  
  
3.  使用 Windows 容錯移轉叢集管理工具，為新的子網路加入新的 IP 位址，並將 IP 位址資源相依性設定為 OR。  
  
## <a name="next-steps"></a>後續步驟  
 在升級為 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]之後，請完成下列工作：  
  
-   [完成資料庫引擎升級](../../../database-engine/install-windows/complete-the-database-engine-upgrade.md)  
  
-   [變更資料庫相容性模式並使用查詢存放區](../../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)  
  
-   [善用新的 SQL Server 2016 功能](http://msdn.microsoft.com/library/d8879659-8efa-4442-bcbb-91272647ae16)  
  
## <a name="see-also"></a>另請參閱  
 [升級 SQL Server 容錯移轉叢集執行個體](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)   
 [檢視與讀取 SQL Server 安裝程式記錄檔](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [將功能加入 SQL Server 2016 的執行個體 &#40;安裝程式&#41;](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)  
  
  
