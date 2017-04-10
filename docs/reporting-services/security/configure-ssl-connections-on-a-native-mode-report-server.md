---
title: "在原生模式報表伺服器上設定 SSL 連接 | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "安全通訊端層 (SSL) (Secure Sockets Layer (SSL))"
ms.assetid: 212f2042-456a-4c0a-8d76-480b18f02431
caps.latest.revision: 34
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 34
---
# 在原生模式報表伺服器上設定 SSL 連接
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式會使用 HTTP SSL (安全通訊端層) 服務來建立與報表伺服器的加密連接。 如果您在報表伺服器電腦的本機憑證存放區內有安裝憑證 (.cer) 檔案，您可以將此憑證繫結到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 保留項目，以便透過加密通道支援報表伺服器連接。  
  
> [!TIP]  
>  如果您正在使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式，請參閱 SharePoint 文件集取得詳細資訊。 例如，[How to enable SSL on a SharePoint 2010 web application (如何在 SharePoint 2010 Web 應用程式上啟用 SSL) (http://blogs.msdn.com/b/sowmyancs/archive/2010/02/12/how-to-enable-ssl-on-a-sharepoint-web-application.aspx)](http://blogs.msdn.com/b/sowmyancs/archive/2010/02/12/how-to-enable-ssl-on-a-sharepoint-web-application.aspx)。  
  
 由於 Internet Information Services (IIS) 也使用 HTTP SSL，所以如果您在同一部電腦上執行 IIS 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，將必須負責解決重要的互通性問題。 請務必檢閱「與 IIS 的互通性問題」一節，以取得如何對付這些問題的指引。  
  
## 伺服器憑證需求  
 電腦上必須已安裝伺服器憑證 (不支援用戶端憑證)。 Reporting Services 不提供要求、產生、下載或安裝憑證的功能。 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 會提供一個憑證嵌入式管理單元，可用它來從信任的憑證授權單位要求憑證。  
  
 如果是為了測試，您可以在本機產生憑證。 如果您使用 **MakeCert** 公用程式和範例命令當做範本，請務必將伺服器名稱指定為主機，並在執行此命令之前先移除所有分行符號。 如果您在 DOS 視窗中執行此命令，可能需要增加視窗的緩衝區大小，以容納整個命令。  
  
 如果您在同一部電腦上一起執行 IIS 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，您可以使用 [!INCLUDE[iismgr](../../includes/iismgr-md.md)] 主控台應用程式來取得電腦上所安裝的憑證。 [!INCLUDE[iismgr](../../includes/iismgr-md.md)] 包括了一些選項，可讓您建立及封裝憑證要求 (.crt) 檔案，以供信任的憑證授權單位進行後續處理。 您所使用的憑證授權單位將會產生憑證 (.cer) 檔案，並將它送回給您。 您可以使用 IIS 管理主控台，將憑證檔案安裝在本機存放區。 如需詳細資訊，請參閱 TechNet 上的 [使用 SSL 將機密資料加密](http://go.microsoft.com/fwlink/?LinkId=71123) 。  
  
## 與 IIS 的互通性問題  
 與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 相同的電腦上有存在 IIS，將會大幅影響與報表伺服器的 SSL 連接。  
  
-   如果已安裝 IIS，World Wide Web (W3SVC) 服務永遠都必須在執行中。 HTTP SSL 服務如果偵測到 IIS 正在執行中，它將會與 IIS 相依。 這表示每當 IIS 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝在同一部電腦上，而且您正在為 SSL 連接設定報表伺服器 URL 時，全球資訊網服務 (W3SVC) 都必須在執行中。  
  
-   解除安裝 IIS 會暫時中斷對 SSL 繫結之報表伺服器 URL 的服務。 因此，強烈建議您在解除安裝 IIS 之後，要重新啟動電腦。  
  
     必須要重新開機，才能清除快取中的所有 SSL 工作階段。 某些作業系統最多會快取 10 個小時的 SSL 工作階段，即使當 SSL 繫結已經從 HTTP.SYS 的 URL 保留項目中移除後，https:// URL 仍然繼續運作。 重新開機會關閉使用此通道的任何開啟連接。  
  
## 將 SSL 繫結到 Reporting Services URL 保留項目  
 下列步驟不包含要求、產生、下載或安裝憑證的指示。 您必須已安裝憑證，而且此憑證可供使用。 您所指定的憑證屬性、憑證取自的憑證授權單位，以及您用於要求及安裝此憑證的工具和公用程式都是由您決定。  
  
 您可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具來繫結此憑證。 如果此憑證正確地安裝在本機電腦存放區， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具將會偵測到它，並將它顯示在 **[Web 服務 URL]** 和 **[報表管理員 URL]** 頁面的 **[SSL 憑證]** 清單上。  
  
### 為 SSL 設定報表伺服器 URL  
  
1.  啟動 Reporting Services 組態工具，並連接到報表伺服器。  
  
2.  按一下 **[Web 服務 URL]**。  
  
3.  展開 SSL 憑證的清單。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會偵測本機存放區內的伺服器驗證憑證。 如果您已安裝憑證，而且沒有在清單中看到它，您可能需要重新啟動服務。 您可以在 Reporting Services 組態工具的 **[報表伺服器狀態]** 頁面中，使用 **[停止]** 和 **[啟動]** 按鈕來重新啟動服務。  
  
4.  選取憑證。  
  
5.  按一下 **[套用]**。  
  
6.  按一下此 URL 來確認它是否有效。  
  
 測試此 URL 需要報表伺服器資料庫組態。 如果您尚未建立報表伺服器資料庫，請在測試此 URL 之前先建立。  
  
 報表管理員和報表伺服器 Web 服務的 URL 保留項目會各自獨自設定。 如果您也想要透過 SSL 加密的通道來設定報表管理員存取，請繼續以下步驟：  
  
1.  按一下 **[報表管理員 URL]**。  
  
2.  按一下 **[進階]**。  
  
3.  在 **[報表管理員的多重 SSL 識別]**中，按一下 **[加入]**。  
  
4.  選取此憑證，然後按一下 **[確定]**，再按一下 **[套用]**。  
  
5.  按一下此 URL 來確認它是否有效。  
  
## 憑證繫結的儲存方式  
 憑證繫結將會儲存在 HTTP.SYS 中。 您所定義之繫結的表示法也會儲存在 RSReportServer.config 檔案的 **URLReservations** 區段中。 組態檔中的設定只是在其他地方指定之實際值的一種表示法。 請勿直接修改組態檔中的值。 只有當您使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具或報表伺服器 Windows Management Instrumentation (WMI) 提供者來繫結憑證之後，組態設定才會出現在檔案中。  
  
> [!NOTE]  
>  如果在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中設定 SSL 憑證繫結之後，需要從電腦移除該憑證，請務必先從 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 移除繫結，然後再移除電腦中的憑證。 否則，您將無法使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具或 WMI 來移除繫結，而且會收到「無效的參數」錯誤。 如果您已經從電腦移除憑證，就可以使用 Httpcfg.exe 工具從 HTTP.SYS 移除繫結。 如需有關 Httpcfg.exe 的詳細資訊，請參閱 Windows 產品文件集。  
  
 SSL 繫結是 Microsoft Windows 中的共用資源。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員或其他工具 (像是 IIS 管理員) 所做的變更，可能會影響同一部電腦上的其他應用程式。 最佳做法是使用相同的工具編輯用來建立繫結的繫結。  例如，如果您使用組態管理員建立 SSL 繫結，則建議您使用組態管理員管理繫結的生命週期。 如果您使用 IIS 管理員建立繫結，則建議您使用 IIS 管理員管理繫結的生命週期。 如果在電腦上安裝 IIS 之後才安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，則最好在設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]之前先檢閱 IIS 中的 SSL 組態。  
  
 如果您使用 Reporting Services 組態管理員移除 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的 SSL 繫結，SSL 可能無法再於執行 Internet Information Services (IIS) 的伺服器或另一部 HTTP.SYS 伺服器的網站上運作。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員會移除下列登錄機碼。 移除此登錄機碼時，IIS 的 SSL 繫結也會移除。 若沒有此繫結，就不會對 HTTPS 通訊協定提供 SSL。 若要診斷此問題，請使用 IIS 管理員或 HTTPCFG.exe 命令列公用程式。若要解決此問題，請使用 IIS 管理員還原網站的 SSL 繫結。若要避免未來發生此問題，請使用 IIS 管理員移除 SSL 繫結，然後使用 IIS 管理員還原所需網站的繫結。 如需詳細資訊，請參閱知識庫文章：[SSL no longer works after you remove an SSL binding (移除 SSL 繫結之後 SSL 便不再有用) (http://support.microsoft.com/kb/956209/n)](http://support.microsoft.com/kb/956209/n)。  
  
## 請參閱＜  
 [使用報表伺服器驗證](../../reporting-services/security/authentication-with-the-report-server.md)   
 [設定和管理報表伺服器 &#40;SSRS 原生模式&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [設定報表伺服器 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  