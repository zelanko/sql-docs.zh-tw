---
title: 建立網站對話方塊 (Master Data Services 組態管理員) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.createsite.f1
ms.assetid: 179c9c1e-3b06-421b-b71b-1cb64d104f5e
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c7021ff628c0b5da5b95c0eacf141596ecf63e41
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48143318"
---
# <a name="create-website-dialog-box-master-data-services-configuration-manager"></a>建立網站對話方塊 (Master Data Services 組態管理員)
  使用 **[建立網站]** 對話方塊可在本機電腦上建立新的網站。 當您在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中建立網站時，網站會新增至本機電腦上的 Internet Information Services (IIS)，而且包含設定為 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式的根應用程式。 也會建立新的應用程式集區，而 Web 應用程式會放在該應用程式集區內。  
  
## <a name="web-site"></a>網站  
  
|控制項名稱|描述|  
|------------------|-----------------|  
|**網站名稱**|輸入網站的名稱或使用預設名稱。 這個名稱是僅用來識別 IIS 中站台的易記名稱。 它不是用來從 Web 瀏覽器存取網站。<br /><br /> 此名稱在本機電腦上 IIS 的所有網站當中必須是唯一的。|  
|**通訊協定**|顯示 **http**。 當您不需要透過加密通道進行用戶端和伺服器通訊時，請選取超文字傳輸協定 (HTTP)。<br /><br /> 注意：您無法在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中建立 HTTPS 網站。 HTTPS 是使用安全通訊端層 (SSL) 的 HTTP 通訊協定，而且當您交換機密或個人資料，或是當您希望使用者先確認伺服器的識別再傳輸個人資訊時，將會很實用。 如果您需要透過加密通道在用戶端和伺服器之間傳輸資訊，必須使用 IIS 工具 (如 IIS 管理員) 來設定具有 HTTPS 繫結的網站，並將網站繫結與伺服器憑證產生關聯，在您於 Web 瀏覽器中成功開啟網站之前需要這項處理。 如需有關伺服器憑證的詳細資訊，請參閱 [TechNet 上的](http://go.microsoft.com/fwlink/?LinkId=163220) IIS 7.0：在 IIS 7.0 中設定伺服器憑證 [!INCLUDE[msCoName](../includes/msconame-md.md)] 。|  
|**IP 位址**|選取使用者可用來存取網站的 IP 位址。 預設會選取 **[全未指派]** 。 除非您有理由要使用特定的 IPv4 或 IPv6 位址，否則請使用預設值。<br /><br /> 當您選取 **[全未指派]** 時，這個網站會回應您所指定之通訊埠和選擇性主機名稱上所有 IP 位址的要求。 如果伺服器上的另一個網站在相同的通訊埠上擁有繫結，但使用特定的 IP 位址，該網站會接收該通訊埠與特定 IP 位址的 HTTP 要求，而且具有 **[全未指派]** IP 位址的網站會接收送到該通訊埠與其他 IP 位址的所有其他 HTTP 要求。|  
|**通訊埠**|輸入對這個網站所做之要求的通訊埠。 如果您選取 HTTP 通訊協定，預設通訊埠為 80。 如果您指定與預設通訊埠不同的通訊埠，用戶端就必須指定通訊埠編號，才能連接網站。<br /><br /> 注意：IIS 中的 [預設的網站]  會設定為在所有未指派 IP 位址的通訊埠 80 上使用 HTTP 通訊協定。 如果您嘗試在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中使用預設繫結資訊來建立網站，您會收到一個錯誤，指出有重複的繫結存在。 您必須在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中變更網站的繫結資訊，或是使用 IIS 工具 (如 IIS 管理員) 來變更預設網站的繫結資訊。 或者您也可以指定主機標頭，讓 IIS 以唯一的方式識別網站。 請務必設定您的防火牆，以接受透過您指定之通訊埠的流量。|  
|**主機標頭**|選擇性的值。 輸入主機標頭名稱。 當您想要將主機名稱 (也稱為網域名稱) 指派給使用單一 IP 位址或通訊埠的電腦時，請使用這個選項。 當您指定主機名稱時，用戶端必須使用該名稱而非 IP 位址來存取網站。 當您設定主機名稱時，要等到 DNS 伺服器擁有該主機名稱的項目之後，您才可以在 Web 瀏覽器中開啟網站。<br /><br /> 例如，如果您希望使用者存取網站 http://www.contoso.com/，您必須指定 www.contoso.com 當作主機名稱，而且 DNS 伺服器必須擁有這個主機名稱的項目。<br /><br /> 如果內部網路上可以使用您的網站，當使用者在瀏覽器鍵入伺服器名稱 (例如 http://server_name) 時，您就不必指定主機名稱。 不過，如果您環境中的 DNS 伺服器設定為儲存此 Web 伺服器的其他名稱，您可以建立每個主機名稱的個別繫結，好讓使用者可以使用 DNS 伺服器所儲存的其他名稱。 如果您必須為網站設定一個以上的主機名稱，請使用 IIS 工具 (如 IIS 管理員) 來加入其他網站繫結。|  
  
## <a name="application-pool"></a>應用程式集區  
  
|控制項名稱|描述|  
|------------------|-----------------|  
|**名稱**|請輸入新應用程式集區的唯一易記名稱，或使用所提供的預設名稱。 這個網站的根 Web 應用程式會在此應用程式集區中執行。<br /><br /> 應用程式集區提供了界限，可防止一個應用程式集區中的應用程式影響另一個應用程式集區中的應用程式。|  
|**使用者名稱**|輸入 Active Directory 中的網域和使用者名稱。 此帳戶是 Web 應用程式在其中執行之應用程式集區的識別。<br /><br /> 這個帳戶會加入至 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫的 mds_exec 資料庫角色，來進行資料庫存取。 如需詳細資訊，請參閱[資料庫登入、使用者和角色 &#40;Master Data Services&#41;](database-logins-users-and-roles-master-data-services.md)。 它也會新增至 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Windows 群組 (**MDS_ServiceAccounts**)，而這個群組在檔案系統中已被授與暫存編譯目錄 **MDSTempDir** 的權限。 如需詳細資訊，請參閱[資料夾和檔案的權限 &#40;Master Data Services&#41;](../../2014/master-data-services/folder-and-file-permissions-master-data-services.md)。|  
|**密碼**|輸入指定之使用者帳戶的密碼。|  
|**確認密碼**|重新輸入指定之使用者帳戶的密碼。 **[密碼]** 和 **[確認密碼]** 欄位必須包含相同的密碼。|  
  
## <a name="see-also"></a>另請參閱  
 [Web 組態 頁面&#40;Master Data Services 組態管理員&#41;](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md)   
 [設定 Master Data Services 資料庫和網站](../../2014/master-data-services/set-up-the-database-and-website-for-master-data-services.md)   
 [Web 應用程式需求&#40;Master Data Services&#41;](install-windows/web-application-requirements-master-data-services.md)   
 [建立主資料管理員 Web 應用程式 &#40;Master Data Services&#41;](install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
