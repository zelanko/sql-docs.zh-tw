---
description: 僅限檔案安裝 (Reporting Services)
title: 僅限檔案安裝 (Reporting Services) | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- files-only installation [Reporting Services]
- installation options [Reporting Services]
ms.assetid: bdc74a8f-046c-4aa0-bfbd-4f1711dfb9ce
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a2b27341f5181b8774f56d0d648cfdfe40b1629a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418644"
---
# <a name="files-only-installation-reporting-services"></a>僅限檔案安裝 (Reporting Services)
  「僅限檔案安裝」** 是指安裝程式會建立 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 程式檔案的資料夾結構、將檔案複製到磁碟、在本機電腦上註冊報表伺服器服務、設定服務帳戶、授與檔案權限給此服務帳戶，並註冊 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI 提供者的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝。  
  
 僅限檔案安裝包含以下 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能：報表伺服器服務 (主控報表伺服器 Web 服務和背景處理應用程式)、報表產生器、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 命令列公用程式 (rsconfig.exe、rskeymgmt.exe 和 rs.exe)。 此安裝不會套用到類似 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的共用功能。如果您想要安裝這些功能，則必須將其指定為個別項目。  
  
 與其他安裝模式相較之下，當安裝程式完成時，在僅限檔案模式下安裝的報表伺服器將不會運作。 您必須使用 [Reporting Services 設定管理員 &#40;原生模式&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md) 進行其他組態設定，才能讓報表伺服器在線上工作。  
  
## <a name="when-to-select-files-only-installation-mode"></a>何時選取僅限檔案安裝模式  
 當發生以下狀況時，必須執行僅限檔案安裝：  
  
-   您想要將報表伺服器連接到遠端報表伺服器資料庫。  
  
-   您想要將報表伺服器安裝成具名執行個體。  
  
-   您的部署需求包括使用自訂設定或功能，而且您對於設定伺服器的時機和方式想要擁有完整控制權。  
  
-   正在安裝含有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]容錯移轉叢集。  
  
## <a name="how-to-perform-a-files-only-installation"></a>如何執行僅限檔案安裝  
 僅限檔案安裝是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的預設值。  
  
 您可以透過命令列或安裝精靈來指定僅限檔案安裝。 下列主題提供逐步指示：  
  
-   [從安裝精靈 &#40;安裝程式&#41; 安裝 SQL Server](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)。  
  
-   [從命令提示字元安裝 SQL Server](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)。  
  
#### <a name="example-command-line-script"></a>命令列指令碼範例  
 為了清楚起見，此範例包含 /RSINSTALLMODE="FilesOnlyMode"。 但是，由於僅限檔案模式為預設值，所以當您忽略此設定時，仍然可以得到僅限檔案模式的安裝。  
  
```  
setup /q /ACTION=install /FEATURES=RS /InstanceName=MSSQLSERVER /RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /RSINSTALLMODE="FilesOnlyMode"  
```  
  
#### <a name="installation-wizard"></a>安裝精靈  
 當您在 [特徵選取] 頁面中選取 [ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ] 時，安裝程式會提供 [ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態] 頁面，好讓您指定安裝模式。 若要指定僅限檔案安裝，請在 [[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 設定] 頁面上選取 [安裝但不設定報表伺服器]****。  
  
## <a name="see-also"></a>另請參閱  
 [驗證 Reporting Services 安裝](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
 [設定報表伺服器服務帳戶 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [設定報表伺服器 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [設定報表伺服器資料庫連接 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

 [安裝 Reporting Services SharePoint 模式](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)   

::: moniker-end

 [安裝 Reporting Services 原生模式報表伺服器](~/reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)   
 [Reporting Services 工具](../../reporting-services/tools/reporting-services-tools.md)  
  
  

