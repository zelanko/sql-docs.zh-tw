---
title: "SQL Server 2016 版本支援的 Reporting Services 功能 | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 39f03d2d-6e48-4b34-a9d3-07f86313b937
caps.latest.revision: "3"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: ef2e6405ce01442ca8a9709db2f1aa61a4934dc3
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="reporting-services-features-supported-by-the-editions-of-sql-server-2016"></a>SQL Server 2016 版本支援的 Reporting Services 功能

本主題提供不同 SQL Server 2016 版本所支援功能的詳細資訊。  
  
 SQL Server Evaluation Edition 提供了 180 天的試用期。  
  
 如需最新版本資訊，請參閱 [SQL Server 2016 版本資訊](../sql-server/sql-server-2016-release-notes.md)。 如需新功能的最新資訊，請參閱 [Reporting Services (SSRS) 的新功能](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)。
    
 **試用 SQL Server 2016！**    
    
 > [![從 Evaluation Center 下載](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[從 Evaluation Center 下載 SQL Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![Azure 虛擬機器小型](../analysis-services/media/azure-virtual-machine-small.png) **[使用已安裝的 SQL Server 2016 加速虛擬機器](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)**    

如需 Evaluation 和 Developer Edition 所支援的功能，請參閱＜SQL Server Enterprise Edition＞。

若要瀏覽 SQL Server 技術的資料表，請按一下其連結：  

-   [Reporting Services](#SSRS)  
  
-   [商業智慧用戶端](#BIC)  

##  <a name="SSRS"></a> Reporting Services  
  
|功能名稱|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Developer|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|行動報表和 KPI|是||||||是|  
|支援的目錄 DB [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|Standard 或更高版本|Standard 或更高版本|Web|Express|||Standard 或更高版本|  
|支援的資料來源 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 所有版本|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 所有版本|Web|Express|||[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 所有版本|  
|報表伺服器|是|是|是|是|||是|  
|報表設計師|是|是|是|是|||是|  
|報表設計師的入口網站|是|是|是|是|||是|  
|以角色為基礎的安全性|是|是|是|是|||是|  
|匯出至 Excel、PowerPoint、Word、PDF 和影像|是|是|是|是|||是|  
|增強的量測計和圖表|是|是|是|是|||是|  
|將報表項目釘選到 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]儀表板|是|是|是|是|||是|  
|自訂驗證|是|是|是|是|||是|  
|報告成資料摘要|是|是|是|是|||是|  
|模型支援|是|是|是||||是|  
|針對以角色為基礎的安全性建立自訂角色|是|是|||||是|  
|模型項目安全性|是|是|||||是|  
|無限點選連結|是|是|||||是|  
|共用元件程式庫|是|是|||||是|  
|電子郵件和檔案共用訂閱與排程|是|是|||||是|  
|報表記錄、執行快照集和快取|是|是|||||是|  
|SharePoint 整合|是|是|||||是|  
|遠端及非 SQL 資料來源支援<sup>1</sup>|是|是|||||是|  
|資料來源、傳遞和轉譯、RDCE 擴充性|是|是|||||是|  
|自訂商標|是||||||是|  
|資料驅動報表訂閱|是||||||是|  
|向外延展部署 (Web 伺服器陣列)|是||||||是|  
|警示<sup>2</sup>|是||||||是|  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] <sup>2</sup>|是||||||是|  
  
 <sup>1</sup> 如需 SQL Server 2016 Reporting Services (SSRS) 支援資料來源的詳細資訊，請參閱 [Reporting Services 支援的資料來源 &#40;SSRS&#41;](../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  
  
 <sup>2</sup> SharePoint 模式中需要 Reporting Services。 如需詳細資訊，請參閱 [安裝 Reporting Services SharePoint 模式](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)。  
  
## <a name="report-server-database-server-edition-requirements"></a>報表伺服器資料庫伺服器版本需求  
 建立報表伺服器資料庫時，並非所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本都可以用來主控資料庫。 下表顯示哪些 [!INCLUDE[ssDE](../includes/ssde-md.md)] 版本可用於特定的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]版本。  
  
|對於這一版的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services|使用這一版的 Database Engine 執行個體來主控資料庫|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|Enterprise 或 Standard Edition (本機或遠端)|  
|Standard|Enterprise 或 Standard Edition (本機或遠端)|  
|Web|Web Edition (僅限本機)|  
|Express with Advanced Services|Express with Advanced Services (僅限本機)。|  
|Evaluation|Evaluation|  
  
##  <a name="BIC"></a> 商業智慧用戶端  
 您可以透過 Microsoft 下載中心取得下列軟體用戶端應用程式，這些應用程式是提供來協助您建立可在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體上執行的商業智慧文件。 當您在伺服器環境中裝載這些文件時，請使用支援該文件類型的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 下表將識別哪些 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本包含裝載在這些用戶端應用程式中建立之文件所需的伺服器功能。  
  
|工具名稱|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Developer|  
|---------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion-md.md)] (.rdl 和 .rds)|是|是|||||是|  
|[!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long-md.md)] (.rsmobile)|是||||||是|  
|Power BI 行動裝置應用程式 (iOS、Windows 10、Android) (.rsmobile)|是||||||是|  
  
> [!NOTE]  
> 1.  上表識別啟用這些用戶端工具所需的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本；不過，這些工具可以存取任何 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本上裝載的資料。  
> 2.  [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long-md.md)] 是建立行動報表的單一點。 連接到 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 伺服器存取資料來源以及建立報表。 然後將它們發佈至 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 伺服器，供組織中的其他人在伺服器或行動裝置上存取。 您也可以使用獨立 [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long-md.md)] 與本機資料來源  
> 3.  無論您使用內部部署  [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 、雲端 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] ，或兩個一起作為報表傳遞解決方案，您只需要一個行動裝置應用程式來存取行動裝置上的儀表板和行動報表。 您可從 Windows、iOS 或 Android 應用程式存放區下載 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 應用程式。  

## <a name="next-steps"></a>後續步驟

[SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)  
[SQL Server 2016 的產品規格](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)  
[SQL Server 2016 安裝](../database-engine/install-windows/installation-for-sql-server-2016.md) 

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
