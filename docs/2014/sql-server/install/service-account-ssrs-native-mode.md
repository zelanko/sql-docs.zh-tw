---
title: 服務帳戶 （SSRS 原生模式） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.serviceaccount.F1
ms.assetid: face8120-4d32-4c6c-a1e8-99f27d1ff15d
caps.latest.revision: 8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 36b1b0621cd660855638e4fa0a936e9700efb4d5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37153549"
---
# <a name="service-account-ssrs-native-mode"></a>服務帳戶 (SSRS 原生模式)
  使用 [服務帳戶] 頁面，即可指定報表伺服器服務執行所用的帳戶。 此帳戶是在安裝期間進行初始設定。 如果想要變更帳戶或密碼，就可以修改它。 報表伺服器 Web 服務、報表管理員和背景處理應用程式都會使用您在此頁面上指定的服務識別來執行。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式。  
  
 您為報表伺服器服務所指定的帳戶需要可存取登錄、報表伺服器程式檔和報表伺服器資料庫的權限。 當您使用時，會有所有的權限的帳戶自動設定[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Configuration Manager 來設定此帳戶。 如果您使用的服務帳戶來連接到報表伺服器資料庫時，Configuration Manager 會建立資料庫登入帳戶，並設定資料庫權限上時，將帳戶指派給 RSExecRole[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]裝載執行個體報表伺服器資料庫。 報表伺服器資料庫是報表伺服器寫入的唯一資料存放區， 此服務帳戶不需要任何其他資料存放區的權限。  
  
 若要開啟此頁面，請啟動[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Configuration Manager，然後選取 [瀏覽] 窗格中的連結。 如需詳細資訊，請參閱 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
> [!IMPORTANT]  
>  每當您需要更新帳戶或密碼，強烈建議您改用[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Configuration Manager。 使用組態管理員更新帳戶可確保取決於此服務識別的其他內部設定會同時自動更新。  
  
## <a name="options"></a>選項。  
 **使用內建帳戶**  
 從清單中選取 **[網路服務]**、 **[本機系統]** 或 **[本機服務]** 。 只建議您使用 **[網路服務]** ；但是，您可以設定此帳戶使用任何可用的帳戶。  
  
 **使用其他帳戶**  
 選取這個選項可指定 Windows 使用者帳戶。 您可以輸入本機 Windows 使用者帳戶或網域使用者帳戶。 以此格式指定網域帳戶： *\<網域 >\\< 使用者\>*。 以此格式指定本機 Windows 使用者帳戶： *\<電腦名稱 >\\< 使用者\>*。 您只能選取現有的帳戶；您無法在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態中建立新帳戶。  
  
 此帳戶的最大字元限制為 20 個字元。  
  
 如果您的網路使用 Kerberos 驗證，而且您設定報表伺服器在網域使用者帳戶下執行，您就必須使用此使用者帳戶註冊服務。 如需詳細資訊，請參閱[為報表伺服器註冊服務主體名稱 &#40;SPN&#41;](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md)。  
  
 如果您切換帳戶類型 (例如，以其他 Windows 帳戶來取代某個 Windows 帳戶，或是以 Windows 網域帳戶來取代內建帳戶)，系統就會提示您建立加密金鑰的備份副本。 當您選取了新帳戶，就會自動還原備份複本。  
  
> [!NOTE]  
>  每當您修改服務帳戶時，[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員都會提示您備份及還原加密金鑰。 為了確保已加密的資料仍能供報表伺服器使用，這些步驟是必要的。 如需有關這些動作的詳細資訊，請參閱 <<c0> [ 加密金鑰&#40;SSRS 原生模式&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)。</c0>  
  
 此外，如果您是報表伺服器設定為執行以 SharePoint 整合模式，而且您變更服務帳戶使用[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]組態管理員 中，您必須開啟 SharePoint 管理中心內，並使用[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**授與資料庫存取權**頁面來重新套用報表伺服器和執行個體設定。 此步驟中將新服務帳戶存取權授與 SharePoint 資料庫中，所需的整合[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]與 SharePoint 產品或技術。 如需如何授與在 SharePoint 管理中心內的資料庫存取權的詳細資訊，請參閱[設定和管理報表伺服器的&#40;Reporting Services SharePoint 模式&#41;](../../../2014/reporting-services/configure-administer-report-server-reporting-services-sharepoint-mode.md)並[Reporting Services SharePoint 模式安裝&#40;SharePoint 2010 和 SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)。  
  
## <a name="choosing-an-account"></a>選擇帳戶  
 為了取得最佳結果，請指定具有網路連接權限的帳戶，以存取網域控制站和企業的 SMTP 伺服器或閘道。 下表摘要列出這些帳戶並提供使用這些帳戶的建議。  
  
|帳戶|說明|  
|-------------|-----------------|  
|網域使用者帳戶|如果您的 Windows 網域使用者帳戶具有報表伺服器作業所需的最低權限，您應該使用此帳戶。<br /><br /> 建議使用網域使用者帳戶，因為它會將報表伺服器服務與其他應用程式隔離。 在共用帳戶 (如網路服務) 下執行多個應用程式增加了惡意使用者控管報表伺服器的風險，因為任何一個應用程式的安全性缺口都可輕易地延伸到在相同帳戶下執行的所有應用程式。<br /><br /> 如果您設定報表伺服器進行限制委派，或是用於搭配 SharePoint 2010 產品的 SharePoint 整合模式 (這些產品需要網域使用者帳戶而不是內建電腦帳戶)，此時就需要網域使用者帳戶。<br /><br /> 請注意，如果您使用網域使用者帳戶，則當您的組織強制實施密碼到期原則時，您將必須定期變更密碼。 您也可能需要使用此使用者帳戶來註冊服務。 如需詳細資訊，請參閱[為報表伺服器註冊服務主體名稱 &#40;SPN&#41;](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md)。<br /><br /> 避免使用本機 Windows 使用者帳戶。 本機帳戶通常沒有足夠的權限可存取其他電腦上的資源。 如需使用本機帳戶如何限制報表伺服器功能的詳細資訊，請參閱本主題中的 [使用本機帳戶的考量](#localaccounts) 。|  
|**網路服務**|[網路服務] 是權限最低的內建帳戶，具有網路登入權限。 如果您沒有可用的網域使用者帳戶，或是您想要避免因密碼逾期原則所可能產生的任何服務中斷，則建議您使用此帳戶。<br /><br /> 如果您選取 **[網路服務]**，請嘗試將相同帳戶下執行的其他服務數目降到最低。 任何一個應用程式的安全性缺口都將危害相同帳戶下執行之所有其他應用程式的安全。|  
|**本機服務**|**[本機服務]** 是一個內建帳戶，類似於經過驗證的本機 Windows 使用者帳戶。 以 **[本機服務]** 帳戶身分執行的服務會以不含認證的 Null 工作階段來存取網路資源。 此帳戶不適合內部網路部署狀況，在此狀況下，報表伺服器必須連接到遠端報表伺服器資料庫或網域控制站，才能在開啟報表或處理訂閱之前先驗證使用者。|  
|**本機系統**|**[本機系統]** 是具有高權限的帳戶，執行報表伺服器不需要使用它。 請避免使用此帳戶進行報表伺服器安裝。 請改為選擇網域帳戶或 **[網路服務]** 。|  
  
##  <a name="localaccounts"></a> 使用本機帳戶的考量  
 使用本機帳戶的主要考量為報表伺服器是否需要存取遠端資料庫伺服器、郵件伺服器和網域控制站。 如果您設定報表伺服器以本機 Windows 使用者帳戶、本機服務或本機系統的身分執行，您就必須考量您要如何設定其他組態設定，以及考量訂閱的建立和傳遞方式：  
  
-   如果使用本機帳戶執行服務，則您稍後在設定遠端報表伺服器資料庫的連接時，所能使用的選項將會受到限制。 更明確地說，如果您使用遠端報表伺服器資料庫，您就必須將連接設定為使用網域使用者帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫使用者 (該使用者具有登入遠端 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的權限)。  
  
-   如果使用本機帳戶執行服務，將會產生訂閱建立方面的新需求。 報表伺服器會儲存建立訂閱之使用者的相關資訊。 如果使用者在使用網域帳戶登入的期間建立訂閱，則報表伺服器服務會嘗試連接到網域控制站，以便在處理訂閱時驗證使用者。 如果此服務是使用本機帳戶執行，則當報表伺服器嘗試將要求傳送到遠端網域控制站時，驗證要求將會失敗。 若要處理這項限制，可以使用自訂的表單架構驗證延伸模組，或讓所有使用者使用本機使用者帳戶連接到報表伺服器。  
  
-   如果使用本機帳戶執行服務，將會產生訂閱傳遞方面的新需求。 有些傳遞延伸模組會在訂閱定義中包含使用者帳戶資訊。 如果您要將報表傳送到以網域使用者帳戶為基礎的電子郵件地址，而且您是使用本機帳戶來執行報表伺服器服務，則該服務就無法存取遠端網域控制站來解析目標電子郵件帳戶。  
  
-   不支援使用內建 Windows 服務帳戶 (本機服務或網路服務) 做為屬於網域控制站之電腦上的報表伺服器服務帳戶。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表伺服器服務帳戶 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [設定服務帳戶&#40;SSRS 組態管理員&#41;](../../../2014/sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)   
 [Reporting Services 組態管理員 F1 說明主題&#40;SSRS 原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)  
  
  
