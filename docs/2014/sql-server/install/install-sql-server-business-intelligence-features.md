---
title: 安裝 SQL Server 2014 BI 功能
ms.custom: ''
ms.prod: sql-server-2014
ms.reviewer: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: kfile
ms.date: 10/24/2018
ms.technology: install
ms.openlocfilehash: 44805d6fd7512a5180a2b62e2c8808b890901705
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52808350"
---
# <a name="install-sql-server-2014-bi-features"></a>安裝 SQL Server 2014 BI 功能

  屬於 Microsoft Business Intelligence 平台的 SQL Server 功能包括 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，以及用來建立或處理分析資料的數種用戶端應用程式。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式文件集中的本節將說明如何安裝這些功能。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 可以安裝成獨立伺服器、向外延展的組態，或是 SharePoint 伺服器陣列中的共用服務應用程式等形式。 將這些服務安裝在伺服器陣列中，可以啟用僅限在 SharePoint 中使用的 BI 功能，包括 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 及 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]，後者是在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 或 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 表格式模型資料庫上執行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 隨選互動式報表設計工具。  
  
 您若已熟悉 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 PowerPivot for SharePoint 的安裝步驟，可以直接前往指引您如何啟用特定案例的檢查清單。 如需詳細資訊，請參閱 < [for sharepoint 安裝 BI 功能的檢查清單](checklists-for-installing-bi-features-with-sharepoint.md)。  
  
## <a name="contents"></a>目錄

本節內容：
  
|連結|工作|  
|----------|----------|  
|[安裝 BI 功能來搭配 SharePoint 的檢查清單](checklists-for-installing-bi-features-with-sharepoint.md)|您若已確定所要安裝的服務，並十分熟悉 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的安裝步驟，可以使用本節中指引您有關安裝順序、帳戶及權限需求，以及部署包括多部伺服器與多功能部署在內之進階拓撲的檢查清單的步驟。|  
|[安裝具有 SharePoint 的 SQL Server BI 功能&#40;PowerPivot 和 Reporting Services&#41;](install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)|本節說明如何在 SharePoint 環境中安裝 SQL Server 功能， 同時也會列出特定版本 SharePoint 所能使用的 SQL Server 功能。 除此之外還會提供 PowerPivot for SharePoint 及 SharePoint 模式下的 Reporting Services 安裝程序。|  
|[以多維度及資料採礦模式安裝 Analysis Services](install-analysis-services-in-multidimensional-and-data-mining-mode.md)<br /><br /> [以表格式模式安裝 Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services.md)<br /><br /> [安裝 Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)<br /><br /> [安裝 Integration Services](../../integration-services/install-windows/install-integration-services.md)<br /><br /> [安裝 Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)<br /><br /> [安裝 Reporting Services 原生模式報表伺服器](../../reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)|本節提供安裝 Analysis Services、Integration Services、Master Data Services 及 Reporting Services 的指示，其中 Analysis Services 與 Reporting Services 不使用 SharePoint 進行安裝。 這有時稱為*原生模式*，且最常見的 Reporting Services 和 Analysis Services 的安裝案例。 本節將告訴您可以直接決定您伺服器運作內容的安裝選項。 對於 Reporting Services 而言，這可能是預先設定的伺服器，或是需要經過數個設定組態步驟之後才可使用的伺服器。 而對於 Analysis Services 而言，您所選取的安裝選項，將會決定您所能部署到伺服器的專案類型。|  
|[確認或疑難排解 SQL Server BI 功能安裝問題](../../../2014/sql-server/install/verify-or-troubleshoot-sql-server-bi-feature-installation-problems.md)|本節除提供驗證安裝的步驟之外， 還包含可以連結到網路上有關問題解決方法資訊的連結。|  
  
## <a name="related-content"></a>相關內容  
  
|連結|工作|  
|----------|----------|  
|[升級到 SQL Server 2014](../../database-engine/install-windows/upgrade-sql-server.md)<br /><br /> [升級 Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)<br /><br /> [升級 PowerPivot for SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)<br /><br /> [升級和移轉 Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)|您可以使用本節的指示，將舊版的伺服器與內容升級成 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|[解除安裝 SQL Server 2014](uninstall-sql-server.md)<br /><br /> [解除安裝 PowerPivot for SharePoint](../../../2014/sql-server/install/uninstall-power-pivot-for-sharepoint.md)<br /><br /> [解除安裝 Reporting Services](../../../2014/sql-server/install/uninstall-reporting-services.md)|您可以使用本節的指示來解除安裝 BI 功能。|  
  
## <a name="see-also"></a>另請參閱

* [新功能&#40;Reporting Services&#41;](../../../2014/reporting-services/what-s-new-reporting-services.md)

* [新 Analysis Services 和 Business Intelligence 功能](../../analysis-services/what-s-new-in-analysis-services.md)

* [安裝 SQL Server 2014](../../database-engine/install-windows/install-sql-server.md)

* [升級到 SQL Server 2014](../../database-engine/install-windows/upgrade-sql-server.md)
