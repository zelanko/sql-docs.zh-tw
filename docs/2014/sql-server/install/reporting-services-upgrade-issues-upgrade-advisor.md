---
title: Reporting Services 升級問題（Upgrade Advisor） |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Report Manager [Reporting Services], upgrade issues
- Reporting Services, upgrades
- upgrading Reporting Services
- report servers [Reporting Services], upgrade issues
ms.assetid: d9663f25-98d7-4508-ae3c-55a7277211bd
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 75c3bda5d15e3930fcdeba9ca73d70128fd90336
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952063"
---
# <a name="reporting-services-upgrade-issues-upgrade-advisor"></a>Reporting Services 升級問題 (Upgrade Advisor)
  下列主題描述可能會影響升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 個問題。 這些主題會描述一些可讓您採取的動作，以便減輕這些變更對環境的影響。  
  
 Upgrade Advisor 會分析報表伺服器安裝。 如果只安裝用戶端元件 (例如，如果「報表設計師」是安裝在電腦上的唯一 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 元件)，則不會報告任何問題。  
  
 根據設定安裝的方式而定，您可能會遇到 Upgrade Advisor 未報告的其他問題。 雖然這些問題不會導致 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 升級失敗，但它們可能會影響報表和應用程式在升級完成後的執行方式。 若要進一步了解這些問題，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜Reporting Services 回溯相容性＞。  
  
 如果您無法使用安裝程式來升級 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝，可以安裝新的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體，然後將現有的安裝移轉至新的執行個體。 如需詳細資訊，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的「升級並遷移 Reporting Services」， [Reporting Services 升級和遷移](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)。  
  
 下列主題將描述 Upgrade Advisor 所報告的已知問題，以及說明如何修改現有的安裝，以便允許進行升級。  
  
> [!IMPORTANT]  
>  Upgrade Advisor 必須安裝在報表伺服器上，才能分析 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不支援遠端分析。  
>   
>  如需詳細資訊，請參閱[安裝 Upgrade Advisor](../../../2014/sql-server/install/installing-upgrade-advisor.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [報表伺服器網站&#40;Upgrade Advisor 上的用戶端憑證&#41;](../../../2014/sql-server/install/client-certificates-on-the-report-server-web-site-upgrade-advisor.md)  
  
-   [在報表伺服器&#40;Upgrade Advisor 上偵測到自訂延伸模組&#41;](../../../2014/sql-server/install/custom-extensions-were-detected-on-the-report-server-upgrade-advisor.md)  
  
-   [在報表伺服器&#40;Upgrade Advisor 上偵測到自訂報表專案&#41;](../../../2014/sql-server/install/custom-report-items-were-detected-on-the-report-server-upgrade-advisor.md)  
  
-   [未偵測到&#40;IIS 回溯相容性元件 Upgrade Advisor&#41;](../../../2014/sql-server/install/iis-backward-compatibility-components-were-not-detected-upgrade-advisor.md)  
  
-   [IP 位址限制偵測&#40;到 Upgrade Advisor&#41;](../../../2014/sql-server/install/ip-address-restriction-detected-upgrade-advisor.md)  
  
-   [在報表伺服器 site &#40;Upgrade Advisor 上偵測到 ISAPI 篩選器&#41;](../../../2014/sql-server/install/isapi-filters-detected-on-the-report-server-site-upgrade-advisor.md)  
  
-   [在報表伺服器電腦&#40;Upgrade Advisor 上偵測到過時的延伸模組&#41;](../../../2014/sql-server/install/obsolete-extensions-were-detected-on-the-report-server-computer-upgrade-advisor.md)  
  
-   [未設定&#40;報表伺服器資料庫的 Upgrade Advisor&#41;](../../../2014/sql-server/install/report-server-database-is-not-configured-upgrade-advisor.md)  
  
-   [SQL Server 2005 報表伺服器 Web 服務群組偵測&#40;到 Upgrade Advisor&#41;](../../../2014/sql-server/install/sql-server-2005-report-server-web-service-group-detected-upgrade-advisor.md)  
  
-   [虛擬目錄是未&#40;指定的 Upgrade Advisor&#41;](../../../2014/sql-server/install/virtual-directories-are-unspecified-upgrade-advisor.md)  
  
-   [虛擬目錄具有不支援的&#40;驗證方法 Upgrade Advisor&#41;](../../../2014/sql-server/install/virtual-directory-has-unsupported-authentication-method-upgrade-advisor.md)  
  
-   [SQL Server Standard 和 Enterprise &#40;Upgrade ADVISOR 的 CPU 和記憶體限制的變更&#41;](../../../2014/sql-server/install/cpu-memory-limits-changes-sql-server-standard-enterprise-upgrade-advisor.md)  
  
-   [SharePoint 伺服器&#40;陣列 Upgrade Advisor 所需的網域帳戶&#41;](../../../2014/sql-server/install/domain-accounts-required-for-sharepoint-farm-upgrade-advisor.md)  
  
-   [直接流覽至報表伺服器&#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/direct-browsing-to-report-server-upgrade-advisor.md)  
  
-   [Microsoft SharePoint 2007 已安裝&#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/microsoft-sharepoint-2007-is-installed-upgrade-advisor.md)  
  
-   [Microsoft SQL Server Reporting Services SharePoint 共用服務已安裝並存&#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/sql-server-reporting-services-sharepoint-shared-service-side-by-side-upgrade-advisor.md)  
  
-   [資料庫引擎 Server 定序&#40;升級建議程式不相容&#41;](../../../2014/sql-server/install/incompatible-database-engine-server-collation-upgrade-advisor.md)  
  
-   [其他 Reporting Services 升級問題](../../../2014/sql-server/install/other-reporting-services-upgrade-issues.md)  
  
  
