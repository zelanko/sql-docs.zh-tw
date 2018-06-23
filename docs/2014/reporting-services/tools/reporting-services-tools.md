---
title: Reporting Services 工具 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SSRS, tools
- Reporting Services, tools
- components [Reporting Services]
- components [Reporting Services], about components
- Reporting Services, components
- SSRS, components
- reports [Reporting Services], tools
- SQL Server Reporting Services, components
- SQL Server Reporting Services, tools
- architecture [Reporting Services]
ms.assetid: 23d616e3-eb90-43fb-9b7a-869bd7e22e7b
caps.latest.revision: 73
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: f1b80d3c9ef634b606bc8c86713fd3c115b3f83a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133620"
---
# <a name="reporting-services-tools"></a>Reporting Services 工具
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包含一組圖形和指令碼工具，支援在受管理的環境中開發與使用豐富的報表功能。 此工具集包含開發工具、組態與管理工具，以及報表檢視工具。 本主題提供 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中各個工具與其存取方式的簡短概觀。  
  
 如需立即找到工具，請參閱[教學課程：如何尋找及啟動 Reporting Services 工具 &#40;SSRS&#41;](tutorial-how-to-locate-and-start-reporting-services-tools-ssrs.md)。  
  
## <a name="tools-for-report-authoring"></a>報表撰寫工具  
 下表列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中可用於報表撰寫的工具。  
  
|工具|描述|如何存取|  
|----------|-----------------|-------------------|  
|[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]|互動式的資料探索和視覺呈現體驗設計為可讓您建立以及與依據 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 表格式模型的報表進行互動。<br /><br /> 注意： 需要[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]以 SharePoint 模式。|Sliverlight 瀏覽器|  
|報表設計師|使用此工具設計報表並部署至原生模式或 SharePoint 報表伺服器。<br /><br /> 裝載於 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]<br /><br /> 報表資料窗格可組織用於報表的資料<br /><br /> 互動式報表設計之 [設計] 和 [預覽] 的索引標籤式檢視<br /><br /> 查詢設計工具可協助您指定要從資料來源擷取哪些資料會在資料來源類型相關聯[RSReportDesigner 組態檔](../report-server/rsreportdesigner-configuration-file.md)<br /><br /> 使用智慧感知的運算式編輯器可建立自訂報表內容和外觀的 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 運算式<br /><br /> 支援自訂報表項目和自訂查詢設計工具<br /><br /> <br /><br /> 如需詳細資訊，請參閱 [SQL Server Data Tools &#40;SSDT&#41; 中的 Reporting Services](reporting-services-in-sql-server-data-tools-ssdt.md)。|[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]|  
|報表產生器|使用此工具設計報表並部署至原生模式或 SharePoint 報表伺服器。<br /><br /> 與 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office 相似的撰寫環境<br /><br /> 將報表項目儲存為報表組件的能力<br /><br /> 建立地圖精靈<br /><br /> 彙總的彙總<br /><br /> 增強的運算式支援<br /><br /> 查詢設計工具可協助您指定要從內建資料來源類型擷取的資料<br /><br /> <br /><br /> 如需詳細資訊，請參閱[報表產生器&#40;SSRS&#41;](report-builder-authoring-environment-ssrs.md)。|下載 MSI 或從報表管理員/SharePoint 開啟|  
  
## <a name="tools-for-report-server-administration"></a>適用於報表伺服器管理的工具  
 一組圖形和指令碼工具可用於管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中的報表伺服器。 所使用工具取決於報表伺服器的部署模式。  
  
### <a name="native-mode"></a>原生模式  
 下表列出可用以管理部署於原生模式中報表伺服器的工具。  
  
|工具|描述|如何存取|  
|----------|-----------------|-------------------|  
|Reporting Services 組態管理員|請使用此工具設定 Reporting Services 安裝。 請注意，Reporting Services 組態管理員不會協助您管理報表伺服器內容、 啟用其他功能，或授與伺服器的存取權。 可用的工作包括：<br /><br /> 設定本機和遠端報表伺服器執行個體<br /><br /> 設定報表伺服器服務帳戶。<br /><br /> 建立及設定一個或多個 Web 服務 URL。<br /><br /> 設定報表管理員 URL。<br /><br /> 建立及設定報表伺服器資料庫。<br /><br /> 設定向外延展部署。<br /><br /> 備份、還原或取代用於加密已儲存之連接字串和認證的對稱金鑰。<br /><br /> 設定自動執行帳戶。<br /><br /> 設定電子郵件傳遞的 SMTP 伺服器。<br /><br /> <br /><br /> 如需詳細資訊，請參閱 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)。|開始功能表|  
|Transact-SQL|使用此工具即可在單一環境中管理一個或多個報表伺服器執行個體，包括：<br /><br /> 管理本機和遠端報表伺服器執行個體<br /><br /> 設定報表伺服器屬性<br /><br /> 修改角色定義<br /><br /> 關閉您不要使用的報表伺服器功能<br /><br /> 管理作業<br /><br /> 管理共用排程|開始功能表|  
|SQL Server 組態管理員|使用此工具可以：<br /><br /> 啟動及停止 Reporting Services Windows 服務<br /><br /> 設定客戶回函報表、傾印目錄位置和錯誤報告<br /><br /> <br /><br /> **\*\* 警告\* \*** 請勿使用此工具來設定服務帳戶。 請改用 Reporting Services 組態工具。<br /><br /> 如需詳細資訊，請參閱 [SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)。|開始功能表|  
|Rsconfig 公用程式|使用此工具可設定及管理連線到報表伺服器資料庫的報表伺服器。 您也可以使用它來指定自動執行報表處理所使用的使用者帳戶。<br /><br /> 如需詳細資訊，請參閱[報表伺服器命令提示字元公用程式 &#40;SSRS&#41;](report-server-command-prompt-utilities-ssrs.md)。|命令提示字元|  
|Rskeymgmt 公用程式|使用此工具可以：<br /><br /> 擷取、還原、建立及刪除用於加密報表伺服器資料的對稱金鑰<br /><br /> 在向外延展部署中加入報表伺服器執行個體<br /><br /> <br /><br /> 如需詳細資訊，請參閱[報表伺服器命令提示字元公用程式 &#40;SSRS&#41;](report-server-command-prompt-utilities-ssrs.md)。|命令提示字元|  
|Windows Management Instrumentation (WMI) 類別|使用這些類別可自動化 Reporting Services 組態管理員中的組態工作，且無須使用圖形化使用者介面。<br /><br /> 如需詳細資訊，請參閱[WMI 提供者以程式設計方式存取](../accessing-the-wmi-provider-programmatically.md)。|Visual Basic 指令碼|  
  
### <a name="sharepoint-integrated-mode"></a>SharePoint 整合模式  
 在 SharePoint 模式中，Reporting Services 是在 SharePoint 架構中的服務應用程式，並且直接透過 SharePoint 進行管理  
  
|工具|描述|如何存取|  
|----------|-----------------|-------------------|  
|SharePoint 管理中心|使用 SharePoint 管理中心可建立、查詢及管理 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的共用服務應用程式。<br /><br /> 如需詳細資訊，請參閱[設定和管理報表伺服器 &#40;Reporting Services SharePoint 模式&#41;](../configure-administer-report-server-reporting-services-sharepoint-mode.md)。|前往管理中心之 SharePoint 網站 URL 的瀏覽器|  
|PowerShell Cmdlet|使用 PowerShell Cmdlet 可建立、查詢及管理 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的共用服務應用程式。<br /><br /> 如需詳細資訊，請參閱[Reporting Services SharePoint 模式的 PowerShell 指令程式](../powershell-cmdlets-for-reporting-services-sharepoint-mode.md)。|SharePoint 2010 管理命令介面|  
  
## <a name="tools-for-report-content-management"></a>用於報表內容管理的工具  
 一組圖形和指令碼工具可用於管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中的內容。 所使用工具取決於報表伺服器的部署模式。  
  
|工具|描述|如何存取|  
|----------|-----------------|-------------------|  
|報表伺服器 Web 服務 URL|使用此工具可在一般項目瀏覽頁面的報表目錄中瀏覽內容。<br /><br /> 如需詳細資訊，請參閱[報表伺服器 Web 服務](../report-server-web-service/report-server-web-service.md)。|瀏覽器|  
|報表管理員|**(僅限於原生模式)** 使用此工具可從遠端位置透過 HTTP 連線管理單一報表伺服器執行個體。 您可以執行下列工作：<br /><br /> 檢視、搜尋、列印與訂閱報表。<br /><br /> 建立、保護和維護資料夾階層，以組織伺服器上的項目。<br /><br /> 設定以角色為基礎的安全性，此安全性決定對項目與作業的存取權。<br /><br /> 設定報表執行屬性、報表記錄和報表參數。<br /><br /> 建立可連接並可從 Microsoft SQL Server Analysis Services 資料來源或從 SQL Server 關聯式資料來源擷取資料的報表模型。<br /><br /> 設定模型項目安全性以存取模型中的特定項目，或將項目對應到您事先建立之預先定義的點選連結報表。<br /><br /> 建立共用排程與共用資料來源，讓排程與資料來源連接更容易管理。<br /><br /> 建立資料驅動訂閱，將報表傳遞至大型收件者清單。<br /><br /> 建立連結報表，以重複使用並以不同的方式重新決定現有報表的用途。<br /><br /> 啟動報表產生器來建立可以在報表伺服器上儲存與執行的報表。<br /><br /> <br /><br /> 如需詳細資訊，請參閱[報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)。||  
|RS 公用程式|此工具是您可用於執行編寫指令碼作業的 Script Host。 使用此工具即可執行 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 指令碼，於報表伺服器資料庫間複製資料、發行報表、在報表伺服器資料庫中建立項目等等。<br /><br /> 如需詳細資訊，請參閱[報表伺服器命令提示字元公用程式 &#40;SSRS&#41;](report-server-command-prompt-utilities-ssrs.md)。|命令提示字元|  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services Report Server](../reporting-services-report-server.md)   
 [Reporting Services 概念 &#40;SSRS&#41;](../reporting-services-concepts-ssrs.md)   
 [Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
  