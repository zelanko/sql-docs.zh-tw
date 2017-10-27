---
title: "使用 Web 服務和.NET Framework 建置應用程式 |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
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
caps.latest.revision: 38
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: e228d60a4ae01aa345f007be91109b7bccb76f5a
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="building-applications-using-the-web-service-and-the-net-framework"></a>Building Applications Using the Web Service and the .NET Framework
  與[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]，您可以使用熟悉的程式設計建構，例如方法、 基本類型，以及使用者定義的複雜類型來使用 Web 服務。 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 包含您可用以建立 Web 服務用戶端的基礎結構與工具，而這些用戶端可呼叫任何全球資訊網協會 (W3C) 符合標準的 Web 服務。  
  
 報表伺服器 Web 服務用戶端是與使用簡易物件存取通訊協定 (SOAP) 訊息的報表伺服器，進行通訊的任何元件或是應用程式。  
  
 **若要建立報表伺服器 Web 服務的用戶端，使用.NET Framework，請遵循下列基本步驟：**  
  
1.  建立 Web 服務的 Proxy 類別。  
  
     若要這樣做，請將 Proxy 類別或是 Web 參考加入開發專案、參考用戶端程式碼中的 Proxy 類別，並建立該 Proxy 的執行個體。 如需詳細資訊，請參閱[建立 Web 服務 Proxy](../../../reporting-services/report-server-web-service/net-framework/creating-the-web-service-proxy.md)。  
  
2.  在報表伺服器中驗證 Web 服務用戶端。  
  
     若要這樣做，請將服務物件的 <xref:System.Web.Services.Protocols.WebClientProtocol.Credentials%2A> 屬性設定為等於報表伺服器上已驗證使用者的認證。 如需詳細資訊，請參閱[Web 服務驗證](../../../reporting-services/report-server-web-service/net-framework/web-service-authentication.md)。  
  
3.  請呼叫對應至您要叫用之 Web 服務作業的 Proxy 類別之方法。  
  
     若要這樣做，請呼叫 Web 服務方法並提供必要的引數。 如需 Web 服務方法的詳細資訊，請參閱[報表伺服器 Web 服務方法](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)。 如需有關呼叫的詳細資訊，請參閱[呼叫 Web 服務方法](../../../reporting-services/report-server-web-service/net-framework/calling-web-service-methods.md)。  
  
## <a name="in-this-section"></a>섹션 내용  
  
|主題|Description|  
|-----------|-----------------|  
|[建立 Web 服務 Proxy](../../../reporting-services/report-server-web-service/net-framework/creating-the-web-service-proxy.md)|描述如何將 proxy 類別加入您的專案使用[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]。|  
|[Web 服務驗證](../../../reporting-services/report-server-web-service/net-framework/web-service-authentication.md)|描述如何驗證報表伺服器 Web 服務的呼叫。|  
|[呼叫 Web 服務方法](../../../reporting-services/report-server-web-service/net-framework/calling-web-service-methods.md)|描述如何使用 SOAP API 來呼叫 Web 服務方法[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]。|  
|[設定 Web 服務的 Url 屬性](../../../reporting-services/report-server-web-service/net-framework/setting-the-url-property-of-the-web-service.md)|說明如何在建立 Web 參考之後，以程式設計方式將 Web 服務 Proxy 導向新伺服器 URL。|  
|[提供 Web 服務方法引數](../../../reporting-services/report-server-web-service/net-framework/supplying-web-service-method-arguments.md)|描述如何叫用 Web 服務方法並提供方法引數。|  
|[省略選擇性 Web 服務物件的值](../../../reporting-services/report-server-web-service/net-framework/omitting-values-for-optional-web-service-objects.md)|描述如何為選擇性 Web 服務物件省略值。|  
|[使用安全的 Web 服務方法](../../../reporting-services/report-server-web-service/net-framework/using-secure-web-service-methods.md)|描述**SecureConnectionLevel**設定以及它影響 Reporting Services SOAP API 使用的方式。|  
|[將裝置資訊設定傳遞至轉譯延伸模組](../../../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)|描述用以將報表轉譯成不同格式的裝置資訊設定。|  
|[Reporting Services 傳遞延伸模組設定](../../../reporting-services/report-server-web-service/net-framework/reporting-services-delivery-extension-settings.md)|描述使用報表伺服器電子郵件傳遞報表所用的設定。|  
|[使用 Reporting Services SOAP 標頭](../../../reporting-services/report-server-web-service-net-framework-soap-headers/using-reporting-services-soap-headers.md)|說明 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中 SOAP 標頭的用法。|  
|[Reporting Services 中的例外狀況處理簡介](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)|提供有關 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 處理錯誤之方法的資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [報表伺服器 Web 服務](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [技術參考 &#40;SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  

