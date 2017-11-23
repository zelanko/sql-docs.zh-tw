---
title: "設定 Windows Server Update Services (WSUS) (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a10b2884-468e-41ef-bd59-8df894381254
caps.latest.revision: "41"
ms.openlocfilehash: d2b37819663009df090c76d516d629199691472c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="configure-windows-server-update-services-wsus"></a>設定 Windows Server Update Services (WSUS)
這些指示會引導您完成使用 Windows Server Update Services (WSUS) 設定精靈設定 WSUS Analytics Platform System 的步驟。 您需要將 WSUS 設定之前您可以將軟體更新套用至應用裝置。 VMM 虛擬機器應用裝置上已安裝 WSUS。  
  
如需有關如何設定 WSUS 的詳細資訊，請參閱[WSUS 的逐步安裝手冊 》](http://go.microsoft.com/fwlink/?LinkId=202417) WSUS 網站上。 設定 WSUS 之後，請參閱[下載並套用 Microsoft 更新 &#40;Analytics Platform System &#41;](download-and-apply-microsoft-updates.md)起始更新。  
  
> [!WARNING]  
> 如果您在這個設定程序期間發生任何錯誤，停止並連絡支援服務尋求協助。 不要忽略錯誤或接收錯誤之後繼續處理序中。  
  
## <a name="before-you-begin"></a>開始之前  
若要設定 WSUS 時，您需要：  
  
-   包含 Analytics Platform System 應用裝置網域系統管理員帳戶登入資訊。  
  
-   具有存取權限的 Analytics Platform System 登入**管理主控台**並檢視應用裝置狀態資訊。  
  
-   如果您打算將從上游 WSUS 伺服器而不是同步處理更新，直接從 Microsoft Update 同步處理更新，知道上游 WSUS 伺服器的 IP 位址。 請確定您上游 WSUS 伺服器設定為允許匿名連線，而且支援 SSL。  
  
-   如果您的應用裝置會使用 proxy 伺服器存取的上游伺服器或 Microsoft Update，知道 proxy 伺服器的 IP 位址。  
  
-   在大部分情況下，WSUS 需要存取應用裝置以外的伺服器。 若要支援分析平台系統 DNS 可以設定為支援的外部名稱轉寄站，要使用外部 DNS 伺服器來解析名稱 Analytics Platform System 主機和虛擬機器 (Vm) 可讓外部的這個使用案例應用裝置。 如需詳細資訊，請參閱[使用 DNS 轉寄站來解析非應用裝置的 DNS 名稱 &#40;Analytics Platform System &#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
## <a name="to-configure-windows-server-update-services-wsus"></a>若要設定 Windows Server Update Services (WSUS)  
  
1.  登入**管理主控台**。 在**應用裝置狀態**索引標籤上，確認**叢集**和**網路**資料行會顯示綠色 (或**NA**) 所有節點。 在確認所有節點的狀態指示器**應用裝置狀態**。  
  
    -   它可以安全地繼續綠色或 NA 指標。  
  
    -   評估非重大的警告 （黃色） 錯誤。 在某些情況下的警告訊息不會封鎖更新。 如果沒有非重要磁碟磁碟區錯誤不是位於 C:\ 磁碟機，您可以繼續進行下一個步驟之前解決磁碟的磁碟區錯誤。  
  
    -   大部分的紅色指示器必須解決才能繼續進行。 如果磁碟失敗，請使用**管理主控台警示**頁面，確認每個伺服器或 SAN 陣列內有一個以上的磁碟失敗。 每台伺服器或 SAN 陣列內有一個以上的磁碟失敗時，您可以繼續進行下一個步驟才能修復磁碟失敗。 請務必連絡 Microsoft 支援以儘速修正磁碟失敗。  
  
2.  應用裝置網域系統管理員身分登入 VMM 虛擬機器。  
  
3.  啟動組態精靈。  
  
    #### <a name="to-launch-the-configuration-wizard"></a>若要啟動組態精靈  
  
    1.  在**伺服器管理員儀表板**上**工具**功能表上，按一下  **Windows Server Update Services**。  
  
    2.  在左窗格中**Update Services**視窗中，按一下以展開虛擬機器管理節點伺服器 (***appliance_domain*VMM**)，然後按一下  **選項**。  
  
    3.  在**選項**] 窗格中，按一下 [ **WSUS 伺服器設定精靈**啟動組態精靈。  
  
        ![伺服器管理員儀表板功能表](./media/configure-windows-server-update-services-wsus/WSUS_Wiz0.png "WSUS_Wiz0")  
  
    4.  如果這是第一次您執行 WSUS 精靈，可能會要求您設定來儲存更新的目錄。 `C:\wsus`是適當的位置。不過，您可能會提供不同的路徑。  
  
        ![WSUS 路徑](./media/configure-windows-server-update-services-wsus/WSUS_Wiz1.png "WSUS_Wiz1")  
  
    5.  檢閱**在您開始前**完成，才能完成精靈的項目清單。  
  
        ![WSUS 開始之前](./media/configure-windows-server-update-services-wsus/WSUS_Wiz2.png "WSUS_Wiz2")  
  
    6.  在**參加 Microsoft Update 改進方案**頁面上，選取**是，我願意參加 Microsoft Update 改進方案**，然後按一下 **下一步**。  
  
        ![WSUS 改進計畫](./media/configure-windows-server-update-services-wsus/WSUS_Wiz3.png "WSUS_Wiz3")  
  
    您現在應該會看到**選擇上游伺服器**頁面。 下列螢幕擷取畫面是 「 組態精靈 」 的起點。  
  
    ![WSUS 上游伺服器同步處理](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
4.  選擇上游伺服器。  
  
    在**選擇上游伺服器**頁面上的 WSUS 設定精靈 中，您將選取的虛擬機器管理節點上的 WSUS 如何連接到上游伺服器取得軟體更新。 兩個選擇要同步處理的上游伺服器[Microsoft Update](http://go.microsoft.com/fwlink/?LinkId=133349)或另一部 Windows Server Update Services 伺服器同步處理更新。  
  
    #### <a name="to-update-by-using-microsoft-update"></a>若要使用 Microsoft Update 來更新  
  
    1.  如果您選擇使用 Microsoft Update 同步處理，您不需要進行任何變更**選擇上游伺服器**頁面。 按一下 **[下一步]**。  
  
        ![WSUS 上游伺服器同步處理](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
    #### <a name="to-update-from-another-wsus-server"></a>從另一部 WSUS 伺服器更新  
  
    1.  如果您選擇與 Microsoft 更新 （上游伺服器） 以外的來源同步處理，指定的伺服器 （輸入 IP 位址） 和連接埠的此伺服器會與上游伺服器通訊。  
  
        ![WSUS 上游伺服器同步處理，從 WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4b.png "WSUS_Wiz4b")  
  
    2.  若要使用安全通訊端層 (SSL)，選取**同步處理更新資訊時使用 SSL**核取方塊。 在此情況下的伺服器將使用連接埠 443 進行同步處理。  
  
        ![WSUS 上游伺服器同步處理，從 WSUS SSL](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4c.png "WSUS_Wiz4c")  
  
    3.  如果複本伺服器，請選取**這是上游伺服器的複本**核取方塊。 可以同時選取**同步處理更新資訊時使用 SSL**和**這是上游伺服器的複本**。  
  
        ![WSUS 上游伺服器複本](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4d.png "WSUS_Wiz4d")  
  
    4.  此時，您已完成與上游伺服器設定。 按一下**下一步**，或選取**指定 proxy 伺服器**左側的導覽窗格中。  
  
5.  指定 proxy 伺服器。  
  
    如果這個伺服器需要有 proxy 伺服器才能存取 Microsoft Update 或不同的上游伺服器，您可以設定 proxy 伺服器設定。否則，請按一下**下一步**。  
  
    ![WSUS Proxy](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5a.png "WSUS_Wiz5a")  
  
    #### <a name="to-configure-proxy-server-settings"></a>若要設定 proxy 伺服器設定  
  
    1.  在**指定 Proxy 伺服器**頁面的 組態精靈中，選取**同步處理時使用 proxy 伺服器**核取方塊，，然後輸入 proxy 伺服器 IP 位址 （不是名稱） 和連接埠號碼 （連接埠 80預設值） 對應的方塊中。  
  
    2.  如果您想要使用特定使用者認證，選取連線到 proxy 伺服器**使用使用者認證來連線至 proxy 伺服器**核取方塊，，然後輸入在對應的 使用者名稱、 網域和使用者的密碼方塊。 如果您想要啟用基本驗證的使用者連線到 proxy 伺服器，選取**允許基本驗證 （密碼會以純文字傳送）**核取方塊。  
  
        ![WSUS Proxy 認證](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5b.png "WSUS_Wiz5b")  
  
    3.  此時，您便已完成 proxy 伺服器設定。 按一下**下一步**移至下一個頁面中，您可以開始設定同步處理程序。  
  
6.  啟動連線。  
  
    ![WSUS Proxy 開始連接](./media/configure-windows-server-update-services-wsus/WSUS_Wiz6.png "WSUS_Wiz6")  
  
    按一下**開始連接**。  
  
    已成功連線之後，請按一下**下一步**移至下一個頁面中，您可以在其中選擇語言。  
  
7.  選擇語言。  
  
    選取**只下載更新這些語言**。  
  
    選取**英文**，然後按一下 **下一步**。  
  
    ![選擇語言](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseLanguages.png "SQL_Server_PDW_WSUSChooseLanguages")  
  
8.  選擇產品。  
  
    > [!NOTE]  
    > 如果您使用上游伺服器，您可能無法與選擇的產品。 如果不使用此選項，則略過此步驟。  
  
    取消選取所有選取的更新。  
  
    選取**SQL Server 2014**， **Windows Server 2012 R2**，和**System Center 2012 R2 Virtual Machine Manager**，然後按一下 **下一步**。  
  
9. 選擇分類。  
  
    > [!NOTE]  
    > 如果您使用上游伺服器，您可能無法選擇分類。  如果不使用此選項，則略過此步驟。  
  
    取消選取所有先前選取的更新。  
  
    選取**重大更新**和**安全性更新**Analytics Platform System 應用裝置中，將會同步處理，然後按一下 更新**下一步**。  
  
    ![選擇分類](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseClassifications.png "SQL_Server_PDW_WSUSChooseClassifications")  
  
10. 設定同步處理排程。  
  
    選取**手動同步處理**，然後按一下 **下一步**。  
  
    ![設定同步處理排程](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSyncSchedule.png "SQL_Server_PDW_WSUSSyncSchedule")  
  
11. 開始初始同步處理。  
  
    選取**開始初始同步處理**，然後按一下 **下一步**。  
  
12. [完成]。  
  
    按一下 **[完成]**。  
  
## <a name="bkmk_WSUSGroup"></a>群組應用裝置中的伺服器 WSUS  
為 Analytics Platform System 中設定 WSUS 之後, 的下一個步驟是群組的應用裝置伺服器。 將所有的應用裝置伺服器新增至群組，WSUS 都將能夠將軟體更新套用至應用裝置中的所有伺服器。  
  
> [!NOTE]  
> WSUS 系統被設計來以非同步方式執行。 起始活動不一定會產生立即更新。 因此，您可能需要稍待片刻，直到電腦會顯示在 [WSUS] 對話方塊。 執行`setup.exe /action=ReportMicrosoftUpdateClientStatus /DomainAdminPassword="<password>"`命令說明於主題的結尾[下載並套用 Microsoft 更新 &#40;Analytics Platform System &#41;](download-and-apply-microsoft-updates.md)可協助您重新整理的對話方塊。  
  
#### <a name="to-group-the-appliance-servers"></a>若要群組的應用裝置的伺服器  
  
1.  開啟 WSUS 主控台，以滑鼠右鍵按一下**所有電腦**，然後按一下 **新增電腦群組**。  
  
    ![新增電腦群組。] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSAddComputerGroup.png "SQL_Server_PDW_WSUSAddComputerGroup")  
  
2.  輸入電腦群組的名稱"APS"，然後按一下**新增**。  
  
    ![輸入新的電腦群組的名稱。] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSpecifyGroupName.png "SQL_Server_PDW_WSUSSpecifyGroupName")  
  
3.  按一下**所有電腦**同樣地，變更中的狀態**狀態**下拉式功能表來**任何**，然後按一下 **重新整理**。 您可能需要展開**所有電腦**才能看到新的群組按一下左邊樹狀目錄控制項上您剛才加入。  
  
    ![狀態變更為任何並按一下 重新整理。] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusToAny.png "SQL_Server_PDW_WSUSChangeStatusToAny")  
  
4.  選取 所有電腦，以及該應用裝置、 按一下滑鼠右鍵，然後按一下**變更成員資格**。  
  
    ![變更所有 PDW 電腦的成員資格。] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeMembership.png "SQL_Server_PDW_WSUSChangeMembership")  
  
5.  選取新的電腦群組，而按一下核取方塊，然後按一下建立**確定**。  
  
    ![設定電腦群組成員資格](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSetComputerGroupMembership.png "SQL_Server_PDW_WSUSSetComputerGroupMembership")  
  
6.  選取新的電腦群組，變更其**狀態**至**任何**，然後按一下 **重新整理**。 應該現在指派給此群組並在右窗格中列出的所有電腦。 通常安全地繼續時，節點會顯示警告，例如**此節點還沒有回報狀態**。  
  
    ![狀態變更為任何並按一下 重新整理。] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusAnyRefresh.png "SQL_Server_PDW_WSUSChangeStatusAnyRefresh")  
  
