---
title: 安裝 Master Data Services |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: bb7aa3e7-8807-42c8-884f-0e41d7a20837
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2645ae5b16ffa4738f06e1439abac977c8e18894
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65479337"
---
# <a name="install-master-data-services"></a>安裝 Master Data Services
  下列工作流程提供如何安裝及設定 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]的概觀。 
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 安裝程序包含三個部分：  
  
-   [預先安裝](#preinstall)工作：安裝[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]之前，請先確認系統需求。  
  
-   [安裝作業](#install)：使用[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝程式或命令提示字元來安裝。  
  
-   [安裝後](#postinstall)工作：開啟[!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]以完成安裝後作業。 建立並設定 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式和 Web 服務，然後部署範例模型。  
  
##  <a name="preinstall"></a>預先安裝工作  
  
|動作|詳細資料|相關主題|  
|------------|-------------|--------------------|  
|確認安裝需求|執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式的電腦，必須符合以下項目的基本需求：<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Setup.<br /><br /> 
  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式和 Web 服務。<br /><br /> 
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫，如果您在與 Web 應用程序相同的電腦中裝載資料庫。<br /><br /> 請注意，您可以只在 web 伺服器電腦上執行安裝程式，並在執行支援之版本的[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]遠端電腦上建立資料庫，來分隔 web 伺服器電腦和資料庫伺服器電腦。|[SQL Server 2014 各版本所支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)<br /><br /> [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)<br /><br /> [&#40;Master Data Services&#41;的 Web 應用程式需求](web-application-requirements-master-data-services.md)<br /><br /> [資料庫需求 &#40;Master Data Services&#41;](database-requirements-master-data-services.md)|  
|設定必要角色、角色服務和功能|執行安裝程式之前，使用必要 Windows 角色、角色服務和功能來設定電腦。<br /><br /> 注意：雖然您可以在稍後的工作流程中執行此步驟，但在執行安裝程式之前先設定此內容，有助於在安裝之後立即執行 Web 設定工作。|[&#40;Master Data Services&#41;的 Web 應用程式需求](web-application-requirements-master-data-services.md)|  
|檢閱語言支援考量|決定您要安裝及執行 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 的語言。|[多語言和全域部署 &#40;Master Data Services&#41;](multi-lingual-and-global-deployments-master-data-services.md)|  
  
##  <a name="install"></a>安裝作業  
  
|動作|詳細資料|相關主題|  
|------------|-------------|--------------------|  
|執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式|在即將裝載 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式與 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web 服務的電腦上，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式或於命令提示字元處，安裝 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]。 當您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式時，可以從 [功能選擇][!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** 頁面的 [共用功能]**** 下方存取 **。 當您使用命令提示字元時， [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 可當做功能參數。 請注意，命令列安裝程序會安裝 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]但不會進行設定。 您必須使用 Master Data Services 組態管理員進行設定。 安裝程序：<br /><br /> 在您為共用功能指定的位置上安裝 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料夾和檔案，並指派這些物件的權限。<br /><br /> 在全域組件快取 (GAC) 中註冊 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 組件。<br /><br /> 安裝 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。|[從安裝精靈安裝 SQL Server 2014 &#40;安裝程式&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)<br /><br /> [資料夾和檔案許可權 &#40;Master Data Services&#41;](../folder-and-file-permissions-master-data-services.md)|  
  
##  <a name="postinstall"></a>安裝後工作  
  
|動作|詳細資料|相關主題|  
|------------|-------------|--------------------|  
|開啟 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 到完整的後續安裝作業中|安裝程式完成之後，請開啟 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。 
  [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 會在本機電腦上執行下列安裝後作業：<br /><br /> 建立 Windows 群組 **MDS_ServiceAccounts**，包含應用程式集區的 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 服務帳戶。<br /><br /> 在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 安裝路徑之下建立 MDSTempDir 資料夾，並為 **MDS_ServiceAccounts**指派權限。 此為編譯 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式暫存編譯檔的資料夾。<br /><br /> [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]在 web.config 檔案中，使用 MDSTempDir 資料夾的路徑，設定** \<編譯>** 專案的`tempDirectory`屬性。<br /><br /> <br /><br /> 若您撰寫安裝程序的指令碼，可以開啟 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 註冊 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 嵌入式管理單元，但您必須手動執行其他步驟以完成設定。 
  [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 為您提供一個由精靈驅動的設定程序。 沒有任何命令列程序可設定 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]。|[資料夾和檔案許可權 &#40;Master Data Services&#41;](../folder-and-file-permissions-master-data-services.md)<br /><br /> [Web 設定參考 &#40;Master Data Services&#41;](../web-configuration-reference-master-data-services.md)|  
|建立 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫|使用 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 可針對您的主要資料建立 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫。|[建立 Master Data Services 資料庫](create-a-master-data-services-database.md)|  
|建立 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式|使用 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 建立及設定 Web 應用程式，以供裝載 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]。|[建立主資料管理員 Web 應用程式 &#40;Master Data Services&#41;](create-a-master-data-manager-web-application-master-data-services.md)|  
|讓 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫與 Web 應用程式產生關聯|使用 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] ，讓 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式與 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫產生關聯。|[建立 Master Data Services 資料庫與 Web 應用程式的關聯](associate-a-master-data-services-database-and-web-application.md)|  
|設定 Internet Explorer 增強式安全性|當您在 Windows Server 2008 或 Windows Server 2008 R2 電腦上安裝 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 時，可能需要設定 Internet Explorer 增強式安全性，以允許[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]應用程式網站的指令碼。 否則，瀏覽至伺服器電腦上的 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 應用程式網站將會失敗。|[Internet Explorer：增強式安全性設定](https://go.microsoft.com/fwlink/p/?LinkId=223869)|  
|安裝 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|處理主要資料的使用者可以安裝 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]。|[https://go.microsoft.com/fwlink/?LinkId=219530](https://go.microsoft.com/fwlink/?LinkId=219530)|  
|啟用 Data Quality Services (DQS) 整合|如果是 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]的使用者，請啟用與 DQS 功能的整合來比對類似的資料。|[啟用 Data Quality Services 與 Master Data Services 的整合](enable-data-quality-services-integration-with-master-data-services.md)|  
|部署範例模型|範例模型封裝會與 Master Data Services 一起安裝，而且可以使用 MDSModelDeploy.exe 進行部署。|[在 SQL Server 中部署 MDS 範例](https://go.microsoft.com/fwlink/?LinkId=251486&clcid=0x409)|  
  
 若在安裝程序或初始組態期間發生問題，請參閱 TechNet Wiki 上的 [Troubleshooting Installation and Configuration Issues](https://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-installation-and-configuration-issues-master-data-services.aspx) (疑難排解安裝和組態問題)。  
  
 如果電腦上不再需要 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] ，可以解除安裝 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] ，並且判斷是否要移除不受解除安裝程序影響的項目。 如需詳細資訊，請參閱 [解除安裝及移除 Master Data Services](../../sql-server/install/uninstall-and-remove-master-data-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [安裝 SQL Server 2014](../../database-engine/install-windows/install-sql-server.md)  
  
  
