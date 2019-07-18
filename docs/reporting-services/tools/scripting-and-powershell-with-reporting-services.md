---
title: 指令碼與 PowerShell 搭配 Reporting Services | Microsoft Docs
ms.date: 09/14/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services]
- Reporting Services, scripting
- scripting [Reporting Services]
ms.assetid: 1ac2646d-ed5a-4436-b18f-2150c33f3d87
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a59fb73e4abc987a258405a5b3ee8f5e9ec62c64
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65571675"
---
# <a name="scripting-and-powershell-with-reporting-services"></a>指令碼與 PowerShell 搭配 Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 支援透過指令碼進行各種開發和管理案例，包括 rs.exe 命令列公用程式、適用於 SharePoint 模式報表伺服器的 PowerShell Cmdlet，以及從原生和 SharePoint 模式的 PowerShell 運用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 物件模型。  
  
-   管理員可以利用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 撰寫指令碼，將其部署和管理報表伺服器安裝的方式自動化。 管理員也可以產生並執行能夠建立、設定與更新報表伺服器資料庫的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。 管理員也可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的錄製和播放指令碼功能，將例行的維護工作自動化。  
  
-   開發人員可以建立包括指令碼的自訂應用程式。 您可以執行呼叫報表伺服器 Web 服務的指令碼。 幾乎所有您可以使用 Managed 程式碼撰寫的作業也都可以使用指令碼撰寫。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 支援將 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET 指令碼做為可供 RS.exe 公用程式處理的指令碼語言，此公用程式是在報表伺服器上執行的指令碼主機。  
  
## <a name="reporting-services-sharepoint-mode-powershell-cmdlets-and-samples"></a>Reporting Services SharePoint 模式的 PowerShell Cmdlet 和範例  
 ![PowerShell 相關內容](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 相關內容")  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式包含用於管理報表伺服器的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Cmdlet。  
  
-   [PowerShell cmdlets for Reporting Services SharePoint Mode](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md) 包含下列範例：  
  
    -   建立服務應用程式和 Proxy  
  
    -   檢閱及更新傳遞延伸模組  
  
    -   取得並設定 Reporting Services 應用程式資料庫的屬性，例如資料庫逾時  
  
    -   列出資料延伸模組  
  
## <a name="reporting-services-object-model-and-powershell-samples"></a>Reporting Services 物件模型和 Powershell 範例  
 ![PowerShell 相關內容](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 相關內容")  
  
 PowerShell 呼叫核心物件模型，並在大部分情況適用於 SharePoint 和原生模式，例如移轉工作、訂閱工作和其他相關的 SQL15 訂閱工作範例。  
  
-   [使用 PowerShell 變更及列出 Reporting Services 訂閱擁有者並執行訂閱](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)。  
  
-   [透過原生模式報表伺服器使用 PowerShell 建立 Azure VM](https://msdn.microsoft.com/library/azure/dn449661.aspx)。  
  
-   請參閱[存取 Reporting Services WMI 提供者](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)中的＜使用 PowerShell 存取 WMI 類別＞一節。  
  

## <a name="rsexe-scripting-samples"></a>RS.exe 指令碼範例  
  
-   [在報表伺服器之間複製內容的範例 Reporting Services rs.exe 指令碼](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)。  
  
-   如需其他指令碼、應用程式及延伸模組範例，請參閱 [SQL Server Reporting Services 產品範例](https://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="see-also"></a>另請參閱  
 [RS.exe 公用程式 &#40;SSRS&#41;](../../reporting-services/tools/rs-exe-utility-ssrs.md)   
 [編寫部署和管理工作的指令碼](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
 [利用 rs.exe 公用程式與 Web 服務編寫指令碼](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md)  
  
  
