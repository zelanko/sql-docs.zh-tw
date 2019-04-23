---
title: 設定原生模式報表伺服器進行本機管理 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
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
manager: kfile
ms.openlocfilehash: 96926b2c7c305bf685bc91206072755081ed35a4
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59967924"
---
# <a name="configure-a-native-mode-report-server-for-local-administration-ssrs"></a>設定原生模式報表伺服器進行本機管理 (SSRS)
  如果您想要在本機管理報表伺服器執行個體，則在下列其中一個作業系統上部署 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器需要其他組態步驟。 本主題說明如何設定報表伺服器以進行本機管理。 如果您有尚未安裝，或將報表伺服器設定，請參閱[從安裝精靈安裝 SQL Server 2014&#40;安裝&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)並[管理 Reporting Services 原生模式報表伺服器](manage-a-reporting-services-native-mode-report-server.md).  
  
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
  
-   [若要設定本機報表伺服器和報表管理員的管理](#bkmk_configure_local_server)  
  
-   [若要設定 SQL Server Management Studio (SSMS) 來進行本機報表伺服器管理](#bkmk_configure_ssms)  
  
-   [若要設定 SQL Server Data Tools BI (SSDT) 來發行至本機報表伺服器](#bkmk_configure_ssdt)  
  
-   [其他資訊](#bkmk_addiitonal_informaiton)  
  
##  <a name="bkmk_configuraiton_overview"></a> 組態變更概觀  
 下列組態變更會設定伺服器，好讓您可以使用標準使用者權限來管理報表伺服器內容和作業：  
  
-   將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 加入至信任的網站。 根據預設，在列出的作業系統上執行的 Internet Explorer 會在 **[受保護模式]** 下執行，此功能會封鎖瀏覽器要求，使其無法到達相同電腦上執行的高層級處理序。 您可以為報表伺服器應用程式停用受保護模式，只要將這些應用程式加入為信任的網站即可。  
  
-   建立授與您 (亦即報表伺服器管理員) 有權管理內容和作業的角色指派，而不需要使用 Internet Explorer 上的 **[以系統管理員身分執行]** 功能。 為 Windows 使用者帳戶建立角色指派，就可以使用內容管理員和系統管理員權限取得報表伺服器的存取權 (透過可取代 Reporting Services 建立之預先定義的內建角色指派的明確角色指派)。  
  
##  <a name="bkmk_configure_local_server"></a> 若要設定本機報表伺服器和報表管理員的管理  
 如果您瀏覽至本機報表伺服器而且看到類似於以下的錯誤，請完成本章節的組態步驟：  
  
-   使用者 `'Domain\[user name]`' 沒有必要權限。 請確認已授與足夠的權限，而且滿足 Windows 使用者帳戶控制 (UAC) 的限制。  
  
###  <a name="bkmk_site_settings"></a> 瀏覽器中受信任的站台設定  
  
1.  使用 [以系統管理員身分執行] 權限開啟瀏覽器視窗。 從 **[開始]** 功能表按一下 **[所有程式]**，再以滑鼠右鍵按一下 **[Internet Explorer]**，並選取 **[以系統管理員身分執行]**。  
  
2.  按一下 **[允許]** 繼續進行。  
  
3.  在 URL 網址中，輸入報表管理員 URL。 如需指示，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的[報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)。  
  
4.  按一下 **[工具]**。  
  
5.  按一下 **[網際網路選項]**。  
  
6.  按一下 **[安全性]**。  
  
7.  按一下 **[信任的網站]**。  
  
8.  按一下 **[網站]**。  
  
9. 加入 `http://<your-server-name>`。  
  
10. 如果您並未針對預設網站使用 HTTPS，請清除 **[此區域內的所有網站需要伺服器驗證 (https:)]** 核取方塊。  
  
11. 按一下 **[加入]**。  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
###  <a name="bkmk_configure_folder_settings"></a> 報表管理員資料夾設定  
  
1.  在報表管理員的首頁上，按一下 **[資料夾設定]**。  
  
2.  在 [資料夾設定] 頁面中，按一下 **[安全性]**。  
  
3.  按一下 **[新增角色指派]**。  
  
4.  在 [群組或使用者名稱]  欄位中，使用以下格式輸入您的 Windows 使用者帳戶： `<domain>\<user>`。  
  
5.  選取 **[內容管理員]**。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
###  <a name="bkmk_configure_site_settings"></a> 報表管理員網站設定  
  
1.  以系統管理權限開啟瀏覽器，並瀏覽至報表管理員 `http://<server name>/reports`。  
  
2.  按一下首頁上方角落的 **[站台設定]** 。  
  
    > [!TIP]  
    >  **注意：** 如果您看不見**站台設定**選項，請關閉並重新開啟瀏覽器並瀏覽至報表管理員，以系統管理權限。  
  
3.  按一下 **[安全性]**。  
  
4.  按一下 **[新增角色指派]**。  
  
5.  在 [群組或使用者名稱]  欄位中，使用以下格式輸入您的 Windows 使用者帳戶： `<domain>\<user>`。  
  
6.  選取 **[系統管理員]**。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  關閉報表管理員。  
  
9. 在 Internet Explorer 中重新開啟報表管理員，而不使用 **[以系統管理員身分執行]**。  
  
##  <a name="bkmk_configure_ssms"></a> 若要設定 SQL Server Management Studio (SSMS) 來進行本機報表伺服器管理  
 根據預設，您無法存取 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中所提供的所有報表伺服器屬性，除非您使用系統管理權限啟動 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 。  
  
 **若要設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]** 角色屬性和角色指派，好讓您不必每次都使用更高權限啟動 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ：  
  
-   在 [開始] 功能表中，依序按一下 [所有程式] 與 [SQL Server 2014]、以滑鼠右鍵按一下 [[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]]，然後按一下 [以系統管理員身分執行]。  
  
-   連接到本機 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 伺服器。  
  
-   在 **[安全性]** 節點中，按一下 **[系統角色]**。  
  
-   以滑鼠右鍵按一下 **[系統管理員]** ，然後按一下 **[屬性]**。  
  
-   在 **[系統角色屬性]** 頁面中，選取 **[檢視報表伺服器屬性]**。 選取您想要與系統管理員角色成員產生關聯的任何其他屬性。  
  
-   按一下 [確定] 。  
  
-   關閉 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
-   若要將使用者加入「系統管理員」系統角色，請參閱本主題稍早的＜ [報表管理員網站設定](#bkmk_configure_site_settings) ＞一節。  
  
 現在當您開啟 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 而且未明確選取 **[以系統管理員身分執行]** 時，還是可以存取報表伺服器屬性。  
  
##  <a name="bkmk_configure_ssdt"></a> 若要設定 SQL Server Data Tools BI (SSDT) 來發行至本機報表伺服器  
 如果您已經在本主題的第一個章節所列的其中一個作業系統上安裝 [!INCLUDE[SSDTDev11](../../includes/ssdtdev11-md.md)] ，而且您希望 SSDT 與本機原生模式報表伺服器互動，您將會遇到權限錯誤，除非您以更高權限開啟 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或設定報表服務角色。 例如，如果您沒有足夠的權限，您將會遇到類似以下的問題：  
  
-   當您嘗試將報表項目部署到本機報表伺服器時，您會在 **[錯誤清單]** 視窗中看到類似下列的錯誤訊息：  
  
    -   授與使用者 'Domain\\<使用者名稱\>' 的權限不足，無法執行此作業。  
  
 **若要在每次開啟 SSDT 時都以更高權限執行：**  
  
1.  從 [開始] 畫面中，輸入`sql server`然後按一下滑鼠右鍵**SQL Server Data Tools for Visual Studio**。 按一下 **[以系統管理員身分執行]**。  
  
     **或者**，在舊版作業系統上：  
  
     在 [開始]  功能表中，依序按一下 [所有程式] 與 [SQL Server 2014] 、以滑鼠右鍵按一下 [SQL Server Data Tools] ，然後按一下 [以系統管理員身分執行] 。  
  
2.  按一下 [ **繼續**]。  
  
3.  按一下 **[執行程式]**。  
  
 您現在應該能夠將報表和其他項目部署到本機報表伺服器。  
  
 **若要設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 角色指派，好讓您不必每次都使用更高權限啟動 SSDT：**  
  
-   請參閱本主題稍早的＜ [報表管理員資料夾設定](#bkmk_configure_folder_settings) ＞和＜ [報表管理員網站設定](#bkmk_configure_site_settings) ＞章節。  
  
##  <a name="bkmk_addiitonal_informaiton"></a> 其他資訊  
 與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 管理相關的額外且常見的組態步驟如下：在 Windows 防火牆中開啟通訊埠 80，以允許存取報表伺服器電腦。 如需指示，請參閱 [Configure a Firewall for Report Server Access](configure-a-firewall-for-report-server-access.md)。  
  
## <a name="see-also"></a>另請參閱  
 [管理 Reporting Services 原生模式報表伺服器](manage-a-reporting-services-native-mode-report-server.md)  
  
  
