---
title: 設定原生模式報表伺服器進行本機管理 | Microsoft Docs
description: 了解如果在特定環境中安裝 Reporting Services 報表伺服器，可如何設定報表伺服器以進行本機管理。
ms.date: 05/28/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- UAC
- installing Reporting Services
- Windows Vista
- Localhost
- windows server 2008
- Vista
ms.assetid: 312c6bb8-b3f7-4142-a55f-c69ee15bbf52
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 07a5040138bb19bd456a11ad9dcc15dc4cf06e4d
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545610"
---
# <a name="configure-a-native-mode-report-server-for-local-administration-ssrs"></a>設定原生模式報表伺服器進行本機管理 (SSRS)
  如果您想要在本機管理報表伺服器執行個體，則在下列其中一個作業系統上部署 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器需要其他組態步驟。 本主題說明如何設定報表伺服器以進行本機管理。 如果您尚未安裝或設定報表伺服器，請參閱[從安裝精靈 &#40;安裝程式&#41; 安裝 SQL Server](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md) 和[管理 Reporting Services 原生模式報表伺服器](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式|  
  
-   [!INCLUDE[winblue_server_2](../../includes/winblue-server-2-md.md)]  
  
-   [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]  
  
-   [!INCLUDE[win8](../../includes/win8-md.md)]  
  
-   [!INCLUDE[win8srv](../../includes/win8srv-md.md)]  
  
-   [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]  
  
-   [!INCLUDE[win7](../../includes/win7-md.md)]  
  
-   [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]  
  
 由於標示的作業系統會限制權限，所以屬於本機管理員群組的成員會執行大部分的應用程式，就像使用標準使用者帳戶一樣。  
  
 雖然這個作法會提升系統的整體安全性，但是也會妨礙您使用 Reporting Services 為本機管理員建立之預先定義的內建角色指派。  
  
-   [組態變更概觀](#bkmk_configuraiton_overview)  
  
-   [設定本機報表伺服器和入口網站的管理](#bkmk_configure_local_server)  
  
-   [若要設定 SQL Server Management Studio (SSMS) 來進行本機報表伺服器管理](#bkmk_configure_ssms)  
  
-   [若要設定 SQL Server Data Tools (SSDT) 來發行至本機報表伺服器](#bkmk_configure_ssdt)  
  
-   [其他資訊](#bkmk_addiitonal_informaiton)  
  
##  <a name="overview-of-configuration-changes"></a><a name="bkmk_configuraiton_overview"></a> 組態變更概觀  
 下列組態變更會設定伺服器，好讓您可以使用標準使用者權限來管理報表伺服器內容和作業：  
  
-   將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 加入至信任的網站。 根據預設，在列出的作業系統上執行的 Internet Explorer 會在 **[受保護模式]** 下執行，此功能會封鎖瀏覽器要求，使其無法到達相同電腦上執行的高層級處理序。 您可以為報表伺服器應用程式停用受保護模式，只要將這些應用程式加入為信任的網站即可。  
  
-   建立授與您 (亦即報表伺服器管理員) 有權管理內容和作業的角色指派，而不需要使用 Internet Explorer 上的 **[以系統管理員身分執行]** 功能。 為 Windows 使用者帳戶建立角色指派，就可以使用內容管理員和系統管理員權限取得報表伺服器的存取權 (透過可取代 Reporting Services 建立之預先定義的內建角色指派的明確角色指派)。  
  
##  <a name="to-configure-local-report-server-and-web-portal-administration"></a><a name="bkmk_configure_local_server"></a> 設定本機報表伺服器和入口網站的管理  
 如果您瀏覽至本機報表伺服器而且看到類似於以下的錯誤，請完成本章節的組態步驟：  
  
-   使用者 `'Domain\[user name]`' 沒有必要權限。 請確認已授與足夠的權限，而且滿足 Windows 使用者帳戶控制 (UAC) 的限制。  
  
###  <a name="trusted-site-settings-in-the-browser"></a><a name="bkmk_site_settings"></a> 瀏覽器中受信任的網站設定  
  
1.  使用 [以系統管理員身分執行] 權限開啟瀏覽器視窗。 從 [開始] 功能表，以滑鼠右鍵按一下 [Internet Explorer]，然後選取 [以系統管理員身分執行]。  
  
2.  若出現提示，請選取 [是] 以繼續。  
  
3.  在 URL 網址中，輸入入口網站 URL。 如需指示，請參閱[報表伺服器的入口網站 &#40;SSRS 原生模式&#41;](../../reporting-services/web-portal-ssrs-native-mode.md)。  
  
4.  按一下 **[工具]** 。  
  
5.  按一下 **[網際網路選項]** 。  
  
6.  按一下 **[安全性]** 。  
  
7.  按一下 **[信任的網站]** 。  
  
8.  按一下 **[網站]** 。  
  
9. 加入 `https://<your-server-name>`。  
  
10. 如果您並未針對預設網站使用 HTTPS，請清除 **[此區域內的所有網站需要伺服器驗證 (https:)]** 核取方塊。  
  
11. 按一下 [新增] 。  
  
12. 選取 [確定]。  
  
###  <a name="web-portal-folder-settings"></a><a name="bkmk_configure_folder_settings"></a> 入口網站資料夾設定  
  
1.  在入口網站中，於首頁上按一下 [管理資料夾]。  
  
2.  在 [管理] 資料夾頁面中，按一下 [安全性]，然後選取 [新增群組或使用者]。  
  
3.  在 [新增角色指派] 頁面的 [群組或使用者] 欄位中，使用以下格式輸入您的 Windows 使用者帳戶：`<domain>\<user>`。  
  
5.  選取 **[內容管理員]** 。  
  
6.  選取 [確定]。  
  
###  <a name="web-portal-site-settings"></a><a name="bkmk_configure_site_settings"></a> 入口網站網站設定  
  
1.  以系統管理權限開啟瀏覽器，並瀏覽至入口網站 `https://<server name>/reports`。  
  
2.  選取首頁頂端列上的齒輪圖示，然後從下拉式功能表中選取 [網站設定]。 
  
    ![齒輪圖示](../media/ssrsgearmenu.png).
    >[!TIP]  
    >**注意：** 如果您沒看到 [網站設定] 選項，請關閉並使用系統管理權限重新開啟瀏覽器，然後瀏覽至入口網站。  
  
3.  在 [網站設定] 頁面上，選取 [安全性]，然後選取 [新增群組或使用者]。  
  
4.  在 [群組或使用者名稱]  欄位中，使用以下格式輸入您的 Windows 使用者帳戶： `<domain>\<user>`。  

5.  選取 **[系統管理員]** 。  
  
6.  選取 [確定]。  
  
7.  關閉入口網站。  
  
8. 在不使用 [以系統管理員身分執行] 的情況下，於 Internet Explorer 中重新開啟入口網站。  
  
##  <a name="to-configure-sql-server-management-studio-ssms-for-local-report-server-administration"></a><a name="bkmk_configure_ssms"></a> 設定 SQL Server Management Studio (SSMS) 來進行本機報表伺服器管理  
 根據預設，您無法存取 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中所提供的所有報表伺服器屬性，除非您使用系統管理權限啟動 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 。  
  
 **若要設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]** 角色屬性和角色指派，好讓您不必每次都使用更高權限啟動 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ：  
  
-   在 [開始] 功能表中，以滑鼠右鍵按一下 [Microsoft SQL Server [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]]，然後按一下 [以系統管理員身分執行]。  
  
-   連接到本機 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 伺服器。  
  
-   在 **[安全性]** 節點中，按一下 **[系統角色]** 。  
  
-   以滑鼠右鍵按一下 **[系統管理員]** ，然後按一下 **[屬性]** 。  
  
-   在 **[系統角色屬性]** 頁面中，選取 **[檢視報表伺服器屬性]** 。 選取您想要與系統管理員角色成員產生關聯的任何其他屬性。  
  
-   按一下 [確定]。  
  
-   關閉 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
-   若要將使用者加入「系統管理員」系統角色，請參閱本文稍早的[入口網站網站設定](#bkmk_configure_site_settings)一節。  
  
 現在當您開啟 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 而且未明確選取 **[以系統管理員身分執行]** 時，還是可以存取報表伺服器屬性。  
  
##  <a name="to-configure-sql-server-data-tools-ssdt-to-publish-to-a-local-report-server"></a><a name="bkmk_configure_ssdt"></a> 設定 SQL Server Data Tools (SSDT) 來發行至本機報表伺服器  
 如果您已經在本主題的第一個章節所列的其中一個作業系統上安裝 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ，而且您希望 SSDT 與本機原生模式報表伺服器互動，您將會遇到權限錯誤，除非您以更高權限開啟 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或設定報表服務角色。 例如，如果您沒有足夠的權限，您將會遇到類似以下的問題：  
  
-   當您嘗試將報表項目部署到本機報表伺服器時，您會在 **[錯誤清單]** 視窗中看到類似下列的錯誤訊息：  
  
    -   授與使用者 'Domain\\<使用者名稱\>' 的權限不足，無法執行此作業。  
  
 **若要在每次開啟 SSDT 時都以更高權限執行：**  
  
1.  在 [開始] 功能表中，選取 [Microsoft SQL Server]，然後以滑鼠右鍵按一下 [SQL Server Data Tools]。 按一下 **[以系統管理員身分執行]** 。  
  
2.  若出現提示，請選取 [是] 以繼續。  
  
您現在應該能夠將報表和其他項目部署到本機報表伺服器。  
  
 **若要設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 角色指派，好讓您不必每次都使用更高權限啟動 SSDT：**  
  
-   請參閱本主題稍早的[入口網站資料夾設定](#bkmk_configure_folder_settings)與[入口網站網站設定](#bkmk_configure_site_settings)小節。  
  
##  <a name="additional-information"></a><a name="bkmk_addiitonal_informaiton"></a> 其他資訊  
 與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 管理相關的額外且常見的組態步驟如下：在 Windows 防火牆中開啟通訊埠 80，以允許存取報表伺服器電腦。 如需指示，請參閱 [Configure a Firewall for Report Server Access](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)。  
  
## <a name="see-also"></a>另請參閱  
 [管理 Reporting Services 原生模式報表伺服器](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
  
  
