---
title: "設定供報表伺服器存取的防火牆 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "09/14/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "防火牆系統 [Reporting Services]"
  - "設定伺服器 [Reporting Services]"
ms.assetid: 04dae07a-a3a4-424c-9bcb-a8000e20dc93
caps.latest.revision: 13
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 13
---
# 設定供報表伺服器存取的防火牆
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器應用程式和發行的報表是透過指定 IP 位址、通訊埠和虛擬目錄的 URL 來加以存取。 如果開啟了 Windows 防火牆，則設定報表伺服器使用的通訊埠很可能已關閉。 當您從遠端用戶端電腦嘗試開啟 **報表管理員** 時出現空白網頁，或要求報表之後出現空白網頁，即表示某個連接埠可能已關閉。  
  
 若要開啟通訊埠，您必須在報表伺服器電腦上使用 Windows 防火牆公用程式。 Reporting Services 將不會為您開啟通訊埠，您必須手動執行這個步驟。  
  
 根據預設，報表伺服器會接聽通訊埠 80 上的 HTTP 要求。 因此，下列指示包含了指定該通訊埠的步驟。 如果您設定報表伺服器 URL 使用不同的通訊埠，當您遵循底下的指示進行時，就必須指定該通訊埠編號。  
  
 如果您要存取外部電腦上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 關聯式資料庫，或者報表伺服器資料庫位於外部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上，您就必須開啟外部電腦上的通訊埠 1433 和 1434。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》的[設定用於 Database Engine 存取的 Windows 防火牆](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)。 如需預設 Windows 防火牆設定的詳細資訊，以及影響 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 之 TCP 通訊埠的描述，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的[設定 Windows 防火牆以允許 SQL Server 存取](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
## 必要條件  
 這些指示假設您已經為報表伺服器 Web 服務和報表管理員設定服務帳戶、建立報表伺服器資料庫及設定 URL。 如需詳細資訊，請參閱[管理 Reporting Services 原生模式報表伺服器](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)。  
  
 您也應該已經確認，報表伺服器可透過本機報表伺服器執行個體的本機網頁瀏覽器連接來加以存取。 此步驟會確認您有使用中的安裝。 在您開始開啟通訊埠之前，應該先確認安裝已正確設定。 若要在 Windows Server 上完成這個步驟，您也必須已經將報表伺服器網站加入至 [信任的網站]。 如需詳細資訊，請參閱[設定原生模式報表伺服器進行本機管理 &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
## 在 Windows 防火牆中開啟通訊埠  
  
#### 開啟連接埠 80  
  
1.  在 **[開始]** 功能表中，按一下 **[控制台]**、按一下 **[系統及安全性]**，然後按一下 **[Windows 防火牆]**。 如果 [控制台] 沒有設定為「類別目錄」檢視，您只需要選取 **[Windows 防火牆]**。  
  
2.  按一下 **[進階設定]**。  
  
3.  按一下 **[輸入規則]**。  
  
4.  在 **[動作]** 視窗中，按一下 **[新增規則]** 。  
  
5.  按一下 **[連接埠]** 的 **[規則類型]**。  
  
6.  按一下 **[下一步]**。  
  
7.  在 **[通訊協定及連接埠]** 頁面上，按一下 **[TCP]**。  
  
8.  選取 **[特定本機連接埠]** ，然後輸入值： **80**。  
  
9. 按一下 **[下一步]**。  
  
10. 在 **[動作]** 頁面上，按一下 **[允許該連線]**。  
  
11. 按一下 **[下一步]**。  
  
12. 在 **[設定檔]** 頁面上，按一下適用於您環境的選項。  
  
13. 按一下 **[下一步]**。  
  
14. 在 [名稱] 頁面上，輸入名稱：**ReportServer (TCP 在連接埠 80 上)**  
  
15. 按一下 **[完成]**。  
  
16. 重新啟動電腦。  
  
## 後續步驟  
 在您開啟此通訊埠之後，以及確認遠端使用者是否可以在您開啟的通訊埠上存取報表伺服器之前，您必須透過首頁和網站層級的角色指派，為使用者授與此報表伺服器的存取權。 如果使用者沒有足夠的權限，雖然您可以正確開啟通訊埠，不過報表伺服器連接仍然會失敗。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的[將報表伺服器的存取權授與使用者 &#40;報表管理員&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md)。  
  
 您也可以在另一部電腦上啟動報表管理員，以確認此通訊埠已正確開啟。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的[報表管理員 &#40;SSRS 原生模式&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md)。  
  
## 請參閱＜  
 [設定報表伺服器服務帳戶 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [設定報表伺服器 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [建立報表伺服器資料庫 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/create-a-report-server-database-ssrs-configuration-manager.md)   
 [設定報表伺服器服務帳戶 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [管理 Reporting Services 原生模式報表伺服器](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
  
  