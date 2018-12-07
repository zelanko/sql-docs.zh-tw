---
title: 設定原生模式報表伺服器向外延展部署 | Microsoft Docs
ms.date: 11/29/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], deployments
- deploying [Reporting Services], scale-out deployment model
- scale-out deployments [Reporting Services]
ms.assetid: b30d0308-4d9b-4f85-9f83-dece4dcb2775
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a0e990b52a9433f959288dcf2e3518f85b8a6f67
ms.sourcegitcommit: c7febcaff4a51a899bc775a86e764ac60aab22eb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/30/2018
ms.locfileid: "52710639"
---
# <a name="configure-a-native-mode-report-server-scale-out-deployment"></a>設定原生模式報表伺服器向外延展部署

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE [ssrs-appliesto-pbirs](../../includes/ssrs-appliesto-pbirs.md)]

Reporting Services 原生模式支援向外延展部署模型，它可讓您在執行多個報表伺服器執行個體時共用單一報表伺服器資料庫。 向外延展部署是用來提高報表伺服器的延展性，以便處理更多的並行使用者及更大量的報表執行負載。 它也可以給特定伺服器專用，以處理互動式或已排程的報表。

若為 Power BI 報表伺服器，您需要在負載平衡器上針對所有向外延展環境設定用戶端親和性 (有時稱為黏性工作階段)，以確保適當的效能。  
  
若為 SQL Server 2016 Reporting Services 和更早版本，SharePoint 模式報表伺服器會利用 SharePoint 產品基礎結構進行向外延展。SharePoint 模式向外延展是透過將其他 SharePoint 模式報表伺服器加入至 SharePoint 伺服器陣列來執行。 如需 SharePoint 模式中向外延展的資訊，請參閱[將其他報表伺服器新增至伺服器陣列 &#40;SSRS 向外延展&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)。  
 
  *「向外延展部署」* (Scale-out Deployment) 的使用案例如下：  
  
-   這是讓伺服器叢集內的多部報表伺服器負載平衡的必要條件。 在您可以讓多部報表伺服器負載平衡之前，您必須先設定這些伺服器，讓它們共用相同的報表伺服器資料庫。  
  
-   若要在不同的電腦上分割報表伺服器應用程式，則使用一部伺服器來處理互動式報表，並使用另一部伺服器來處理已排程報表。 在此狀況下，每一個伺服器執行個體都會針對共用報表伺服器資料庫內儲存的相同報表伺服器內容來處理不同類型的要求。  
  
 **向外延展部署是由以下項目所組成：**  
  
-   共用單一報表伺服器資料庫的兩個或多個報表伺服器執行個體。  
  
-   選擇性的網路負載平衡 (NLB) 叢集，以便將互動式使用者負載散佈在不同的報表伺服器執行個體之間。  
  
 如果您在 NLB 叢集上設定 Reporting Services，您需要確定 NLB 虛擬伺服器名稱用於報表伺服器 URL 的組態中，而且伺服器設定為可共用相同的檢視狀態。  
  
 Reporting Services 不會參與 Microsoft Cluster Services 叢集。 但是，您可以在屬於容錯移轉叢集之一部分的 Database Engine 執行個體上建立報表伺服器資料庫。  
  
 **若要規劃、安裝及設定向外延展部署，請遵循以下步驟：**  
  
-   如需如何安裝報表伺服器執行個體的指示，請檢閱[從安裝精靈 &#40;安裝程式&#41; 安裝 SQL Server](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)。  
  
-   如果您打算在網路負載平衡 (NLB) 叢集上主控向外延展部署，您應該先設定 NLB 叢集，然後再設定向外延展部署。 如需詳細資訊，請參閱 [在網路負載平衡叢集上設定報表伺服器](../../reporting-services/report-server/configure-a-report-server-on-a-network-load-balancing-cluster.md)。  
  
-   如需如何共用報表伺服器資料庫以及將報表伺服器加入向外延展的指示，請檢閱本主題中的程序。  
  
     下列程序說明如何設定兩個節點之報表伺服器的向外延展部署。 請重複本主題所述的步驟，將其他報表伺服器節點加入部署中。  
  
    -   使用安裝程式可安裝將要加入向外延展部署的每一個報表伺服器執行個體。  
  
         若要避免在將伺服器執行個體連接到共用資料庫時發生資料庫相容錯誤，請確定所有的執行個體都是相同的版本。 例如，如果您使用 SQL Server 2016 報表伺服器執行個體來建立報表伺服器資料庫，則相同部署中的所有其他執行個體也都必須為 SQL Server 2016。  
  
    -   使用 Reporting Services 組態管理員可將每一部報表伺服器連接到共用資料庫。 您一次只能連接並設定一個報表伺服器。  
  
    -   使用 Reporting Services 組態工具可完成向外延展，其方式是將新的報表伺服器執行個體加入已經連接至報表伺服器資料庫的第一個報表伺服器執行個體。  
  
## <a name="to-install-a-sql-server-instance-to-host-the-report-server-databases"></a>安裝 SQL Server 執行個體以便主控報表伺服器資料庫  
  
1.  在即將主控報表伺服器資料庫的電腦上安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 您至少要安裝 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
2.  如有需要，請針對遠端連接啟用報表伺服器。 某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本預設並不會啟用遠端 TCP/IP 和具名管道連接。 若要確認是否允許遠端連接，請使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員並檢視目標執行個體的網路組態設定。 如果遠端執行個體也是具名執行個體，請確認 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務已啟用，而且在目標伺服器上執行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務提供了用來連接具名執行個體的通訊埠編號。 

## <a name="service-accounts"></a>服務帳戶

用於 Reporting Services 執行個體的服務帳戶在處理向外延展部署時很重要。 您應該在部署 Reporting Services 執行個體時，執行下列其中一項。

**選項 1：** 所有 Reporting Services 執行個體都應該設定為使用服務帳戶的相同網域使用者帳戶。

**選項 2：** 每個服務帳戶不論是否為網域帳戶，都必須授與主控 ReportServer 目錄資料庫之 SQL Server 資料庫執行個體的 dbadmin 權限。

如果您已設定與上述兩個選項不同的設定，則可能會修改 SQL Agent 工作時發生斷斷續續的失敗。 編輯報表訂閱時，這會同時在 Reporting Services 記錄和入口網站上顯示為一個錯誤。

```
An error occurred within the report server database.  This may be due to a connection failure, timeout or low disk condition within the database.
``` 

此問題會斷斷續續發生，只有建立 SQL Agent 工作的伺服器才有權檢視、刪除或編輯該項目。 如果您未執行上述任一選項，則只有在負載平衡器將該訂閱的所有要求傳送至建立 SQL Agent 工作的伺服器時，作業才會成功。 
  
## <a name="to-install-the-first-report-server-instance"></a>若要安裝第一個報表伺服器執行個體  
  
1.  安裝屬於部署之一部分的第一個報表伺服器執行個體。 當您安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 時，請在 [報表伺服器安裝選項] 頁面上選擇 [安裝但不設定伺服器] 選項。  
  
2.  啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具。  
  
3.  設定報表伺服器 Web 服務 URL、入口網站 URL 和報表伺服器資料庫。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的[設定報表伺服器 &#40;Reporting Services 原生模式&#41;](../../reporting-services/report-server/configure-a-report-server-reporting-services-native-mode.md)。  
  
4.  確認報表伺服器可運作。 如需詳細資訊，請參閱《 [線上叢書》的](../../reporting-services/install-windows/verify-a-reporting-services-installation.md) 驗證 Reporting Services 安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="to-install-and-configure-the-second-report-server-instance"></a>若要安裝和設定第二個報表伺服器執行個體  
  
1.  執行安裝程式，將第二個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體安裝在另一部電腦上，或做為相同電腦上的具名執行個體。 當您安裝 Reporting Services 時，請在 [報表伺服器安裝選項] 頁面上選擇 [安裝但不設定伺服器] 選項。  
  
2.  啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，並連接到您剛才安裝的新執行個體。  
  
3.  請將報表伺服器連接到您用於第一個報表伺服器執行個體的相同資料庫：  
  
    1.  選取 [資料庫] 開啟 [資料庫] 頁面。  
  
    2.  選取 [變更資料庫]。  
  
    3.  選取 [選擇現有報表伺服器資料庫]。  
  
    4.  輸入主控您要使用之報表伺服器資料庫的 SQL Server Database Engine 執行個體的伺服器名稱。 這必須是您在先前的指示集內所連接的相同伺服器。  
  
    5.  選取 [測試連線]，然後選取 [下一步]。  
  
    6.  在 [報表伺服器資料庫] 中，選取您針對第一部報表伺服器所建立的資料庫，然後選取 [下一步]。 預設名稱為 ReportServer。 請勿選取 ReportServerTempDB，因為它只能在處理報表時用來儲存暫存資料。 如果資料庫清單是空的，請重複前四個步驟來建立與伺服器的連接。  
  
    7.  在 [認證] 頁面中，選取報表伺服器將用來連接到報表伺服器資料庫的帳戶類型和認證。 您可以使用與第一個報表伺服器執行個體相同的認證，或是不同的認證。 選取 **[下一步]**。  
  
    8.  選取 [摘要]，然後選取 [完成]。  
  
4.  設定報表伺服器 [Web 服務 URL]。 還不要測試 URL， 要等到報表伺服器加入向外延展部署之後，才會解析此 URL。  
  
5.  設定 [入口網站 URL]。 還不要測試此 URL 或嘗試驗證部署。 要等到報表伺服器加入向外延展部署之後，報表伺服器才可以使用。  
  
## <a name="to-join-the-second-report-server-instance-to-the-scale-out-deployment"></a>將第二個報表伺服器執行個體加入向外延展部署  
  
1.  開啟 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，並重新連接到第一個報表伺服器執行個體。 由於第一部報表伺服器已針對可回復的加密作業初始化，因此它可用來將其他報表伺服器執行個體加入向外延展部署中。  
  
2.  按一下 [向外延展部署]，開啟 [向外延展部署] 頁面。 您應該會看到兩個項目，一個項目適用於連接到報表伺服器資料庫的每一個報表伺服器執行個體。 第一個報表伺服器執行個體應該會加入， 第二部報表伺服器應該是「正在等候加入」。 如果您沒有看到類似於部署的項目，請確認您已連接到已設定及初始化來使用報表伺服器資料庫的第一部報表伺服器。  
  
     ![[向外延展部署] 頁面的局部螢幕擷取畫面](../../reporting-services/install-windows/media/scaloutscreen.gif "[向外延展部署] 頁面的局部螢幕擷取畫面")  
  
3.  在 [向外延展部署] 頁面上，選取正等候加入此部署的報表伺服器執行個體，然後選取 [加入伺服器]。  
  
    > [!NOTE]  
    >  **問題：** 嘗試將 Reporting Services 報表伺服器執行個體加入向外延展部署時，您可能會遇到像是「拒絕存取」之類的錯誤訊息。  
    >   
    >  **因應措施** ：從第一個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體備份 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 加密金鑰，然後將此金鑰還原到第二部 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器。 接著嘗試將第二部伺服器加入 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 向外延展部署。  
  
4.  您現在應該能夠確認這兩個報表伺服器執行個體都可運作。 若要確認第二個執行個體，您可以使用 Reporting Services 設定工具連線到報表伺服器，然後按一下 [Web 服務 URL] 或 [入口網站 URL]。  
  
 如果您打算在負載平衡的伺服器叢集中執行報表伺服器，還需要其他組態。 如需詳細資訊，請參閱 [在網路負載平衡叢集上設定報表伺服器](../../reporting-services/report-server/configure-a-report-server-on-a-network-load-balancing-cluster.md)。  

## <a name="next-steps"></a>後續步驟

[設定服務帳戶](https://msdn.microsoft.com/library/25000ad5-3f80-4210-8331-d4754dc217e0)   
[設定 URL](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
[建立原生模式報表伺服器資料庫](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
[設定報表伺服器 URL](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
[設定報表伺服器資料庫連線](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
[新增和移除向外延展部署的加密金鑰](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)   
[管理 Reporting Services 原生模式報表伺服器](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
