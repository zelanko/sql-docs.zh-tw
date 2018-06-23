---
title: 使用報表伺服器驗證 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connections [Reporting Services], configuring
- connections [Reporting Services], accounts
- Windows authentication [Reporting Services]
- authentication [Reporting Services]
- Forms authentication
ms.assetid: 753c2542-0e97-4d8f-a5dd-4b07a5cd10ab
caps.latest.revision: 32
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 6ee89d1d6b01fe39f3798eef9f39c1ca460cc799
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029984"
---
# <a name="authentication-with-the-report-server"></a>使用報表伺服器驗證
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS) 會提供多種可設定選項，便於針對報表伺服器進行使用者及用戶端應用程式的驗證。 依預設，報表伺服器預設會使用 Windows 整合式驗證，以及假設用戶端及網路資源全都位於相同網域或信任網域的信任關係。 視網路拓撲及組織需求而定，您可以自訂用於 Windows 整合式驗證的驗證通訊協定，以及使用基本驗證，或是使用所提供的表單型驗證延伸模組。 每一個驗證類型都可以個別開啟或關閉。 如果您希望報表伺服器接受多種類型的要求，可以啟用一種以上的驗證。  
  
> [!NOTE]  
>  在舊版的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中，IIS 支援所有的驗證類型。 從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 版本開始，不再使用 IIS。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 在內部處理所有驗證要求。  
  
 所有要求存取至報表伺服器內容或作業的使用者或應用程式都必須在允許存取前驗證完畢。  
  
## <a name="authentication-types"></a>驗證類型  
 所有要求存取至報表伺服器內容或作業的使用者或應用程式都必須在允許存取前，使用報表伺服器上設定的驗證類型驗證完畢。 下表描述 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]支援的驗證類型。  
  
|AuthenticationType 名稱|HTTP 驗證層的值|預設使用|描述|  
|-----------------------------|-------------------------------------|---------------------|-----------------|  
|RSWindowsNegotiate|交涉|是|先嘗試使用 Windows 整合式驗證的 Kerberos 驗證，但是如果 Active Directory 無法將用戶端要求的票證授與報表伺服器，就會回到 NTLM。 只有當票證無法使用時，Negotiate 才會回到 NTLM。 如果第一次嘗試所產生的錯誤並不是遺失票證，報表伺服器不會進行第二次的嘗試。|  
|EnableAuthPersistance|NTLM|是|使用 Windows 整合式驗證的 NTLM。<br /><br /> 將不會在其他要求上委派或模擬認證。 後續的要求將遵循新的挑戰-回應序列。 根據網路安全性設定，系統可能會提示使用者輸入認證，否則將會以透明的方式處理驗證要求。|  
|RSWindowsKerberos|Kerberos|否|使用 Windows 整合式驗證的 Kerberos。 您必須藉由設定服務帳戶的安裝程式服務主要名稱 (SPN)，才能設定 Kerberos，而這需要具有網域管理員權限。 如果您使用 Kerberos 設定識別委派，要求報表之使用者的 Token 也可以用於提供資料給報表之外部資料來源的其他連接。<br /><br /> 在您指定 RSWindowsKerberos 之前，請確定您所使用的瀏覽器類型實際上可支援它。 如果您使用 Internet Explorer，Kerberos 驗證只能透過 Negotiate 來支援。 Internet Explorer 將不會構成一個直接指定 Kerberos 的驗證要求。|  
|RSWindowsBasic|[基本]|否|基本驗證定義在 HTTP 通訊協定中，而且只能用於驗證報表伺服器的 HTTP 要求。<br /><br /> 認證會以 base64 編碼的形式傳入 HTTP 要求中。 如果您使用基本驗證，請利用安全通訊端層 (SSL) 來加密使用者帳戶資訊，然後再透過網路傳送這項資訊。 SSL 提供了透過 HTTP TCP/IP 連接將連接要求從用戶端傳送到報表伺服器的加密通道。 如需詳細資訊，請參閱 [TechNet 網站上的](http://go.microsoft.com/fwlink/?LinkId=71123) 使用 SSL 加密機密資料 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。|  
|Custom|(Anonymous)|否|匿名驗證會指引報表伺服器忽略 HTTP 要求中的驗證標頭。 報表伺服器會接受所有的要求，但是會在您提供的自訂 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 表單驗證上呼叫來驗證使用者。<br /><br /> 只有當您部署自訂驗證模組來處理報表伺服器上的所有驗證要求時，才能指定 `Custom`。 您不能搭配預設 Windows 驗證延伸模組來使用 Custom 驗證類型。|  
  
## <a name="unsupported-authentication-methods"></a>支援的驗證方法  
 下列的驗證方法和要求不受到支援。  
  
|驗證方法|說明|  
|---------------------------|-----------------|  
|匿名|報表伺服器將不會接受來自匿名使用者的未驗證要求，但是包含自訂驗證延伸模組的部署除外。<br /><br /> 如果您在有設定基本驗證的報表伺服器上啟用報表產生器的存取，報表產生器將會接受未經過驗證的要求。<br /><br /> 在其他所有的情況下，當要求到達 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]之前，匿名使用者都會遭到拒絕，並產生「HTTP 狀態 401」拒絕存取的錯誤。 收到「401 拒絕存取」錯誤的用戶端必須使用有效的驗證類型來重新構成要求。|  
|單一登入技術 (SSO)|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中的單一登入技術並沒有原生支援。 如果您想要使用單一登入技術，您必須建立自訂驗證延伸模組。<br /><br /> 主控環境的報表伺服器不支援 ISAPI 篩選。 如果您所使用的 SSO 技術實作為 ISAPI 篩選，請考慮針對 RSASecueID 或 RADIUS 通訊協定使用 ISA Server 內建支援。 否則，您可以建立 ISA Server ISAPI 或 HTTPModule for RS，但是建議您直接使用 ISA Server。|  
|Passport|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]不支援此項目。|  
|Digest|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]不支援此項目。|  
  
## <a name="configuration-of-authentication-settings"></a>設定驗證設定  
 當保留報表伺服器 URL 時，會將驗證設定設定為使用預設安全性。 如果您錯誤地修改這些設定，報表伺服器將會針對無法驗證的 HTTP 要求傳回「HTTP 401 拒絕存取」錯誤。 選擇驗證類型時，您必須已經知道您的網路支援 Windows 驗證的方式。 至少必須指定一個驗證類型。 可以針對 RSWindows 指定多個驗證類型。 RSWindows 驗證類型 (也就是`RSWindowsBasic`， `RSWindowsNTLM`， `RSWindowsKerberos`，和**RSWindowsNegotiate**) 與自訂互斥。  
  
> [!IMPORTANT]  
>  Reporting Services 不會驗證您所指定的設定來判斷它們對於您的運算環境是否正確。 預設安全性無法在您的安裝中運作，或是您指定的組態設定對於安全性基礎結構無效，都是有可能發生的事情。 因此，您一定要先在受到控制的測試環境中仔細測試您的報表伺服器部署，然後才可以將它提供給較大的組織使用。  
  
 報表伺服器 Web 服務和報表管理員一定會使用相同的驗證類型。 您無法針對報表伺服器服務的功能區來設定不同的驗證類型。 如果您具有向外延展部署，請務必複製部署中所有節點的所有變更。 在相同的向外延展部署中，您不能設定不同的節點使用不同的驗證類型。  
  
 背景處理不接受來自使用者的要求，但是它會驗證自動執行目的的所有要求。 它一定會使用 Windows 驗證，然後使用報表伺服器服務或自動執行帳戶 (如果有設定的話) 來驗證要求。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [設定報表伺服器上的 Windows 驗證](configure-windows-authentication-on-the-report-server.md)  
  
-   [設定報表伺服器上的基本驗證](configure-basic-authentication-on-the-report-server.md)  
  
-   [設定報表伺服器上的自訂或表單驗證](configure-custom-or-forms-authentication-on-the-report-server.md)  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|連結|  
|-----------------------|-----------|  
|設定 Windows 整合式驗證類型。|[設定報表伺服器上的 Windows 驗證](configure-windows-authentication-on-the-report-server.md)|  
|設定基本驗證類型。|[設定報表伺服器上的基本驗證](configure-basic-authentication-on-the-report-server.md)|  
|設定表單型驗證或是自訂驗證類型。|[設定報表伺服器上的自訂或表單驗證](configure-custom-or-forms-authentication-on-the-report-server.md)|  
|啟用報表管理員以處理自訂驗證狀況。|[設定報表管理員傳遞自訂驗證 Cookie](configure-the-web-portal-to-pass-custom-authentication-cookies.md)|  
  
## <a name="see-also"></a>另請參閱  
 [在原生模式報表伺服器上授與權限](granting-permissions-on-a-native-mode-report-server.md)   
 [RSReportServer 組態檔](../report-server/rsreportserver-config-configuration-file.md)   
 (建立-和-管理-角色-assignments.md)   
 [指定報表資料來源的認證及連線資訊](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
 [實作安全性延伸模組](../extensions/security-extension/implementing-a-security-extension.md)   
 [原生模式報表伺服器上設定 SSL 連接](configure-ssl-connections-on-a-native-mode-report-server.md)   
 [設定報表產生器存取](../report-server/configure-report-builder-access.md)   
 [安全性延伸模組概觀](../extensions/security-extension/security-extensions-overview.md)   
 [Reporting Services 中的驗證](../extensions/security-extension/authentication-in-reporting-services.md)   
 [Reporting Services 中的授權](../extensions/security-extension/authorization-in-reporting-services.md)  
  
  