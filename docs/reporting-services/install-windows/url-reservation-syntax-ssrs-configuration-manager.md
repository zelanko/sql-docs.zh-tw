---
title: URL 保留項目語法 (SSRS 設定管理員) | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- URL reservations
ms.assetid: 30e4be2e-e65d-462c-895a-5a0a636d042f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2aba888fd9dee3c96cf87310e1987edd851884c5
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43270440"
---
# <a name="url-reservation-syntax--ssrs-configuration-manager"></a>URL 保留項目語法 (SSRS 組態管理員)
  本主題描述報表伺服器 Web 服務和報表管理員的 URL 字串部分。 儲存於內部的 URL 字串結構與您在瀏覽器視窗的網址列中輸入的 URL 不同。 當您設定 URL 而且它位於 RSReportServer.config 檔案中時，URL 保留項目字串會出現在 Reporting Services 組態工具的 [結果] 視窗中。 如果您要排除 URL 保留項目問題或是查詢 HTTP.SYS 來檢視伺服器上所定義的內部 URL 保留項目，知道 URL 字串如何定義將會很有幫助。  
  
## <a name="url-syntax"></a>URL 語法  
 報表伺服器 URL 會儲存在 **UrlString** 元素和 **VirtualDirectory** 元素中。 將 **UrlString** 和 **VirtualDirectory** 分成不同元素的理由，是為了讓您可以擁有多個 URL 字串，但是每一個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 應用程式只會有一個虛擬目錄名稱。  
  
 在 HTTP.SYS 中，URL 保留項目包含 **UrlString** 和 **VirtualDirectory**兩者。 URL 保留項目的語法包含以下部分：  
  
 \<配置>://\<主機名稱>:\<連接埠>/\<虛擬目錄>  
  
 下表將描述每一個屬性以及對每一個屬性有效的值。  
  
|屬性|有效的值|Description|  
|--------------|------------------|-----------------|  
|配置|http 或 https|非 SSL 和 SSL 連接的前置詞。|  
|主機名稱|(+) 強式萬用字元，等於 IP 位址的 [(全部指派)] 值。<br /><br /> (\*) 弱式萬用字元，等於 [(全未指派)] 的 IP 位址。<br /><br /> 完整網域名稱<br /><br /> 電腦名稱<br /><br /> IP 位址 (IPV4)<br /><br /> IP 位址 (IPV6)|識別網路上的伺服器。<br /><br /> (+) 強式萬用字元是預設值。 HTTP.SYS 將會接受所有網路介面卡上對於給定通訊埠和虛擬目錄組合的所有要求。 報表伺服器將會接受此通訊埠上的任何要求。<br /><br /> (\*) 弱式萬用字元。 HTTP.SYS 將會接受所有網路介面卡上，對於給定通訊埠和虛擬目錄組合而且未由其他 URL 保留項目處理的所有要求。<br /><br /> 電腦名稱是電腦在網路上的 NETBIOS 名稱。<br /><br /> 完整網域名稱包含網域位址和伺服器名稱 (該名稱已經向網域控制站或公用網域名稱伺服器註冊)。<br /><br /> IP 位址 (IPV4) 是電腦上網路介面卡的 IP 位址，它是使用 IPV4 格式： *nnn.nnn.nnn.nnn*。<br /><br /> IP 位址 (IPV6) 是電腦上網路介面卡的 IP 位址，它是使用 IPV6 格式：\<標頭>:\<標頭>:*nnn.nnn.nnn.nnn*。|  
|通訊埠|80<br /><br /> 443<br /><br /> \<自訂>|通訊埠 80 是與伺服器之間往來之 HTTP 要求的標準通訊埠。<br /><br /> 通訊埠 443 是 SSL 連接的標準通訊埠。<br /><br /> 您可以使用尚未被另一個應用程式保留的任何通訊埠。|  
|VirtualDirectory|ReportServer *[_InstanceName]*<br /><br /> Reports *[_InstanceName]*<br /><br /> \<自訂>|指定應用程式的名稱。 這個值為字串。 根據預設， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會使用 ReportServer 和 Reports 當做報表伺服器 Web 服務和報表管理員應用程式的應用程式名稱。 如果您要的話，可以使用不同的名稱。<br /><br /> 這是必要的值。 它會識別應用程式。<br /><br /> 只能針對每一個應用程式執行個體指定一個虛擬目錄。 若要針對相同執行個體內的相同應用程式建立多個 URL，請建立多個版本的 **UrlString**。 若要針對多個應用程式執行個體建立唯一的虛擬目錄名稱，請考慮在虛擬目錄名稱中包含此執行個體名稱 (使用底線字元 (_) 來附加此執行個體名稱)。 *InstanceName* 為選擇性，但是如果您在相同電腦上有多個執行個體，則建議您使用它。 如需如何設定具名執行個體之 URL 保留項目的詳細資訊，請參閱[多重執行個體報表伺服器部署的 URL 保留項目&#40;SSRS 設定管理員&#41;](../../reporting-services/install-windows/url-reservations-for-multi-instance-report-server-deployments.md)。<br /><br /> 虛擬目錄的值不區分大小寫。 任何字串只要不包含 URL 分隔符號或 URL 編碼，就可以使用它。|  
  
## <a name="see-also"></a>另請參閱  
 [設定報表伺服器 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [設定 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
  
  
