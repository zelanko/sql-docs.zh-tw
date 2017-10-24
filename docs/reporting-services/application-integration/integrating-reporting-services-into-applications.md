---
title: "應用程式整合 Reporting Services |Microsoft 文件"
ms.custom: 
ms.date: 10/19/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 26e1da5a720aab965d014cada16f85086e0f70a0
ms.contentlocale: zh-tw
ms.lasthandoff: 10/20/2017

---
# <a name="integrating-reporting-services-into-applications"></a>將 Reporting Services 整合到應用程式

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 是開放且可延伸的報表平台，用以提供開發人員一組完整的 API 以開發方案。

> [!NOTE]
> 從 SQL Server 2017 Reporting Services，REST API 的存取是可用來開發方案。 SOAP API 存取已被取代。 如需詳細資訊，請參閱[Reporting services REST api 開發](../developer/rest-api.md)。
  
 有三個選項用於整合[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]到自訂應用程式： 報表伺服器 Web 服務，也稱為[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SOAP API 的 ReportViewer 控制項[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，以及 URL 存取。 每個選項都提供不同的方法，將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 整合到應用程式中。
  
## <a name="report-server-web-service"></a>報表伺服器 web 服務

 報表伺服器 Web 服務是用於針對 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 進行開發的主要介面。 不論您是開發程式碼以管理報表目錄，或是開發程式碼將報表轉譯成支援的格式，Web 服務都會公開所需的方法，來將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 整合到應用程式。 一個這類應用程式的範例是報表管理員中，隨附於[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]; 使用 Web 服務來管理報表伺服器資料庫。  
  
## <a name="reportviewer-controls-for-visual-studio"></a>適用於 Visual Studio ReportViewer 控制項

 可用的 ReportViewer 控制項[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]用於整合報表到應用程式檢視。 有兩個控制項：一個用於 Windows Form 應用程式，另一個用於 Web Forms 應用程式。 每個控制項都提供可檢視已部署到報表伺服器的報表功能，以及轉譯尚未安裝報表伺服器的環境中所存在之報表的能力。  
  
## <a name="url-access"></a>URL 存取  
 如果 ReportViewer 控制項不是一個選項，則 URL 存取是將報表檢視整合到應用程式的另一個選項。 此外，URL 存取對於透過電子郵件將報表連結傳送到使用者非常有用。  
  
## <a name="in-this-section"></a>本節內容

 [使用 SOAP 整合 Reporting Services](../../reporting-services/application-integration/integrating-reporting-services-using-soap.md)  
 描述如何使用報表伺服器 Web 服務，將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表導覽與管理整合到現有的商務應用程式。  
  
 [使用 ReportViewer 控制項整合 Reporting Services](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md)  
 描述如何使用 ReportViewer 控制項將報表檢視整合到現有的應用程式。  
  
 [使用 URL 存取整合 Reporting Services](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)  
 描述如何使用 URL 存取，將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表導覽整合到現有的商務應用程式。  
  
## <a name="next-steps"></a>後續的步驟

決定使用 URL 存取或 SOAP Api，請參閱[URL 存取與 SOAP in Reporting Services 之間的選擇](choosing-between-url-access-and-soap.md)。

如需 SQL Server 2017 Reporting Services REST API 的資訊，請參閱[Reporting services REST api 開發](../developer/rest-api.md)。

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
