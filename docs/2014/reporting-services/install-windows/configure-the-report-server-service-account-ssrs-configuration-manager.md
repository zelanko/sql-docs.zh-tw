---
title: 設定報表伺服器服務帳戶 (SSRS 設定管理員) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: f880c623-67c8-4167-b98b-ace17e800faa
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 546cf8172cbfc2e13b0953207078f3b2cc9dc146
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082518"
---
# <a name="configure-the-report-server-service-account-ssrs-configuration-manager"></a>設定報表伺服器服務帳戶 (SSRS 組態管理員)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會實作成單一服務，其中包含報表伺服器 Web 服務、報表管理員，以及用於排程報表處理和訂閱傳遞的背景處理應用程式。 本主題將說明如何在一開始設定服務帳戶，以及如何使用 Reporting Services 組態工具來修改此帳戶或密碼。  
  
## <a name="initial-configuration"></a>初始組態  
 報表伺服器服務帳戶是在安裝期間所定義。 您可以執行底下的網域使用者帳戶或內建的服務，例如`NetworkService`帳戶。 沒有預設帳戶;您在中指定任何帳戶[伺服器組態-服務帳戶](../../sql-server/install/server-configuration-service-accounts.md)安裝精靈的頁面都會成為報表伺服器服務的初始帳戶。  
  
> [!IMPORTANT]  
>  雖然報表伺服器 Web 服務和報表管理員是[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]應用程式，他們無法執行下[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]帳戶。 單一服務架構會在相同的報表伺服器處理序識別內執行這兩個 ASP.NET 應用程式， 這是與舊版不同的重大變更，在舊版中，報表伺服器 Web 服務和報表管理員都是在 IIS 內指定的 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 工作處理序識別內執行。  
  
## <a name="changing-the-service-account"></a>變更服務帳戶  
 若要檢視及重新設定服務帳戶資訊，請務必使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具。 服務識別資訊會儲存在內部的多個位置。 使用此工具可確保每當您變更帳戶或密碼時，所有的參考也會隨著更新。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具會執行下列其他步驟，以確保報表伺服器保持可用：  
  
-   自動將新帳戶加入本機電腦上所建立的報表伺服器群組中。 此群組是在保護 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 檔案安全的存取控制清單 (ACL) 中指定。  
  
-   自動更新用來主控報表伺服器資料庫之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的登入權限。 新的帳戶會加入至 **RSExecRole**。  
  
     舊帳戶的資料庫登入將不會自動移除。 請務必移除不再使用的帳戶。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的[管理報表伺服器資料庫 &#40;SSRS 原生模式&#41;](../report-server/report-server-database-ssrs-native-mode.md)。  
  
     只有在一開始設定報表伺服器資料庫連接使用新的服務帳戶，才能將資料庫權限授與給這個服務帳戶。 如果您設定報表伺服器資料庫連接使用網域使用者帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫登入，則連接資訊將不會受到服務帳戶更新的影響。  
  
-   自動更新加密金鑰，加入新帳戶的設定檔資訊。  
  
    > [!NOTE]  
    >  如果報表伺服器是向外延展部署的一部分，則只有您更新的報表伺服器會受到影響。 部署中其他報表伺服器的加密金鑰，不會受到服務帳戶變更的影響。  
  
 如需有關如何設定帳戶的指示，請參閱 <<c0> [ 設定的服務帳戶&#40;SSRS 組態管理員&#41;](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)。</c0>  
  
## <a name="choosing-an-account"></a>選擇帳戶  
 您可以將報表伺服器服務設定為在以下任何一種帳戶類型下執行：  
  
-   最低權限的 Windows 使用者帳戶  
  
-   NetworkService  
  
-   LocalSystem  
  
-   LocalService  
  
 在選擇帳戶類型時，並沒有單一的最佳方法。 每個帳戶都有您必須考量的優點和缺點。 如果您要部署[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]在實際執行伺服器上，最佳做法建議您設定要在網域使用者帳戶下執行，好讓您可以避免損害擴大，如果共用的帳戶遭到惡意使用者入侵的服務。 此外，您也可以更輕鬆地為此帳戶稽核登入活動。 若要使用 Windows 使用者帳戶的取捨的是，如果您要部署[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]在網路中使用 Kerberos 驗證，您必須向該服務的使用者帳戶。 如需詳細資訊，請參閱[為報表伺服器註冊服務主體名稱 &#40;SPN&#41;](../report-server/register-a-service-principal-name-spn-for-a-report-server.md)。  
  
 本節中的下列指導方針和連結可以協助您決定最適合用於您的部署的方法。  
  
-   [服務帳戶&#40;SSRS 原生模式&#41;](../../sql-server/install/service-account-ssrs-native-mode.md)。  
  
-   《SQL Server 線上叢書》中的[設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) 。  
  
-   MSDN 上的《[Services and Service Accounts Security Planning Guide](http://go.microsoft.com/fwlink/?LinkId=69155) 》。  
  
## <a name="updating-an-expired-password"></a>更新已過期的密碼  
 如果報表伺服器服務是以網域帳戶執行，而且在您可以於 Reporting Services 組態工具內更新密碼以前，密碼就已經過期，則要先指定新的密碼，才能啟動該服務。 如果此服務無法啟動，您就無法使用 Reporting Services 組態工具連接該伺服器來更新帳戶。 在此情況下，您必須使用一些工具的組合，才能讓伺服器重新在線上工作。  
  
 若要重設密碼，請執行以下動作：  
  
1.  在 **[開始]** 功能表上，依序指向 **[控制台]**、 **[系統管理工具]**，再按一下 **[服務]**。  
  
2.  以滑鼠右鍵按一下 **[SQL Server Reporting Services]**，然後選取 **[內容]**。  
  
3.  按一下 **[登入]**，並輸入新的密碼。  
  
4.  在更新密碼之後，請啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，並在 [服務帳戶] 頁面中更新密碼。 對於更新報表伺服器儲存於內部的帳戶資訊而言，這個額外步驟是必要的。  
  
 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服務帳戶密碼已過期，則當您嘗試連接至報表伺服器時便會發生 `rsReportServerDatabaseUnavailable` 錯誤。 重設密碼即可解決此錯誤。  
  
## <a name="configuring-the-report-server-service-for-a-sharepoint-integrated-report-server"></a>為 SharePoint 整合報表伺服器設定報表伺服器服務  
 如果您是以 SharePoint 整合模式執行報表伺服器，當下列其中一個條件成立時，您必須更新儲存於 SharePoint 組態資料庫中的服務帳戶資訊：  
  
-   修改[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]服務帳戶 （例如，從 NetworkService 切換到網域使用者帳戶）。  
  
-   擴充 SharePoint 伺服陣列，使其包含其他 SharePoint Web 應用程式。 如果設定伺服器陣列進行報表伺服器整合，而且新加入的應用程式所設定要執行的使用者帳戶，與伺服器陣列中的其他應用程式不同，您就必須更新資料庫存取資訊。  
  
 在重設資料庫存取資訊之後，您應該要重新啟動 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 服務，以確保不再使用舊的連接。  
  
1.  在 **[系統管理工具]** 中，按一下 **[SharePoint 2010 管理中心]**。  
  
2.  按一下 **[應用程式管理]**。  
  
3.  在 [Reporting Services] 區段中按一下 **[授與資料庫存取權]**。  
  
4.  按一下 [確定] 。 [輸入認證] 對話方塊隨即出現。  
  
5.  輸入使用者屬於裝載報表伺服器之電腦上的本機系統管理員群組成員的認證。 這些認證將針對擷取服務帳戶資訊的目的，用於報表伺服器電腦的一次連接。 為每個服務帳戶所建立的資料庫登入將會在 SharePoint 資料庫中更新。  
  
6.  若要重新啟動此服務，請按一下 **[作業]**。  
  
7.  在 [拓撲與服務] 中，按一下 **[伺服器上的服務]**。  
  
8.  如果是 Windows SharePoint Services Web 應用程式，請按一下 **[停止]**。  
  
9. 等候此服務停止。  
  
10. 按一下 **[啟動]**。  
  
> [!NOTE]  
>  SharePoint 產品與技術需要網域帳戶來處理類似 Reporting Services SharePoint 模式的服務組態。  
  
## <a name="see-also"></a>另請參閱  
 [設定服務帳戶&#40;SSRS 組態管理員&#41;](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)   
 [服務帳戶&#40;SSRS 原生模式&#41;](../../sql-server/install/service-account-ssrs-native-mode.md)   
 [設定報表伺服器 Url &#40;SSRS 組態管理員&#41;](configure-report-server-urls-ssrs-configuration-manager.md)   
 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
