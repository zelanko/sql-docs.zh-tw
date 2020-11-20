---
title: 設定 WSUS
description: 這些指示會逐步引導您完成使用 Windows Server Update Services (WSUS) Configuration Wizard 設定 WSUS for Analytics Platform System 的步驟。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 06ac0126bb12668654c04e6a82b20ca551dd925e
ms.sourcegitcommit: a49a66dbda0cb16049e092b49c8318ac3865af3c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2020
ms.locfileid: "94983054"
---
# <a name="configure-windows-server-update-services-wsus-in-analytics-platform-system"></a>在 Analytics Platform System 中設定 Windows Server Update Services (WSUS) 
這些指示會逐步引導您完成使用 Windows Server Update Services (WSUS) Configuration Wizard 設定 WSUS for Analytics Platform System 的步驟。 您必須先設定 WSUS，才能將軟體更新套用至設備。 WSUS 已安裝在設備的 VMM 虛擬機器上。  
  
如需有關設定 WSUS 的詳細資訊，請參閱 WSUS 網站上的 [Wsus 逐步安裝指南](/windows/deployment/deploy-whats-new) 。 設定 WSUS 之後，請參閱 [下載並套用 Microsoft Updates &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md) 以起始更新。  
  
> [!WARNING]  
> 如果您在此設定過程中遇到任何錯誤，請停止並聯絡支援人員以取得協助。 在收到錯誤之後，請勿忽略錯誤或繼續處理。  
  
## <a name="before-you-begin"></a>開始之前  
若要設定 WSUS，您需要：  
  
-   擁有 Analytics Platform System 設備的網域系統管理員帳戶登入資訊。  
  
-   擁有具有存取 **管理主控台** 和查看設備狀態資訊之許可權的 Analytics Platform System 登入。  
  
-   如果您打算從上游 WSUS 伺服器同步處理更新，而不是直接從 Microsoft Update 同步處理更新，請知道上游 WSUS 伺服器的 IP 位址。 請確定您的上游 WSUS 伺服器已設定為允許匿名連線，並支援 SSL。  
  
-   如果您的設備將使用 proxy 伺服器來存取上游伺服器或 Microsoft Update，請知道 proxy 伺服器的 IP 位址。  
  
-   在大多數情況下，WSUS 需要存取設備以外的伺服器。 為了支援此使用案例，可將 Analytics Platform System DNS 設定為支援外部名稱轉寄站，讓分析平臺系統主機和虛擬機器 (Vm) 使用外部 DNS 伺服器來解析設備以外的名稱。 如需詳細資訊，請參閱 [使用 DNS 轉寄站來解析非設備 DNS 名稱 &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)。  
  
## <a name="to-configure-windows-server-update-services-wsus"></a>設定 Windows Server Update Services (WSUS)   
  
1.  登入 **管理主控台**。 在 [**設備狀態**] 索引標籤上，確認 [叢集] 和 [**網路**] 資料行顯示所有 **節點的綠色** (或 **NA**) 。 確認 **設備狀態** 上所有節點的狀態指示器。  
  
    -   您可以安全地繼續使用綠色或 NA 指標。  
  
    -   評估非關鍵性的 (黃色) 警告錯誤。 在某些情況下，警告訊息不會封鎖更新。 如果有非重大磁片區錯誤，不在 C：\ 上磁片磁碟機，您可以在解決磁片區錯誤之前繼續進行下一個步驟。  
  
    -   大部分的紅色指標都必須先解決才能繼續。 如果發生磁片失敗，請使用 [ **管理主控台警示** ] 頁面來確認每個伺服器或 SAN 陣列內不會有一個以上的磁片失敗。 如果每個伺服器或 SAN 陣列中沒有一個以上的磁片故障，您可以在修正磁片失敗之前繼續進行下一個步驟。 請務必聯絡 Microsoft 支援服務，儘快修正磁片失敗。  
  
2.  以設備網域系統管理員身分登入 VMM 虛擬機器。  
  
3.  啟動設定 wizard。  
  
    #### <a name="to-launch-the-configuration-wizard"></a>啟動設定向導  
  
    1.  在 **伺服器管理員的儀表板** 中，按一下 [ **工具** ] 功能表上的 [ **Windows Server Update Services**]。  
  
    2.  在 [ **Update Services** ] 視窗的左窗格中，按一下以展開 [虛擬機器管理] 節點伺服器 (**_appliance_domain_-VMM**) ，然後按一下 [**選項**]。  
  
    3.  在 [ **選項** ] 窗格中，按一下 [ **WSUS 伺服器設定向導]** ，以啟動 [設定向導]。  
  
        ![伺服器管理員儀表板功能表](./media/configure-windows-server-update-services-wsus/WSUS_Wiz0.png "WSUS_Wiz0")  
  
    4.  如果這是您第一次執行 WSUS wizard，系統可能會要求您設定用來儲存更新的目錄。 `C:\wsus` 是適當的位置;不過，您可以提供不同的路徑。  
  
        ![WSUS 路徑](./media/configure-windows-server-update-services-wsus/WSUS_Wiz1.png "WSUS_Wiz1")  
  
    5.  在您完成嚮導之前，請先查看要完成的專案清單，再 **開始** 進行。  
  
        ![WSUS 開始之前](./media/configure-windows-server-update-services-wsus/WSUS_Wiz2.png "WSUS_Wiz2")  
  
    6.  在 [ **加入 Microsoft Update 改進計畫** ] 頁面上，選取 **[是，我要加入 Microsoft Update 改進計畫]**，然後按一下 **[下一步]**。  
  
        ![WSUS 改進計畫](./media/configure-windows-server-update-services-wsus/WSUS_Wiz3.png "WSUS_Wiz3")  
  
    您現在應該會看到 [ **選擇上游伺服器** ] 頁面。 下列螢幕擷取畫面是 configuration wizard 的起點。  
  
    ![WSUS 上游伺服器同步處理](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
4.  選擇上游伺服器。  
  
    在 WSUS 設定向導的 [ **選擇上游伺服器** ] 頁面上，您將選取 [虛擬機器管理] 節點上的 WSUS 將如何連線到上游伺服器以取得軟體更新。 您的兩個選擇是將上游伺服器與 [Microsoft Update](https://go.microsoft.com/fwlink/?LinkId=133349) 同步處理，或與另一個 Windows Server Update Services 伺服器同步處理更新。  
  
    #### <a name="to-update-by-using-microsoft-update"></a>若要使用 Microsoft Update 進行更新  
  
    1.  如果您選擇與 Microsoft Update 同步處理，則不需要對 [ **選擇上游伺服器** ] 頁面進行任何變更。 按 [下一步] 。  
  
        ![WSUS 上游伺服器同步處理](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
    #### <a name="to-update-from-another-wsus-server"></a>若要從另一部 WSUS 伺服器更新  
  
    1.  如果您選擇與 Microsoft Update (上游伺服器) 的來源進行同步處理，請指定伺服器 (輸入 IP 位址) 以及此伺服器將與上游伺服器通訊的埠。  
  
        ![WSUS 上游伺服器從 WSUS 同步處理](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4b.png "WSUS_Wiz4b")  
  
    2.  若要使用安全通訊端層 (SSL) ，請選取 [ **同步處理更新資訊時使用 SSL** ] 核取方塊。 在此情況下，伺服器將會使用埠443進行同步處理。  
  
        ![WSUS 上游伺服器從 WSUS SSL 同步處理](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4c.png "WSUS_Wiz4c")  
  
    3.  如果這是複本伺服器，選取 [這是上游伺服器的複本] 核取方塊。 您可以選取 [同步處理 **更新資訊時使用 SSL** ]， **這是上游伺服器的複本**。  
  
        ![WSUS 上游伺服器複本](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4d.png "WSUS_Wiz4d")  
  
    4.  到目前為止，您已完成上游伺服器設定。 按 **[下一步**]，或選取左側導覽窗格中的 [ **指定 proxy 伺服器** ]。  
  
5.  指定 proxy 伺服器。  
  
    如果這部伺服器需要 proxy 伺服器才能存取 Microsoft Update 或不同的上游伺服器，您可以在這裡設定 proxy 伺服器設定;否則，請按 **[下一步]**。  
  
    ![WSUS Proxy](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5a.png "WSUS_Wiz5a")  
  
    #### <a name="to-configure-proxy-server-settings"></a>進行 Proxy 伺服器設定  
  
    1.  在 [設定] 的 [ **指定 Proxy 伺服器** ] 頁面上，選取 [ **同步處理時使用 proxy 伺服器** ] 核取方塊，然後在對應的方塊中輸入 (不是) 的 proxy 伺服器 IP 位址和埠號碼 (埠) 80。  
  
    2.  如果您想要使用特定使用者認證連線到 Proxy 伺服器，選取 [使用使用者認證連線到 Proxy 伺服器] 核取方塊，然後在對應的方塊中輸入使用者名稱、網域和使用者密碼。 如果您想要為連線到 proxy 伺服器的使用者啟用基本驗證，請選取 [ **允許基本驗證 (密碼以純文字傳送)** ] 核取方塊。  
  
        ![WSUS Proxy 認證](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5b.png "WSUS_Wiz5b")  
  
    3.  到目前為止，您已完成 proxy 伺服器設定。 按 [下一步] 前往下一個頁面，開始設定同步處理程序。  
  
6.  開始連接。  
  
    ![WSUS Proxy 開始連接](./media/configure-windows-server-update-services-wsus/WSUS_Wiz6.png "WSUS_Wiz6")  
  
    按一下 [ **開始連接**]。  
  
    連接成功後，請按 **[下一步** ] 前往下一個頁面，您可以在其中選擇語言。  
  
7.  選擇語言。  
  
    選取 [ **只下載下列語言的更新**]。  
  
    選取 [ **英文**]，然後按 **[下一步]**。  
  
    ![選取語言](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseLanguages.png "SQL_Server_PDW_WSUSChooseLanguages")  
  
8.  選擇 [產品]。  
  
    > [!NOTE]  
    > 如果您使用上游伺服器，可能無法選擇產品。 如果無法使用此選項，請略過此步驟。

    > [!WARNING]  
    > 請排除任何 SQL Server 2016 更新。
  
    取消選取所有選取的更新。  
  
    選取 **SQL Server 2012**、 **SQL Server 2014**、 **Windows Server 2012 R2**、 **System Center 2012 R2-Virtual Machine Manager**、 **Windows Server 2016** 和 **System center 2016-Virtual Machine Manager** 然後按 **[下一步]**。  
  
9. 選擇 [分類]。  
  
    > [!NOTE]  
    > 如果您使用上游伺服器，可能無法選擇分類。  如果無法使用此選項，請略過此步驟。  
  
    取消選取所有先前選取的更新。  
  
    針對將針對分析平臺系統裝置同步處理的更新，選取 **重大更新**、 **安全性更新** 和 **更新彙總套件** ，然後按 **[下一步]**。  
  
    ![選擇分類](./media/configure-windows-server-update-services-wsus/sql-server-pdw-wsus-choose-classifications.png "sql-伺服器-pdw-wsus-選擇分類")  
  
10. 設定同步處理排程。  
  
    選取 [ **手動同步處理**]，然後按一下 **[下一步]**。  
  
    ![設定同步處理排程](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSyncSchedule.png "SQL_Server_PDW_WSUSSyncSchedule")  
  
11. 開始初始同步處理。  
  
    選取 [ **開始初始同步** 處理]，然後按一下 **[下一步]**。  
  
12. [完成]。  
  
    按一下 [完成] 。  
  
## <a name="group-the-appliance-servers-in-wsus"></a><a name="bkmk_WSUSGroup"></a>在 WSUS 中將設備伺服器分組  
設定 WSUS for Analytics Platform System 之後，下一步就是將設備伺服器分組。 藉由將所有的設備伺服器新增到群組中，WSUS 將能夠將軟體更新套用至設備中的所有伺服器。  
  
> [!NOTE]  
> WSUS 系統是設計來以非同步方式執行。 起始活動不一定會產生立即更新。 因此，您可能需要等候一段時間，才會在 WSUS 對話方塊中看到電腦。 執行 `setup.exe /action=ReportMicrosoftUpdateClientStatus /DomainAdminPassword="<password>"` 主題結尾所述的命令 [，將 Microsoft Updates &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md) 可協助重新整理對話方塊。  
  
#### <a name="to-group-the-appliance-servers"></a>將設備伺服器分組  
  
1.  開啟 WSUS 主控台，在 [ **所有電腦** ] 上按一下滑鼠右鍵，然後按一下 [ **新增電腦群組**]。  
  
    ![加入電腦群組。](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSAddComputerGroup.png "SQL_Server_PDW_WSUSAddComputerGroup")  
  
2.  輸入電腦群組的「AP」名稱，然後按一下 [ **新增**]。  
  
    ![輸入新電腦群組的名稱。](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSpecifyGroupName.png "SQL_Server_PDW_WSUSSpecifyGroupName")  
  
3.  再次按一下 [**所有電腦**]，將 [**狀態**] 下拉式功能表中的狀態變更為 [**任何**]，然後按一下 [重新整理 **]。** 您可能需要展開 **所有電腦** ，方法是在左邊的樹狀目錄控制項上按一下該電腦，以查看您剛加入的新群組。  
  
    ![將狀態變更為 [任何]，然後按一下 [重新整理]。](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusToAny.png "SQL_Server_PDW_WSUSChangeStatusToAny")  
  
4.  選取屬於設備的所有電腦、按一下滑鼠右鍵，然後按一下 [ **變更成員資格**]。  
  
    ![變更所有 PDW 電腦的成員資格。](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeMembership.png "SQL_Server_PDW_WSUSChangeMembership")  
  
5.  按一下核取方塊，然後按一下 **[確定]**，以選取您所建立的新電腦群組。  
  
    ![設定電腦群組成員資格](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSetComputerGroupMembership.png "SQL_Server_PDW_WSUSSetComputerGroupMembership")  
  
6.  選取新的電腦群組，將其 **狀態** 變更為 [ **任何**]， **然後按一下 [** 重新整理]。 所有電腦現在都應該指派給這個群組，然後在右窗格中列出。 當節點顯示警告時（例如 **這個節點尚未回報狀態**），通常可以安全地繼續。  
  
    ![將狀態變更為 [任何]，然後按一下 [重新整理]。](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusAnyRefresh.png "SQL_Server_PDW_WSUSChangeStatusAnyRefresh")  
