---
title: "設定報表伺服器 Url （SSRS 組態管理員） |Microsoft 文件"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Report Server Windows service, virtual directories
- report servers [Reporting Services], virtual directories
- virtual directories [Reporting Services]
- Report Manager [Reporting Services], virtual directories
ms.assetid: a0134ef0-086c-443e-93b9-7213a3d76393
caps.latest.revision: 10
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 9e69b9e38fde1183d4bd77b7759faf25b6a4ec50
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="configure-report-server-urls--ssrs-configuration-manager"></a>設定報表伺服器 URL (SSRS 組態管理員)
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，URL 是用來存取報表伺服器 Web 服務和 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]。 在您可以使用其中一個應用程式以前，您至少必須為此 Web 服務和 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]設定一個 URL。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 將會針對在大多數部署方案下運作良好的這兩個應用程式 URL 提供預設值，其中包括與其他 Web 服務和應用程式並存的部署。  
  
-   如果您安裝了預設組態，就表示已經使用預設值自動建立 URL。  
  
-   如果您要使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具來建立或修改 URL，您可以接受 URL 的預設值或是指定自訂值。 當您定義此 URL 時，頁面上會出現此 URL 的測試連結，好讓您可以立刻確認您所指定的設定可產生有效的連接。 如需如何設定及測試 URL 的逐步指示，請參閱 [設定 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)。  
  
## <a name="defining-a-report-server-url"></a>定義報表伺服器 URL  
 此 URL 會精確識別報表伺服器應用程式執行個體在網路上的位置。 當您建立報表伺服器 URL 時，必須指定以下部分。  
  
|部分|描述|  
|----------|-----------------|  
|主機名稱|TCP/IP 網路會使用 IP 位址來唯一識別網路上的裝置。 電腦上安裝的每一張網路卡都有一個實體 IP 位址。 如果此 IP 位址解析成主機標頭，您就可以指定主機標頭。 如果您正在企業網路上部署報表伺服器，可以使用電腦的網路名稱。|  
|通訊埠|TCP 通訊埠是裝置上的端點。 報表伺服器將會接聽指定之通訊埠上的要求。|  
|虛擬目錄|通訊埠通常是由多個 Web 服務或應用程式所共用。 因此，報表伺服器 URL 一定會包含可對應至取得要求之應用程式的虛擬目錄。 您必須針對接聽相同 IP 位址和通訊埠的每一個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 應用程式指定唯一的虛擬目錄名稱。|  
|SSL 設定|您可以將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的 URL 設定為使用之前安裝在電腦上的現有 SSL 憑證。 如需詳細資訊，請參閱《 [線上叢書》中的](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) 在原生模式報表伺服器上設定 SSL 連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
  
## <a name="default-urls"></a>預設 URL  
 當您透過 URL 存取報表伺服器或 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 時，此 URL 應該包含主機名稱，而不是 IP 位址。 在 TCP/IP 網路上，IP 位址將會解析為主機名稱 (或是電腦的網路名稱)。 如果您使用預設值來設定 URL，您應該能夠使用將電腦名稱或 localhost 指定為主機名稱的 URL 來存取報表伺服器 Web 服務：  
  
-   `http://<computername>/reportserver`  
  
-   `http://localhost/reportserver`  
  
 讓這些 URL 可用的設定會出現在下表中， 這個表格會顯示可透過包含主機名稱的 URL 來啟用報表伺服器連接的預設值：  
  
|部分|值|說明|  
|----------|-----------|-----------------|  
|IP 位址|全部指派|網路上的網域名稱服務會將 URL 上的主機名稱解析為電腦的 IP 位址。 只要您定義的 URL 中有指定此 IP 位址，傳送給特定主機的要求都將到達所要的目標。|  
|通訊埠|80|通訊埠 80 是電腦上 TCP/IP 連接的預設通訊埠。 由於報表伺服器會接聽通訊埠 80，所以您可以省略 URL 中的通訊埠編號。 如果您指定另一個通訊埠，就必須在 URL 中指定它。|  
|虛擬目錄|ReportServer|請注意，這兩個範例 URL 都包含虛擬目錄名稱。 除非您自訂 URL 定義，否則您一定要在 URL 上指定應用程式的虛擬目錄名稱。|  
  
> [!NOTE]  
>  基礎 URL 保留項目會啟用 URL 上所要使用的任何有效主機名稱。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具會使用可允許主機名稱變化的語法來解析為特定的報表伺服器執行個體，以便在 HTTP.SYS 中建立 URL 保留項目。 如需 URL 保留項目的詳細資訊，請參閱 [關於 URL 保留項目和註冊 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md)。  
  
## <a name="server-side-permissions-on-a-report-server-url"></a>報表伺服器 URL 的伺服器端權限  
 每一個 URL 端點的權限會專門授與給報表伺服器服務帳戶。 只有這個帳戶具有可接受導向 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 之要求的權限。 當您透過安裝程式或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具來設定服務識別時，將會為此帳戶建立及維護判別存取控制清單 (DACL)。 如果您變更此服務帳戶， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具將會更新您建立來收取新帳戶資訊的所有 URL 保留項目。 如需詳細資訊，請參閱《 [URL 保留項目語法 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md)。  
  
## <a name="authenticating-client-requests-sent-to-a-report-server-url"></a>驗證傳送給報表伺服器 URL 的用戶端要求  
 根據預設，在 URL 端點上支援的驗證類型為 Windows 驗證。 這是預設的安全性延伸模組。 如果您要實作自訂或表單驗證提供者，您必須修改報表伺服器上的驗證設定。 您也可以選擇變更 Windows 驗證設定，使其符合網路中使用的驗證子系統。 如需詳細資訊，請參閱《 [線上叢書》中的](../../reporting-services/security/authentication-with-the-report-server.md) 使用報表伺服器驗證 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="in-this-section"></a>本節內容  
 [設定 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
 此主題提供在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具中設定及修改 URL 保留項目的指示。  
  
 [關於 URL 保留項目和註冊 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md)  
 URL 是用來存取應用程式和報表。 此主題將說明應用程式 URL、預設 URL，以及 URL 保留項目和註冊在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中的運作方式。  
  
 [URL 保留項目語法 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md)  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用的預設 URL 保留項目對於大多數狀況是有效的。 但是，如果您想要限制存取或擴充部署來啟用網際網路或外部網路存取，您可能必須自訂設定以符合您的需求。 此主題將描述 URL 保留項目的語法，並提供為部署建立自訂保留項目的建議。  
  
 [組態檔中的 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)  
 RSReportServer.config 檔包含了多個 URL 保留項目，以及 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 和報表伺服器電子郵件傳遞所使用的 URL。 此主題將摘要列出 URL 組態設定，好讓您可以了解其比較方式。  
  
 [多重執行個體報表伺服器部署的 URL 保留項目 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/url-reservations-for-multi-instance-report-server-deployments.md)  
 當您在單一電腦上安裝多個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體時，您便增加了在註冊 URL 時遇到 URL 重複的機率。 為了避免這些錯誤，請遵循本主題的建議來建立執行個體特有的 URL 保留項目。  
  
## <a name="see-also"></a>另請參閱  
 [設定 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) 

