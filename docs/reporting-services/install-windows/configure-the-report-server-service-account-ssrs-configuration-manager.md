---
title: "設定報表伺服器服務帳戶 (SSRS 設定管理員) | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f880c623-67c8-4167-b98b-ace17e800faa
caps.latest.revision: "14"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Active
ms.openlocfilehash: e68467845079107509d7cf259b06b8f5c52dbb06
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="configure-the-report-server-service-account-ssrs-configuration-manager"></a>設定報表伺服器服務帳戶 (SSRS 組態管理員)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會實作成單一服務，其中包含報表伺服器 Web 服務、 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]，以及用於排程報表處理和訂閱傳遞的背景處理應用程式。 本主題將說明如何在一開始設定服務帳戶，以及如何使用 Reporting Services 組態工具來修改此帳戶或密碼。  
  
## <a name="initial-configuration"></a>初始組態  
 報表伺服器服務帳戶是在安裝期間所定義。 您可以在網域使用者帳戶或內建帳戶 (例如 **虛擬服務帳戶**) 之下執行此服務。 沒有預設帳戶；您在安裝精靈的 [服務帳戶] 頁面中指定的任何帳戶都會成為報表伺服器服務的初始帳戶。  
  
> [!IMPORTANT]  
>  雖然報表伺服器 Web 服務和 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] 為個別的 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 應用程式，但是它們會在同一個報表伺服器處理序識別內的單一服務架構下執行。  
  
> [!NOTE]  
>  不支援使用內建 Windows 服務帳戶 (本機服務或網路服務) 做為屬於網域控制站之電腦上的報表伺服器服務帳戶。  
  
## <a name="changing-the-service-account"></a>變更服務帳戶  
 若要檢視及重新設定服務帳戶資訊，請務必使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員。 服務識別資訊會儲存在內部的多個位置。 使用此工具可確保每當您變更帳戶或密碼時，所有的參考也會隨著更新。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員會執行下列其他步驟，以確保報表伺服器保持可用：  
  
-   自動將新帳戶加入本機電腦上所建立的報表伺服器群組中。 此群組是在保護 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 檔案安全的存取控制清單 (ACL) 中指定。  
  
-   自動更新用來主控報表伺服器資料庫之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的登入權限。 新的帳戶會加入至 **RSExecRole**。  
  
     舊帳戶的資料庫登入將不會自動移除。 請務必移除不再使用的帳戶。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的[管理報表伺服器資料庫 &#40;SSRS 原生模式&#41;](../../reporting-services/report-server/administer-a-report-server-database-ssrs-native-mode.md)。  
  
     只有在一開始設定報表伺服器資料庫連接使用新的服務帳戶，才能將資料庫權限授與這個服務帳戶。 如果您設定報表伺服器資料庫連接使用網域使用者帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫登入，則連接資訊將不會受到服務帳戶更新的影響。  
  
-   自動更新加密金鑰，加入新帳戶的設定檔資訊。  
  
    > [!NOTE]  
    >  如果報表伺服器是向外延展部署的一部分，則只有您更新的報表伺服器會受到影響。 部署中其他報表伺服器的加密金鑰，不會受到服務帳戶變更的影響。  
      
## <a name="to-configure-the-report-server-service-account"></a>若要設定報表伺服器服務帳戶  
  
1.  啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員，並連接到報表伺服器。  
  
2.  在 [服務帳戶] 頁面上，選取可描述您想要使用之帳戶類型的選項。  
  
3.  如果您選取了 Windows 使用者帳戶，請指定新的帳戶和密碼。 此帳戶不能超過 20 個字元。  
  
     如果在支援 Kerberos 驗證的網路中部署報表伺服器，您就必須使用您剛剛指定的網域使用者帳戶來註冊報表伺服器的「服務主要名稱」(SPN)。 如需詳細資訊，請參閱[為報表伺服器註冊服務主體名稱 &#40;SPN&#41;](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md)。  
  
4.  按一下 **[套用]**。  
  
5.  如果出現提示要求備份對稱金鑰，請輸入對稱金鑰備份的檔案名稱和位置，然後輸入用來鎖定和解除檔案鎖定的密碼，再按一下 **[確定]**。  
  
6.  如果報表伺服器使用此服務帳戶來連接報表伺服器資料庫，將會更新連接資訊來使用新的帳戶或密碼。 更新連接資訊時，將需要連接到資料庫。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **[資料庫連接]** 對話方塊出現，請輸入有權連接此資料庫的認證，然後按一下 **[確定]**。  
  
7.  當系統提示您還原對稱金鑰時，請輸入您在步驟 5 中指定的密碼，然後按一下 **[確定]**。  
  
8.  檢閱 [結果] 窗格中的狀態訊息，以確認所有工作都已順利完成。  
  
## <a name="choosing-an-account"></a>選擇帳戶  
 為了取得最佳結果，請指定具有網路連接權限的帳戶，以存取網域控制站和企業的 SMTP 伺服器或閘道。 下表摘要列出這些帳戶並提供使用這些帳戶的建議。  
  
|帳戶|說明|  
|-------------|-----------------|  
|網域使用者帳戶|如果您的 Windows 網域使用者帳戶具有報表伺服器作業所需的最低權限，您應該使用此帳戶。<br /><br /> 建議使用網域使用者帳戶，因為它會將報表伺服器服務與其他應用程式隔離。 在共用帳戶 (如網路服務) 下執行多個應用程式增加了惡意使用者控管報表伺服器的風險，因為任何一個應用程式的安全性缺口都可輕易地延伸到在相同帳戶下執行的所有應用程式。<br /><br /> 請注意，如果您使用網域使用者帳戶，則當您的組織強制實施密碼到期原則時，您將必須定期變更密碼。 您也可能需要使用此使用者帳戶來註冊服務。 如需詳細資訊，請參閱[為報表伺服器註冊服務主體名稱 &#40;SPN&#41;](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md)。<br /><br /> 避免使用本機 Windows 使用者帳戶。 本機帳戶通常沒有足夠的權限可存取其他電腦上的資源。 如需使用本機帳戶如何限制報表伺服器功能的詳細資訊，請參閱本主題中的 [使用本機帳戶的考量](#localaccounts) 。|  
|**虛擬服務帳戶**|[虛擬服務帳戶] 代表 Windows 服務。 它是權限最低的內建帳戶，具有網路登入權限。 如果您沒有可用的網域使用者帳戶，或是您想要避免因密碼逾期原則所可能產生的任何服務中斷，則建議您使用此帳戶。|  
|**網路服務**|[網路服務] 是權限最低的內建帳戶，具有網路登入權限。 <br /><br /> 如果您選取 **[網路服務]**，請嘗試將相同帳戶下執行的其他服務數目降到最低。 任何一個應用程式的安全性缺口都將危害相同帳戶下執行之所有其他應用程式的安全。|  
|**本機服務**|**[本機服務]** 是一個內建帳戶，類似於經過驗證的本機 Windows 使用者帳戶。 以 **[本機服務]** 帳戶身分執行的服務會以不含認證的 Null 工作階段來存取網路資源。 此帳戶不適合內部網路部署狀況，在此狀況下，報表伺服器必須連接到遠端報表伺服器資料庫或網域控制站，才能在開啟報表或處理訂閱之前先驗證使用者。|  
|**本機系統**|**[本機系統]** 是具有高權限的帳戶，執行報表伺服器不需要使用它。 請避免使用此帳戶進行報表伺服器安裝。 請改為選擇網域帳戶或 **[網路服務]** 。|  
  
##  <a name="localaccounts"></a> 使用本機帳戶的考量  
 使用本機帳戶的主要考量為報表伺服器是否需要存取遠端資料庫伺服器、郵件伺服器和網域控制站。 如果您設定報表伺服器以本機 Windows 使用者帳戶、本機服務或本機系統的身分執行，您就必須考量您要如何設定其他組態設定，以及考量訂閱的建立和傳遞方式：  
  
-   如果使用本機帳戶執行服務，則您稍後在設定遠端報表伺服器資料庫的連接時，所能使用的選項將會受到限制。 更明確地說，如果您使用遠端報表伺服器資料庫，您就必須將連接設定為使用網域使用者帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫使用者 (該使用者具有登入遠端 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的權限)。  
  
-   如果使用本機帳戶執行服務，將會產生訂閱建立方面的新需求。 報表伺服器會儲存建立訂閱之使用者的相關資訊。 如果使用者在使用網域帳戶登入的期間建立訂閱，則報表伺服器服務會嘗試連接到網域控制站，以便在處理訂閱時驗證使用者。 如果此服務是使用本機帳戶執行，則當報表伺服器嘗試將要求傳送到遠端網域控制站時，驗證要求將會失敗。 若要處理這項限制，可以使用自訂的表單架構驗證延伸模組，或讓所有使用者使用本機使用者帳戶連接到報表伺服器。  
  
-   如果使用本機帳戶執行服務，將會產生訂閱傳遞方面的新需求。 有些傳遞延伸模組會在訂閱定義中包含使用者帳戶資訊。 如果您要將報表傳送到以網域使用者帳戶為基礎的電子郵件地址，而且您是使用本機帳戶來執行報表伺服器服務，則該服務就無法存取遠端網域控制站來解析目標電子郵件帳戶。  
  
-   不支援使用內建 Windows 服務帳戶 (本機服務或網路服務) 做為屬於網域控制站之電腦上的報表伺服器服務帳戶。  
  
本節中的下列指導方針和連結可以協助您決定最適合用於您的部署的方法。  
  
-   《SQL Server 線上叢書》中的[設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) 。  
  
-   MSDN 上的《[Services and Service Accounts Security Planning Guide](http://go.microsoft.com/fwlink/?LinkId=69155) 》。  
  
## <a name="updating-an-expired-password"></a>更新已過期的密碼  
 如果報表伺服器服務是以網域帳戶執行，而且在您可以於 Reporting Services 組態管理員內更新密碼以前，密碼就已經過期，則要先指定新的密碼，才能啟動該服務。  
  
 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服務帳戶密碼已過期，則當您嘗試連接至報表伺服器時便會發生 **rsReportServerDatabaseUnavailable** 錯誤。 重設密碼即可解決此錯誤。  
  
## <a name="troubleshooting-service-identity-update-errors"></a>排除服務識別更新錯誤  
 變更此服務識別會起始一連串的事件，其中包括重新啟動此服務、更新受密碼保護的加密金鑰、更新 URL 保留項目，以及更新報表伺服器資料庫連接資訊 (如果您使用此服務帳戶連接到報表伺服器資料庫)。 您可以檢視此頁面底部之 [結果] 窗格內的通知，以監視這些事件的狀態。 如果此程序進行期間發生錯誤，您可以使用以下方法嘗試加以解決：  
  
-   如果無法還原對稱金鑰，您可以使用 [加密金鑰] 頁面中的 **[還原]** ，嘗試手動將它還原。 如果這樣做無效，請考慮刪除加密的內容。 您將必須重新建立資料來源連接資訊和訂閱，但是仍然可以使用內容的其餘部分。 如需詳細資訊，請參閱 [備份與還原 Reporting Services 加密金鑰](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)。  
  
-   如果此服務無法啟動，請使用系統管理員工具內的服務主控台應用程式，手動將它重新啟動。  
  
-   當您更新此服務帳戶時，可能會發生 URL 保留項目錯誤。 每一個 URL 保留項目都包含一個內含「判別存取控制清單」(DACL) 的安全性描述項，該清單會授與服務帳戶接受 URL 要求的權限。 當您更新此帳戶時，必須重新建立此 URL，以便使用新的帳戶資訊來更新 DACL。 如果無法重新建立此 URL 保留項目，而且您知道此帳戶確實有效，請嘗試重新啟動電腦。 如果錯誤持續存在，請嘗試使用不同的帳戶。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表伺服器 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)
