---
title: 進階多重網站組態 （SSRS 原生模式） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.advancedmultiplewebsiteconfig.F1
ms.assetid: af4ede43-2225-45b5-ae7e-9202411551ba
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 01ed7ed806cc064b05180347fa41905b57c4c98e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66096833"
---
# <a name="advanced-multiple-web-site-configuration-ssrs-native-mode"></a>進階多重網站組態 (SSRS 原生模式)
  使用此對話方塊可建立及管理用來存取報表伺服器或報表管理員的 URL。 **[進階多重網站組態]** 對話方塊是用來建立其他 URL (亦即包含主機標頭名稱的自訂 URL)，或是指定 IPv4 或 IPv6 格式的 IP 位址。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式。  
  
 如果您想要設定不同的方式來存取報表伺服器，建立多個 URL 將會非常實用。 例如，透過內部網路和外部網路連接的報表伺服器存取，通常需要對每一種連接類型都有不同的 URL。  
  
 若要開啟 **[進階多重網站組態]** 對話方塊，請在 **組態管理員的** [Web 服務 URL] **或** [報表管理員 URL] **頁面上按一下** [進階] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。 當 **[進階多重網站組態]** 對話方塊開啟之後，您可以按一下 **[加入]** 或 **[編輯]** ，以定義新的 URL 或是修改或刪除現有的 URL。  
  
 按一下 **[確定]** 儲存您的變更。 如果您加入或移除 URL，然後沒有先按一下 **[確定]** 就關閉此對話方塊，您的變更將會遺失。  
  
## <a name="options"></a>選項。  
 **IP 位址**  
 識別 TCP/IP 網路上的報表伺服器電腦。 有效值包括：  
  
-   **[全部指派]** 會指定指派給電腦的任何一個 IP 位址都可以用於指向報表伺服器應用程式的 URL。 這個值也包含易記主機名稱 (如電腦名稱)，網域名稱伺服器可將該名稱解析為指派給電腦的 IP 位址。 這是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 的預設值。  
  
-   **[全未指派]** 會指定報表伺服器將會接受未完全符合 IP 位址或主機名稱的任何要求。 如果有另一個 Web 應用程式已經在使用這個值，請勿使用它。 如果您這樣做，您將會中斷其他應用程式的服務。  
  
-   **[127.0.0.1]** 是用來存取 localhost， 它可支援報表伺服器電腦上的本機管理。 如果您只選取這個值，則只有在本機登入報表伺服器電腦的使用者才會擁有此應用程式的存取權。  
  
-   *Nnn.nnn.nnn.nnn* 是電腦網路卡的 IPv4 位址。 如果您的網路使用 IPv6 定址的 IP 位址會是 128 位元值的 8 4 位元組欄位，類似於下列格式：\<標頭 >:*nnnn:nnnn:nnnn:nnnn*。  
  
     如果您有多張網路卡，您會看到每一張網路卡都有一個 IP 位址。 如果您只選取這個值，它會將應用程式存取限制為只有該 IP 位址 (以及網域名稱伺服器對應至該位址的任何主機名稱)。 您無法使用 localhost 來存取報表伺服器，而且也不能使用安裝於報表伺服器電腦上之其他網路卡的 IP 位址。  
  
 **通訊埠**  
 指定報表伺服器用來監視要求的通訊埠。 通訊埠 80 是預設通訊埠。 如果您使用通訊埠 80，您不需要在 URL 中包含此通訊埠。 如果您使用任何其他連接埠號碼，您必須一律包含在 URL (例如 http://localhost:8181/reports)。  
  
 **主機標頭**  
 如果您已經在網域名稱伺服器上定義解析為電腦的主機標頭，您可以在設定報表伺服器存取的 URL 中指定該主機標頭。  
  
 主機標頭是可讓多個網站共用單一 IP 位址和通訊埠的唯一名稱。 主機標頭名稱要比 IP 位址和通訊埠編號更容易記得和輸入。 主機標頭名稱的一個範例為 www.adventure-works.com 。  
  
 **SSL 通訊埠**  
 為 SSL 連接指定通訊埠。 SSL 的預設通訊埠是 443。  
  
 **SSL 憑證**  
 指定您安裝在這部電腦上之 SSL 憑證的憑證名稱。 如果此憑證對應到萬用字元，您可以將它用於報表伺服器連接。  
  
 指定註冊憑證的完整電腦名稱。 所指定的名稱必須與註冊的憑證名稱相同。  
  
 您必須安裝了憑證，才能使用此選項。 您也必須修改 RSReportServer.config 檔案中的 UrlRoot 組態設定，使它指定註冊憑證之電腦的完整名稱。 如需詳細資訊，請參閱《 [線上叢書》中的](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) 在原生模式報表伺服器上設定 SSL 連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 **發給**  
 顯示建立憑證的電腦名稱。  
  
 **[加入]**  
 定義其他 URL。  
  
 **編輯**  
 修改 URL 語法的任何部分。  
  
 **移除**  
 從清單中清除 URL 項目。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [設定 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [設定報表伺服器 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
