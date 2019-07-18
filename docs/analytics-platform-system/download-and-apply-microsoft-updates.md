---
title: 下載 Microsoft Updates-Analytics Platform System |Microsoft Docs
description: 本主題討論如何以 Windows Server Update Services (WSUS) 從 Microsoft Update Catalog 下載更新，並將這些更新套用至 Analytics Platform System appliance 伺服器。 Microsoft Update 會安裝所有適用的更新，適用於 Windows 和 SQL Server。 VMM 虛擬機器的應用裝置上安裝 WSUS。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 78da7bd46282bb42bc3630c71c1cafd1ea0f11bc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961042"
---
# <a name="download-and-apply-microsoft-updates-for-analytics-platform-system"></a>下載並套用 Analytics Platform System 的 Microsoft 更新
本主題討論如何以 Windows Server Update Services (WSUS) 從 Microsoft Update Catalog 下載更新，並將這些更新套用至 Analytics Platform System appliance 伺服器。 Microsoft Update 會安裝所有適用的更新，適用於 Windows 和 SQL Server。 VMM 虛擬機器的應用裝置上安裝 WSUS。  
  
## <a name="TOP"></a>開始之前  
  
> [!WARNING]  
> 請勿嘗試套用更新，如果您的設備或簽訂任何設備元件已關閉或處於容錯移轉狀態。 在此情況下，連絡支援服務尋求協助。  
>   
> 設備在使用中時，請不要套用 Microsoft 更新。 套用更新，可能會導致重新啟動的應用裝置節點。 未使用的應用裝置時，應該在維護期間套用的更新。  
  
### <a name="prerequisites"></a>先決條件  
執行這些步驟之前，您需要：  
  
-   中的指示，在您的設備上設定 WSUS[設定 Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)。  
  
-   網狀架構網域系統管理員帳戶登入資訊的知識。  
  
-   已經有登入來存取分析平台的系統管理主控台並檢視應用裝置狀態資訊的權限。  
  
-   在大部分情況下，WSUS 需要存取外部應用裝置的伺服器。 若要支援 Analytics Platform System DNS 可以設定為支援可讓 Analytics Platform System 主機和虛擬機器 (Vm)，若要使用外部 DNS 伺服器來解析名稱的外部名稱轉寄站外部的這個使用案例應用裝置。 如需詳細資訊，請參閱 <<c0> [ 使用 DNS 轉寄站解析非設備 DNS 名稱&#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)。</c0>  
  
## <a name="bkmk_ImportUpdates"></a>若要下載並套用 Microsoft 更新  
  
#### <a name="verify-the-appliance-state-indicators"></a>確認應用裝置狀態指標  
  
1.  開啟系統管理員主控台，然後瀏覽至 [應用裝置狀態] 頁面。 如需詳細資訊，請參閱 <<c0> [ 使用管理主控台來監視設備&#40;Analytics Platform System&#41;</c0>](monitor-the-appliance-by-using-the-admin-console.md)  
  
2.  請確認應用裝置狀態的所有節點的狀態指示器。  
  
    -   它可以安全地繼續進行 綠色 或 NA 標記。  
  
    -   評估非重大的警告 （黃色） 錯誤。 在某些情況下的警告訊息不會封鎖更新。 如果沒有不在 C:\ 磁碟機的非重要磁碟的磁碟區錯誤，您可以繼續下一個步驟之前解決磁碟的磁碟區時發生錯誤。  
  
    -   繼續之前，必須先解決大部分的紅色指示器。 如果發生磁碟失敗，使用 [系統管理員主控台中警示] 頁面來確認每個伺服器或 SAN 陣列內不超過一個磁碟故障。 如果有一個以上的磁碟失敗，每個伺服器或 SAN 陣列內，您可以繼續下一個步驟之前修正磁碟失敗。 請務必連絡 Microsoft 支援服務，以儘速修正磁碟失敗。  
  
#### <a name="synchronize-the-wsus-server"></a>同步處理 WSUS 伺服器  
  
1.  網域系統管理員身分登入 VMM 虛擬機器。  
  
2.  在 **伺服器管理員儀表板**上**工具**功能表上，按一下  **Windows Server Update Services** (**wsus.msc**)。  
  
3.  在 WSUS 管理主控台中，按一下**同步處理**。  
  
4.  如果未執行同步處理，請按一下**立即同步處理**右窗格中。 在底部窗格中，會同步處理狀態。 等到同步處理完成。  
  
#### <a name="approve-microsoft-updates-in-wsus"></a>核准 WSUS 中的 Microsoft 更新  
  
1.  在左窗格中，WSUS 主控台中，按一下**所有更新**。  
  
2.  在**所有更新**窗格中，按一下**核准**下拉式選單中，將**核准**至**Any 除了拒絕**。 按一下 **狀態**下拉式選單中，將**狀態**來**任何**。 按一下 **[重新整理]** 。  
  
    以滑鼠右鍵按一下**標題**資料行，然後選取**檔案狀態**下載完成之後，請確認檔案狀態。  
  
    您也可以選取**重大更新**或是**安全性更新**在左窗格並檢視可用的更新這些類別。  
  
    ![選取 所有更新，並將狀態變更為任何。](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectAllUpdates.png "SQL_Server_PDW_WSUSSelectAllUpdates")  
  
3.  選取 所有更新，然後按一下**核准**右窗格中的連結。  
  
    您可以也在所選的更新，以滑鼠右鍵按一下，然後按一下**核准**。 系統可能會提示您接受 「 Microsoft 軟體授權條款 」。 如果是的話，按一下**我接受**在視窗中，以繼續。  
  
    ![選取 全部套用更新，並按一下 [核准]。](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprove.png "SQL_Server_PDW_WSUSSelectApprove")  
  
4.  選取您在中建立的應用裝置伺服器群組[設定 Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)。  
  
5.  按一下 **已核准安裝**，然後按一下**確定**。  
  
    ![核准您的電腦群組的更新。](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprovalType.png "SQL_Server_PDW_WSUSSelectApprovalType")  
  
6.  在 [**核准進度**] 對話方塊中，核准程序完成時，按一下**關閉**。  
  
    ![在核准更新時，請關閉視窗。](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSCloseApprovalProgressWindow.png "SQL_Server_PDW_WSUSCloseApprovalProgressWindow")  
  
#### <a name="verify-that-the-updates-are-in-wsus"></a>確認已在 WSUS 更新  
  
-  請確認所有更新的檔案狀態。 每個檔案必須有標題的左邊的綠色箭號圖示。 這表示檔案已準備好進行安裝。  
  
    ![檔案狀態為成功](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUS_File_Status.png "SQL_Server_PDW_WSUS_File_Status")  
  
    之前安裝更新，請確定它們都已下載且可在 WSUS 主控台。  
  
#### <a name="to-verify-that-all-updates-are-downloaded"></a>若要確認已下載所有更新  
  
-  請檢查**下載狀態**的更新在 WSUS 主控台，如下列螢幕擷取畫面所示。 請確認**需要檔案的更新**為 0 時，確認已下載所有更新。 如果這個數字是零個以上，您可能需要返回並核准其他更新。  
  
    ![請確認已下載所有更新。](./media/download-and-apply-microsoft-updates/SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG.png "SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG")  
  
#### <a name="apply-microsoft-updates"></a>套用 Microsoft 更新  
  
1.  在開始之前，開啟[使用管理主控台來監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)，按一下 **設備狀態**索引標籤，並確認**叢集**並**網路**欄顯示綠色 （或 NA） 的所有節點。 如果任何警示都存在於這些資料行，設備可能無法正確安裝更新。 位址中的所有現有警示**叢集**並**網路**再繼續進行的資料行。  
  
2.  登入 _< 網域名稱 >_ **-HST01**節點為網狀架構網域系統管理員。  
  
3.  若要套用所有適用於 WSUS 中核准的更新，執行更新程式。 請參閱[執行更新程式](#RunUpdateWizard)下方的指示。  
  
#### <a name="verify-the-updates-on-all-nodes"></a>確認所有節點上的更新  
  
1.  在 [VMM] 節點中，啟動在 WSUS 管理主控台。 您可以找到此應用程式**開始**，**系統管理工具**， **Windows Server Update Services**。  
  
2.  依序展開**電腦**。  
  
3.  依序展開**的所有電腦**。  
  
4.  選取您在中建立的應用裝置伺服器群組[設定 Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)。  
  
5.  在 **狀態**下拉式選單中，選取**任何**然後按一下**重新整理**。  
  
6.  依序展開**更新服務**， *<appliance name>* VMM，**更新**，**所有更新**，其中 *<appliance name>* 是您的應用裝置名稱。  
  
7.  在 [**所有更新**] 視窗中設定**核准**來**Any 除了拒絕**。  
  
8.  在 **所有更新**視窗中，將**狀態**來**失敗或需要**。  
  
9. 按一下 **[重新整理]** 。  
  
10. 如果**所需的更新**大於零，請連絡支援服務，以取得協助。  
  
#### <a name="ensure-there-are-no-critical-alerts-in-the-sql-server-pdw-admin-console"></a>請確定在 SQL Server PDW 管理主控台中沒有任何重要的警示  
  
1.  開啟管理主控台，請按一下 [應用裝置狀態] 索引標籤。請參閱[使用管理主控台來監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)。  
  
2.  確認**叢集**並**網路**欄顯示綠色 （或 NA） 的所有節點。 如果任何警示都存在於這些資料行，設備可能無法正確安裝更新。 如果有任何重大警示，請連絡支援服務。  
  
## <a name="RunUpdateWizard"></a>執行更新程式  
請遵循下列指示來執行分析平台的系統更新程式。  
  
> [!NOTE]  
> WSUS 系統設計為執行以非同步方式可能需要一些時間才能完全套用所有更新。 起始更新排程更新，但不保證立即更新活動。  
  
1.  請確定您已登入 HST01 節點為網狀架構網域系統管理員。  
  
2.  開啟命令提示字元視窗並輸入下列命令。 取代 *<parameter>* 與指定的資訊。  
  
**若要執行 Microsoft Update:**  
  
```  
C:\pdwinst\media\setup.exe /action="MicrosoftUpdate" /DomainAdminPassword="<password>"  
```  
  
**若要報告的 Microsoft 更新狀態：**  
  
```  
C:\pdwinst\media\setup.exe /action="ReportMicrosoftUpdateClientStatus" /DomainAdminPassword="<password>"  
```  
  
## <a name="see-also"></a>另請參閱  
[解除安裝 Microsoft 更新&#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[套用 Analytics Platform System Hotfix &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
[解除安裝 Analytics Platform System Hotfix &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[軟體服務&#40;Analytics Platform System&#41;](software-servicing.md)  
  
