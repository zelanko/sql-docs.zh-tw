---
title: 開啟或關閉 Reporting Services 功能 | Microsoft Docs
ms.date: 06/10/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, configuration
- security [Reporting Services], strategies
ms.assetid: b69db02a-43a7-4fdc-ad9b-438d817a7f83
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 67945db1fd131b27b37a7e34853987c38fad8d84
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67140375"
---
# <a name="turn-reporting-services-features-on-or-off"></a>開啟或關閉 Reporting Services 功能
  您可以關閉鎖定策略中未使用的報表伺服器功能，以減少實際執行報表伺服器的攻擊面。 在大多數情況下，您會想要同時執行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能，以便能夠使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中所提供的所有功能。 不過，根據部署模型而定，您可以停用不需要的功能。 例如，如果所有報表處理都設定為排程的作業，您就可以只啟用背景處理。 同樣地，如果只想要視需要執行的互動式報表，可以只執行報表伺服器 Web 服務。  
  
 本文中的程序將示範如何關閉原生模式 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能。 您可以透過不同的方式來設定功能，例如直接編輯 `RsReportServer.config` 檔案，或是在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，使用以原則為基礎之管理的 [Reporting Services 的介面區設定]  Facet。 使用下列連結即可找到說明如何開啟或關閉功能的程序：  
  
-   [報表伺服器 Web 服務](#RSWebSvc)  
  
-   [排程的事件和處理](#Sched)  
  
-   [入口網站](#WebPortal)  
  
-   [報表資料來源的 Windows 整合式安全性](#WinIntSec)  
  
##  <a name="RSWebSvc"></a> 報表伺服器 Web 服務  
  
### <a name="to-turn-on-or-off-the-report-server-web-service-by-editing-configuration"></a>透過編輯組態來開啟或關閉報表伺服器 Web 服務  
  
1.  在文字編輯器中開啟 `RsReportServer.config` 檔案。 如需詳細資訊，請參閱[修改 Reporting Services 組態檔 &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)。  
  
2.  若要開啟報表伺服器 Web 服務，請將 **IsWebServiceEnabled** 設定為 **true**：  
  
    ```  
    <IsWebServiceEnabled>true</IsWebServiceEnabled>  
    ```  
  
3.  若要關閉報表伺服器 Web 服務，請將 **IsWebServiceEnabled** 設定為 **false**：  
  
    ```  
    <IsWebServiceEnabled>false</IsWebServiceEnabled>  
    ```  
  
4.  儲存您的變更，然後關閉檔案。  
  
#### <a name="to-turn-on-or-off-the-report-server-web-service-by-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 來開啟或關閉報表伺服器 Web 服務  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 並連接至您想要設定的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體。  
  
2.  在物件總管中，以滑鼠右鍵按一下 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 節點，指向 [原則]  ，然後按一下 [Facet]  。  
  
3.  在 **[Facet]** 清單中，選取 **[Reporting Services 的介面區組態]** 。  
  
4.  在 **[Facet 屬性]** 底下：  
  
    -   若要開啟報表伺服器 Web 服務，請將 **[WebServiceAndHTTPAccessEnabled]** 設定為 **True**。  
  
    -   若要關閉報表伺服器 Web 服務，請將 **[WebServiceAndHTTPAccessEnabled]** 設定為 **False**。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="Sched"></a> 排程的事件和傳遞  
  
#### <a name="to-turn-on-or-off-scheduled-events-and-delivery-by-editing-configuration"></a>透過編輯組態來開啟或關閉排程的事件和傳遞  
  
1.  在文字編輯器中開啟 RsReportServer.config 檔。 如需詳細資訊，請參閱[修改 Reporting Services 組態檔 &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)。  
  
2.  若要開啟排程的報表處理和傳遞，請將 **IsSchedulingService**、 **IsNotificationService**和 **IsEventService** 設定為 **true**：  
  
    ```  
    <IsSchedulingService>true</IsSchedulingService>  
    <IsNotificationService>true</IsNotificationService>  
    <IsEventService>true</IsEventService>  
    ```  
  
3.  若要關閉排程的報表處理和傳遞，請將 **IsSchedulingService**、 **IsNotificationService**和 **IsEventService** 設定為 **false**：  
  
    ```  
    <IsSchedulingService>false</IsSchedulingService>  
    <IsNotificationService>false</IsNotificationService>  
    <IsEventService>false</IsEventService>  
    ```  
  
4.  儲存您的變更，然後關閉檔案。  
  
> [!NOTE]  
>  您不能完全關閉背景處理，因為它提供了伺服器作業所需的資料庫維護功能。  
  
##  <a name="WebPortal"></a> 入口網站
  
從 SQL Server 2016 Reporting Services 累計更新 2 開始，入口網站一律會啟用。
  
##  <a name="WinIntSec"></a> Windows 整合式安全性  
  
### <a name="to-turn-on-or-off-windows-integrated-security-by-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 來開啟或關閉 Windows 整合式安全性  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 並連接至您想要設定的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體。  
  
2.  在物件總管中，以滑鼠右鍵按一下 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 節點，然後按一下 [屬性]  。  
  
3.  在 [伺服器屬性]  對話方塊的 [選取頁面]  底下，選取 [安全性]  。  
  
    -   若要開啟 Windows 整合式安全性，請選取 [為報表資料來源啟用 Windows 整合式安全性]  選項。  
  
    -   若要關閉 Windows 整合式安全性，請取消選取 [為報表資料來源啟用 Windows 整合式安全性]  選項。  
  
4.  選取 [確定]  。  
  
## <a name="see-also"></a>另請參閱  
[Reporting Services 組態管理員 (原生模式)](../install-windows/reporting-services-configuration-manager-native-mode.md)

 更多問題嗎？ [試試 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
  
