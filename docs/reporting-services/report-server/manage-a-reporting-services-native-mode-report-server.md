---
title: 管理 Reporting Services 原生模式報表伺服器 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Configuration tool
- configuration options [Reporting Services]
- report servers [Reporting Services], configuring
ms.assetid: 6ca03a09-d6a8-4c93-ba12-1c99dcbfb618
caps.latest.revision: 10
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: b6322c4aca621aa668286f82bf144ec579657cc3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="manage-a-reporting-services-native-mode-report-server"></a>管理 Reporting Services 原生模式報表伺服器
  本節包含使用 Reporting Services 組態管理員來設定原生模式報表伺服器執行個體的程序。  
  
## <a name="in-this-section"></a>本節內容  
 本章節的主題將組織成數個類別，好讓您可以更輕鬆地找到所要的指示。 第一節包含原生模式報表伺服器之基本組態工作的主題， 第二節包含進階組態主題， 第三節包含設定報表伺服器於 SharePoint 整合模式下執行的主題。  
  
### <a name="basic-configuration"></a>基本組態  
 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
 提供啟動 Reporting Services 組態工具的步驟。  
  
 [設定服務帳戶 &#40;SSRS 組態管理員&#41;](http://msdn.microsoft.com/library/25000ad5-3f80-4210-8331-d4754dc217e0)  
 說明如何指定報表伺服器服務的帳戶和密碼資訊。  
  
 [為報表伺服器註冊服務主要名稱 &#40;SPN&#41;](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md)  
 說明如何手動為報表伺服器註冊 SPN，該伺服器會在使用 Kerberos 驗證之網路的網域使用者帳戶之下執行。  
  
 [設定 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
 說明如何建立用來存取報表伺服器 Web 服務和報表管理員的一個或多個 URL。  
  
 [建立原生模式報表伺服器資料庫 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)  
 提供建立報表伺服器資料庫的步驟。 這是部署 Reporting Services 安裝的必要步驟。  
  
### <a name="advanced-or-optional-configuration"></a>進階或選擇性組態  
 [設定原生模式報表伺服器向外延展部署 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
 提供設定多個報表伺服器來共用報表伺服器資料庫的步驟。  
  
 [為電子郵件傳遞設定報表伺服器 (SSRS 組態管理員)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83)  
 提供有關為電子郵件散發設定報表伺服器的步驟。  
  
 [設定供報表伺服器存取的防火牆](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
 說明如何開啟用於來自報表伺服器之傳入要求和傳出回應的通訊埠。  
  
 [設定原生模式報表伺服器進行本機管理 &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)  
 描述使用 `http://localhost` 連線報表管理員或報表伺服器所需的其他步驟。  
  
 [設定報表伺服器來進行遠端管理](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)  
 說明如何設定遠端報表伺服器執行個體，好讓您可以從其他電腦連接及設定它。  
  
 [開啟或關閉 Reporting Services 功能](../../reporting-services/report-server/turn-reporting-services-features-on-or-off.md)  
 說明如何移除 Reporting Services 安裝中未使用的功能。  
  
 [啟用遠端錯誤 &#40;Reporting Services&#41;](../../reporting-services/report-server/enable-remote-errors-reporting-services.md)  
 說明如何在報表伺服器上設定伺服器屬性，以傳回有關遠端伺服器上發生之錯誤狀況的其他資訊。  
  
## <a name="see-also"></a>另請參閱  
 [設定和管理報表伺服器 &#40;SSRS 原生模式&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [設定和管理報表伺服器 &#40;Reporting Services SharePoint 模式&#41;](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md)  
  
  
