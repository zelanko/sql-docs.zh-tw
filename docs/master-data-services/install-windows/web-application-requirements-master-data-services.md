---
title: Web 應用程式需求
ms.custom: ''
ms.date: 02/13/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
keywords:
- Master Data Services
ms.assetid: 9455d3cf-c1b7-4d48-8aff-7dc636ed5dc3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 851452cd5170abb6328210ecb35bd95b2bb951a3
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728092"
---
# <a name="web-application-requirements-master-data-services"></a>Web 應用程式需求 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 是由 Internet Information Services (IIS) 裝載的 Web 應用程式。 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 僅適用於 Internet Explorer (IE) 9 或更新版本。 不支援 IE 8 和更早版本、Microsoft Edge 和 Chrome。  

**如需如何安裝及設定 IIS 的指示**，請參閱[安裝和設定 IIS](../../master-data-services/master-data-services-installation-and-configuration.md#InstallIIS)。
  
 使用 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 可以建立及設定 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式。 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 會在本機電腦上設定 IIS，因此最適合用於初始 Web 組態工作。 例如在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 環境中設定單一 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式，或在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]的向外延展部署中設定第一個 Web 應用程式。 您可以使用 IIS 工具執行更複雜的工作，例如在向外延展部署中設定多部 Web 伺服器。  
  
> [!NOTE]  
>  安裝 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 元件的任何電腦都必須獲得授權。 如需詳細資訊，請參閱使用者授權合約 (EULA)。  
  
## <a name="requirements"></a>需求  
  
### <a name="operating-system"></a>作業系統  
 在安裝 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]之前，請檢閱下列需求：    
    
-   [安裝 SQL Server 2016 的硬體與軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)    
  
### <a name="microsoft-silverlight"></a>Microsoft Silverlight  
 若要在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式中工作，用戶端電腦必須安裝 Silverlight 5。 如果您沒有必要的 Silverlight 版本，系統將會在您導覽至需要 Silverlight 的 Web 應用程式區域時提示安裝 Silverlight。 您可以從 [這裡](https://go.microsoft.com/fwlink/?LinkId=243096)安裝 Silverlight 5。  
  
### <a name="role-and-role-services"></a>角色和角色服務  
 在 Windows Server 2012 或 Windows Server 2012 R2 上，您可以使用 Microsoft Management Console (MMC) 中所提供的 [伺服器管理員]，以安裝 [網頁伺服器 (IIS)] 角色及必要的角色服務。  
 
 
> [!IMPORTANT]  
>預設會啟用 [動態內容壓縮]。 如此可大幅降低 xml 回應的大小並省掉了網路 I/O，但 CPU 使用量會增加。  如需詳細資訊，請參閱 [Master Data Services &#40;MDS&#41; 的新功能](../../master-data-services/what-s-new-in-master-data-services-mds.md)中的＜[CTP 2.0] 改良的效能＞。  
  
||  
|-|  
|Internet Information Services<br /><br /> Web 管理工具<br /><br /> IIS 管理主控台<br /><br /> World Wide Web 服務<br /><br /> 應用程式開發<br /><br /> .NET 擴充性 3.5<br /><br /> .NET 擴充性 4.5<br /><br /> ASP.NET 3.5<br /><br /> ASP.NET 4.5<br /><br /> ISAPI 擴充功能<br /><br /> ISAPI 篩選器<br /><br /> 一般 HTTP 功能<br /><br /> 預設文件<br /><br /> 瀏覽目錄<br /><br /> HTTP 錯誤<br /><br /> 靜態內容<br /><br /> [注意：不要安裝 WebDAV 發行]<br /><br /> 健康情況及診斷<br /><br /> HTTP 記錄<br /><br /> 要求監視器<br /><br /> 效能<br /><br /> 靜態內容壓縮<br /><br /> 安全性<br /><br /> 要求篩選<br /><br /> Windows 驗證|  
  
### <a name="features"></a>功能 
 在 Windows Server 2012 和 Windows Server 2012 R2 上，您可以使用 [伺服器管理員] 來安裝下列必要的功能。  
  
||  
|-|  
|.NET Framework 3.5 (包括 .NET 2.0 和 3.0)<br /><br /> .NET Framework 4.5 進階服務<br /><br /> ASP.NET 4.5<br /><br /> WCF Services<br /><br /> HTTP 啟用 [注意：這是必要的。]<br /><br /> TCP 連接埠共用<br /><br /> Windows 處理序啟用服務<br /><br /> 處理序模型<br /><br /> .NET 環境<br /><br /> 設定 API<br/><br/>動態內容壓縮|  
  
 以下是要加入必要伺服器角色和功能的範例 PowerShell 指令碼。 必要伺服器角色和功能會因環境而異。  
  
```powershell  
Install-WindowsFeature Web-Mgmt-Console, AS-NET-Framework, Web-Asp-Net, Web-Asp-Net45, Web-Default-Doc, Web-Dir-Browsing, Web-Http-Errors, Web-Static-Content, Web-Http-Logging, Web-Request-Monitor, Web-Stat-Compression, Web-Filtering, Web-Windows-Auth, NET-Framework-Core, WAS-Process-Model, WAS-NET-Environment, WAS-Config-APIs  
  
Install-WindowsFeature Web-App-Dev, NET-Framework-45-Features -IncludeAllSubFeature -Restart  
```  
  
 如需 PowerShell 命令的詳細資訊，請參閱 [Install-WindowsFeature](/powershell/module/servermanager/install-windowsfeature)。  
  
### <a name="accounts-and-permissions"></a>帳戶和權限  
  
|Type|Description|  
|----------|-----------------|  
|Windows 帳戶|您必須使用具備設定 Windows 角色、角色服務與功能，以及在本機電腦之 IIS 中建立與管理應用程式集區、網站與 Web 應用程式的 Windows 帳戶登入 Web 伺服器電腦。|  
|服務帳戶|建立 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 中的 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]Web 應用程式時，必須為應用程式執行所在之應用程式集區指定識別。 此帳戶可能與建立 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫時所指定的服務帳戶不同。<br /><br /> 這個識別必須是網域使用者帳戶，而且加入至 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫的 mds_exec 資料庫角色來進行資料庫存取。 如需詳細資訊，請參閱[資料庫登入、使用者和角色](../../master-data-services/database-logins-users-and-roles-master-data-services.md)。 這個帳戶也會加入 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Windows 群組 **MDS_ServiceAccounts**，而這個群組在檔案系統中已被授與暫存編譯目錄 **MDSTempDir**的權限。 如需詳細資訊，請參閱[資料夾和檔案的權限 &#40;Master Data Services&#41;](../../master-data-services/folder-and-file-permissions-master-data-services.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [安裝 Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)   
      
 [建立主資料管理員 Web 應用程式 &#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)   
 [Web 組態頁面 &#40;Master Data Services 組態管理員&#41;](../../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)  
  
  
