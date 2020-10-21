---
title: 設定 Reporting Services 來使用主體別名 (SAN) | Microsoft Docs
description: 了解如何透過修改 rsreportserver.config 檔案及使用 Netsh.exe 工具來設定 SQL Server Reporting Services 與 Power BI 報表伺服器，以使用 SAN。
ms.date: 09/27/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 40ddab224d24e566ad346d64d5238ca5c81d9f48
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891588"
---
# <a name="configure-reporting-services-to-use-a-subject-alternative-name-san"></a>設定 Reporting Services 來使用主體別名 (SAN)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

此主題說明如何透過修改 rsreportserver.config 檔案及使用 Netsh.exe 工具來設定 Reporting Services (SSRS) 與 Power BI 報表伺服器，以使用主體別名 (SAN)。

這些指示適用於 Web 服務 URL 及報表伺服器組態管理員工具中的入口網站 URL。

如果要使用 SAN，TLS/SSL 憑證必須在伺服器上註冊、簽署，且具有私密金鑰。 您無法使用自我簽署憑證。

Reporting Services 及 Power BI 報表伺服器中的 URL 可設定為使用 TLS/SSL 憑證。 憑證通常只有一個主體名稱，因此一個傳輸層安全性 (TLS) (先前稱為安全通訊端層 (SSL)) 工作階段只允許一個 URL。 SAN 是憑證中的一個額外欄位，其可以允許 TLS 服務接聽許多 URL，並可和其他應用程式共用 TLS 連線埠。 例如，SAN 看起來可能會像 `www.myreports.com`。

如需 Reporting Services 之 TLS 設定的詳細資訊，請參閱[在原生模式報表伺服器上設定 TLS 連線](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)。  
  
## <a name="configure-to-use-a-subject-alternative-name-for-web-service-url"></a>進行設定，以針對 Web 服務 URL 使用主體別名
  
1.  啟動報表伺服器組態管理員。  
  
     如需詳細資訊，請參閱[報表伺服器組態管理員 &#40;原生模式&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)。  
  
2.  在 [Web 服務 URL]  頁面上，選取 TLS/SSL 連接埠和 TLS/SSL 憑證。  
  
     ![報表伺服器組態管理員](../../reporting-services/report-server-sharepoint/media/reportingservices-configurationmanager.png "報表伺服器組態管理員")  
  
     Configuration Manager 會針對連接埠註冊 TLS/SSL 憑證。  
  
3.  開啟 rsreportserver.config 檔案。  
  
     針對 SSRS 2016 原生模式，檔案的預設位置為下列資料夾：  
  
    ```  
    \Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer  
    ```  
  
     針對 SSRS 2017 和更新版本，檔案的預設位置為下列資料夾：  
  
    ```  
    \Program Files\Microsoft SQL Server Reporting Services\SSRS\ReportServer  
    ```  
    
     針對 Power BI 報表伺服器，檔案的預設位置為下列資料夾：  
  
    ```  
    \Program Files\Microsoft Power BI Report Server\PBIRS\ReportServer  
    ```  
  
4.  複製 **ReportServerWebService** 應用程式的 URL 區段。
  
     例如，下列是原始的 URL 區段：  
  
    ```  
        <URL>  
         <UrlString>https://+:443</UrlString>  
         <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051</AccountSid>  
         <AccountName>NT Service\ReportServer</AccountName>  
        </URL>  
  
    ```  
  
     下列是修改後的 URL 區段：
  
    ```  
    <URL>  
         <UrlString>https://+:443</UrlString>  
         <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051</AccountSid>  
         <AccountName>NT Service\ReportServer</AccountName>  
        </URL>  
        <URL>  
         <UrlString>https://www.myreports.com:443</UrlString>  
         <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051/AccountSid>  
         <AccountName>NT Service\ReportServer</AccountName>  
        </URL>  
  
    ```  
  
  > [!TIP]  
>  * 若為 SSRS 2017 和更新版本，`AccountSid` 值為 `S-1-5-80-4050220999-2730734961-1537482082-519850261-379003301`，且 `AccountName` 值為 `NT SERVICE\SQLServerReportingServices`。
>  * 若為 Power BI 報表伺服器，`AccountSid` 值為 `S-1-5-80-1730998386-2757299892-37364343-1607169425-3512908663`，且 `AccountName` 值為 `NT SERVICE\PowerBIReportServer`。
  
5.  儲存 rsreportserver.config 檔案。  
  
6.  使用 [以系統管理員身分執行] 來開啟命令提示字元，然後執行 Netsh.exe 工具。  
  
    ```  
    C:\windows\system32\netsh  
    ```  
  
7.  輸入下列命令以切換到 http 內容。  
  
    ```  
    Netsh>http  
    ```  
  
8.  鍵入下列命令以顯示現有的 urlacls：
  
    ```  
    Netsh http>show urlacl  
    ```  
  
     會出現類似以下的項目。  
  
    ```  
    Reserved URL            : https://+:443/ReportServer/  
        User: NT SERVICE\ReportServer  
            Listen: Yes  
            Delegate: No  
            SDDL: D:(A;;GX;;;S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051)  
    ```  
  
     urlacl是 保留之的 URL 的 DACL (任意存取控制清單)。  
  
9. 輸入下列命令以使用與現有項目相同的使用者及 SDDL 為主體別名，並建立新項目：  
  
    ```  
    netsh http>add urlacl  url=https://www.myreports.com:443/ReportServer    
    user="NT Service\ReportServer" sddl=D:(A;;GX;;;S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051)  
  
    ```  
  
10. 針對 [入口網站 URL]，輸入下列內容以建立主體別名的新項目：

    ```  
    netsh http>add urlacl  url=https://www.myreports.com:443/Reports  
    user="NT Service\ReportServer" sddl=D:(A;;GX;;;S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051)  
  
    ```  
> [!TIP]  
>  * 若為 SSRS 2017 和更新版本，`user` 值為 `NT SERVICE\SQLServerReportingServices`，且 `sddl` 值為 `D:(A;;GX;;;S-1-5-80-4050220999-2730734961-1537482082-519850261-379003301)`。
>  * 若為 Power BI 報表伺服器，`user` 值為 `NT SERVICE\PowerBIReportServer`，且 `sddl` 值為 `S-1-5-80-1730998386-2757299892-37364343-1607169425-3512908663`

> [!NOTE]  
> 針對 Power BI 報表伺服器，您必須輸入下列命令來為主體別名建立兩個額外的項目：
>  * `add urlacl url=https://www.myreports.com:443/PowerBI user="NT SERVICE\PowerBIReportServer" sddl=D:(A;;GX;;;S-1-5-80-1730998386-2757299892-37364343-1607169425-3512908663)`
>  * `add urlacl url=https://www.myreports.com:443/wopi user="NT SERVICE\PowerBIReportServer" sddl=D:(A;;GX;;;S-1-5-80-1730998386-2757299892-37364343-1607169425-3512908663)`

11. 在報表伺服器組態管理員的 [報表伺服器狀態] 頁面中，按一下 [停止]，然後按一下 [啟動] 以重新啟動報表伺服器。  
  
## <a name="see-also"></a>另請參閱

 [RsReportServer.config 設定檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [報表伺服器組態管理員](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [修改 Reporting Services 設定檔](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [設定報表伺服器 URL](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
