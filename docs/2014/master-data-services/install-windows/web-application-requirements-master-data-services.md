---
title: Web 應用程式需求 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9455d3cf-c1b7-4d48-8aff-7dc636ed5dc3
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 762be955372568ad7930611b0216bbb3f1437158
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134970"
---
# <a name="web-application-requirements-master-data-services"></a>Web 應用程式需求 (Master Data Services)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 是由 Internet Information Services (IIS) 裝載的 Web 應用程式。 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 只在 Internet Explorer (IE) 7 或更新版本的運作方式。 不支援 IE 7 及更新版本、Microsoft Edge 和 Chrome。  
  
 使用 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 可以建立及設定 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式。 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 會在本機電腦上設定 IIS，因此最適合用於初始 Web 組態工作。 例如在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 環境中設定單一 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式，或在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]的向外延展部署中設定第一個 Web 應用程式。 您可以使用 IIS 工具執行更複雜的工作，例如在向外延展部署中設定多部 Web 伺服器。  
  
> [!NOTE]  
>  安裝 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 元件的任何電腦都必須獲得授權。 如需詳細資訊，請參閱使用者授權合約 (EULA)。  
  
## <a name="requirements"></a>需求  
  
### <a name="operating-system"></a>作業系統  
 下列 Windows 作業系統包含了 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web 應用程式及 Web 服務所需的 Internet Information Services (IIS) 功能。  
  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Developer （64 位元） x64|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise （64 位元） x64|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Business Intelligence (64 位元) x64|  
|-------------------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------|  
|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2<br /><br /> Windows Server 2008 R2 SP1<br /><br /> Windows 7 專業版、企業版與旗艦版<br /><br /> Windows 8.0 專業版、企業版與旗艦版|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2<br /><br /> Windows Server 2008 R2 SP1<br /><br /> Windows Server 2012|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2<br /><br /> Windows Server 2008 R2 SP1<br /><br /> Windows Server 2012|  
  
 如需完整的 Windows 作業系統所支援的版本清單[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請參閱[硬體和軟體需求，安裝 SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。  
  
### <a name="microsoft-silverlight"></a>Microsoft Silverlight  
 若要在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式中工作，用戶端電腦必須安裝 Silverlight 5。 如果您沒有必要的 Silverlight 版本，系統將會在您導覽至需要 Silverlight 的 Web 應用程式區域時提示安裝 Silverlight。 您可以從 [這裡](http://go.microsoft.com/fwlink/?LinkId=243096)安裝 Silverlight 5。  
  
### <a name="role-and-role-services-windows-server-2008-or-windows-server-2008-r2-windows-7-operating-systems"></a>角色和角色服務 (Windows Server 2008 或 Windows Server 2008 R2、Windows 7 作業系統)  
 在 Windows Server 2008 R2 上，您可以使用 Microsoft Management Console (MMC) 中所提供的 **[伺服器管理員]**，以安裝 **[網頁伺服器 (IIS)]** 角色及下列必要的角色服務。  
  
> [!NOTE]  
>  在[!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)]和 Windows 7 作業系統中，使用**程式和功能**中啟用這些選項來控制台中**Windows 功能** 對話方塊。  
  
||  
|-|  
|網頁伺服器<br /><br /> 一般 HTTP 功能<br /><br /> 靜態內容<br /><br /> 預設文件<br /><br /> 瀏覽目錄<br /><br /> HTTP 錯誤<br /><br /> 應用程式開發<br /><br /> ASP.NET<br /><br /> .NET 擴充性<br /><br /> ISAPI 擴充功能<br /><br /> ISAPI 篩選器<br /><br /> 健康情況及診斷<br /><br /> HTTP 記錄<br /><br /> 要求監視器<br /><br /> Security<br /><br /> Windows 驗證<br /><br /> 要求篩選<br /><br /> 效能<br /><br /> 靜態內容壓縮<br /><br /> 管理工具<br /><br /> IIS 管理主控台|  
  
### <a name="role-and-role-services-windows-server-2012-or-windows-8-operating-systems"></a>角色和角色服務 (Windows Server 2012 或 Windows 8 作業系統)  
 在 Windows Server 2012 上，您可以使用 Microsoft Management Console (MMC) 中所提供的 **[伺服器管理員]** 來安裝 **[網頁伺服器 (IIS)]** 角色及下列必要的角色服務。  
  
> [!NOTE]  
>  在 Windows 8 作業系統上，請使用 [控制台] 內的 **[程式和功能]** ，在 **[Windows 功能]** 對話方塊中啟用這些選項。  
  
||  
|-|  
|Internet Information Services<br /><br /> Web 管理工具<br /><br /> IIS 管理主控台<br /><br /> World Wide Web 服務<br /><br /> 應用程式開發<br /><br /> .NET 擴充性 3.5<br /><br /> .NET 擴充性 4.5<br /><br /> ASP.NET 3.5<br /><br /> ASP.NET 4.5<br /><br /> ISAPI 擴充功能<br /><br /> ISAPI 篩選器<br /><br /> 一般 HTTP 功能<br /><br /> 預設文件<br /><br /> 瀏覽目錄<br /><br /> HTTP 錯誤<br /><br /> 靜態內容<br /><br /> [注意：請勿安裝 WebDAV 發行]<br /><br /> 健康情況及診斷<br /><br /> HTTP 記錄<br /><br /> 要求監視器<br /><br /> 效能<br /><br /> 靜態內容壓縮<br /><br /> Security<br /><br /> 要求篩選<br /><br /> Windows 驗證|  
  
### <a name="features-windows-server-2008-or-windows-server-2008-r2-windows-7-operating-systems"></a>功能 (Windows Server 2008 或 Windows Server 2008 R2、Windows 7 作業系統)  
 在[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]或 Windows Server 2008 R2，您可以使用**伺服器管理員**來安裝下列必要的功能。  
  
> [!NOTE]  
>  在[!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)]和 Windows 7 作業系統中，使用**程式和功能**中啟用這些選項來控制台中**Windows 功能** 對話方塊。  
  
||  
|-|  
|.NET Framework 3.0 功能<br /><br /> WCF 啟用<br /><br /> HTTP 啟用<br /><br /> 非 HTTP 啟用<br /><br /> Windows 處理序啟用服務<br /><br /> 處理序模型<br /><br /> .NET 環境<br /><br /> 設定 API|  
  
### <a name="features-windows-server-2012-or-windows-8-operating-systems"></a>功能 (Windows Server 2012 或 Windows 8 作業系統)  
 在 Windows Server 2012 上，您可以使用 **[伺服器管理員]** 來安裝下列必要的功能。  
  
> [!NOTE]  
>  在 Windows 8 作業系統上，請使用 [控制台] 內的 **[程式和功能]** ，在 **[Windows 功能]** 對話方塊中啟用這些選項。  
  
||  
|-|  
|.NET Framework 3.5 (包括 .NET 2.0 和 3.0)<br /><br /> .NET Framework 4.5 進階服務<br /><br /> ASP.NET 4.5<br /><br /> WCF Services<br /><br /> HTTP 啟用 [注意：這是必要項。]<br /><br /> TCP 連接埠共用<br /><br /> Windows 處理序啟用服務<br /><br /> 處理序模型<br /><br /> .NET 環境<br /><br /> 設定 API|  
  
### <a name="accounts-and-permissions"></a>帳戶和權限  
  
|類型|描述|  
|----------|-----------------|  
|Windows 帳戶|您必須使用具備設定 Windows 角色、角色服務與功能，以及在本機電腦之 IIS 中建立與管理應用程式集區、網站與 Web 應用程式的 Windows 帳戶登入 Web 伺服器電腦。|  
|服務帳戶|建立 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 中的 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]Web 應用程式時，必須為應用程式執行所在之應用程式集區指定識別。 此帳戶可能與建立 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫時所指定的服務帳戶不同。<br /><br /> 這個識別必須是網域使用者帳戶，而且加入至 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫的 mds_exec 資料庫角色來進行資料庫存取。 如需詳細資訊，請參閱[資料庫登入、使用者和角色 &#40;Master Data Services&#41;](../database-logins-users-and-roles-master-data-services.md)。 這個帳戶也會加入 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Windows 群組 **MDS_ServiceAccounts**，而這個群組在檔案系統中已被授與暫存編譯目錄 **MDSTempDir** 的權限。 如需詳細資訊，請參閱[資料夾和檔案的權限 &#40;Master Data Services&#41;](../folder-and-file-permissions-master-data-services.md)。<br /><br /> 應用程式集區帳戶需要 VIEW SERVER STATE 權限，以避免發生伺服器錯誤。 例如，MDS 驗證版本命令因伺服器錯誤而失敗。 如需詳細資訊，請參閱 [MDS 驗證版本命令因 SQL Server 2012 和 SQL Server 2014 伺服器錯誤而失敗](http://go.microsoft.com/fwlink/p/?LinkId=526304)|  
  
## <a name="see-also"></a>另請參閱  
 [安裝 Master Data Services](install-master-data-services.md)   
 [建立主資料管理員 Web 應用程式&#40;Master Data Services&#41;](create-a-master-data-manager-web-application-master-data-services.md)   
 [Web 組態頁面 &#40;Master Data Services 組態管理員&#41;](../web-configuration-page-master-data-services-configuration-manager.md)  
  
  