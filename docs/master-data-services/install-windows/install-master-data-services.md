---
title: Master Data Services 的安裝工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/24/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: bb7aa3e7-8807-42c8-884f-0e41d7a20837
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 55f67c71bfa1247d9b8df411889091527c95de48
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51703886"
---
# <a name="installation-tasks-for-master-data-services"></a>Master Data Services 的安裝工作

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  本文概述安裝工作以及指示的連結。 如需安裝和設定 Master Data Services 的逐步解說，請參閱 [Master Data Services 安裝和組態](../../master-data-services/master-data-services-installation-and-configuration.md)。 
  
-   [安裝前工作](#preinstall)：安裝 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]之前，先確認系統需求。  
  
-   [安裝作業](#install)：使用 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 安裝程式或命令提示字元，安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   [安裝後工作](#postinstall)：開啟 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 以完成安裝後的作業。 建立並設定 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式和 Web 服務，然後部署範例模型。  
  
##  <a name="preinstall"></a> 安裝前工作  
  
|動作|詳細資料|相關主題|  
|------------|-------------|--------------------|  
|確認安裝需求|執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式的電腦，必須符合以下項目的基本需求：<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式。<br /><br /> [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式和 Web 服務。<br /><br /> [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫，如果您在與 Web 應用程序相同的電腦中裝載資料庫。<br /><br /> <br /><br /> 您可以只在網頁伺服器電腦上執行安裝程式，且在執行支援之 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 版本的遠端電腦上建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫，分開網頁伺服器電腦與資料庫伺服器電腦。|[SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)<br /><br /> [安裝 SQL Server 2016 的硬體與軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)<br /><br /> [Web 應用程式需求 &#40;Master Data Services&#41;](../../master-data-services/install-windows/web-application-requirements-master-data-services.md)<br /><br /> [資料庫需求 &#40;Master Data Services&#41;](../../master-data-services/install-windows/database-requirements-master-data-services.md)|  
|設定必要角色、角色服務和功能|執行安裝程式之前，使用必要 Windows 角色、角色服務和功能來設定電腦。<br /><br /> 注意：雖然您可以在稍後的工作流程中執行此步驟，但在執行安裝程式之前先設定此內容，有助於在安裝之後立即執行 Web 設定工作。|[Web 應用程式需求 &#40;Master Data Services&#41;](../../master-data-services/install-windows/web-application-requirements-master-data-services.md)|  
|檢閱語言支援考量|決定您要安裝及執行 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 的語言。|[多語言及全域部署 &#40;Master Data Services&#41;](../../master-data-services/install-windows/multi-lingual-and-global-deployments-master-data-services.md)|  
  
##  <a name="install"></a> 安裝作業  
  
|動作|詳細資料|相關主題|  
|------------|-------------|--------------------|  
|執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式|在即將裝載 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]Web 應用程式與 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web 服務的電腦上，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式或於命令提示字元處，安裝 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]。 當您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式時，可以從 [功能選擇] 頁面的 [共用功能] 下方存取 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]。 當您使用命令提示字元時，[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 可當做功能參數。 請注意，命令列安裝程序會安裝 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]但不會進行設定。 您必須使用 Master Data Services 組態管理員進行設定。<br /><br /> 安裝程序：<br /><br /> 在您為共用功能指定的位置上安裝 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料夾和檔案，並指派這些物件的權限。<br /><br /> 在全域組件快取 (GAC) 中註冊 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 組件。<br /><br /> 安裝 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。|[從安裝精靈安裝 SQL Server 2016 &#40;安裝程式&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)<br /><br /> [資料夾和檔案的權限 &#40;Master Data Services&#41;](../../master-data-services/folder-and-file-permissions-master-data-services.md)|  
  
##  <a name="postinstall"></a> 安裝後工作  
  
|動作|詳細資料|相關主題|  
|------------|-------------|--------------------|  
|開啟 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 到完整的後續安裝作業中|安裝程式完成之後，請開啟 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 會在本機電腦上執行下列安裝後作業：<br /><br /> 建立 Windows 群組 **MDS_ServiceAccounts**，包含應用程式集區的 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 服務帳戶。<br /><br /> 在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 安裝路徑之下建立 MDSTempDir 資料夾，並為 **MDS_ServiceAccounts**指派權限。 此為編譯 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式暫存編譯檔的資料夾。<br /><br /> 在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web.config 檔案中，以 MDSTempDir 資料夾的路徑設定 **\<compilation>** 項目的 **tempDirectory** 屬性。|[資料夾和檔案的權限 &#40;Master Data Services&#41;](../../master-data-services/folder-and-file-permissions-master-data-services.md)<br /><br /> [Web 組態參考 &#40;Master Data Services&#41;](../../master-data-services/web-configuration-reference-master-data-services.md)|  
|建立 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫|使用 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 可針對您的主要資料建立 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫。|[建立 Master Data Services 資料庫](../../master-data-services/install-windows/create-a-master-data-services-database.md)|  
|建立 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式|使用 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 建立及設定 Web 應用程式，以供裝載 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]。|[建立主資料管理員 Web 應用程式 &#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)|  
|讓 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫與 Web 應用程式產生關聯|使用 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] ，讓 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式與 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫產生關聯。|[建立 Master Data Services 資料庫與 Web 應用程式的關聯](../../master-data-services/install-windows/associate-a-master-data-services-database-and-web-application.md)|  
|設定 Internet Explorer 增強式安全性|當您在 Windows Server 2012 電腦上安裝 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 時，可能需要設定 Internet Explorer 增強式安全性，以允許 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 應用程式網站的指令碼。 否則，瀏覽至伺服器電腦上的 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 應用程式網站將會失敗。|[Internet Explorer：增強式安全性設定](https://go.microsoft.com/fwlink/p/?LinkId=223869)|  
|安裝 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|處理主要資料的使用者可以安裝 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]。|[https://go.microsoft.com/fwlink/?LinkID=398159](https://go.microsoft.com/fwlink/?LinkID=398159)|  
|啟用 Data Quality Services (DQS) 整合|如果是 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]的使用者，請啟用與 DQS 功能的整合來比對類似的資料。|[啟用 Data Quality Services 與 Master Data Services 的整合](../../master-data-services/install-windows/enable-data-quality-services-integration-with-master-data-services.md)|  
|部署範例模型|範例模型封裝會與 Master Data Services 一起安裝，而且可以使用 MDSModelDeploy.exe 進行部署。|[在 SQL Server 中部署 MDS 範例](~/master-data-services/sql-server-samples-model-deployment-packages-mds.md)|
  
 若在安裝程序或初始組態期間發生問題，請參閱 TechNet Wiki 上的 [Troubleshooting Installation and Configuration Issues](https://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-installation-and-configuration-issues-master-data-services.aspx) (疑難排解安裝和組態問題)。  
  
 如果電腦上不再需要 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] ，可以解除安裝 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] ，並且判斷是否要移除不受解除安裝程序影響的項目。 如需詳細資訊，請參閱 [解除安裝及移除 Master Data Services](../../sql-server/install/uninstall-and-remove-master-data-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [安裝 SQL Server 2016](../../database-engine/install-windows/install-sql-server.md)  
  
  
