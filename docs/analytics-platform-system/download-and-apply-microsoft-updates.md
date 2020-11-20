---
title: 下載 Microsoft 更新
description: 本主題討論如何從 Microsoft Update 目錄將更新下載至 Windows Server Update Services (WSUS) ，然後將這些更新套用至 Analytics Platform System 設備伺服器。 Microsoft Update 將會安裝所有適用于 Windows 和 SQL Server 的更新。 WSUS 安裝在設備的 VMM 虛擬機器上。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: e5f336c3c2c475523d2081bcf01189e67b77fe19
ms.sourcegitcommit: ce15cbbcb0d5f820f328262ff5451818e508b480
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2020
ms.locfileid: "94947913"
---
# <a name="download-and-apply-microsoft-updates-for-analytics-platform-system"></a>下載並套用適用于 Analytics Platform System 的 Microsoft updates
本主題討論如何從 Microsoft Update 目錄將更新下載至 Windows Server Update Services (WSUS) ，然後將這些更新套用至 Analytics Platform System 設備伺服器。 Microsoft Update 將會安裝所有適用于 Windows 和 SQL Server 的更新。 WSUS 安裝在設備的 VMM 虛擬機器上。  
  
## <a name="before-you-begin"></a><a name="TOP"></a>開始之前  
  
> [!WARNING]  
> 如果您的應用裝置或任何設備元件關閉或處於容錯移轉狀態，請勿嘗試套用更新。 在此情況下，請聯絡支援人員以取得協助。  
>   
> 當設備正在使用中時，請勿套用 Microsoft 更新。 套用更新可能會導致設備節點重新開機。 當設備未使用時，應該在維護期間套用更新。  
  
### <a name="prerequisites"></a>Prerequisites  
執行這些步驟之前，您必須：  
  
-   遵循 [設定 Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)中的指示，在您的設備上設定 WSUS。  
  
-   網狀架構網域系統管理員帳戶登入資訊的知識。  
  
-   具有具有存取 Analytics Platform System 管理主控台和查看設備狀態資訊之許可權的登入。  
  
-   在大多數情況下，WSUS 需要存取設備以外的伺服器。 為了支援此使用案例，可將 Analytics Platform System DNS 設定為支援外部名稱轉寄站，讓分析平臺系統主機和虛擬機器 (Vm) 使用外部 DNS 伺服器來解析設備以外的名稱。 如需詳細資訊，請參閱 [使用 DNS 轉寄站來解析非設備 DNS 名稱 &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)。  
  
## <a name="to-download-and-apply-microsoft-updates"></a><a name="bkmk_ImportUpdates"></a>下載並套用 Microsoft 更新  
  
#### <a name="verify-the-appliance-state-indicators"></a>確認設備狀態指示器  
  
1.  開啟管理主控台，並流覽至 [設備狀態] 頁面。 如需詳細資訊，請參閱 [使用管理主控台 &#40;Analytics Platform System 監視設備&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
2.  確認設備狀態上所有節點的狀態指示器。  
  
    -   您可以安全地繼續使用綠色或 NA 指標。  
  
    -   評估非關鍵性的 (黃色) 警告錯誤。 在某些情況下，警告訊息不會封鎖更新。 如果有非重大磁片區錯誤，不在 C：\ 上磁片磁碟機，您可以在解決磁片區錯誤之前繼續進行下一個步驟。  
  
    -   大部分的紅色指標都必須先解決才能繼續。 如果發生磁片失敗，請使用 [管理主控台警示] 頁面來確認每個伺服器或 SAN 陣列內不會有一個以上的磁片失敗。 如果每個伺服器或 SAN 陣列中沒有一個以上的磁片故障，您可以在修正磁片失敗之前繼續進行下一個步驟。 請務必聯絡 Microsoft 支援服務，儘快修正磁片失敗。  
  
#### <a name="synchronize-the-wsus-server"></a>同步處理 WSUS 伺服器  
  
1.  以網域系統管理員身分登入 VMM 虛擬機器。  
  
2.  在 **伺服器管理員的儀表板** 中，按一下 [ **工具** ] 功能表上的 [ **Windows Server Update Services** ] ([ **services.msc** ]) 。  
  
3.  在 WSUS 管理主控台中，按一下 **[同步處理]**。  
  
4.  如果同步處理未執行，請按一下右窗格中的 [ **立即同步處理** ]。 在下方窗格中，會有同步處理狀態。 等候同步處理完成。  
  
#### <a name="approve-microsoft-updates-in-wsus"></a>在 WSUS 中核准 Microsoft 更新  
  
1. 拒絕不是來自 **System Center** 的任何更新彙總套件。

2. 在 [WSUS 主控台] 的左窗格中，按一下 [ **所有更新**]。  
  
3.  在 [ **所有更新** ] 窗格中，按一下 [ **核准** ] 下拉式功能表，並將 [ **核准** ] 設定為 [拒絕] **以外的任何** 一個。 按一下 [ **狀態** ] 下拉式功能表，將 [ **狀態** ] 設定為 [ **任何**]。 按一下 [重新整理]。  
  
    以滑鼠右鍵按一下 [ **標題** ] 資料行，然後選取 [檔案 **狀態** ]，在下載完成之後驗證檔案狀態。  
  
    您也可以在左窗格中選取 **重大更新** 或 **安全性更新** ，並查看這些類別的可用更新。  
  
    ![選取所有更新並將狀態變更為 [任何]。](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectAllUpdates.png "SQL_Server_PDW_WSUSSelectAllUpdates")  
  
4.  選取 [所有更新]，然後按一下右窗格中的 [ **核准** ] 連結。  
  
    您也可以用滑鼠右鍵按一下選取的更新，然後按一下 [ **核准**]。 系統可能會提示您接受「Microsoft 軟體授權條款」。 如果是的話，請按一下視窗中的 [ **我接受** ] 繼續進行。  
  
    ![選取要套用的所有更新，然後按一下 [核准]。](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprove.png "SQL_Server_PDW_WSUSSelectApprove")  
  
5.  選取您在 [設定 Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)中建立的設備伺服器群組。  
  
6.  按一下 [已核准安裝]  ，然後按一下 [確定]  。  
  
    ![核准您的電腦群組更新。](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprovalType.png "SQL_Server_PDW_WSUSSelectApprovalType")  
  
7.  在 [ **核准進度** ] 對話方塊中，當核准程式完成時，按一下 [ **關閉**]。  
  
    ![已核准更新時，請關閉視窗。](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSCloseApprovalProgressWindow.png "SQL_Server_PDW_WSUSCloseApprovalProgressWindow")  
  
#### <a name="verify-that-the-updates-are-in-wsus"></a>確認更新是在 WSUS 中  
  
-  確認所有更新的檔案狀態。 每個檔案的標題左邊都必須有綠色箭號圖示。 這表示檔案已準備好安裝。  
  
    ![檔案狀態顯示成功](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUS_File_Status.png "SQL_Server_PDW_WSUS_File_Status")  
  
    在安裝更新之前，請確定它們都已下載並可在 WSUS 主控台中使用。  
  
#### <a name="to-verify-that-all-updates-are-downloaded"></a>確認下載所有更新  
  
-  在 WSUS 主控台中檢查更新的 **下載狀態** ，如下列螢幕擷取畫面所示。 檢查需要檔案的 **更新** 是否為0，以確認是否已下載所有更新。 如果此數位超過零，您可能需要返回並核准其他更新。  
  
    ![確認是否已下載所有更新。](./media/download-and-apply-microsoft-updates/SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG.png "SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG")  
  
#### <a name="apply-microsoft-updates"></a>套用 Microsoft 更新  
  
1.  開始之前，請 [使用管理主控台 &#40;Analytics Platform System&#41;開啟 [監視設備](monitor-the-appliance-by-using-the-admin-console.md)]，按一下 [**設備狀態**] 索引標籤，然後確認 [叢集] 和 [**網路**] 資料行顯示所有 **節點的綠色** (或 NA) 。 如果任一個資料行中有任何警示，設備可能無法正確安裝更新。 繼續 **之前，請** 先解決叢集和 **網路** 資料行中的所有現有警示。  
  
2.  以網狀架構網域系統管理員身分登入 _<domain_name>_ **HST01** 節點。  
  
3.  若要套用所有針對 WSUS 核准的更新，請執行更新程式。 如需相關指示，請參閱 [執行以下更新程式](#RunUpdateWizard) 。  
  
#### <a name="verify-the-updates-on-all-nodes"></a>確認所有節點上的更新  
  
1.  從 VMM 節點啟動 WSUS 管理主控台。 您可以在 [ **開始**]、[系統 **管理工具**] **Windows Server Update Services** 中找到此應用程式。  
  
2.  展開 [ **電腦**]。  
  
3.  展開 [ **所有電腦**]。  
  
4.  選取您在 [設定 Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)中建立的設備伺服器群組。  
  
5.  在 [ **狀態** ] 下拉式功能表中，選取 [ **任何** ]， **然後按一下 [** 重新整理]。  
  
6.  展開 [ **更新服務**]、[ *<appliance name>* VMM]、[ **更新**]、[ **所有更新**]，其中 *<appliance name>* 是您的設備名稱。  
  
7.  在 [ **所有更新** ] 視窗中，將 [ **核准** ] 設定為 [已 **拒絕**]。  
  
8.  在 [ **所有更新** ] 視窗中，將 **狀態** 設為 [ **失敗] 或 [必要**]。  
  
9. 按一下 [重新整理]。  
  
10. 如果 **需要的更新** 大於零，請聯絡支援人員以取得協助。  
  
#### <a name="ensure-there-are-no-critical-alerts-in-the-sql-server-pdw-admin-console"></a>確定 SQL Server PDW 管理主控台中沒有重大警示  
  
1.  開啟管理主控台，按一下 [設備狀態] 索引標籤。請參閱 [使用管理主控台 &#40;Analytics Platform System&#41;來監視設備 ](monitor-the-appliance-by-using-the-admin-console.md)。  
  
2.  確認 [叢集] 和 [**網路**] 資料行顯示所有 **節點的綠色** (或 NA) 。 如果任一個資料行中有任何警示，設備可能無法正確安裝更新。 如果有任何重大警示，請聯絡支援人員。  
  
## <a name="run-the-update-program"></a><a name="RunUpdateWizard"></a>執行更新程式  
請遵循下列指示來執行 Analytics Platform System 更新程式。  
  
> [!NOTE]  
> WSUS 系統是設計來以非同步方式執行，可能需要一些時間才能完全套用所有更新。 起始更新會排定更新，但不保證立即更新活動。  
  
1.  請確定您已以網狀架構網域系統管理員的身分登入 HST01 節點。  
  
2.  開啟 [命令提示字元] 視窗，並輸入下列命令。 取代 *<parameter>* 為指定的資訊。  
  
**若要執行 Microsoft Update：**  
  
```  
C:\pdwinst\media\setup.exe /action="MicrosoftUpdate" /DomainAdminPassword="<password>"  
```  
  
**若要報告 Microsoft Update 狀態：**  
  
```  
C:\pdwinst\media\setup.exe /action="ReportMicrosoftUpdateClientStatus" /DomainAdminPassword="<password>"  
```  
  
## <a name="see-also"></a>另請參閱  
[&#40;Analytics Platform System&#41;卸載 Microsoft Updates ](uninstall-microsoft-updates.md)  
[將 Analytics Platform System 修補程式套用 &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
[將 Analytics platform System 修補程式卸載 &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[軟體服務 &#40;Analytics Platform System&#41;](software-servicing.md)  
  
