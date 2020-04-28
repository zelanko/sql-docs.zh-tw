---
title: 設定服務帳戶（SSRS Configuration Manager） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Report Server Web service, accounts
- service accounts [Reporting Services]
- Report Server Windows service, accounts
- Web service [Reporting Services], report server
ms.assetid: 25000ad5-3f80-4210-8331-d4754dc217e0
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 04dff943d1227f84ff514e593f65c2ce4d7a918f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952578"
---
# <a name="configure-a-service-account-ssrs-configuration-manager"></a>設定服務帳戶 (SSRS 組態管理員)
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝中，報表伺服器 Web 服務、報表管理員和背景處理應用程式會在單一服務中執行。 當您在 [服務識別] 頁面中指定此服務執行所用的帳戶時，安裝期間會定義此帳戶，但是如果您想要使用不同的帳戶或更新密碼，可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具。  
  
 如果您擁有一個設定成使用 SharePoint 整合模式的報表伺服器，而且您使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具來變更服務帳戶，也必須開啟 SharePoint 管理中心並且使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **[授與資料庫存取權]** 頁面來重新套用報表伺服器和執行個體設定。 這個步驟會將 SharePoint 資料庫的存取權授與新的服務帳戶，而這是整合 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 與 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]所需的存取權。  
  
 一定要使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具來更新此服務帳戶，好讓與此服務識別相依的其他設定可以並行更新。  
  
> [!NOTE]  
>  不支援使用內建 Windows 服務帳戶 (本機服務或網路服務) 做為屬於網域控制站之電腦上的報表伺服器服務帳戶。  
  
 程序  
  
### <a name="to-configure-the-report-server-service-account"></a>若要設定報表伺服器服務帳戶  
  
1.  啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員，並連接到報表伺服器。  
  
2.  在 [服務帳戶] 頁面上，選取可描述您想要使用之帳戶類型的選項。 如需所要指定之帳戶類型的建議，請參閱[將報表伺服器服務帳戶設定 &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)。  
  
3.  如果您選取了 Windows 使用者帳戶，請指定新的帳戶和密碼。 此帳戶不能超過 20 個字元。  
  
     如果在支援 Kerberos 驗證的網路中部署報表伺服器，您就必須使用您剛剛指定的網域使用者帳戶來註冊報表伺服器的「服務主要名稱」(SPN)。 如需詳細資訊，請參閱[為報表伺服器註冊服務主體名稱 &#40;SPN&#41;](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md)。  
  
4.  按一下 [套用]  。  
  
5.  如果出現提示要求備份對稱金鑰，請輸入對稱金鑰備份的檔案名稱和位置，然後輸入用來鎖定和解除檔案鎖定的密碼，再按一下 **[確定]**。  
  
6.  如果報表伺服器使用此服務帳戶來連接報表伺服器資料庫，將會更新連接資訊來使用新的帳戶或密碼。 更新連接資訊時，將需要連接到資料庫。 如果  [資料庫連接][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **** 對話方塊出現，請輸入有權連線此資料庫的認證，然後按一下 [確定]****。  
  
7.  當系統提示您還原對稱金鑰時，請輸入您在步驟 5 中指定的密碼，然後按一下 **[確定]**。  
  
8.  檢閱 [結果] 窗格中的狀態訊息，以確認所有工作都已順利完成。  
  
## <a name="troubleshooting-service-identity-update-errors"></a>排除服務識別更新錯誤  
 變更此服務識別會起始一連串的事件，其中包括重新啟動此服務、更新受密碼保護的加密金鑰、更新 URL 保留項目，以及更新報表伺服器資料庫連接資訊 (如果您使用此服務帳戶連接到報表伺服器資料庫)。 您可以檢視此頁面底部之 [結果] 窗格內的通知，以監視這些事件的狀態。 如果此程序進行期間發生錯誤，您可以使用以下方法嘗試加以解決：  
  
-   如果無法還原對稱金鑰，您可以使用 [加密金鑰] 頁面中的 **[還原]** ，嘗試手動將它還原。 如果這樣做無效，請考慮刪除加密的內容。 您將必須重新建立資料來源連接資訊和訂閱，但是仍然可以使用內容的其餘部分。 如需詳細資訊，請參閱 [備份與還原 Reporting Services 加密金鑰](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)。  
  
-   如果此服務無法啟動，請使用系統管理員工具內的服務主控台應用程式，手動將它重新啟動。  
  
-   當您更新此服務帳戶時，可能會發生 URL 保留項目錯誤。 每一個 URL 保留項目都包含一個內含「判別存取控制清單」(DACL) 的安全性描述項，該清單會授與服務帳戶接受 URL 要求的權限。 當您更新此帳戶時，必須重新建立此 URL，以便使用新的帳戶資訊來更新 DACL。 如果無法重新建立此 URL 保留項目，而且您知道此帳戶確實有效，請嘗試重新啟動電腦。 如果錯誤持續存在，請嘗試使用不同的帳戶。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [設定報表伺服器服務帳戶 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [&#40;SSRS Configuration Manager 設定報表伺服器資料庫連接&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [服務帳戶 &#40;SSRS 原生模式&#41;](../../../2014/sql-server/install/service-account-ssrs-native-mode.md)   
 [設定和管理加密金鑰 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
