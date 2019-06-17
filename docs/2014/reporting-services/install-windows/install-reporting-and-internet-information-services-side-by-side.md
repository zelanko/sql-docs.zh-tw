---
title: 安裝 Reporting Services 和網際網路資訊服務的並存 （SSRS 原生模式） |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], IIS
ms.assetid: 9b651fa5-f582-4f18-a77d-0dde95d9d211
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6555f47c1d390180bbf2d2ccca1f29f07889465d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108794"
---
# <a name="install-reporting-services-and-internet-information-services-side-by-side-ssrs-native-mode"></a>並存安裝 Reporting Services 和 Internet Information Services (SSRS 原生模式)
  您可以在同一部電腦上安裝和執行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS) 與 Internet Information Services (IIS)。 您所使用的 IIS 版本會決定必須處理的互通性問題。  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式|  
  
|IIS 版本|問題|描述|  
|-----------------|------------|-----------------|  
|IIS 6.0、7.0、8.0、8.5|適用於某個應用程式的要求被不同的應用程式所接受。<br /><br /> HTTP.SYS 會針對 URL 保留項目強制執行優先順序規則。 如果 URL 保留項目比另一個應用程式的 URL 保留項目更弱，傳送至具有相同虛擬目錄名稱而且共同監視通訊埠 80 之應用程式的要求可能無法送達預期的目標。|在特定條件底下，在 URL 保留項目配置中取代另一個 URL 端點的已註冊端點可能會收到適用於其他應用程式的 HTTP 要求。<br /><br /> 針對報表伺服器 Web 服務和報表管理員使用唯一的虛擬目錄名稱可協助您避免這項衝突。<br /><br /> 本主題將提供有關這個狀況的詳細資訊。|  
  
## <a name="precedence-rules-for-url-reservations"></a>URL 保留項目的優先順序規則  
 在您處理 IIS 與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]之間的互通性問題之前，必須了解 URL 保留項目的優先順序規則。 優先順序規則可以歸納成為下列陳述式：具有更多明確定義值的 URL 保留項目會優先接收符合此 URL 的要求。  
  
-   指定虛擬目錄的 URL 保留項目會比省略虛擬目錄的 URL 保留項目更明確。  
  
-   指定單一位址 (透過 IP 位址、完整網域名稱、網路電腦名稱或主機名稱) 的 URL 保留項目會比萬用字元更明確。  
  
-   指定強式萬用字元的 URL 保留項目會比弱式萬用字元更明確。  
  
 下列範例會顯示 URL 保留項目的範圍，從最明確到最不明確的順序排列：  
  
|範例|要求|  
|-------------|-------------|  
|http://123.234.345.456:80/reports|接收的所有要求傳送至 http://123.234.345.456/reports 或 http://\< 電腦名稱 > / 如果網域名稱服務可以解析成該主機名稱的 IP 位址。|  
|http://+:80/reports|只要此 URL 包含 "reports" 虛擬目錄名稱，便接收傳送至適用於該電腦之任何 IP 位址或主機名稱的任何要求。|  
|http://123.234.345.456:80|任何指定的要求會收到 http://123.234.345.456 或 http://\< computername > 如果網域名稱服務可以將 IP 位址解析成該主機名稱。|  
|http://+:80|若為對應至 [全部指派]  的應用程式端點，便接收尚未由其他應用程式接收的要求。|  
|http://*:80|若為對應至 [全未指派]  的應用程式端點，便接收尚未由其他應用程式接收的要求。|  
  
 連接埠衝突的其中一個指標是您會看到下列錯誤訊息：' System.IO.FileLoadException:此程序無法存取檔案，因為它正由另一個處理序。 (來自 HRESULT 的例外狀況：0x80070020)。 '  
  
## <a name="url-reservations-for-iis-60-70-80-85-with-includesssql14includessssql14-mdmd-reporting-services"></a>IIS 6.0、7.0、8.0、8.5 與 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Reporting Services 的 URL 保留項目  
 根據上一節所描述的優先順序規則，您可以開始了解針對 Reporting Services 和 IIS 所定義的 URL 保留項目如何提升互通性。 Reporting Services 會接收明確指定其應用程式之虛擬目錄名稱的要求。IIS 會接收所有其餘要求，然後您可以將這些要求導向至 IIS 處理模型內部執行的應用程式。  
  
|應用程式|URL 保留項目|描述|要求接收|  
|-----------------|---------------------|-----------------|---------------------|  
|報表伺服器|http://+:80/ReportServer|通訊埠 80 的強式萬用字元，以及報表伺服器虛擬目錄。|在通訊埠 80 上接收指定報表伺服器虛擬目錄的所有要求。 報表伺服器 Web 服務會接收 http://\<電腦名稱>/reportserver 的所有要求。|  
|報表管理員|http://+:80/Reports|通訊埠 80 的強式萬用字元，以及 Reports 虛擬目錄。|在通訊埠 80 上接收指定 Reports 虛擬目錄的所有要求。 報表管理員會接收 http:// 的所有要求\<電腦名稱 > / 報告。|  
|IIS|http://*:80/|通訊埠 80 的弱式萬用字元。|在通訊埠 80 上接收其他應用程式未接收的任何其餘要求。|  
  
## <a name="side-by-side-deployments-of-includesscurrentincludessscurrent-mdmd-and-sql-server-2005-reporting-services-on-iis-60-70-80-85"></a>在 IIS 6.0、7.0、8.0、8.5 上並存部署 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 與 SQL Server 2005 Reporting Services  
 當 IIS 網站的虛擬目錄名稱與 Reporting Services 所使用的虛擬目錄名稱完全相同時，IIS 與 Reporting Services 之間就會發生互通性問題。 例如，假設您有下列組態：  
  
-   指派至通訊埠 80 以及名為 "Reports" 之虛擬目錄的 IIS 網站。  
  
-   A[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]安裝在預設組態中，其中 URL 保留項目也指定了連接埠 80 而報表管理員應用程式也將"Reports"用於虛擬目錄名稱的報表伺服器執行個體。  
  
 指定此組態中，要求傳送至 http://\<電腦名稱 >: 80/reports 將會收到由報表管理員。 安裝了 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 報表伺服器執行個體之後，透過 IIS 中 Reports 虛擬目錄存取的應用程式將不會再接收要求。  
  
 如果您要執行舊版與新版 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的並存部署，可能會遇到上述路由傳送的問題。 這是因為所有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本都會使用 "ReportServer" 和 "Reports" 當做報表伺服器與報表管理員應用程式的虛擬目錄名稱，因而增加您在 IIS 中設有 "reports" 和 "reportserver" 虛擬目錄的可能性。  
  
 為了確保所有應用程式都會接收要求，請遵循下列指導方針：  
  
-   針對 Reporting Services 安裝，請使用 IIS 網站與 Reporting Services 在相同通訊埠上尚未使用的虛擬目錄名稱。 如果發生衝突，請以「僅限檔案」模式安裝 Reporting Services (使用「安裝」，但不要在安裝精靈中設定伺服器選項)，以便您可以在安裝完成之後設定虛擬目錄。 您的組態有衝突的其中一個指標是您會看到錯誤訊息：System.IO.FileLoadException:此程序無法存取檔案，因為它正由另一個處理序。 (來自 HRESULT 的例外狀況：0x80070020)。  
  
-   針對手動設定的安裝，請在設定的 URL 中採用預設命名慣例。 如果您將 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 安裝成具名執行個體，請在建立虛擬目錄時加入執行個體名稱。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表伺服器 URL &#40;SSRS 組態管理員&#41;](configure-report-server-urls-ssrs-configuration-manager.md)   
 [設定 URL &#40;SSRS 組態管理員&#41;](configure-a-url-ssrs-configuration-manager.md)   
 [安裝 Reporting Services 原生模式報表伺服器](install-reporting-services-native-mode-report-server.md)  
  
  
