---
title: 報表伺服器資料庫 (SSRS 原生模式) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- databases [Reporting Services]
- report servers [Reporting Services], databases
- temporary databases [Reporting Services]
- report server database
- reportservertempdb
- reportserver database
ms.assetid: 0fc5c033-3fe1-4cea-86c7-66ea5e424d65
caps.latest.revision: 48
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d1f1eeeeaf960fbfe8659abd5a7299dd6b924212
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="report-server-database-ssrs-native-mode"></a>報表伺服器資料庫 (SSRS 原生模式)
  報表伺服器是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 儲存中繼資料和物件定義的無狀態伺服器。 原生模式 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝會使用兩個資料庫來分隔永續性資料儲存與暫時儲存需求。 兩個資料庫會一起建立，並依名稱繫結。 根據預設，資料庫名稱分別為 **ReportServer** 和 **ReportServerTempdb**。  
  
 SharePoint 模式 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝也會針對資料更改功能建立資料庫。 SharePoint 模式中的三個資料庫與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式相關聯。 如需詳細資訊，請參閱 [管理 Reporting Services SharePoint 服務應用程式](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)  
  
 資料庫可以在本機或遠端 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體上執行。 如果您有足夠的系統資源或想要保留軟體授權，可以選擇本機執行個體，但在遠端電腦上執行資料庫則可提升效能。  
  
 您可以從先前的安裝或具有其他報表伺服器執行個體的不同執行個體，報告或重複使用現有的報表伺服器資料庫。 報表伺服器資料庫的結構描述必須與報表伺服器執行個體相容。 如果資料庫的格式是舊的，系統將會提示您將其升級到目前的格式。 但是無法讓新版降級為舊版。 如果您有新版的報表伺服器資料庫，您無法將其用於舊版的報表伺服器執行個體。 如需如何將報表伺服器資料庫升級到新格式的詳細資訊，請參閱 [升級報表伺服器資料庫](../../reporting-services/install-windows/upgrade-a-report-server-database.md)。  
  
> [!IMPORTANT]  
>  資料庫的資料表結構會針對伺服器作業最佳化，而且不應該修改或微調。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 前後版次的資料表結構可能會變更。 如果您修改或擴充資料庫，可能會限制或妨礙執行未來升級或套用 Service Pack 的功能。 您也可能會導入影響報表伺服器作業的變更。 例如，如果您在 ReportServer 資料庫上開啟 READ_COMMITTED_SNAPSHOT，您會中斷互動式排序功能。  
  
 所有對報表伺服器資料庫的存取，都必須透過報表伺服器處理。 若要存取報表伺服器資料庫中的內容，您可以使用報表伺服器管理工具 (例如報表管理員和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]) 或程式設計介面 (例如 URL 存取、報表伺服器 Web 服務，或 Windows Management Instrumentation (WMI) 提供者)。  
  
 報表伺服器資料庫的連接通常是透過 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員定義。 但是，如果您選擇安裝預設組態，則可以在安裝過程中定義它。 如需報表伺服器連接到資料庫的詳細資訊，請參閱[設定報表伺服器資料庫連線 &#40;SSRS 設定管理員&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)。  
  
## <a name="report-server-database"></a>報表伺服器資料庫  
 報表伺服器資料庫是儲存下列內容的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫：  
  
-   報表伺服器所管理的項目 (報表與連結報表、共用資料來源、報表模型、資料夾、資源)，以及與這些項目相關聯的所有屬性和安全性設定。  
  
-   訂閱與排程定義。  
  
-   報表快照集 (包含查詢結果) 與報表記錄。  
  
-   系統屬性與系統層級安全性設定。  
  
-   報表執行記錄資料。  
  
-   報表資料來源的對稱金鑰與加密連接和認證。  
  
 由於報表伺服器資料庫會儲存應用程式狀態和永續性資料，您應建立備份排程來備份此資料庫，以避免資料遺失。 如需如何備份資料庫的建議和指示，請參閱[將報表伺服器資料庫移至其他電腦 &#40;SSRS 原生模式&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)。  
  
## <a name="report-server-temporary-database"></a>報表伺服器暫存資料庫  
 每個報表伺服器資料庫會使用一個相關的暫存資料庫，以儲存報表伺服器所產生的工作階段和執行資料、快取報表，以及工作資料表。 背景伺服器處理序將定期從暫存資料庫的資料表中移除較舊及未使用的項目。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 如果暫存資料庫遺失，不會重新建立暫存資料庫，也不會修復遺失或修改過的資料表。 雖然暫存資料庫並不包含永續性資料，不過您仍應備份該資料庫，以避免萬一需要執行失敗復原作業時還要重新建立。  
  
 如果您備份暫存資料庫並在後續加以復原，應該要刪除其內容。 一般而言，在任何時候刪除暫存資料庫內容都是安全的。 但是，您必須在刪除內容後重新啟動報表伺服器 Windows 服務。  
  
## <a name="see-also"></a>另請參閱  
 [在 SQL Server 容錯移轉叢集中裝載報表伺服器資料庫](../../reporting-services/install-windows/host-a-report-server-database-in-a-sql-server-failover-cluster.md)   
 [儲存加密的報表伺服器資料 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Reporting Services Report Server](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md)   
 [管理報表伺服器資料庫 &#40;SSRS 原生模式&#41;](../../reporting-services/report-server/administer-a-report-server-database-ssrs-native-mode.md)   
 [建立報表伺服器資料庫 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)   
 [Reporting Services 的備份與還原作業](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md)  
  
  
