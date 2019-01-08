---
title: 設定 WSUS-Analytics Platform System |Microsoft Docs
description: 這些指示會引導您完成使用 Windows Server Update Services (WSUS) 組態精靈設定 WSUS Analytics Platform System 的步驟。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2d1e07fca7c18bdecba265a9e69994a9f728e9ba
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52398613"
---
# <a name="configure-windows-server-update-services-wsus-in-analytics-platform-system"></a>Analytics Platform System 中設定 Windows Server Update Services (WSUS)
這些指示會引導您完成使用 Windows Server Update Services (WSUS) 組態精靈設定 WSUS Analytics Platform System 的步驟。 您需要將 WSUS 設定，才能將軟體更新套用至應用裝置。 VMM 虛擬機器的應用裝置上已安裝 WSUS。  
  
如需有關如何設定 WSUS 的詳細資訊，請參閱 < [WSUS 逐步安裝手冊 》](https://go.microsoft.com/fwlink/?LinkId=202417) WSUS 網站上。 設定 WSUS 之後，請參閱[下載並套用 Microsoft 更新&#40;Analytics Platform System&#41; ](download-and-apply-microsoft-updates.md)起始更新。  
  
> [!WARNING]  
> 如果您在此組態程序期間發生任何錯誤，停止並連絡支援服務尋求協助。 不要忽略錯誤或繼續處理序中之後會收到錯誤。  
  
## <a name="before-you-begin"></a>開始之前  
若要將 WSUS 設定，您需要：  
  
-   有 Analytics Platform System appliance 網域系統管理員帳戶登入資訊。  
  
-   已經具有存取權限的 Analytics Platform System 登入**管理主控台**並檢視應用裝置狀態資訊。  
  
-   如果您打算從上游 WSUS 伺服器而不是同步處理更新，直接從 Microsoft Update 同步處理更新，請了解上游 WSUS 伺服器的 IP 位址。 確定您的上游 WSUS 伺服器設定為允許匿名連線，而且支援 SSL。  
  
-   如果您的應用裝置會使用 proxy 伺服器存取的上游伺服器或 Microsoft Update，知道 proxy 伺服器的 IP 位址。  
  
-   在大部分情況下，WSUS 需要存取外部應用裝置的伺服器。 若要支援 Analytics Platform System DNS 可以設定為支援可讓 Analytics Platform System 主機和虛擬機器 (Vm)，若要使用外部 DNS 伺服器來解析名稱的外部名稱轉寄站外部的這個使用案例應用裝置。 如需詳細資訊，請參閱 <<c0> [ 使用 DNS 轉寄站解析非設備 DNS 名稱&#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)。</c0>  
  
## <a name="to-configure-windows-server-update-services-wsus"></a>若要設定 Windows Server Update Services (WSUS)  
  
1.  登入**管理主控台**。 上**設備狀態**索引標籤上，確認**叢集**並**網路**資料行會顯示綠色 (或**NA**) 的所有節點。 在確認所有節點的狀態指示器**設備狀態**。  
  
    -   它可以安全地繼續進行 綠色 或 NA 標記。  
  
    -   評估非重大的警告 （黃色） 錯誤。 在某些情況下的警告訊息不會封鎖更新。 如果沒有不在 C:\ 磁碟機的非重要磁碟的磁碟區錯誤，您可以繼續下一個步驟之前解決磁碟的磁碟區時發生錯誤。  
  
    -   繼續之前，必須先解決大部分的紅色指示器。 如果磁碟失敗，請使用**系統管理員主控台警示**頁面，確認每個伺服器或 SAN 陣列內的一個以上的磁碟失敗。 如果有一個以上的磁碟失敗，每個伺服器或 SAN 陣列內，您可以繼續下一個步驟之前修正磁碟失敗。 請務必連絡 Microsoft 支援服務，以儘速修正磁碟失敗。  
  
2.  設備網域系統管理員身分登入 VMM 虛擬機器。  
  
3.  啟動組態精靈。  
  
    #### <a name="to-launch-the-configuration-wizard"></a>若要啟動組態精靈  
  
    1.  在 **伺服器管理員儀表板**上**工具**功能表上，按一下  **Windows Server Update Services**。  
  
    2.  在左窗格中**Update Services**視窗中，按一下以展開虛擬機器管理節點伺服器 (***appliance_domain *-VMM**)，然後按一下**選項**。  
  
    3.  在 **選項** 窗格中，按一下**WSUS 伺服器設定精靈**啟動組態精靈。  
  
        ![伺服器管理員儀表板功能表](./media/configure-windows-server-update-services-wsus/WSUS_Wiz0.png "WSUS_Wiz0")  
  
    4.  如果這是第一次您執行的 WSUS 精靈 中，可能會要求您設定儲存更新的目錄。 `C:\wsus` 是適當的位置;不過，您可能會提供不同的路徑。  
  
        ![WSUS 路徑](./media/configure-windows-server-update-services-wsus/WSUS_Wiz1.png "WSUS_Wiz1")  
  
    5.  檢閱**在您開始前**完成，才能完成精靈 的項目清單。  
  
        ![WSUS 開始之前](./media/configure-windows-server-update-services-wsus/WSUS_Wiz2.png "WSUS_Wiz2")  
  
    6.  在 [**參加 Microsoft Update 改進方案**頁面上，選取**是，我想要參加 Microsoft Update 改進方案**，然後按一下**下一步]**。  
  
        ![WSUS 改進計畫](./media/configure-windows-server-update-services-wsus/WSUS_Wiz3.png "WSUS_Wiz3")  
  
    您現在應該會看到**選擇上游伺服器**頁面。 下列螢幕擷取畫面是 「 組態精靈 」 的起點。  
  
    ![WSUS 上游伺服器同步處理](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
4.  選擇上游伺服器。  
  
    在 **選擇上游伺服器**頁面的 WSUS 設定精靈 中，您將選取的虛擬機器管理節點上的 WSUS 如何連接到上游伺服器來取得軟體更新。 您的兩個選擇要同步處理的上游伺服器[Microsoft Update](https://go.microsoft.com/fwlink/?LinkId=133349)或另一部 Windows Server Update Services 伺服器同步處理更新。  
  
    #### <a name="to-update-by-using-microsoft-update"></a>使用 Microsoft Update 來更新  
  
    1.  如果您選擇與 Microsoft Update 同步處理，您不需要進行任何變更**選擇上游伺服器**頁面。 按 [下一步] 。  
  
        ![WSUS 上游伺服器同步處理](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
    #### <a name="to-update-from-another-wsus-server"></a>若要從另一部 WSUS 伺服器更新  
  
    1.  如果您選擇與 Microsoft Update （上游伺服器） 以外的來源同步處理，指定的伺服器 （輸入 IP 位址） 和連接埠此伺服器會與上游伺服器通訊。  
  
        ![WSUS 上游伺服器同步處理，從 WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4b.png "WSUS_Wiz4b")  
  
    2.  若要使用 Secure Sockets Layer (SSL)，請選取**同步處理更新資訊時使用 SSL**核取方塊。 在此情況下伺服器會使用連接埠 443 進行同步處理。  
  
        ![WSUS 上游伺服器同步處理，從 WSUS SSL](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4c.png "WSUS_Wiz4c")  
  
    3.  如果這是複本伺服器，請選取**這是上游伺服器的複本**核取方塊。 可以同時選取**同步處理更新資訊時使用 SSL**並**這是上游伺服器的複本**。  
  
        ![WSUS 上游伺服器複本](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4d.png "WSUS_Wiz4d")  
  
    4.  此時，您已完成與上游伺服器設定。 按一下 **下一步**，或選取**指定 proxy 伺服器**左側的導覽窗格中。  
  
5.  指定 proxy 伺服器。  
  
    如果這個伺服器需要 proxy 伺服器來存取 Microsoft Update 或不同的上游伺服器，您可以設定 proxy 伺服器設定否則，請按一下**下一步**。  
  
    ![WSUS Proxy](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5a.png "WSUS_Wiz5a")  
  
    #### <a name="to-configure-proxy-server-settings"></a>若要設定 proxy 伺服器設定  
  
    1.  在 [**指定 Proxy 伺服器**組態精靈]，選取頁面**同步處理時使用 proxy 伺服器**核取方塊，，然後輸入 proxy 伺服器 IP 位址 （不是名稱） 和連接埠號碼 （連接埠 80預設值） 對應的方塊中。  
  
    2.  如果您想要使用特定的使用者認證，選取連線到 proxy 伺服器**使用使用者認證來連線到 proxy 伺服器**核取方塊，，然後輸入在對應的 使用者名稱、 網域和使用者的密碼方塊。 如果您想要為連線到 proxy 伺服器，選取的使用者啟用基本驗證**允許基本驗證 （密碼會以純文字傳送）** 核取方塊。  
  
        ![WSUS Proxy 認證](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5b.png "WSUS_Wiz5b")  
  
    3.  此時，您已完成與 proxy 伺服器設定。 按一下 [**下一步]** 移至下一個頁面中，您可以開始設定同步處理程序。  
  
6.  開始連接。  
  
    ![WSUS Proxy 開始連接](./media/configure-windows-server-update-services-wsus/WSUS_Wiz6.png "WSUS_Wiz6")  
  
    按一下 **開始連接**。  
  
    已成功建立連接之後，請按一下**下一步**移至下一個頁面中，您可以在其中選擇語言。  
  
7.  選擇語言。  
  
    選取 **僅以這些語言下載更新**。  
  
    選取 [**英文**，然後按一下**下一步]**。  
  
    ![選擇語言](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseLanguages.png "SQL_Server_PDW_WSUSChooseLanguages")  
  
8.  選擇產品。  
  
    > [!NOTE]  
    > 如果您使用的上游伺服器，您可能無法選擇產品。 如果不使用此選項，則略過此步驟。  
  
    取消選取所有選取的更新。  
  
    選取 [ **Windows Server 2012 R2**，並**System Center 2012 R2-Virtual Machine Manager**，然後按一下**下一步]**。  
  
9. 選擇 [分類]。  
  
    > [!NOTE]  
    > 如果您使用的上游伺服器，您可能無法選擇分類。  如果不使用此選項，則略過此步驟。  
  
    取消選取所有先前選取的更新。  
  
    選取 [**重大更新**並**安全性更新**之更新的 Analytics Platform System 設備，將會同步處理，然後按一下**下一步]**。  
  
    ![選擇分類](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseClassifications.png "SQL_Server_PDW_WSUSChooseClassifications")  
  
10. 設定同步處理排程。  
  
    選取 [**手動同步處理**，然後按一下**下一步]**。  
  
    ![設定同步處理排程](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSyncSchedule.png "SQL_Server_PDW_WSUSSyncSchedule")  
  
11. 開始初始同步處理。  
  
    選取 [**開始初始同步處理**，然後按一下**下一步]**。  
  
12. 完成。  
  
    按一下 **[完成]**。  
  
## <a name="bkmk_WSUSGroup"></a>群組在 WSUS 中的應用裝置伺服器  
之後您可以設定 WSUS 的 Analytics Platform System 下, 一個步驟是設備伺服器分組。 將所有的設備伺服器新增至群組，WSUS 都將能夠將軟體更新套用至應用裝置中的所有伺服器。  
  
> [!NOTE]  
> WSUS 系統被設計來以非同步方式執行。 起始活動不一定會產生立即更新。 因此，您可能需要稍待片刻，直到電腦將會顯示在 [WSUS] 對話方塊。 執行`setup.exe /action=ReportMicrosoftUpdateClientStatus /DomainAdminPassword="<password>"`命令在本主題結尾所述[下載並套用 Microsoft 更新&#40;Analytics Platform System&#41; ](download-and-apply-microsoft-updates.md)可協助重新整理的對話方塊。  
  
#### <a name="to-group-the-appliance-servers"></a>將設備伺服器  
  
1.  開啟 WSUS 主控台，以滑鼠右鍵按一下**的所有電腦**，然後按一下**新增電腦群組**。  
  
    ![新增電腦群組。](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSAddComputerGroup.png "SQL_Server_PDW_WSUSAddComputerGroup")  
  
2.  輸入電腦群組中，名稱"AP"，然後按一下**新增**。  
  
    ![輸入新電腦群組的名稱。](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSpecifyGroupName.png "SQL_Server_PDW_WSUSSpecifyGroupName")  
  
3.  按一下 **所有電腦**同樣地，變更中的狀態**狀態**下拉式選單來**任何**，然後按一下**重新整理**。 您可能需要展開**的所有電腦**才能看到新的群組左側的樹狀結構控制項上按一下您剛才加入。  
  
    ![將狀態變更為任何，然後按一下 重新整理。](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusToAny.png "SQL_Server_PDW_WSUSChangeStatusToAny")  
  
4.  選取屬於組件，以及與應用裝置、 按一下滑鼠右鍵，然後按一下 所有電腦**變更成員資格**。  
  
    ![變更所有 PDW 電腦的成員資格。](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeMembership.png "SQL_Server_PDW_WSUSChangeMembership")  
  
5.  選取您按一下核取方塊，然後按一下所建立的新電腦群組**確定**。  
  
    ![設定電腦群組成員資格](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSetComputerGroupMembership.png "SQL_Server_PDW_WSUSSetComputerGroupMembership")  
  
6.  選取新的電腦群組，變更其**狀態**要**任何**，然後按一下**重新整理**。 應該現在指派給此群組並在右窗格中列出的所有電腦。 它是通常可以放心繼續進行時節點會顯示警告訊息，例如**此節點還沒有回報狀態**。  
  
    ![將狀態變更為任何，然後按一下 重新整理。](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusAnyRefresh.png "SQL_Server_PDW_WSUSChangeStatusAnyRefresh")  
  
