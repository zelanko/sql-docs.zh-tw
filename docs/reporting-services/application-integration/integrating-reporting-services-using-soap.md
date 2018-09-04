---
title: 使用 SOAP 整合 Reporting Services | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.suite: pro-bi
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Report Server Web service, application integration
- SOAP [Reporting Services]
- SOAP [Reporting Services], about report integration
- integrating reports [Reporting Services]
- Web service [Reporting Services], application integration
ms.assetid: 6bc17af5-883c-4bfa-87d9-48cd7056d145
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 53fc067c50db33b0f0861e2901eec91ac947902c
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43277550"
---
# <a name="integrating-reporting-services-using-soap"></a>使用 SOAP 整合 Reporting Services
  [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SOAP API 為開發自訂報表方案提供數個 Web 服務端點。 這些端點目前分為兩個類別：管理與執行。 管理功能是透過 <xref:ReportService2005>、<xref:ReportService2006> 和 <xref:ReportService2010> 端點公開。 <xref:ReportService2005> 端點是用於管理以原生模式設定的報表伺服器，而 <xref:ReportService2006> 端點則是用於管理為 SharePoint 整合模式所設定的報表伺服器。 <xref:ReportService2010> 合併了 <xref:ReportService2005> 和 <xref:ReportService2006> 的功能，並能管理以原生模式或 SharePoint 整合模式設定的報表伺服器。  
  
> [!NOTE]  
>  <xref:ReportService2005> 和 <xref:ReportService2006> 端點是在 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 中被取代。 <xref:ReportService2010> 端點包含這兩個端點的功能，並包含額外的管理功能。  
  
 執行功能是透過 <xref:ReportExecution2005> 端點來公開，並在以原生模式或 SharePoint 整合模式設定報表伺服器時使用該功能。 下列主題顯示如何使用這些端點在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows、SharePoint 與 Web 應用程式中開發報表方案。  
  
## <a name="in-this-section"></a>本節內容  
 [在 Windows 應用程式中使用 SOAP API](../../reporting-services/application-integration/integrating-reporting-services-using-soap-windows-application.md)  
 描述如何使用 SOAP API 將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 整合到 Windows 環境中。  
  
 [在 Web 應用程式中使用 SOAP API](../../reporting-services/application-integration/integrating-reporting-services-using-soap-web-application.md)  
 描述如何使用 SOAP API 將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 整合到 Web 環境。  
  
## <a name="see-also"></a>另請參閱  
 [將 Reporting Services 整合到應用程式](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [報表伺服器 Web 服務](../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [使用 Web 服務和.NET Framework 建置應用程式](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
