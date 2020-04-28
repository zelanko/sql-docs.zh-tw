---
title: Web 服務 URL （SSRS 原生模式） |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.reportservervirtualdirectory.F1
helpviewer_keywords:
- Reporting Services, Web service
ms.assetid: 9d210b5d-2a08-4e56-a4f5-c16715b00d79
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 01e5393ae638ddcecd04211a0a7e01e8116346a9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952358"
---
# <a name="web-service-url-ssrs-native-mode"></a>Web 服務 URL (SSRS 原生模式)
  使用 [Web 服務 URL] 頁面可設定或修改用來存取報表伺服器的 URL。 將會根據您指定的 URL 來建立 *「URL 保留項目」* 。 此 URL 保留項目會針對後續可用來存取報表伺服器 Web 服務的所有 URL 來定義語法和規則。 它會針對此報表伺服器 Web 服務指定前置詞、主機、通訊埠和虛擬目錄。 根據您指定主機的方式而定，單一保留項目可能會有多個 URL。 主機的預設值會指定強式萬用字元， 強式萬用字元可讓您在 URL 中指定任何可解析為主控報表伺服器之電腦的主機名稱。 如需 URL 設定和保留的詳細資訊，請參閱[configure a url &#40;ssrs Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)和[configure &#40;ssrs Configuration Manager&#41;的報表伺服器 url ](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]原生模式。  
  
 若要開啟此頁面，請啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員，並按一下導覽窗格中的 **[Web 服務 URL]** 。 如需詳細資訊，請參閱 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
 此頁面會提供報表伺服器 URL 中常用的值。 如果您想要建立其他 URL、使用主機標頭，或是指定特定格式的 IP 位址，請按一下 **[進階]**。  
  
 當您按一下 **[套用]** 之後，此頁面上將會出現此 Web 服務的連結。 如果您在建立報表伺服器資料庫之前按一下此連結，您可以預期會看到「找不到網頁」錯誤。 一旦設定此資料庫之後，這個錯誤將不再出現。 如需詳細資訊，請參閱[建立原生模式報表伺服器資料庫 &#40;SSRS 設定管理員&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)。  
  
 如果您已重新安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，然後發現您在嘗試使用 [全部指派] 的預設 IP 位址值和通訊埠 80 時得到錯誤，通常可以在重新啟動此服務之後，重新建立 URL 來解決錯誤。  
  
## <a name="options"></a>選項  
 **虛擬目錄**  
 為報表伺服器 Web 服務指定虛擬目錄名稱。 相同電腦上的每一個報表伺服器 Web 服務執行個體只能有一個虛擬名稱。  
  
 **IP 位址**  
 識別 TCP/IP 網路上的報表伺服器電腦。 有效值包括：  
  
-   **[全部指派]** 會指定指派給電腦的任何一個 IP 位址都可以用於指向報表伺服器應用程式的 URL。 這個值也包含易記主機名稱 (如電腦名稱)，網域名稱伺服器可將該名稱解析為指派給電腦的 IP 位址。 這是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 的預設值。  
  
-   **[全未指派]** 會指定報表伺服器將會接受未完全符合 IP 位址或主機名稱的任何要求。 如果有另一個 Web 應用程式已經在使用這個值，請勿使用它。 如果您這樣做，您將會中斷其他應用程式的服務。  
  
-   **[127.0.0.1]** 是用來存取 localhost， 它可支援報表伺服器電腦上的本機管理。 如果您只選取這個值，則只有在本機登入報表伺服器電腦的使用者才會擁有此應用程式的存取權。  
  
-   *Nnn.nnn.nnn.nnn* 是電腦網路卡的 IPv4 位址。 如果您的網路使用 IPv6 位址，則 IP 位址會是 8 4 位元組欄位的128位值，如下格式所示： \<標頭>：*nnnn： nnnn： nnnn： nnnn*  
  
     如果您有多張網路卡，您會看到每一張網路卡都有一個 IP 位址。 如果您只選取這個值，它會將應用程式存取限制為只有該 IP 位址 (以及網域名稱伺服器對應至該位址的任何主機名稱)。 您無法使用 localhost 來存取報表伺服器，而且也不能使用安裝於報表伺服器電腦上之其他網路卡的 IP 位址。  
  
 **TCP 埠**  
 指定報表伺服器用來監視 HTTP 要求的通訊埠，看看是否有包含報表伺服器虛擬目錄名稱的 URL。  
  
 **SSL 憑證**  
 將憑證繫結至您所指定的 IP 位址。 您必須在電腦上安裝及設定此憑證。 Reporting Services 不提供用來管理憑證的功能。 此憑證必須發行到解析為 IP 位址的主機名稱或電腦名稱。 例如，若要使用發行給http://salesreports的憑證，您指定的 IP 位址必須解析為名為 "salesreports" 的伺服器。  
  
 如果您要使用憑證，也必須修改 RSReportServer.config 檔案中的 `UrlRoot` 組態設定，使它指定註冊憑證之電腦的完整名稱。 如需詳細資訊，請參閱《 [線上叢書》中的](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) 在原生模式報表伺服器上設定 SSL 連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 **SSL 通訊埠**  
 為 SSL 連接指定通訊埠。  
  
 **URL**  
 顯示為目前報表伺服器執行個體定義的 URL。  
  
 **進階**  
 按一下此項目，即可為目前的應用程式執行個體建立其他 URL。  
  
> [!NOTE]
>  如果您有現有的 SSL 繫結和 URL 保留項目，而您想要變更 SSL 繫結，例如使用不同的憑證或主機標頭，則建議您依序完成以下步驟：  
> 
>  1.  先移除所有 URL 保留項目。  
> 2.  然後移除所有 SSL 繫結。  
> 3.  然後重新建立 URL 和 SSL 繫結。  
> 
>  前述步驟可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員完成。  
> 
>  Microsoft Windows 針對每個 IP 位址與通訊埠組合支援一個繫結。 如果您將報表伺服器設定為使用特定主機標頭值，同時將通訊埠至 IP 位址組合上的憑證發給不同的主機標頭值，則會在瀏覽器中看見一個警告，指出憑證與所使用的 URL 不相符。  
> 
>  若要更正這個問題，請刪除所有繫結，然後使用唯一的設定建立新繫結，或設定包含萬用字元的 Reporting Services URL 註冊。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態管理員 &#40;SSRS 原生模式的 F1 說明主題&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [設定報表伺服器 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
