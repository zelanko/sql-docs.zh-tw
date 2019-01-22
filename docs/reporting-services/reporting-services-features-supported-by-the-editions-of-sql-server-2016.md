---
title: SQL Server 版本所支援的 Reporting Services 功能
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.date: 11/01/2018
ms.openlocfilehash: 1b46c6cec15f3a229892116758fe7f147f24c9ac
ms.sourcegitcommit: 1c01af5b02fe185fd60718cc289829426dc86eaa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/10/2019
ms.locfileid: "54185034"
---
# <a name="sql-server-reporting-services-features-supported-by-its-editions"></a>SQL Server 版本所支援的 Reporting Services 功能

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

本文說明 SQL Server 不同版本所支援的 SQL Server Reporting Services (SSRS) 功能。 SQL Server Evaluation Edition 提供了 180 天的試用期。  
  
 如需最新的 SQL Server 版本資訊，請參閱 [SQL Server 2017 版本資訊](../sql-server/sql-server-2017-release-notes.md)。 如需新功能的最新資訊，請參閱 [Reporting Services (SSRS) 中的新功能](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)。

 ## <a name="try-sql-server-2017"></a>試用 SQL Server 2017

> [![下載 SQL Server 2017](../analysis-services/media/download.png)](https://go.microsoft.com/fwlink/?LinkID=829477) **[從 Evaluation Center 下載 SQL Server 2017](https://go.microsoft.com/fwlink/?LinkID=829477)**    
>
> ![Azure 虛擬機器 (小型)](../analysis-services/media/azure-virtual-machine-small.png) **[使用已安裝的 SQL Server 2017 加速虛擬機器](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)**    

若要了解 Evaluation 和 Developer 版所支援的功能，請參閱下表 SQL Server Enterprise 版那一欄。

##  <a name="SSRS"></a> SQL Server Reporting Services  
  
|功能名稱|Enterprise|Standard|Web|Express with Advanced Services|Developer|  
|------------------|---------|------------------------------------|------------------------|-------------|---------------|  
|行動報表和分析|是||||是|  
|支援的目錄資料庫 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|Standard 或更高版本|Standard 或更高版本|Web|Express|Standard 或更高版本|  
|支援的資料來源 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 所有版本|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 所有版本|Web|Express|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 所有版本|  
|報表伺服器|是|是|是|是|是|  
|報表設計師|是|是|是|是|是|  
|報表設計師的入口網站|是|是|是|是|是|  
|以角色為基礎的安全性|是|是|是|是|是|  
|匯出成 Excel、PowerPoint、Word、PDF 和影像|是|是|是|是|是|  
|增強的量測計和圖表|是|是|是|是|是|  
|將報表項目釘選到 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 儀表板|是|是|是|是|是|  
|自訂驗證|是|是|是||是|  
|報告成資料摘要|是|是|是|是|是|  
|模型支援|是|是|是||是|  
|針對以角色為基礎的安全性建立自訂角色|是|是|||是|  
|模型項目安全性|是|是|||是|  
|無限點選連結|是|是|||是|  
|共用元件程式庫|是|是|||是|  
|電子郵件和檔案共用訂閱與排程|是|是|||是|  
|報表記錄、執行快照集和快取|是|是|||是|  
|SharePoint 整合|是|是|||是|  
|遠端及非 SQL 資料來源支援<sup>1</sup>|是|是|||是|  
|資料來源、傳遞和轉譯與 RDCE 擴充性|是|是|||是|  
|自訂商標|是||||是|  
|資料驅動報表訂閱|是||||是|  
|向外延展部署 (Web 伺服陣列)|是||||是|  
|警示<sup>2</sup> (SSRS 2016) |是||||是|  
|Power View<sup>2</sup> (SSRS 2016) |是||||是| 
|註解<sup>3</sup> |是|是|是|是|是|  

 <sup>1</sup> 如需 SQL Server Reporting Services (SSRS) 支援的資料來源詳細資訊，請參閱 [Reporting Services 支援的資料來源 &#40;SSRS&#41;](../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  
  
 <sup>2</sup> 需要 SharePoint 模式的 SQL Server 2016 Reporting Services。 如需詳細資訊，請參閱[以 SharePoint 模式安裝 SQL Server Reporting Services](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)。 自 SQL Server 2017 起，不再提供 Reporting Services 與 SharePoint 的整合。 

<sup>3</sup> 僅於 Power BI 報表伺服器和 SQL Server 2017 Reporting Services 及更新版本中提供。

> [!NOTE]
> SQL Server Express with Tools 和 SQL Server Express 不支援 SQL Server Reporting Services。
  
## <a name="edition-requirements-for-the-report-server-database"></a>報表伺服器資料庫的版本需求
 在建立報表伺服器資料庫時，並非所有 SQL Server [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本都可以用來裝載資料庫。 下表顯示哪些 [!INCLUDE[ssDE](../includes/ssde-md.md)] 版本可用於特定的 SQL Server [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 版本。  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services 的這個版本，|使用資料庫引擎執行個體的這個版本來裝載資料庫。|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|Enterprise 或 Standard 版 (本機或遠端)|  
|Standard|Enterprise 或 Standard 版 (本機或遠端)|  
|Web|Web Edition (僅限本機)|  
|Express with Advanced Services|Express with Advanced Services (僅限本機)|  
|Evaluation|Evaluation|  
  
##  <a name="BIC"></a> 商業智慧用戶端  
下列軟體用戶端應用程式可從 Microsoft 下載中心取得。 這些應用程式可協助您建立執行於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的商業智慧文件。 當您在伺服器環境中裝載這些文件時，請使用支援該文件類型的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 下表將識別哪些 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本包含裝載在這些用戶端應用程式中建立之文件所需的伺服器功能。  
  
|工具名稱|Enterprise|Standard|Web|Express with Advanced Services|Developer|  
|---------------|----------------|--------------|------------------------|-------------|---------------|  
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)]、**.rdl** 和 **.rds**|是|是|是|是|是|  
|[!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)]、**.rsmobile**|是||||是|  
|Power BI 行動裝置應用程式 (iOS、Windows 10 和 Android)、**.rsmobile**|是||||是|  
  
> [!NOTE]  
> * 上表指出了啟用這些用戶端工具所需的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 不過，這些工具能夠存取裝載於任何 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本的資料。  
> * [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] 是建立行動報表的單一點。 連線到 SSRS 伺服器即可存取資料來源及建立報表。 接著將其發佈至 SSRS 伺服器，供組織中的其他人在伺服器或行動裝置上存取。 您也可以使用獨立 [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] 搭配本機資料來源。  
> * 無論您使用內部部署的 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]、雲端的 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 或同時使用兩者作為報表傳遞解決方案，都只需要一個行動裝置應用程式，就可以在行動裝置上存取儀表板和行動報表。 您可從 Windows、iOS 或 Android 應用程式存放區下載 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 應用程式。  

## <a name="next-steps"></a>後續步驟

* 閱讀 [Features supported by the editions of SQL Server 2017](~/sql-server/editions-and-components-of-sql-server-2017.md) (SQL Server 2017 版本所支援的功能)。 

* [規劃 SQL Server 安裝](../sql-server/install/planning-a-sql-server-installation.md)。

* 更多問題嗎？ 歡迎在 [SQL Server Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)提問。
