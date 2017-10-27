---
title: "設定 Reporting Services 使用主體替代名稱 |Microsoft 文件"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 73f48b2978055481f1ee93952fb3a35eb84ec416
ms.contentlocale: zh-tw
ms.lasthandoff: 10/06/2017

---
# <a name="configure-reporting-services-to-use-a-subject-alternative-name"></a>設定 Reporting Services 使用主體替代名稱

本主題說明如何設定 Reporting Services (SSRS) 使用主體替代名稱 (SAN) 修改 rsreportserver.config 檔，並使用 Netsh.exe 工具。

這些指示適用於 Reporting Service URL 和 Web 服務 URL。

如果要使用 SAN，必須在伺服器上註冊 SSL 憑證、必須簽署 SSL 憑證，且 SSL 憑證需有私密金鑰。 您不能使用自我簽署憑證。  
  
 Reporting Services 中的 Url 可以設定為使用 SSL 憑證。 憑證通常只有一個主體名稱，因此一個 SSL (安全通訊端層) 工作階段只允許一個 URL。 SAN 是憑證，可讓 SSL 服務接聽對許多 Url，並與其他應用程式共用 SSL 連接埠中的其他欄位。 SAN 看起來像`www.s2.com`。  
  
 如需有關 Reporting Services 的 SSL 設定的詳細資訊，請參閱[原生模式報表伺服器上設定 SSL 連接](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)。  
  
## <a name="configure-ssrs-to-use-a-subject-alternative-name-for-web-service-url"></a>設定 SSRS 使用主體替代名稱的 web 服務 URL
  
1.  啟動 Reporting Services 組態管理員。  
  
     如需詳細資訊，請參閱 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)。  
  
2.  在 [Web 服務 URL] 頁面中，選取 SSL 連接埠和 SSL 憑證。  
  
     ![Reporting Services 組態管理員](../../reporting-services/report-server-sharepoint/media/reportingservices-configurationmanager.png "Reporting Services 組態管理員")  
  
     組態管理員會針對通訊埠註冊 SSL 憑證。  
  
3.  開啟 rsreportserver.config 檔案。  
  
     SSRS 原生模式中，此檔案位於預設會在下列資料夾：  
  
    ```  
    \Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\ReportServer  
    ```  
  
4.  複製報表伺服器 Web 服務應用程式的 URL 區段。  
  
     例如，下列原始的 URL 區段是：  
  
    ```  
        <URL>  
         <UrlString>https://localhost:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
  
    ```  
  
     下列修改過的 URL 區段是：
  
    ```  
    <URL>  
         <UrlString>https://www.s1.com:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
        <URL>  
         <UrlString>https://www.s2.com:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
  
    ```  
  
5.  儲存 rsreportserver.config 檔案。  
  
6.  以系統管理員身分開啟命令提示字元，然後執行 Netsh.exe 工具。  
  
    ```  
    C:\windows\system32\netsh  
    ```  
  
7.  輸入下列命令以切換到 http 內容。  
  
    ```  
    Netsh>http  
    ```  
  
8.  顯示現有的 urlacls 輸入下列命令：
  
    ```  
    Netsh http>show urlacl  
    ```  
  
     會出現類似以下的項目。  
  
    ```  
    Reserved URL            : https:// www.s1.com:443/ReportServer/  
        User: NT SERVICE\ReportServer  
            Listen: Yes  
            Delegate: No  
            SDDL: D:(A;;GX;;;S-1-5-80-1234567890-123456789-123456789-123456789-1234567890)  
    ```  
  
     urlacl是 保留之的 URL 的 DACL (任意存取控制清單)。  
  
9. 輸入以下命令以使用和現有項目相同的使用者和 SDDL 為主體替代名稱建立新項目。  
  
    ```  
    netsh http>add urlacl  url=https://www.s2.com:443/ReportServer    
    user="NT Service\ReportServer" sddl=D:(A;;GX;;;S-1-5-80-1234567980-12346579-123456789-123456789-1234567890)  
  
    ```  
  
10. 在**報表伺服器狀態**頁面的 Reporting Services 組態管理員，按一下**停止**，然後按一下**啟動**重新啟動報表伺服器。  
  
## <a name="see-also"></a>另請參閱

 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Reporting Services 組態管理員](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [修改 Reporting Services 組態檔](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [設定報表伺服器 Url](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)

