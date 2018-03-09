---
title: "解除安裝及移除 Master Data Services | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: efc2431c-588b-42e7-b23b-c875145a33f6
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bf5fe32060d6026c6a62b589fbdd991ef561eda6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="uninstall-and-remove-master-data-services"></a>解除安裝及移除 Master Data Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體解除安裝 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 功能時，請依照[解除安裝現有的 SQL Server 執行個體 &#40;安裝程式&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md) 的步驟，並於 [選取功能] 頁面指定 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 為應移除的功能。 解除安裝程序會從本機電腦移除 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料夾和檔案，以及解除安裝 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
 為避免資料遺失且避免影響系統中的其他電腦，解除安裝程序不會移除或變更某些項目。 請檢閱下表，判斷要保留或移除項目。  
  
|項目|描述|  
|----------|-----------------|  
|資料夾和檔案|解除安裝程序會從安裝路徑移除大部分資料夾和檔案。<br /><br /> 解除安裝程序不會從安裝位置移除 Master Data Services 和 MDSTempDir 資料夾。 解除安裝程序完成之後，您可以從檔案系統手動刪除這些資料夾。 如需詳細資訊，請參閱[資料夾和檔案的權限 &#40;Master Data Services&#41;](../../master-data-services/folder-and-file-permissions-master-data-services.md)。|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 組件|解除安裝程序會從全域組件快取 (GAC) 移除 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 組件。|  
|[資料庫]|解除安裝程序不會影響 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體中的資料庫保持不變，因此您不會遺失任何資料，包括主要資料、模型物件、使用者和群組權限、商務規則等。<br /><br /> 若您不需要該資料庫，未來也不打算將它連接到另一個 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 網站或應用程式，您可以從主控該資料庫的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體刪除該資料庫。 如需詳細資訊，請參閱 [刪除資料庫](../../relational-databases/databases/delete-a-database.md)。|  
|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 和 Web.config|解除安裝程序會從檔案系統移除 WebApplication 資料夾。 WebApplication 資料夾包含 Web 應用程式檔以及 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]的 Web.config 檔。<br /><br /> **\*\* 重要 \*\*** 解除安裝之前，您可能要將 Web.config 檔案複製到另一個位置，以保留此檔案中的任何自訂設定或其他資訊。 解除安裝程序完成之後，便無法復原 Web.config 檔案。|  
|Internet Information Services (IIS) 項目|解除安裝程序不會影響本機電腦上 IIS 中的任何應用程式集區、網站或 Web 應用程式。 因為解除安裝程序會移除 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]的 WebApplication 資料夾與 Web.config 檔，所以任何需要這些檔案的 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式，將不再提供內容。 若使用者嘗試存取該 Web 應用程式，就會收到 HTTP 錯誤 500.19-內部伺服器錯誤：「無法存取要求的網頁，因為與該網頁相關的設定資料不正確。」<br /><br /> 若您不再需要該網站或應用程式以及提供您網站或應用程式的應用程式集區，可以使用 IIS 工具將其刪除。 如需詳細資訊，請參閱 [TechNet 上的](http://go.microsoft.com/fwlink/?LinkId=184885) IIS 7 操作手冊 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。|  
|**MDS_ServiceAccounts** 群組|解除安裝程序完成之後， **MDS_ServiceAccounts** Windows 群組以及已加入此群組中的任何服務帳戶會保留。 如果您不再需要此群組和帳戶，可以移除它們。|  
|登錄|解除安裝程序會從 Windows 登錄移除所有 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 登錄機碼。|  
  
## <a name="see-also"></a>另請參閱  
 [安裝 Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
