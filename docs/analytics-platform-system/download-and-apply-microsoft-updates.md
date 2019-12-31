---
title: 下載 Microsoft Updates
description: 本主題討論如何將更新從 Microsoft Update 目錄下載至 Windows Server Update Services （WSUS），並將這些更新套用至分析平臺系統裝置伺服器。 Microsoft Update 將會安裝 Windows 和 SQL Server 的所有適用更新。 WSUS 安裝在設備的 VMM 虛擬機器上。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2b24d55720d6db5997bfa85c2621f0e8d58c5f95
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401196"
---
# <a name="download-and-apply-microsoft-updates-for-analytics-platform-system"></a>下載並套用適用于分析平臺系統的 Microsoft 更新
本主題討論如何將更新從 Microsoft Update 目錄下載至 Windows Server Update Services （WSUS），並將這些更新套用至分析平臺系統裝置伺服器。 Microsoft Update 將會安裝 Windows 和 SQL Server 的所有適用更新。 WSUS 安裝在設備的 VMM 虛擬機器上。  
  
## <a name="TOP"></a>開始之前  
  
> [!WARNING]  
> 如果您的應用裝置或任何應用裝置元件關閉或處於故障狀態，請勿嘗試套用更新。 在此情況下，請聯絡支援人員以尋求協助。  
>   
> 當設備在使用中時，請勿套用 Microsoft Updates。 套用更新可能會導致應用裝置節點重新開機。 應用程式不使用時，應該在維護期間套用更新。  
  
### <a name="prerequisites"></a>必要條件  
執行這些步驟之前，您必須：  
  
-   遵循[設定 Windows Server Update Services &#40;wsus&#41; &#40;分析平臺系統&#41;](configure-windows-server-update-services-wsus.md)中的指示，在您的設備上設定 WSUS。  
  
-   瞭解網狀架構網域系統管理員帳戶的登入資訊。  
  
-   擁有具有許可權的登入，可存取分析平臺系統管理主控台及查看設備狀態資訊。  
  
-   在大部分情況下，WSUS 需要存取設備以外的伺服器。 若要支援此使用案例，可以將分析平臺系統 DNS 設定為支援外部名稱轉寄站，以允許分析平臺系統主機和虛擬機器（Vm）使用外部 DNS 伺服器來解析位於以外的名稱台. 如需詳細資訊，請參閱[使用 DNS 轉寄站來解析非設備 DNS 名稱 &#40;分析平臺系統&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)。  
  
## <a name="bkmk_ImportUpdates"></a>下載並套用 Microsoft update  
  
#### <a name="verify-the-appliance-state-indicators"></a>確認設備狀態指示器  
  
1.  開啟管理主控台，並流覽至 [設備狀態] 頁面。 如需詳細資訊，請參閱[使用管理主控台監視設備 &#40;分析平臺系統&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
2.  確認設備狀態上所有節點的狀態指示器。  
  
    -   可以安全地繼續使用綠色或 NA 指示器。  
  
    -   評估非重大（黃色）警告錯誤。 在某些情況下，警告訊息不會封鎖更新。 如果有非嚴重的磁片區錯誤（不在 C：\ 上）磁片磁碟機，您可以繼續進行下一個步驟，再解決磁片區錯誤。  
  
    -   在繼續之前，您必須先解決大部分的紅色指標。 如果發生磁片失敗，請使用 [管理主控台警示] 頁面，確認每個伺服器或 SAN 陣列內不會有一個以上的磁片失敗。 如果每個伺服器或 SAN 陣列內不會有一個以上的磁片失敗，您可以在修正磁片失敗之前繼續進行下一個步驟。 請務必聯絡 Microsoft 支援服務，儘快修正磁片故障。  
  
#### <a name="synchronize-the-wsus-server"></a>同步處理 WSUS 伺服器  
  
1.  以網域系統管理員身分登入 VMM 虛擬機器。  
  
2.  在 [**伺服器管理員] 儀表板**的 [**工具**] 功能表上，按一下 [ **Windows Server Update Services** （**wsus**）]。  
  
3.  在 WSUS 管理主控台中，按一下 **[同步處理]**。  
  
4.  如果同步處理未執行，請按一下右窗格中的 [**立即同步**]。 在下方窗格中，將會有同步處理狀態。 等待同步處理完成。  
  
#### <a name="approve-microsoft-updates-in-wsus"></a>核准 WSUS 中的 Microsoft 更新  
  
1.  在 [WSUS 主控台] 的左窗格中，按一下 [**所有更新**]。  
  
2.  在 [**所有更新**] 窗格中，按一下 [**核准**] 下拉式功能表，將 [**核准**] 設定為 [拒絕]**以外的任何**一個。 按一下 [**狀態**] 下拉式功能表，將 [**狀態**] 設定為 [**任何**]。 按一下 [重新整理]****。  
  
    以滑鼠右鍵按一下 [**標題**] 資料行，然後選取 [檔案**狀態**]，以在下載完成後確認檔案狀態。  
  
    您也可以選取左窗格中的 [**重大更新**] 或 [**安全性更新**]，並查看這些類別的可用更新。  
  
    ![選取所有更新並將狀態變更為 [任何]。](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectAllUpdates.png "SQL_Server_PDW_WSUSSelectAllUpdates")  
  
3.  選取 [所有更新]，然後按一下右窗格中的 [**核准**] 連結。  
  
    您也可以在選取的更新上按一下滑鼠右鍵，然後按一下 [**核准**]。 系統可能會提示您接受「Microsoft 軟體授權條款」。 若是如此，請按一下視窗中的 [**我接受**] 繼續進行。  
  
    ![選取要套用的所有更新，然後按一下 [核准]。](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprove.png "SQL_Server_PDW_WSUSSelectApprove")  
  
4.  選取您在[設定 Windows Server Update Services &#40;WSUS&#41; &#40;分析平臺系統&#41;](configure-windows-server-update-services-wsus.md)中所建立的設備伺服器群組。  
  
5.  按一下 [已核准安裝]****，然後按一下 [確定]****。  
  
    ![核准您的電腦群組更新。](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprovalType.png "SQL_Server_PDW_WSUSSelectApprovalType")  
  
6.  在 [**核准進度**] 對話方塊中，當核准程式完成時，按一下 [**關閉**]。  
  
    ![已核准更新時，請關閉視窗。](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSCloseApprovalProgressWindow.png "SQL_Server_PDW_WSUSCloseApprovalProgressWindow")  
  
#### <a name="verify-that-the-updates-are-in-wsus"></a>確認更新在 WSUS 中  
  
-  確認所有更新的檔案狀態。 每個檔案的標題左邊都必須有綠色箭號圖示。 這表示檔案已準備就緒，可供安裝。  
  
    ![檔案狀態顯示成功](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUS_File_Status.png "SQL_Server_PDW_WSUS_File_Status")  
  
    安裝更新之前，請確定已在 WSUS 主控台中下載並使用它們。  
  
#### <a name="to-verify-that-all-updates-are-downloaded"></a>確認已下載所有更新  
  
-  檢查 WSUS 主控台中更新的**下載狀態**，如下列螢幕擷取畫面所示。 檢查需要檔案的**更新**是否為0，以確認已下載所有更新。 如果此數目大於零，您可能需要返回並核准其他更新。  
  
    ![確認是否已下載所有更新。](./media/download-and-apply-microsoft-updates/SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG.png "SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG")  
  
#### <a name="apply-microsoft-updates"></a>套用 Microsoft 更新  
  
1.  開始之前，請先[使用管理主控台 &#40;分析平臺&#41;系統](monitor-the-appliance-by-using-the-admin-console.md)] 開啟 [監視設備]，按一下 [**設備狀態**] 索引標籤，然後確認 [叢集 **] 和 [** **網路**] 資料行顯示所有節點的綠色（或 NA）。 如果任一個資料行中存在任何警示，設備可能無法正確安裝更新。 請先解決叢集和**網路**資料行中所有現有的警示 **，再繼續**進行。  
  
2.  以網狀架構網域系統管理員身分登入 _<domain_name>_ **HST01** ] 節點。  
  
3.  若要套用針對 WSUS 核准的所有更新，請執行更新程式。 如需相關指示，請參閱[執行以下的更新程式](#RunUpdateWizard)。  
  
#### <a name="verify-the-updates-on-all-nodes"></a>確認所有節點上的更新  
  
1.  從 VMM 節點，啟動 WSUS 管理主控台。 此應用程式可以在 [**啟動**]、[系統**管理工具**] 和 [ **Windows Server Update Services**] 底下找到。  
  
2.  展開 [**電腦**]。  
  
3.  展開 [**所有電腦**]。  
  
4.  選取您在[設定 Windows Server Update Services &#40;WSUS&#41; &#40;分析平臺系統&#41;](configure-windows-server-update-services-wsus.md)中所建立的設備伺服器群組。  
  
5.  在 [**狀態**] 下拉式功能表中，選取 [**任何**]，**然後按一下 [** 重新整理]。  
  
6.  展開 [**更新服務** *<appliance name>*]、[VMM]、[**更新**]、[**所有更新**]，其中*<appliance name>* 是您的設備名稱。  
  
7.  在 [**所有更新**] 視窗中，將**核准**設定為 [**拒絕] 以外的任何**一個。  
  
8.  在 [**所有更新**] 視窗中，將 [**狀態**] 設定為 [**失敗] 或 [必要**]  
  
9. 按一下 [重新整理]****。  
  
10. 如果**需要的更新**大於零，請聯絡支援以取得協助。  
  
#### <a name="ensure-there-are-no-critical-alerts-in-the-sql-server-pdw-admin-console"></a>確保 SQL Server PDW 管理主控台中沒有重大警示  
  
1.  開啟管理主控台，按一下 [設備狀態] 索引標籤。請參閱[使用管理主控台監視設備 &#40;分析平臺系統&#41;](monitor-the-appliance-by-using-the-admin-console.md)。  
  
2.  確認 [叢集 **] 和 [** **網路**] 資料行顯示所有節點的綠色（或 NA）。 如果任一個資料行中存在任何警示，設備可能無法正確安裝更新。 如果有任何重大警示，請聯絡支援人員。  
  
## <a name="RunUpdateWizard"></a>執行更新程式  
請遵循這些指示來執行分析平臺系統更新程式。  
  
> [!NOTE]  
> WSUS 系統的設計是要以非同步方式執行，可能需要一些時間才能完全套用所有更新。 起始更新會排定更新，但不保證立即更新活動。  
  
1.  請確定您以網狀架構網域系統管理員的身分登入 HST01 節點。  
  
2.  開啟 [命令提示字元] 視窗，然後輸入下列命令。 取代*<parameter>* 為指定的資訊。  
  
**若要執行 Microsoft Update：**  
  
```  
C:\pdwinst\media\setup.exe /action="MicrosoftUpdate" /DomainAdminPassword="<password>"  
```  
  
**若要報告 Microsoft Update 狀態：**  
  
```  
C:\pdwinst\media\setup.exe /action="ReportMicrosoftUpdateClientStatus" /DomainAdminPassword="<password>"  
```  
  
## <a name="see-also"></a>另請參閱  
[將 Microsoft Updates 卸載 &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[將分析平臺系統修補程式套用 &#40;分析平臺系統&#41;](apply-analytics-platform-system-hotfixes.md)  
[&#40;分析平臺系統&#41;卸載分析平臺系統修補程式](uninstall-analytics-platform-system-hotfixes.md)  
[軟體服務 &#40;分析平臺系統&#41;](software-servicing.md)  
  
