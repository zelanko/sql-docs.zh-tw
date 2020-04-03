---
title: 使用 Web 服務和 .NET Framework 建置應用程式 | Microsoft Docs
description: 報表伺服器 Web 服務用戶端會透過 SOAP 與報表伺服器通訊。 使用 .NET Framework 建立 Web 服務用戶端，以搭配任何 Web 服務。
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- Report Server Web service, application building
- .NET Framework [Reporting Services]
- XML Web service [Reporting Services], client creation
- reports [Reporting Services], building
- Web service [Reporting Services], application building
- Report Server Web service, client creation
- client configuration [Reporting Services]
- XML Web service [Reporting Services], application building
- Web service [Reporting Services], client creation
ms.assetid: 92a9678c-bc4f-4d7a-ba44-85989bfe27ca
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 37d6552c328daff4793ea65d9670752378e1ab3b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "79509759"
---
# <a name="building-applications-using-the-web-service-and-the-net-framework"></a>Building Applications Using the Web Service and the .NET Framework
  透過 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]，您可以使用熟悉的程式設計建構 (例如方法、基本類型以及使用者定義的複雜類型) 來使用 Web 服務。 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 包含您可用以建立 Web 服務用戶端的基礎結構與工具，而這些用戶端可呼叫任何全球資訊網協會 (W3C) 符合標準的 Web 服務。  
  
 報表伺服器 Web 服務用戶端是與使用簡易物件存取通訊協定 (SOAP) 訊息的報表伺服器，進行通訊的任何元件或是應用程式。  
  
 **若要使用 .NET Framework 來建立報表伺服器 Web 服務用戶端，請遵循以下基本步驟：**  
  
1.  建立 Web 服務的 Proxy 類別。  
  
     若要這樣做，請將 Proxy 類別或是 Web 參考加入開發專案、參考用戶端程式碼中的 Proxy 類別，並建立該 Proxy 的執行個體。 如需詳細資訊，請參閱[建立 Web 服務 Proxy](../../../reporting-services/report-server-web-service/net-framework/creating-the-web-service-proxy.md)。  
  
2.  在報表伺服器中驗證 Web 服務用戶端。  
  
     若要這樣做，請將服務物件的 <xref:System.Web.Services.Protocols.WebClientProtocol.Credentials%2A> 屬性設定為等於報表伺服器上已驗證使用者的認證。 如需詳細資訊，請參閱 [Web 服務驗證](../../../reporting-services/report-server-web-service/net-framework/web-service-authentication.md)。  
  
3.  請呼叫對應至您要叫用之 Web 服務作業的 Proxy 類別之方法。  
  
     若要這樣做，請呼叫 Web 服務方法並提供必要的引數。 如需 Web 服務方法的詳細資訊，請參閱[報表伺服器 Web 服務方法](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)。 如需呼叫的詳細資訊，請參閱[呼叫 Web 服務方法](../../../reporting-services/report-server-web-service/net-framework/calling-web-service-methods.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[建立 Web 服務 Proxy](../../../reporting-services/report-server-web-service/net-framework/creating-the-web-service-proxy.md)|描述使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 將 Proxy 類別新增至專案的方法。|  
|[Web 服務驗證](../../../reporting-services/report-server-web-service/net-framework/web-service-authentication.md)|描述如何驗證報表伺服器 Web 服務的呼叫。|  
|[呼叫 Web 服務方法](../../../reporting-services/report-server-web-service/net-framework/calling-web-service-methods.md)|描述如何使用 SOAP API 呼叫 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中的 Web 服務方法。|  
|[設定 Web 服務的 Url 屬性](../../../reporting-services/report-server-web-service/net-framework/setting-the-url-property-of-the-web-service.md)|說明如何在建立 Web 參考之後，以程式設計方式將 Web 服務 Proxy 導向新伺服器 URL。|  
|[提供 Web 服務方法引數](../../../reporting-services/report-server-web-service/net-framework/supplying-web-service-method-arguments.md)|描述如何叫用 Web 服務方法並提供方法引數。|  
|[省略選擇性 Web 服務物件的值](../../../reporting-services/report-server-web-service/net-framework/omitting-values-for-optional-web-service-objects.md)|描述如何為選擇性 Web 服務物件省略值。|  
|[使用安全的 Web 服務方法](../../../reporting-services/report-server-web-service/net-framework/using-secure-web-service-methods.md)|描述 **SecureConnectionLevel** 設定，以及它影響 Reporting Services SOAP API 使用方式的方法。|  
|[將裝置資訊設定傳遞至轉譯延伸模組](../../../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)|描述用以將報表轉譯成不同格式的裝置資訊設定。|  
|[Reporting Services 傳遞延伸模組設定](../../../reporting-services/report-server-web-service/net-framework/reporting-services-delivery-extension-settings.md)|描述使用報表伺服器電子郵件傳遞報表所用的設定。|  
|[使用 Reporting Services SOAP 標頭](../../../reporting-services/report-server-web-service-net-framework-soap-headers/using-reporting-services-soap-headers.md)|說明 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中 SOAP 標頭的用法。|  
|[Reporting Services 中的例外狀況處理簡介](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)|提供有關 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 處理錯誤之方法的資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [報表伺服器 Web 服務](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [技術參考 &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
