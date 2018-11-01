---
title: 將 Reporting Services 整合到應用程式 | Microsoft Docs
ms.date: 09/18/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
author: markingmyname
ms.author: maghan
monikerRange: = sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f68945ab92db13f80236cfa900067a7d38533849
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47614116"
---
# <a name="integrating-reporting-services-into-applications"></a>將 Reporting Services 整合到應用程式

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 是開放且可延伸的報表平台，用以提供開發人員一組完整的 API 以開發方案。

> [!NOTE]
> 從 SQL Server 2017 Reporting Services 開始，開發方案可使用 REST API 存取。 SOAP API 存取已被取代。 如需詳細資訊，請參閱[使用 Reporting Services 的 REST API 進行開發](../developer/rest-api.md)。
  
 將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 整合到自訂應用程式時有三個選項：報表伺服器 Web 服務 (亦稱為 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SOAP API)、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 的報表檢視器控制項，以及 URL 存取。 每個選項都提供不同的方法，將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 整合到應用程式中。
  
## <a name="report-server-web-service"></a>報表伺服器 web 服務

 報表伺服器 Web 服務是用於針對 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 進行開發的主要介面。 不論您是開發程式碼以管理報表目錄，或是開發程式碼將報表轉譯成支援的格式，Web 服務都會公開所需的方法，來將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 整合到應用程式。 這類應用程式的範例是報表管理員，它是隨附在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中，使用 Web 服務來管理報表伺服器資料庫。  
  
## <a name="report-viewer-controls-for-visual-studio"></a>Visual Studio 的報表檢視器控制項

 適用於 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 的報表檢視器控制項可用來將報表檢視整合到應用程式。 有兩個控制項：一個用於 Windows Form 應用程式，另一個用於 Web Forms 應用程式。 每個控制項都提供可檢視已部署到報表伺服器的報表功能，以及轉譯尚未安裝報表伺服器的環境中所存在之報表的能力。  
  
## <a name="url-access"></a>URL 存取  
 如果報表檢視器控制項不是一個選項，則 URL 存取是將報表檢視整合到應用程式的另一個選項。 此外，URL 存取對於透過電子郵件將報表連結傳送到使用者非常有用。  
  
## <a name="in-this-section"></a>本節內容

 [使用 SOAP 整合 Reporting Services](../../reporting-services/application-integration/integrating-reporting-services-using-soap.md)  
 描述如何使用報表伺服器 Web 服務，將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表導覽與管理整合到現有的商務應用程式。  
  
 [使用報表檢視器控制項整合 Reporting Services](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md)  
 描述如何使用報表檢視器控制項將報表檢視整合到現有的應用程式。  
  
 [使用 URL 存取整合 Reporting Services](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)  
 描述如何使用 URL 存取，將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表導覽整合到現有的商務應用程式。  
  
## <a name="next-steps"></a>後續步驟

若要決定使用 URL 存取或 SOAP API，請參閱[在 Reporting Services 的 URL 存取與 SOAP 之間選擇](choosing-between-url-access-and-soap.md)。

如需 SQL Server 2017 Reporting Services REST API 的資訊，請參閱[使用 Reporting Services 的 REST API 進行開發](../developer/rest-api.md)。

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
