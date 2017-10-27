---
title: "報表伺服器 Web 服務端點 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
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
helpviewer_keywords:
- management endpoints [Reporting Services]
- Web service [Reporting Services], endpoints
- endpoints [Reporting Services]
- execution endpoints [Reporting Services]
- Report Server Web service, endpoints
ms.assetid: f3f5d85f-9359-4508-bc5a-7f78a3cf7421
caps.latest.revision: 26
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 2a0c98cd0c45fc7121a93a51e623dcd2bf36d8bf
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="report-server-web-service-endpoints"></a>報表伺服器 Web 服務端點
  報表伺服器 Web 服務提供幾個端點來管理報表伺服器以及執行和導覽報表。  
  
## <a name="the-management-endpoints"></a>管理端點  
 報表伺服器上有三個端點可用來管理物件：<xref:ReportService2005>、<xref:ReportService2006> 和 <xref:ReportService2010>。 <xref:ReportService2005> 端點是用來在設定為原生模式的報表伺服器上管理物件。 <xref:ReportService2006> 端點是用來在設定為 SharePoint 整合模式的報表伺服器上管理物件。 <xref:ReportService2010> 端點則合併 <xref:ReportService2005> 和 <xref:ReportService2006> 的功能，能夠用來在設定為原生模式或 SharePoint 整合模式的報表伺服器上管理物件。  
  
> [!IMPORTANT]  
>  當報表伺服器設定為 SharePoint 整合模式中， <xref:ReportService2005> Api 會傳回**rsOperationNotSupportedSharePointMode**錯誤。 如果報表伺服器設定為原生模式， <xref:ReportService2006> Api 會傳回**rsOperationNotSupportedNativeMode**錯誤。 同樣地，在非預期的模式上使用 <xref:ReportService2010> 中特屬模式的 API 時，API 會傳回相對應的錯誤。  
  
> [!NOTE]  
>  <xref:ReportService2005> 和 <xref:ReportService2006> 端點是在 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 中被取代。 <xref:ReportService2010> 端點包含這兩個端點的功能，並包含額外的管理功能。  
  
 如果報表伺服器設定為原生模式或 SharePoint 整合模式，您可以使用下列其中一個 URL 來存取管理端點的 WSDL：  
  
```  
http://<Server Name>/ReportServer/ReportService2010.asmx?wsdl  
```  
  
 如需詳細資訊，請參閱[存取 SOAP API](../../../reporting-services/report-server-web-service/accessing-the-soap-api.md)。  
  
## <a name="the-execution-endpoint"></a>執行端點  
 <xref:ReportExecution2005> 端點可讓開發人員輕鬆地自訂報表處理，並在原生模式和 SharePoint 整合模式下從報表伺服器進行轉譯。 此端點包括之前在舊版報表伺服器 Web 服務中存在的類別和方法。 此外，報表伺服器 Web 服務中也加入了許多新的類別和方法，它們可透過執行端點而公開。  
  
 可以使用下列 URL 來存取管理端點的 WSDL：  
  
```  
http://<Server Name>/ReportServer/ReportExecution2005.asmx?wsdl  
```  
  
 如果報表伺服器設定為 SharePoint 整合模式，可以使用下列 URL 來存取 WSDL：  
  
```  
http://<Server Name>/<Site Name>/_vti_bin/ReportServer/ReportExecution2005.asmx?wsdl  
```  
  
 如需詳細資訊，請參閱[存取 SOAP API](../../../reporting-services/report-server-web-service/accessing-the-soap-api.md)。  
  
## <a name="sharepoint-proxy-endpoints"></a>SharePoint Proxy 端點  
 當報表伺服器設定為 SharePoint 整合模式，而且已經安裝 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 增益集時，SharePoint 伺服器上會安裝一組 Proxy 端點。 當報表伺服器設定為 SharePoint 整合模式時，這些 Proxy 端點是用來開發報表方案的主要 API。 當針對 Proxy 端點進行開發時，[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 增益集會在信任帳戶驗證模式下管理 SharePoint 伺服器與報表伺服器之間的認證交換。 當針對報表伺服器端點開發時，呼叫應用程式必須在信任帳戶驗證模式下管理認證交換。 下表將列出隨 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 增益集一起安裝的端點。  
  
|Proxy 端點|Description|  
|--------------------|-----------------|  
|<xref:ReportService2006>|提供 API 以管理設定為 SharePoint 整合模式的報表伺服器。<br /><br /> 注意： 此端點中已被取代[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]。|  
|<xref:ReportService2010>|提供 API 以管理設定為原生模式或 SharePoint 整合模式的報表伺服器。|  
|<xref:ReportExecution2005>|提供 API 來執行及導覽報表。|  
|<xref:ReportServiceAuthentication>|提供 API，在 SharePoint Web 應用程式有設定表單驗證時，針對報表伺服器來驗證使用者。|  
  
 下列是在 SharePoint 網站上參考 Proxy 端點的 URL 範例。  
  
```  
http://<Server Name>/<Site Name>/_vti_bin/ReportServer/ReportService2010.asmx  
```  
  
```  
http://<Server Name>/<Site Name>/_vti_bin/ReportServer/ReportExecution2005.asmx  
```  
  
```  
http://<Server Name>/<Site Name>/_vti_bin/ReportServer/ReportServiceAuthentication.asmx  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用 Web 服務和.NET Framework 建置應用程式](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  

